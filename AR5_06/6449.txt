The VOLINIT processor prepares a disk pack so that it may be used by the CP-6 
system.  After VOLINIT has prepared a disk pack, the Packset Initializer may 
be used to assign the pack to a packset. 
To obtain HELP messages, type: 
HELP (VOLINIT) COMMANDS      For a summary of commands 
HELP (VOLINIT) TOPICS        For a list of VOLINIT HELP topics. 
HELP (VOLINIT) command       For format of a specific command. 
                             then type ? or ?? for more. 
HELP (VOLINIT) command PARAM For only parameter information 
                             on a specific command. 
HELP (VOLINIT) command DESC  For the description of a specific 
                             command. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
For a list of VOLINIT commands, type ? or ??.  For a brief description of a 
specific command, type 
HELP (VOLINIT) COMMANDS command 
Valid command names are DATE, DIRECTORY, DO, DT, DTEND, END, ENTER, ERASE, 
EXIT, HELP, KEYIN, OUTPUT, PRINT_BOOTTIME, PRINT_ONLINE, QUIT, READ, STATUS, 
STOP, TIME, and VOLINIT. 
  Command        Meaning 
  {DATE|TIME} 
                 Displays the current time and date. 
  {DIRECTORY|DIR} 
                 Changes the default account and packset. 
  {DO|!} 
                 Enables IBEX command execution. 
  DT 
                 Specifies known defective tracks.  These commands must 
                 immediately follow the VOLINIT command when DTT=UPDATE or NEW 
                 is specified. 
  DTEND 
                 Indicates the end of the defective track commands. 
  {END|EXIT|QUIT} 
                 Terminates the VOLINIT processor and returns control to the 
                 caller; that is, to TIGR in case of a boot-time VOLINIT 
                 operation and IBEX in the case of an on-line VOLINIT 
                 operation. 
  ENTER 
                 Invokes a CP-6 ADAPT dialog from within this processor. 
  ERASE 
                 Deletes accumulated output for logical devices. 
  HELP 
                 Displays information about commands. 
  KEYIN 
                 Available under boot-time VOLINIT.  It solicits an operator 
                 keyin. 
  OUTPUT 
                 Directs processor output to a destination. 
  PRINT (Boot-Time) 
                 Available only under boot-time VOLINIT.  It directs output to 
                 a printer or to the system console. 
  PRINT (On-Line) 
                 Directs immediate listing of output destined for logical 
                 devices. 
  READ 
                 Available only under boot-time VOLINIT.  It indicates the 
                 source device for the VOLINIT command stream. 
  STATUS 
                 Produces a display of all currently active disk 
                 initialization activities. 
  STOP 
                 Terminates disk initialization activities on a specified 
                 drive. 
  VOLINIT 
                 Specifies the pack to be prepared and the parameters and 
                 options governing its initialization. 
00003
00001
00002
00003
00004
00005
00006
00007
00008
00006
00009
00010
00011
00012
00013
00006
00014
00015
00016
00001
00017
Format: 
{DATE|TIME} 
Description: 
DATE (and its synonym TIME) displays the current date and time.  The format of 
the display is: 
mmm dd 'yy hh:mm  (month)(day)(year)(hours)(minutes) 
Examples: 
*DATE 
requests a display of the current date and time.  A sample display is: 
AUG 02  '88  11:03 
00001
00002
Format: 
{DIR|DIRECTORY} [fid|R[ESET]] 
Parameters: 
fid    specifies the new default account fid, and may consist of an account or 
a packset name and an account. 
RESET    specifies that the default account is to be reset to the running 
account. 
Description: 
DIRECTORY changes the default account and packset.  The default account and 
packset are the account and associated packset that are selected if an account 
is not supplied as part of a disk file fid specification.  Initially, the 
default account is the logon or running account and the packset name is nil. 
When used without parameters, DIRECTORY displays the current directory 
pointer. 
Examples: 
*DIRECTORY .SYSLIB 
This command directs that subsequent fids that do not include an account are 
to default to the .SYSLIB account and the packset associated with that 
account. 
*DIRECTORY DP#UTIL.Y 
This command specifies that subsequent fids that do not include an account are 
to default to the Y account on the packset named UTIL. 
*DIRECTORY RESET 
This command re-establishes the running account and its associated packset as 
the default. 
00002
00003
00001
Format: 
{DO|!} IBEX-command 
Parameters: 
IBEX-command    any legal IBEX command.  (See the CP-6 Programmer Reference 
Manual (CE40)). 
Description: 
The DO command allows the user to execute an IBEX command without exiting the 
current processor. 
Note:  The ! (exclamation point) may be used instead of the word DO.  It 
should be noted however that if the ! is used in an XEQ file, it will 
terminate the current processor session unless preceded by at least one blank, 
or by a double ! (!!). 
Examples: 
*DO DI 
means display the current system status 
*!LDEV LP09 TITLE='report title',PAGE=100,COPIES=3 
means set up a title and page number for a report destination 
00002
00003
00001
Format: 
DT {ccc.hh} 
   {nnnnnn} 
Parameters: 
ccc.hh    is the designation of the defective track by cylinder and head. 
nnnnnn    is the designation of the defective track by granule number. 
Description: 
The DT command instructs VOLINIT to mark a specified track as defective.  If 
the designation is a granule number and the granule is split across two 
tracks, both tracks will be marked defective. 
Usage Notes: 
1.  The DT command may be requested at boot-time or during on-line operation. 
2.  Multiple DT commands may be entered; however, the stream of DT commands 
    must immediately follow the VOLINIT command. 
3.  The DT command is only valid for MSU0451 and MSU0501 devices. 
00002
00001
00003
Format: 
DTE[ND] 
Description: 
The DTEND command informs VOLINIT of the end of the stream of DT commands. 
Usage Note: 
The DTEND command may be requested at boot-time or during on-line operation. 
00001
00002
Format: 
{E[ND]|[E]X[IT]|Q[UIT]} 
Description: 
The END command (and its synonyms EXIT and QUIT) indicates to VOLINIT the end 
of the VOLINIT command stream.  After all disk initialization activities 
called for by the command stream are completed, VOLINIT will return control to 
the caller, i.e., TIGR for a boot-time VOLINIT or IBEX for on-line VOLINIT. 
Usage Notes: 
1.  The END command may be used at boot-time or during on-line operations. 
2.  When on-line or at boot time, additional commands may be entered after END 
    if VOLINIT has not terminated, in which case the END command is forgotten. 
    The BREAK or REQUEST key must be used to get VOLINIT to prompt for more 
    commands. 
00001
00002
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
ERASE deletes the accumulated outputs for logical devices. 
Examples: 
*ERASE ALL 
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
  defective track - 
      HELP DT PARAMETERS: 
  Defective Track Table - 
      HELP VOLINIT PARAMETERS: 
      HELP VOLINIT USAGE_NOTES: 
  DIRECTORY Command - 
      HELP DIRECTORY 
  DO Command - 
      HELP DO 
  DT Command - 
      HELP DT 
  DTEND Command - 
      HELP DTEND 
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
  home address (disk) - 
      HELP VOLINIT USAGE_NOTES: 
I 
  Invoking VOLINIT - 
      HELP INVOKING_VOLINIT 
K 
  KEYIN Command -   
    VOLINIT - 
      HELP KEYIN FORMAT: 
  KEYIN Command - 
      HELP KEYIN 
O 
  OUTPUT Command - 
      HELP OUTPUT 
P 
  PRINT Command (Boot-Time) - 
      HELP PRINT_BOOTTIME_COMMAND 
  PRINT Command (On-Line) - 
      HELP PRINT_ONLINE_COMMAND 
  Privileges Required for VOLINIT - 
      HELP PRIVILEGES 
R 
  READ Command -   
    VOLINIT - 
      HELP READ FORMAT: 
  READ Command - 
      HELP READ 
S 
  SCRATCH option (VOLINIT) - 
      HELP VOLINIT PARAMETERS: 
  STATUS Command -   
    VOLINIT - 
      HELP STATUS FORMAT: 
  STATUS Command - 
      HELP STATUS 
  STOP Command - 
      HELP STOP 
T 
  track - 
      HELP DT PARAMETERS: 
      HELP VOLINIT PARAMETERS: 
V 
  VID - 
      HELP VOLINIT USAGE_NOTES: 
  VOLINIT -   
    DT Command - 
      HELP DT FORMAT: 
    DTEND Command - 
      HELP DTEND FORMAT: 
    KEYIN Command - 
      HELP KEYIN FORMAT: 
    PRINT Command - 
      HELP PRINT_BOOTTIME_COMMAND FORMAT: 
    READ Command - 
      HELP READ FORMAT: 
    STATUS Command - 
      HELP STATUS FORMAT: 
    STOP Command - 
      HELP STOP FORMAT: 
    VOLINIT Command - 
      HELP VOLINIT FORMAT: 
  VOLINIT Command - 
      HELP VOLINIT 
  volume serial number (VSN) - 
      HELP VOLINIT PARAMETERS: 
  VSN - 
      HELP VOLINIT PARAMETERS: 
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
HELP_INDEX
VOLINIT may be invoked as a stand-alone job at boot time (off-line VOLINIT) or 
as a CP-6 processor (on-line VOLINIT).  Except for the method of invocation, 
the processes and commands are the same.  More than one pack may be 
initialized by VOLINIT in any one session. 
The procedure for invoking the boot-time version of VOLINIT is as follows. 
o   Begin a tape boot. 
o   When the prompt TB/DB/OR/VO? occurs, respond VO. 
o   Continue the boot process. 
o   After TIGR finishes executing, VOLINIT will prompt for commands. 
o   After completing VOLINIT, the system will then go idle.  The initialized 
    pack may be dismounted for later use, or the operator may again press the 
    boot button to start a normal boot to the initialized pack. 
The on-line version of VOLINIT may be run in the batch and on-line CP-6 access 
modes.  When run as an on-line job, VOLINIT issues the * character to solicit 
commands. 
To invoke the on-line version of VOLINIT, the format of the command is: 
!VOLINIT [source] [ON, listout] 
where 
source    is the source fid from which commands are to be read.  The default 
is ME (on-line) or the input stream (batch). 
listout    is a fid specifying the destination for VOLINIT printed output, 
such as a printer. 
Note:  When VOLINIT is performing some action, it can be instructed to prompt 
for more commands by keying BREAK on-line or REQUEST at boot time. 
Format: 
KEYIN 
Description: 
The KEYIN command solicits an operator device keyin during boot-time VOLINIT 
operation. 
Usage Note: 
The KEYIN command may be requested at boot-time.  The user gets VOLINIT's 
attention by pressing the BREAK or REQUEST key and entering the KEYIN command 
which results in a prompt to enter a device keyin. 
00001
00002
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
LP    directs output to the default line printer; @location specifies a 
specific line printer. 
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
P[RINT] dev 
Parameters: 
dev    is the identification of the device that is to receive the output: 
system console (SCnn) or line printer (LPnn). 
Description: 
The PRINT command instructs VOLINIT to send its output to a specified device. 
00002
00001
Format: 
PRINT [ALL|ldevlist] 
Parameters: 
ALL    specifies that the accumulated output for all logical devices is to be 
sent to destination(s) immediately.  This is the default. 
ldevlist    specifies that the accumulated output for the specified logical 
device or devices is to be sent to destination(s) immediately.  The list is 
entered in the format 
ldevlist[,ldevname]... 
ldevname is a logical device name established through the LDEV command. 
Description: 
PRINT directs that output accumulated for logical devices be sent to 
destination(s) immediately. 
Examples: 
*PRINT LP01,LP02 
The above example causes the accumulated output associated with logical 
devices LP01 and LP02 to be sent immediately to the associated destinations. 
00002
00003
00001
The user must be authorized for the SPCLMM, IOQ and IOQW privileges or the 
VOLINIT processor privilege to run on-line VOLINIT. 
Format: 
R[EAD] dev 
Parameters: 
dev    is the designation of the input device:  system console (SCnn), card 
reader (CRnn), or tape drive (MTnn). 
Description: 
The READ command instructs VOLINIT to read its command stream from a specified 
device until another READ command is encountered or until an end-of-file on 
the selected device is encountered.  When an end-of-file is encountered, the 
command stream returns to the system console. 
Usage Note: 
The READ command is available only under boot-time VOLINIT. 
00002
00001
00003
Format: 
S[TATUS] 
Description: 
The STATUS command produces a display of all currently active disk 
initialization activities.  The status information displayed includes the 
device identification, the volume serial number of the disk pack, and the 
cylinder and head currently being formatted. 
Usage Note: 
The STATUS command may be requested at boot-time or during on-line operations. 
The user gets VOLINIT's attention by pressing the BREAK or the REQUEST key 
when at boot-time. 
00001
00002
Format: 
STOP [dev] 
Parameters: 
dev    indicates the device on which disk initialization activities are to 
cease. 
Description: 
The STOP command instructs VOLINIT to stop disk initialization activities on a 
specified device or on all devices.  If no dev is specified, all current disk 
initialization activities cease. 
Usage Note: 
The STOP command may be requested at boot-time or during on-line operations. 
00002
00001
00003
DATE
Format: 
                          {O[LD]   } 
V[OLINIT] dev,vsn, [DTT = {U[PDATE]} ] [, opt[, opt] ... ] 
                          {N[EW]   } 
Parameters: 
dev    is the designation of the drive on which the pack to be initialized is 
located, in the form DPnn. 
vsn    is the volume serial number to be written on the disk pack.  The vsn 
must be a decimal number. 
DTT=    indicates what action is to be taken with respect to the Defective 
Track Table portion of the VID. 
DTT=OLD    instructs VOLINIT to use the DTT that exists on the disk pack.  OLD 
is the default if no DTT specification is given.  If no old DTT exists, 
DTT=NEW is the default. 
DTT=UPDATE    instructs VOLINIT to update the DTT on the disk pack with the 
information contained in the DT commands. 
DTT=NEW    instructs VOLINIT to disregard the DTT on the disk pack and create 
a DTT from the DT commands. 
opt    is one of the following: 
    [NO]ALT    instructs VOLINIT whether or not the alternate tracks have been 
    assigned using TOLTS. (If the alternate tracks have been assigned using 
    TOLTS, then the drive must not be reformatted by VOLINIT and the alternage 
    tracks cannot be used as data tracks.)  ALT will force the NOFORMAT 
    option. ALT will also cause VOLINIT to add the alternate cylinders to the 
    defective track table. ALT is valid only on MSU0451 and MSU0501 devices. 
    The default is NOALT (i.e., VOLINIT functions as it did in the past and 
    uses the alternate tracks as data tracks). 
    [NO]FORMAT    instructs VOLINIT whether or not to format each track. 
    FORMAT is only allowed on MSU0451 devices.  The default is NOFORMAT. 
    [NO]SCRATCH    instructs VOLINIT whether or not to scratch the pack.  The 
    default is SCRATCH. 
    [NO]VERIFY    instructs VOLINIT whether or not to verify the home address 
    of a track before formatting it.  The default is NOVERIFY. 
    [NO]TEST    instructs VOLINIT whether or not to test each track.  The test 
    is to write and compare the test bit pattern on the track to verify that 
    it can be read without error.  The default is TEST for 451 and 501 
    devices, and NOTEST for FIPS and MSD devices.  For 451 devices, do not use 
    NOTEST without specifying the FORMAT option. 
    NEWDTS    instructs VOLINIT to format only the tracks specified in the DT 
    commands. 
    [ccc.hh]     [ccc.hh] 
    [nnnnnn] [- ][nnnnnn]    instructs VOLINIT to format only the 
    tracks within the range.  The tracks may be specified by cylinder and head 
    (ccc.hh) or by granule number (nnnnnn).  The range is stated in one of the 
    following formats:  firsttrack (format only firsttrack); firsttrack- 
    (format from firsttrack to the end of the pack); firsttrack-lasttrack 
    (format firsttrack to lasttrack, inclusive). 
    Up to sixty-four ranges can be specified.  Ranges are sorted by track 
    number and if the ranges, and/or their granule numbers overlap, they will 
    be combined. 
It is recommended that no tracks or ranges should be specified when formatting 
or testing a virgin pack.  This is especially true for a MSU050X drive.  No 
CE-DATA is written if the track range is specified; MDR of TOLTS needs the 
CE-DATA. 
If neither NEWDTS nor a track range is specified, the entire pack will be 
reformatted. 
Description: 
The VOLINIT command causes the VOLINIT processor to prepare a disk pack 
mounted on a specified device.  If DTT=UPDATE or NEW is entered, the system 
will respond with the message ENTER DTT:  and a prompt character.  The user 
must respond with a DT command, or stream of DT commands, followed by a DTEND 
command.  VOLINIT always prints all defective tracks known to it during the 
VOLINIT process. 
Usage Notes: 
1.  The VOLINIT command may be requested at boot-time or during on-line 
    operation. 
2.  VOLINIT, when on-line, will require the drive, as designated by the dev 
    parameter, to be partitioned out (via the SYSCON processor).  It is also 
    necessary to obtain diagnostic access to the device.  This is accomplished 
    either by setting the flag TDOK=YES for the device, under SYSCON, or by 
    having the operator grant diagnostic access to the user by entering the 
    DIAG keyin. 
3.  VOLINIT will read the pack's VID and compare the volume serial number in 
    the VID with the volume serial number specified by the vsn parameter in 
    the VOLINIT command.  VOLINIT will proceed if there is no VID on the pack 
    or if the volume serial number on the pack matches the volume serial 
    number in the command.  If there is a discrepancy in the volume serial 
    numbers, VOLINIT will display the pack's volume serial number and will ask 
    the user, if the job is running on-line or at boot time, whether or not to 
    proceed.  If the job is running as a batch job, this command will be 
    aborted. 
4.  If the VERIFY option is specified, VOLINIT will perform home address 
    verification.  The disk drive will position the arm to the specified track 
    and read the home address to verify that the arm has been positioned to 
    the correct cylinder and that the correct head has been selected.  If the 
    verification fails, the command will be aborted. 
5.  If the TEST option is selected and the test finds irrecoverable errors, 
    VOLINIT will reformat the track as defective with no alternate track. 
    VOLINIT will then update the Defective Track Table accordingly.  File 
    management will not allocate defective tracks. 
6.  The FORMAT option is not allowed on MSU0501, MSU33xx or MSU80xx devices. 
7.  All parameters and options except dev and vsn are ignored for MSU33xx and 
    MSU80xx devices.  VOLINIT will only write VIDs with all DTs set to -1 for 
    these devices. 
8.  For an MSU0451, the alternate cylinders are 811 through 813.  For an 
    MSU0501, the alternate cylinder is 840. (This is to prevent dual 
    allocation of these tracks. These tracks are the alternate tracks used for 
    defective tracks found by TOLTS.) 
9.  If the ALT option is specified, then the RANGE option is not accepted. 
10. Formatting of all devices should be done using TOLTS instead of the 
    VOLINIT FORMAT option since the TOLTS formatting tests do a better job of 
    formatting the device than the does the VOLINIT FORMAT option. Also, some 
    devices only can be formatted using TOLTS (i.e., VOLINIT FORMAT cannot 
    format FIPS or MDS devices). And if the device has been formatted using 
    TOLTS, then the NOFORMAT option should be specified to prevent VOLINIT 
    from reformatting the device. 
00002
00001
00003
