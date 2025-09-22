The NETCON processor defines CP-6 networks, maintains network links and 
controls network performance. 
To obtain more information on NETCON, type: 
HELP (NETCON) COMMANDS       For a summary of commands. 
HELP (NETCON) TOPICS         For a list of NETCON HELP topics. 
HELP (NETCON) command        For the format of a specific 
                             command.  Then type ? or ?? for 
                             more. 
HELP (NETCON) command PARAM  For the parameters for a specific 
                             command. 
HELP (NETCON) command DESC   For the description of a specific 
                             command. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
DO
Format: 
BOOT [N[ODE][=]] nodeid[[,]{NO[TIME]|NT}]] 
Parameters: 
nodeid    is the 1 to 8 character name of a local FEP or the local FEP number. 
NOTIME    sets the no timeout flag, which allows the FEP to be debugged 
without the host timing it out and forcing it into recovery.  This option 
should be used only for FEPs DEFINEd with a nodetype of DEBUG. 
Description: 
The BOOT command boots the specified local FEP using the current boot 
information for the FEP.  The boot information for the FEP consists of: 
o   the information supplied by the SET BOOTINFO command or its defaults. 
o   the information supplied by a SET param=value command or its defaults. 
    The type of parameter set (i.e., boot, LCP6, or handler) is determined by 
    the name specified for param in the SET command (See: HELP (NETCON) 
    PARAMETERS).  For example: 
        L6XII   *SET LDCT=20    sets a boot parameter 
        L6XII   *SET QMIN=100   sets a LCP6 parameter 
For a handler parameter, the handler name must be specified prior to setting 
the parameter value (e.g., SEL H = handlername). 
        L6XII   *SEL H=NODEADMN 
        L6XII   *SET LGNRTRY=5    sets an NODEADMN handler parameter. 
o   configuration information for any lines defined as LINKS for the node. 
Only local FEPs can be booted via the BOOT command. 
00002
00001
  Parameter            Description 
Monitor fid          Identifies the LCP6 monitor run unit. 
Number of handlers   Is a decimal value (2 <= number.of.handlers <= n) 
                     that defines how many handlers to boot.  The 
                     maximum number is limited by the size of the 
                     handlers and the amount of physical memory in the 
                     FEP. 
Handler name         Is a 1 to 8 alphanumeric character value that 
                     assigns a name to a handler.  Usually one of the 
                     following predefined handler names: ASYNC, BISYNC, 
                     COUPLER, HDLCX25, NODEADMIN, or UNITREC. 
Handler fid          Identifies the handler run unit. 
Library Account      Identifies the account where the libraries 
                     associated with the handlers reside. 
                     The default is :SYS. 
The BOOTTIME parameter is automatically set to YES. 
BOOTINFOPARAMS
BOOTINFOPARAMS
The parameters are: ACCTS, APESSN, CBUFFER, DEVICES, HMI, IOP, KEEPDELTA, 
LDCT, MAXLINKS, MUIS, PCHANS, SFILE, and TCTX. 
Enter: HELP (NETCON) BOOTPARAMS parameter 
for a description of a specific parameter. 
For a description of all parameters, enter: ??. 
  Parameter   Description 
  ACCTS 
              ACCounTS specifies the number of entries to be allocated in the 
              Account Resource Table.  One is needed for each distinct 
              uacct/uname combination expected to be running in the FEP at any 
              given time. 
              Unit: Table Entry            Default: 15 
              Minimum: 1                   Maximum: Dynamic 
  APESSN 
              Application Protocol Engine SeSsioN specifies context blocks 
              used for FPRG DCBs.  Each user- or comgroup-connected user has 
              two APESSNs, one connected to the Host, and one to the terminal. 
              Each handler except NODEADMN has one, connected to NODEADMN.  A 
              Ghost user typically has one, connected to the Host. 
              Unit: Block                  Default: 40 
              Minimum: MUIS                Maximum: 65535 
  CBUFFER 
              Communications BUFFERs specifies the number of pages to be 
              allocated for transport and network buffers on this FEP. 
              Unit: Page                   Default: 32 
              Minimum: Dynamic             Maximum: 256 
  DEVICES 
              DEVICES specifies the number of devices to be reserved at the 
              second terminal (subnum) level and the third terminal 
              (subsubnum) level.  (See HELP (NETCON) TERMSPEC_PARAMETER.)  One 
              DEVICE is needed for each RBT sub-device, 3270 controller, 3270 
              device, and X29 user connected to the FEP. 
              Note:  Once a subnum or subsubnum level device connects, the 
              device context memory is permanently allocated to the base 
              channel and cannot be recovered until the FEP is rebooted. 
              Unit: Device                 Default: 50 
              Minimum: 0                   Maximum: 65535 
  HMI 
              Handler Monitor Interface specifies the number of handler 
              monitor interfaces available in the FEP.  One is needed for each 
              DCB open with ORG=CQ.  Each handler has one such DCB. 
              Unit: HMI                    Default: 20 
              Minimum: No. of handlers     Maximum: 65535 
  IOP 
              IOP specifies the number of input/output parameter blocks 
              available in the FEP.  One is needed for every outstanding I/O 
              operation in a node.  The requirement never exceeds APESSN. 
              Unit: Context block          Default: 10 
              Minimum: MUIS                Maximum: 65535 
  KEEPDELTA 
              If KEEPDELTA is 1, the boot time initialization portion of the 
              FEP Monitor (BIGFOOT) allocates pages for the data and procedure 
              of FEP DELTA.  This permits debugging of FPRGs via user DELTA, 
              and possibly debugging of handlers and LCP6 via DELTA's DEBUG 
              command.  This is explained in more detail in the Host SRB, 
              Appendix D, "Debug FEP Configuration".  If KEEPDELTA is 0, those 
              pages are released for other purposes, and debugging via DELTA 
              is not possible. 
              Unit:  n/a                  Default:  1 
              Minimum:  0                 Maximum:  1 
  LDCT 
              Logical Device Control Table specifies context for the end point 
              that terminates in this FEP.  One is needed for each end point 
              terminating in the FEP. 
              Unit: Context block          Default: 100 
              Minimum: Dynamic*            Maximum: 65535 
              * Minimum = 4  for Monitor use 
                        + 1  for each link (MAXLINKS) 
                        + 2  for each user (MUIS) 
                        + 4  more for each user that 
                             is comgroup connected 
                             (MUSR_C) 
                        + the number specified for 
                          DEVICES 
                        + the number of physical lines 
  MAXLINKS 
              MAXimum LINKS specifies the number of network links that connect 
              a node to the network. 
              Unit: Link                   Default: 5 
              Minimum: 1                   Maximum: 255 
  MUIS 
              Maximum Users In System specifies the maximum number of users in 
              a FEP. 
              Unit: User                   Default: 20 
              Minimum: No. of handlers     Maximum: 255 
                       from BOOTINFO 
  OSIROUTE 
              OSIROUTE specifies the number of entries in the OSI Routing 
              tables that are to be built on this FEP.  One entry is needed 
              for each OSI network address known to the CP-6 network. 
              Unit:  Number of addresses   Default:  2 
              Minimum:  0                  Maximum:  256 
  PCHANS 
              Specifies the number of channel table entries to be reserved for 
              pseudo channels. 
              Unit: Table entry            Default: 10 
              Minimum: 0                   Maximum: 
                                           .FF80 (highest physical 
                                           channel/.80) 
  SFILE 
              Shared FILE specifies the number of slots for shared files in 
              the Shared File Table. 
              Unit: Table entry            Default: 15 
              Minimum: 2                   Maximum: 255 
  TCTX 
              Transport ConTeXt specifies the number of transport context 
              blocks to be allocated on the FEP.  One is needed for each host 
              node in the system plus one for each adjacent FEP.  If this is a 
              local FEP supporting OSI connections, this number should be 
              increased by the maximum number of OSI connections allowed. 
              Unit: Context block          Default: 32 
              Minimum: Dynamic             Maximum: 65535 
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
BOOTPARAMS
BOOTPARAMS
The current channel state data is changed by use of the NETCON processor 
DISABLE, DISCONNECT, ENABLE and KILL commands.  The following lists the 
channel states. 
  State                     Description 
BUSY                      The channel line is active. 
BUSY DISABLE PENDING      The channel line is currently active.  When 
                          it becomes inactive, the channel line will 
                          be disabled. 
BUSY PARTITION PENDING    The channel line is currently active.  When 
                          it becomes inactive, the channel will be 
                          partitioned. 
DISABLED                  The channel line cannot be used: it is not 
                          scanned for activity. 
ENABLED                   The channel line is available. 
PARTITIONED               The channel line is unavailable to any 
                          user: it is removed from system use. 
UNINITIALIZED             The channel line has never been used. 
  Channel Table Element         CONFIG/Default Setting Option    Default 
Attribute                     ATTR                             * 
Auto logon                    LOGON (CONFIG only)              No 
Auto logon failed             Not Settable                     No 
Break required                BREAK REQUIRED                   No 
CCPDWNLD                      Not Settable                     No 
Clock                         CLOCKING                         No 
Debug                         Not Settable                     No 
Device ID                     Not Settable                     ** 
Direct Connect                HARDWIRE                         Yes 
Download                      Not Settable                     No 
EXT Device ID                 Not Settable                     ** 
Input                         INPUT                            Yes 
Output                        OUTPUT                           Yes 
Profile                       PROFILE                          No 
Remote host                   Not Settable                     No 
Resource                      RESOURCE                         * 
Status                        Not Settable                     Not ready 
SYSID                         Not Settable                     0 
Input CCB Count               Not Settable                     0 
RE_ENB                        REENABLE                         Yes 
Enable                        ENABLE                           Yes 
First device on Cntrlr        Not Settable                     No 
Output CCB Count              Not Settable                     0 
LCT55                         Not Settable                     0 
Input CCB Status ptr valid    Not Settable                     No 
Output DCB Status ptr valid   Not Settable                     No 
Drop DTR                      DROPDTR                          No 
Auto baud                     SPEED                            Yes 
Line speed                    SPEED                            300 
Bug                           Not Settable                     No 
DC1DC3 Network flow control   FLOW CONTROL                     No 
Disable Host down             DISABLEHOSTDOWN                  No 
Kill Host down                KILLHOSTDOWN                     No 
Enable Host up                Not Settable                     No 
Send Salutation               SALUTATION                       Yes 
Echo logon                    ECHOLOGON                        No 
Dead                          Not Settable                     No 
Read Timeout period           READTIMEOUT                      0 
Logon Timeout period          LOGONTIMEOUT                     0 
TP Timeout period             TPTIMEOUT                        0 
Input buffer byte size        BUFSIZ                           32 
Interrupt count               Not settable                     0 
Block                         BLOCK                            0 
Unblock                       UNBLOCK                          0 
__________ 
*Set by looking up the device id (see RESOURCE_DEFAULTS). 
**Set by interrogating the device. 
The options are:  ATTRIBUTE, CHAN, FULL, RESOURCE, and STATE.  Enter: HELP 
(NETCON) CHANTBL_PARAMETERS parameter for a description of a specific 
parameter.  For a description of all parameters, enter:  ??. 
  Option     Description 
ATTRIBUTE  Specifies a four digit hexadecimal number in the Channel 
           Table.  The display will be limited to lines with the 
           specified ATTRIBUTE(s).  See CONFIG_OPTIONS and 
           RESOURCE_DEFAULTS. 
CHAN       If termspec is specified, the display is limited to the 
           specified lines. 
FULL       If FULL is specified, the complete channel table is 
           displayed for each line; otherwise, only a summary is 
           displayed for each line.  If only one line is specified, 
           the display defaults to FULL.  (See Usage Notes and 
           Example.) 
RESOURCE   Resource is specified as a 2-character string.  The 
           display will be limited to lines with the specified 
           RESOURCE(s). 
STATE      The display will be limited to lines where the STATE(s) 
           is one or more of the following: 
               BU[SY] 
               BU[SY] D[ISABLE] P[ENDING] 
               BU[SY] P[ARTITION] P[ENDING] 
               DIAG 
               DIS[ABLED] 
               EN[ABLED] 
               L[INE] P[ROFILE] PE[NDING] B[USY] 
               L[INE] P[ROFILE] PE[NDING] B[USY] D[ISABLED] PE[NDING] 
               L[INE] P[ROFILE] PE[NDING] E[NABLED] 
               N[OT] R[EADY] 
               PART[ITIONED] 
               RE[MOTE] DE[BUG] 
               UN[INIT] 
Example: 
DI CHANTBL N=9 .400 TO .800, ST(PART,BUSY), RES(CL) 
means display a summary channel table line for each channel 
between .400 to .800 whose state is partitioned or busy and that 
has a resource of CL. 
00001
00002
00003
00004
00005
CONFIG
To list a brief description of all commands, type ??.  To list a brief 
description of a specific command, type: 
HELP (NETCON) COMMANDS command 
Valid commands are BOOT, CONFIG, DATE, DEFAULT, DEFINE, DELETE, DIRECTORY, 
DISABLE, DISCONNECT, DISPLAY, DO, ENABLE, END, ENTER, ERASE, EXIT, HELP, KILL, 
OUTPUT, PARTITION, PRINT, QUIT, RESET, RETURN, SELECT, SET, TIME, and UPDATE. 
  Command        Description 
  BOOT 
                 Boots a local FEP. 
  CON[FIG] 
                 Changes attributes of a line or range of lines. 
  {DATE|TIME} 
                 Displays the current (host) system date and time. 
  DEFAULT 
                 Defines default attributes for all lines associated with a 
                 handler. 
  DEF[INE] 
                 Defines a network node or link. 
  DELETE 
                 Deletes a network node, a pseudo resource within a node, a 
                 network link, or a line configuration. 
  {DIRECTORY|DIR} 
                 Changes the default account and packset. 
  DIS[ABLE] 
                 Disables a line or range of lines. 
  DISC[ONNECT] 
                 Specifies that a line or range of lines is to be 
                 disconnected. 
  DI[SPLAY] 
                 Displays boot, configuration, link, status and other network 
                 information. 
  {DO|!} 
                 Enables IBEX command execution. 
  EN[ABLE] 
                 Enables a line or range of lines. 
  {E[ND]|[E]X[IT]|Q[UIT]} 
                 Terminates NETCON as an on-line processor. 
  ENTER 
                 Invokes a CP-6 ADAPT dialog from within this processor. 
  ERASE 
                 Deletes accumulated output for logical devices. 
  HELP 
                 Displays information about NETCON and other processors. 
  KI[LL] 
                 Immediately stops all activity on a line or range of lines. 
  OUTPUT 
                 Directs processor output to a destination. 
  PART[ITION] 
                 Removes a line or range of lines from system use and makes 
                 them available for test and diagnostics. 
  PRINT 
                 Directs that accumulated output for logical devices be sent 
                 to destinations immediately. 
  RES[ET] 
                 Restores the default configuration for a line or range of 
                 lines. 
  RET[URN] 
                 Returns to use a line or range of lines removed from system 
                 use by a PARTITION command. 
  SEL[ECT] 
                 Selects a node, handler, or storage parameter for further 
                 processing. 
  SET 
                 Sets parameters affecting FEP performance or controls 
                 tracing. 
  UPDA[TE] 
                 Changes the definition of a node and initiates an on-line 
                 network configuration update. 
00011
00001
00002
00003
00004
00005
00004
00005
00006
00010
00007
00008
00009
00010
00011
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
00013
00021
00022
00023
00024
00003
00025
00013
COMMANDS
Format: 
CON[FIG] termspec loption[,loption]... 
Parameters: 
termspec    identifies terminals in the format termid [TO termid].  See: HELP 
(NETCON) TERMSPEC_PARAMETER. 
loption    specifies one or more of the line configuration options If more 
than one option is specified, the options are separated with commas.  (see: 
HELP (NETCON) CONFIG_OPTIONS). 
Description: 
The CONFIG command establishes line configuration criteria for the specified 
termid on the selected FEP. 
The CONFIG command is used to change the attributes of a line when attributes 
other than the defaults are desired.  Configuration options take effect the 
next time the line becomes active. 
HASP, 2780, 3780, and 3270 all use SUPER-defined termnames.  A termname is 
associated with a specific line by using the termname as the logon string for 
the line (i.e., CONFIG .1400 LOGON = '3270LINE').  Once the association is 
made, care should be taken to thereafter refer to that line in CONFIG commands 
using the termname, not the channelnum.  CONFIGuration of the channelnum 
(although it may be reflected in :NETCON) will be ignored in the FEP. 
The CONFIG_OPTIONS topic lists the line configuration attributes that can be 
set via the CONFIG and DEFAULT commands.  Some attributes are set via the 
keywords YES, NO or DC.  YES specifies that the attribute is set on; NO 
specifies the attribute is set off.  DC specifies the attribute value is not 
to be changed by the CONFIG command.  If an attribute specification includes a 
decimal value, the value -1 specifies DC. 
The CHANNEL_TABLE_DEFAULTS topic lists the contents of the Default Channel 
Table, specifies the options used to set elements in that table, and lists the 
default values for each element. 
00002
00001
The options are: ATTR, BLOCK, BREAKREQUIRED, BUFSIZE, CLOCKING, 
DISABLEHOSTDOWN, DROPDTR, ECHOLOGON, ENABLE, FLOW_CONTROL, HARDWIRE, INPUT, 
KILLHOSTDOWN, LOGON, LOGONTIMEOUT, OUTPUT, PROFILE, READTIMEOUT, REENABLE, 
RESOURCE, SALUTATION, SPEED, TPTIMEOUT, and UNBLOCK. 
Enter: HELP (NETCON) CONFIG_OPTS option 
for a description of a specific option. 
For a description of all options, enter: ??. 
  Option      Explanation 
  ATTR=.n 
              Specifies a 4-digit hexadecimal number.  This option is used 
              with the RESOURCE option.  A line is associated with a handler 
              if its RESOURCE value matches the handler's RESOURCE value 
              parameter, and if its ATTR value matches the handler's ATTR 
              parameter in those bit-positions where the latter has one-bits, 
              i.e., ATTR-handler-parameter = ATTR-handler-parameter & 
              ATTR-channel-table.  The default is .0, which means DC.  See: 
              HELP (NETCON) RESOURCE_DEFAULTS.  It is recommended that the 
              defaults be used.  However, when reconfiguring devices it may be 
              necessary to respecify the attributes to properly reconfigure 
              the line. 
  BL[OCK] = n 
              Sets a character transmission blocking value for BISYNC (binary 
              synchronous), and UNITREC (unit record device) handlers.  n is a 
              maximum number of characters to be allowed to accumulate in the 
              FEP before blocking transmission from the HOST (see the UNBLOCK 
              option).  If -1 is specified for the CONFIG for both the line 
              and the default for the handler, block defaults to 1000 for 
              BISYNC lines and 700 for UNITREC lines. 
  BRE[AK]R[EQUIRED] = {YES|NO|DC} 
              Determines whether a break is required before a hardwired, 
              asynchronous terminal can log on.  YES specifies that the BREAK 
              key must be depressed before the terminal can receive a logon 
              message.  NO specifies that no break is required.  The default 
              is DC. 
  BUF[SIZE] = n 
              Sets the asynchronous buffer size (in bytes) for asynchronous 
              (only) handlers.  Note that the actual buffer allocated in the 
              FEP is rounded up, if necessary, to the next power of 2; e.g., 
              BUFSIZE=100 results in allocation of a 128-byte buffer.  The 
              maximum size that can be specified for n is 16384.  The default 
              is -1, which means DC. 
  CL[OCKING] = {YES|NO|DC} 
              A clocking signal is to be sent on the line from the FEP.  Used 
              for direct-connect BSC devices and RFEPs that are not connected 
              to a modem or modem-eliminators.  For RFEP direct connections, 
              CLOCKING=YES should be specified in the local FEP but not in the 
              RFEP.  Not applicable for asynchronous devices.  The default is 
              DC. 
              Use of this option requires the following hardware 
              considerations: 
              1.  A special cable that crosses transmit and receive as well as 
              the clocking signals must be used between the FEP and the device 
              or RFEP.  The Bull part number for this cable is 60128766-001 
              Revision C.  It must be revision C. 
              2.  The fixed rate clock switch on the CIB (MLCP) to which the 
              device is connected must be set as follows.  Note that there is 
              only one clock per CIB (MLCP) for all devices attached to it 
              that are using the CLOCKING option. 
              Clock Rate                        Switch Setting 
              (in Bits per Second)              (Hexadecimal) 
              --------------------              -------------- 
                       800                              1 
                     1,200                              2 
                     1,760                              3 
                     2,152                              4 
                     2,400                              5 
                     4,800                              6 
                     9,600                              7 
                    14,400                              8 
                    19,200                              9 
                    28,800(a)                           A 
                    38,400(a)                           B 
                    57,600(a)                           C 
                (a)  Maximum rate depends on adapter type 
                     (channel interface). 
  DIS[ABLEHOSTDOWN] = {YES|NO|DC} 
              Specifies whether or not the line is disabled when the host 
              disconnects.  The default is NO. 
  DR[OPDTR] = {YES|NO|DC} 
              Specifies whether or not the FEP is to drop the DTR signal (Data 
              Terminal Ready) when the line does a logical (e.g., !OFF) or 
              physical disconnect.  Used when connecting to some private or 
              public networks.  The default is DC. 
  EC[HOLOGON] = {YES|NO|DC} 
              Specifies whether or not the logon is to be echoed.  The default 
              is DC. 
  EN[ABLE] = {YES|NO|DC} 
              Specifies whether or not this line is to be enabled (i.e., 
              allowed to accept users) when the FEP is booted.  The default is 
              DC. 
  FL[OW] C[ONTROL] = {YES|NO|DC} 
              Specifies whether or not DC1/DC3 is being used to control 
              asynchronous device line output, but not by the device itself. 
              YES implies some sort of connection between the ASYNC line and 
              the device (such as a network) that requires DC1 and DC3 to be 
              honored to control output.  Note that a better method of 
              effecting this sort of flow control is the manipulating of the 
              FEP's CTS (clear to send) RS-232 line.  Also note that this flow 
              control differs from setting DVCFLWCTRALG=DC1DC3 in the device 
              profile in that this flow control buffers pads.  The default is 
              DC. 
  HARD[WIRE] = {YES|NO|DC} 
              Specifies whether or not the line is hardwired to the FEP, not 
              connected through dial-up modems.  The default is DC. 
  IN[PUT] = {YES|NO|DC} 
              Specifies whether or not this line allows input to the FEP.  The 
              default is DC. 
  KIL[LHOSTDOWN] = {YES|NO|DC} 
              Specifies whether or not this line is killed when the host 
              disconnects.  The default is NO. 
  LO[GON] = {'string'|NONE} 
              Specifies a logon string to be supplied to the host at connect 
              times.  Single quotes around the string are required. 
              Subsequent ENABLE commands for a line do not affect a previously 
              defined logon string.  Specifying NONE eliminates a previously 
              defined logon string.  The default is NONE. 
              Specifying a logon string provides for the "automatic" logon of 
              terminals.  A logon string is required for all non-ASYNC lines 
              except those where CP-6 is acting as a master intelligent remote 
              batch terminal (IRBT). 
              If an automatic logon attempt fails, the line will be 
              disconnected but remain enabled unless HARDWARE=YES, 
              BREAKREQUIRED=NO and SPEED is not AUTO.  In this case, the line 
              will be ignored until it is reconnected.  The reconnection can 
              be caused externally (e.g., by turning the device off and on), 
              or internally by a disconnect or kill-enable operation.  This 
              will happen automatically when the logon timeout period expires. 
              LOGON is not valid for the DEFAULT command. 
  LOGONTI[MEOUT] = n 
              Specifies a time in minutes for timeout of the logon process.  A 
              value of zero specifies no time out.  The default is -1, which 
              means DC. 
  OU[TPUT] = {YES|NO|DC} 
              Specifies whether or not this line allows output from the FEP. 
              The default is DC. 
  PRO[FILE] = {'string'|NONE} 
              Specifies an 11-character SUPER-defined profile for the line. 
              The value specified here will override the handler default and 
              user authorization but not the logon string.  Single quotes 
              around the string are required.  Specifying NONE eliminates a 
              previously defined profile.  The default is NONE. 
  READTI[MEOUT] = n 
              Specifies a time in minutes for timeout of a read to a terminal 
              for other than logons or forms processing (TP).  A value of zero 
              specifies no time out.  The default is -1, which means DC. 
  REEN[ABLE] = {YES|NO|DC} 
              Specifies whether or not a line is to be allowed to logon again 
              after a logoff.  The default is DC. 
  RES[OURCE] = rescode 
              Specifies the general class of device to be assigned in the 
              Channel Table.  rescode is one of the following: 
              CL  Communication Line 
              DK  Diskette 
              HL  Host Link 
              UR  Unit Record 
              Any 2-character string 
              This option is used with the ATTR option.  See: HELP (NETCON) 
              RESOURCE_DEFAULTS 
  SA[LUTATION] = {YES|NO|DC} 
              Specifies whether or not salutation is to be sent at logon time. 
              The default is DC. 
  SP[EED] = {speed|AUTO} 
              Specifies the line speed of the line.  AUTO implies that the FEP 
              will determine the speed for asynchronous terminals by autobaud 
              methods.  The default is AUTO.  The valid values for speed are: 
                  50             200             1800 
                  75             300             2000 
                 110             600             2400 
                 134            1050             4800 
                 150            1200             9600 
                                                19200 
  TPTI[MEOUT] = n 
              Specifies the number of minutes before a read for a forms 
              processing (TP) terminal is timed out and the terminal is 
              disconnected.  The default is -1, which means DC. 
  UNBL[OCK] = n 
              Sets a character transmission unblocking value for BISYNC 
              (binary synchronous) and UNITREC (unit record device) handlers 
              by setting the threshold for resuming character transmission.  n 
              specifies the number of characters at which to unblock.  If -1 
              is specified for the CONFIG for both the line and the default 
              for the handler, unblock defaults to 600 for BISYNC lines and 
              400 for UNITREC lines. 
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
CONFIG_OPTIONS
Format: 
{DATE|TIME} 
Description: 
The DATE command requests a display of the current system date and time.  The 
keywords DATE and TIME are synonyms. 
Example: 
A display formatted as follows is produced when the DATE or TIME command is 
issued: 
mmm dd 'yy  hh:mm 
For example: 
JUL 25 '86  12:08 
00001
00002
DEFAULT
DEFINE
Format: 
DEFAULT [H[ANDLER]=]handlername loption[,loption] ... 
Parameters: 
handlername    is either one of the following system-defined standard handler 
names or a 1 to 8 character user-defined handler name for a special handler. 
The system-defined, standard handler names are: 
ASYNC    = Asynchronous 
BISYNC   = Bisynchronous 
COUPLER  = Host coupler handler 
HDLCX25  = X.25 protocol handler 
NODEADMN = Network node administrator 
UNITREC  = FEP unit record handler 
loption    specifies one or more of the line configuration options (see: HELP 
(NETCON) CONFIG_OPTIONS).  If more than one option is specified, the options 
are separated with commas. 
Description: 
The DEFAULT command establishes default line configuration criteria for a 
handler in the FEP.  The handler uses this default configuration to configure 
lines that the system manager has not specifically configured with the NETCON 
CONFIG command, and to provide values for any CONFIG option that the system 
manager left as DC or -1 in the CONFIG record for a line.  Default options 
take effect when the FEP is booted. 
00002
00001
CONFIG_OPTIONS
CONFIG_OPTIONS
Format: 
         {                 [{, C[ONTROL] = hostname                  }]   } 
         {[NODE =] nodenum [{, L[INK] {= .channelnum|[=](channellist)}]...} 
DEF[INE] {                 [{, N[AME] = nodename                     }]   } 
         {                 [{, T[YPE] = nodetype                     }]   } 
         {                                                                } 
         {L[INK] = .channelnum [, .channelnum] ...                        } 
Parameters: 
nodenum    is a decimal integer (1-n) that assigns the node a number.  n is 
one less than the number of nodes defined via TIGR. 
hostname    is a 1 to 8 character alphanumeric name that identifies the host 
node that controls a FEP. 
 .channelnum    is a hexadecimal number that is the address of the physical 
channel.  The period preceding the hexadecimal value is required. 
channellist    is a list of .channelnum values enclosed in parameters.  The 
numbers of the list are separated by commas. 
nodename    is a 1 to 8 character alphanumeric value that assigns a name to 
the node.  The default is NODEnnnn; where nnnn is the (decimal) node number. 
nodetype    is one of the following: 
    DEBUG    specifies a FEP node to be used for debugging purposes.  A node 
    with a type of DEBUG will not reboot when the system comes up.  Only DEBUG 
    nodes should be booted with the NOTIME option. 
    FEP    specifies a FEP node. 
    HOST    specifies a CP-6 host node. 
    ME    specifies the current CP-6 host. 
    RFEP    specifies a remote FEP node. 
The default nodetype is FEP. 
Description: 
The DEFINE command is used to define nodes and links. 
The DEFINE NODE command: 
o   Assigns the node a node identification.  For host nodes, both a number and 
    name are assigned to the node via the DEFINE command.  For local FEP 
    nodes, the FEP node number is assigned via the TIGR processor; the name is 
    assigned via this command.  For remote FEP nodes, a number and name are 
    assigned to the node and a (physical) channel address must be specified in 
    the DEFINE command. 
o   For local FEP nodes, builds a FEP boot record that contains the standard 
    FEP monitor (M:FEP.:SYS), library (:SYS), and the NODEADMN, COUPLER and 
    ASYNC handlers from :SYS.  Also, builds default records for the NODEADMN, 
    COUPLER and ASYNC handlers.  For RFEP nodes, builds a FEP boot record that 
    contains M:FEP.:SYS, library (:SYS) and the NODEADMN, HDLCX25 and ASYNC 
    handlers from :SYS.  Also builds default records for the NODEADMN, HDLCX25 
    and ASYNC handlers.  The ASYNC handler record is set to BOOTTIME=NO. 
o   Determines which host controls each FEP in the network.  The controlling 
    host: 
    o   at boot time, provides the configuration information for the FEP. 
    o   provides the logon salutation. 
    o   is the host a user will logon to if a host is not specified in the 
        logon string. 
o   Assigns the node a type. 
The newly defined node will be recognized as part of the network immediately. 
The DEFINE LINK command identifies any link lines that need to be used to 
connect an RFEP to the network.  This command takes effect when the FEP is 
booted.  The MAXLINKS parameter determines how many links may be defined.  The 
default is 5. 
Examples: 
HOST    *DEF 16,N=HOSTA, T=HOST 
HOST    *DEF N=20,NAME=NODE0020,TYPE=FEP, C=HOSTA 
HOST    *SEL N=20 
HOST    *DEF LINK=.1400 
00002
00003
00001
Format: 
DELETE {[N[ODE]=]nodenum                      } 
       {PSEUDO=pseudoname                     } 
       {L[INKS]={.channelnum[,.channelnum]...}} 
                {ALL                         }} 
       {C[ONFIG] termspec|ALL                 } 
Parameters: 
nodenum    is the 1 to 4 digit node number. 
pseudoname    is a 1 to 8 character alphanumeric name. 
 .channelnum    is the 3 or 4 digit hexadecimal address of the physical 
 channel. 
ALL    specifies all links on a node or all termspecs. 
termspec    identifies terminals in the format termid [TO termid].  (See The 
Termspec Parameter.) 
Description: 
The DELETE command is used to remove a node, a pseudo resource, a link or a 
configuration record from the network.  The DELETE NODE command takes effect 
immediately.  The DELETE PSEUDO and DELETE LINK and DELETE CONFIG commands 
take effect when the FEP is booted. 
00002
00001
DISPLAY
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
HOST    *DIRECTORY .SYSLIB 
This command directs that subsequent fids that do not include an account are 
to default to the .SYSLIB account and the packset associated with that 
account. 
HOST    *DIRECTORY DP#UTIL.Y 
This command specifies that subsequent fids that do not include an account are 
to default to the Y account on the packset named UTIL. 
HOST    *DIRECTORY RESET 
This command re-establishes the running account and its associated packset as 
the default. 
00002
00003
00001
Format: 
DIS[ABLE] termspec 
Parameters: 
termspec    identifies terminals in the format termid [TO termid].  See HELP 
(NETCON) TERMSPEC_PARAMETER. 
Description: 
The DISABLE command sends a message to the SELECTed FEP to disable specified 
termid(s).  The DISABLE command is used to gracefully disable a line or range 
of lines.  If a DISABLE references a line currently supporting a logged-on 
user, the line will be disabled when the user logs off.  If there is no 
current user, the line will be disabled immediately.  Once disabled, no logons 
will be allowed until a subsequent ENABLE command is issued. 
It is important to note that this command does not necessarily prevent a modem 
connected to the line from answering.  When using this command, it will often 
be desirable to manually busy-out a connected modem, unless the modem will 
answer only if DTR is raised. 
The effect of the DISABLE command is immediate. 
00002
00001
Format: 
DISC[ONNECT] termspec 
Parameters: 
termspec    identifies terminals at the FEP in the format termid [TO termid]. 
See HELP (NETCON) TERMSPEC_PARAMETER. 
Description: 
The DISCONNECT command sends a message to the SELECTed FEP to disconnect the 
specified termid(s) immediately.  Note that the line(s) remain in an enabled 
state. 
The effect of the DISCONNECT command is immediate. 
00002
00001
Format: 
           {BOOT[INFO] [[N[ODE]=]nodeid]                  } 
           {BOOT P[ARAMS]                                 } 
           {CH[ANTBL] [N[ODE]=node] [option[,option]...]  } 
           {CON[FIGURE] [N[ODE=]nodeid] {termspec|FULL};  } 
           {  [[U[SING]] handlername]                     } 
           {DEF[AULT] [H[ANDLER]=]handlername [N=nodeid]  } 
DI[SPLAY] ({HAND[LER] P[ARAMS]                            }) 
           {LCP6 P[ARAMS]                                 } 
           {LINKS                                         } 
           {[NET[WORK]|NODE] [nodeid [,nodeid]...]        } 
           {PSEUDO                                        } 
           {ST[ATUS][/L[ONG]] [[NODE=]nodeid [,nodeid]...]} 
           {parameterlist                                 } 
Parameters: 
BOOTINFO    requests a display of FEP boot handler and library data.  The 
parameters are described under HELP (NETCON) BOOTINFOPARAMS.  nodeid 
identifies a node name or number. 
BOOT PARAMS    requests a display of the following boot time parameters, 
ACCTS, APESSN, CBUFFER, DEVICES, HMI, IOP, KEEPDELTA, LDCT, MAXLINKS, MUIS, 
SFILE and TCTX parameters.  The parameters are described under HELP (NETCON) 
BOOTPARAMS. 
CHANTBL    requests a display of current Channel Table information.  (See 
Examples).  If node is specified, the display is limited to the specified 
node.  option can be any of the following: 
    [CHAN =] termspec 
    FULL 
    RE[SOURCE] [=] (resource[, resource]...) 
    AT[TRIBUTE] [=] ([.]hex-value[,[.]hex-value]...) 
    ST[ATE] [=] (state[, state]...) 
See CHANTBL_PARAMETERS for a description of the option parameters and Examples 
for examples of their use. 
CONFIGURE    requests a display of configuration information.  termspec 
specifies a line or group of lines.  nodeid identifies a node name or number 
and, if specified must be preceded by the keyword NODE.  If nodeid is not 
specified, the node must previously have been selected via a SELECT command. 
If a node is specified and a SELECT command has previously been issued, the 
node specified in the DISPLAY command will not replace the SELECTed node in 
succeeding NETCON commands.  FULL displays all of the lines configured.  USING 
handlername requests that the display include handler default values for 
unconfigured items.  (See Usage Notes.) 
DEFAULT    requests a display of default handler configuration information for 
the specified handler.  (See Examples.)  nodeid identifies a node name or 
number and, if specified must be preceded by the keyword NODE.  If nodeid is 
not specified, the node must previously have been selected via a SELECT 
command.  If a node is specified and a SELECT command has previously been 
issued, the node specified in the DISPLAY command will not replace the 
SELECTed node in succeeding NETCON commands.  handlername is one of the 
following:  ASYNC, BISYNC, COUPLER, HDLCX25, UNITREC, or a user-defined 
handler name. 
HANDLER PARAMS    requests a display of all the handler parameters for the 
specified handler described under HELP (NETCON) HANDPARAMS.  A handler name 
must have been specified via the SEL command before this parameter can be 
specified. 
LCP6 PARAMS    requests a display of all the LCP6 monitor parameters, i.e., 
the CMEM, CMEM_CG, CMEM_GHST, CMEM_HAND, CUSR, CUSR_CG, CUSR_GHST, CUSR_USER, 
CUSR_HAND, MMEM, MMEM_CG, MMEM_GHST, MMEM_HAND, MUSR, MUSR_CG, MUSR_GHST, 
MUSR_USER, MUSR_HAND, QMIN, QUAN and XCON parameters.  The parameters are 
described under HELP (NETCON) LCP6PARAMS. 
LINKS    requests a display of link information (including the number of links 
defined for the node and the physical channel numbers of the links.  (See 
Examples.) 
NETWORK|NODE    requests a listing of the network nodes.  For each node, the 
node number, name, type, links and controlling host are listed.  Both of the 
keywords NETWORK and NODE are optional.  nodeid can be specified as either a 
node number or name.  (See Examples.) 
PSEUDO    requests a listing of the currently defined pseudo resource names. 
See HELP (NETCON) PSEUDOPARAMS. 
STATE    requests a display of the FEP operational state.  (See Examples.) 
/LONG requests a long form of the display.  Either STATE or STATE/LONG can be 
followed by one nodeid or a list of nodeids.  Nodes can be identified by node 
name or node number.  If no node is specified, the status of all nodes will be 
displayed. 
parameterlist    specifies one or more of the following parameters. 
Parameters marked with an <- are display only parameters that cannot be set 
through the SET command.  If more than one parameter is specified, the 
parameters are separated by commas. 
    ACCTS                  IOMEM                  MUSR_H[AND] 
    APESSN                 IOP                    MUSR_U[SER] 
    ATTR                   KEEP[DELTA]            OCQD[BLKSIZ] 
    BLOCK                  LDCT                   OTPBFRBYTSIZBIG 
    CBUFFER                LGNRTRY[NUM]           OTPBFRBYTSIZSML 
    CMEM <-                LINERRD[SCLMT]         PCHANS 
    CMEM_C[G] <-           LINERRLOGB[FRCMT]      QMIN 
    CMEM_G[HST] <-         LINERRLOGL[MT]         QUAN 
    CMEM_H[AND] <-         MAXICQ[TIME]           RCVCQ[BYTSIZ] 
    CMEM_U[SER] <-         M[AX]L[INKS]           RES 
    CUSR <-                MEM                    SF[ILE] 
    CUSR_C[G] <-           MEM_C[G]               SF[ILE_]D[ATA] 
    CUSR_G[HST] <-         MEM_G[HST]             SNDCQ[BYTSIZ] 
    CUSR_H[AND] <-         MEM_H[AND]             SSN[MAX] 
    CUSR_U[SER] <-         MEM_U[SER]             TCTX 
    DEV[ICES]              MMEM                   TYP[AHDBFRLMT] 
    DUMP                   MMR[INTCHC]            UNBLOCK 
    ERRS[ND]               MUIS                   USRPARMn{n|1,2} 
    HMI                    MUSR                   VDH[TRC] 
    HOPCOST                MUSR_C[G]              XCON[TIME] 
    INTLVL                 MUSR_G[HST]            X29MLTMR 
    IOBUF 
See HELP (NETCON) DISPLAY_PARAMETERS for pointers to these parameters. 
Description: 
The DISPLAY command is used to display the current values of boot information, 
the network nodes, pseudo resources, or NETCON-controlled parameters. 
Usage Notes: 
Note that FULL options are available for both DISPLAY CHANTBL and DISPLAY 
CONFIGURE but that they operate differently. 
The display for DISPLAY CONFIGURE is the same whether FULL is specified or 
not.  DISPLAY CONFIGURE FULL means display all configured lines.  Further, if 
a handler name is supplied on a DI CONFIG command, the display will include 
that handler's default values for those items which have not been configured. 
Default values are enclosed in parentheses.  If no handler name is given, 
empty parentheses will be displayed for all defaulted values. 
The display for DISPLAY CHANTBL differs depending on whether or not FULL is 
specified.  If FULL is not specified, a summary display is created (see 
Examples).  If FULL is specified with DISPLAY CHANTBL it means produce a full 
display.  The display will be for either a specific line, a range of lines, or 
all lines, as appropriate. 
Examples: 
!NETCON 
NETCON E04 HERE 
HOST    * SEL N=12 
L6XII   * DI BOOT 
Boot Information for Node L6XII 
Monitor Fid: M:FEP.:SYS 
Library: :SYSTAC 
    user#  name      boot  fid 
      1    NODEADMN  Yes   NODEADMN.:SYS 
      2    HDLCX25   Yes   HDLCX25.:SYS 
      3    ASYNC     No    ASYNC.:SYS 
      4    UNITREC   No    UNITREC.:SYS 
L6XII   * DI CHANTBL .3680 
Termid:  .3680-0-0       Lev: 1  Ttyp:  TTY       Trm name: 
Attributes:  .8001       Echo Logon:     No       Logon Failed:   No 
Autobaud:      Yes       Enable:        Yes       Ntwk flw ctr:   No 
Autologon:      No       Enb hst up:     No       Otp ccb cnt:     0 
Block:           0       Ext Dev Id:  .0000       Otp stt vld:    No 
Break Requird:  No       First Device:   No       Output:        Yes 
Bug:            No       Hand$       .33040       Profile:        No 
CCP loaded:   0000       Inp bfr sz:      0       Re-enable:     Yes 
Clock:          No       Inp ccb cnt:     2       Read Timeout:    0 
Context:    .3F220       Inp stt vld:   Yes       Remote Host:    No 
Dead:           No       Input:         Yes       Resource:       CL 
Debug:          No       Int count:   25483       Send sal:      Yes 
Device Id:   .2118       Kll hst dn:     No       State:        Busy 
Direct cnnct:  Yes       Lct55:         .17       Sub$:       .00000 
Dnld ccp:      Yes       Lgn Timeout:     5       Sysid            3 
Drop DTR:       No       Line Speed:    300       TP Timeout:      0 
Dsb hst dn:     No       Lnk$:       .00000       Unblock:         0 
L6XII   * DI CHANTBL 
DEV  DEV  EXT        CTX            DRC DRP DWN             SND CCB LGN RED 
ADDR ID   ID   ATTR  PTR  RS STATUS CNC DTR LD  ENB INP OTP SLT I O TO  TO 
 400 2017    0 4000     0 DK  Uint  Yes No  No  Yes Yes Yes Yes 0 0   0   0 
 480 2017    0 4000     0 DK  Uint  Yes No  No  Yes Yes Yes Yes 0 0   0   0 
 500 201C    0    0     0 OC  Uint  Yes No  No  Yes Yes Yes Yes 0 0   0   0 
 580 2033    0 8000  CEC0 UR  Enab  Yes No  Yes Yes Yes Yes Yes 0 0   0   0 
 600 2003    0 8000  B140 UR  Enab  Yes No  Yes Yes Yes Yes Yes 0 0   0   0 
 800 2408    0    0     0 HL  Uint  Yes No  No  Yes Yes Yes Yes 0 0   0   0 
 C00 2118    0 8001 3C760 CL  Busy  Yes No  Yes Yes Yes Yes Yes 2 0   0   0 
 C80 2118    0 8001     0 CL  Enab  Yes No  Yes Yes Yes Yes Yes 0 0   5   0 
 D00 2118    0 8001     0 CL  Enab  Yes No  Yes Yes Yes Yes Yes 0 0   5   0 
 D80 2118    0 8001     0 CL  Enab  Yes No  Yes Yes Yes Yes Yes 0 0   5   0 
 E00 2118    0 8001 32460 CL  Busy  Yes No  Yes Yes Yes Yes Yes 2 0   5   0 
     o 
     o 
     o 
L6XII   * DI CON .3680 
Line Configuration for Node# 12 (L6XII) Channel# .3680-0-0 Terminal id 
Logon:        None 
Profile:      PCTX364 
Attribute:     (   )      Block:         (   )      Break Req:     (   ) 
Buffer size:   (   )      Clock:         (   )      Debug:         (   ) 
Dsb hst dwn:   (   )      Drop DTR:      (   )      Echo Logon:    (   ) 
Enable:        (   )      Flow cntrl:    (   )      Hard wired:    (   ) 
Input:         (   )      Kill hst dwn:  (   )      Lgn timeout:   (   ) 
Output:        (   )      Readtimeout:   (   )      Re-enable:     (   ) 
Resource:      (   )      Send Sal:      (   )      Speed:        19200 
TP timeout:    (   )      Unblock:       (   ) 
Note:  Default values are enclosed in parentheses.  No handler was specified 
in the DI CON command, so default values are left blank. 
L6XII   * DI CON .3680 ASYNC 
Line Configuration for Node# 12 (L6XII) Channel# .3680-0-0 Terminal id 
Logon:        None 
Profile:      PCTX364                              (With ASYNC defaults) 
Attribute:    (None)      Block:         (  0)      Break Req:     ( No) 
Buffer size:   (  0)      Clock:         ( No)      Debug:         ( No) 
Dsb hst dwn:   ( No)      Drop DTR:      ( No)      Echo Logon:    ( No) 
Enable:        (Yes)      Flow cntrl:    ( No)      Hard wired:    (Yes) 
Input:         (Yes)      Kill hst dwn:  ( No)      Lgn timeout:   (  5) 
Output:        (Yes)      Readtimeout:   (  0)      Re-enable:     (Yes) 
Resource:     (None)      Send Sal:      (Yes)      Speed:        19200 
TP timeout:    (  0)      Unblock:       (  0) 
Note:  Default values enclosed in parentheses, are read from the ASYNC handler 
default record. 
L6XII   * DI LINKS 
Link information for node L6XII 
      Number of links = 1 
         Link# 0 = .5600 
L6XII   * DI NETWORK 
Node#    Name    Type    Host   Route   Links 
   0   L66A      Host             9 
   1   L6I       Fep     L66A     9 
   2   L6II      Debg    L66B     9 
   3   L6III     Debg    L66A     9 
   4   L6IV      Fep     L66A     9 
   5   L6V       Debg    L66B   None    .4C00 
   6   L6VI      Fep     L66C     9 
   7   L6VII     Debg    L66B   None 
   8   L6VIII    Fep     L66A     9 
   9   L6IX      Fep     L66B   Local 
  10   L6X       Fep     L66B     9 
  12   L6XII     Fep     L66B     9    .4F00    .5400 
  13   L6XIII    Fep     L66A     9 
  15   L6XV      Debg    L66A   None 
  20   L66B      Me 
  21   L66D      Host           None 
  22   L66C      Host             9 
  23   DPS90     Host           None 
  32   DVFEP     Fep     L66A     9    .F000    .F100 
  33   CRFEP     Fep     L66A     9    .9000    .9800 
  34   CP6FEP    Fep     L66A   None 
L6XII   * DI ST 
  Node 0(L66A    ) is running 
  Node 1(L6I     ) is running 
  Node 2(L6II    ) is running 
  Node 3(L6III   ) is running 
  Node 4(L6IV    ) is running 
  Node 5(L6V     ) is disabled 
  Node 6(L6VI    ) is running 
  Node 7(L6VII   ) is disabled 
  Node 8(L6VIII  ) is running 
  Node 9(L6IX    ) is running 
  Node 10(L6X     ) is running 
  Node 12(L6XII   ) is running 
  Node 13(L6XIII  ) is running 
  Node 15(L6XV    ) is disabled 
  Node 20(L66B    ) is disabled 
  Node 21(L66D    ) is disabled 
  Node 22(L66C    ) is running 
  Node 23(DPS90   ) is disabled 
  Node 32(DVFEP   ) is running 
  Node 33(CRFEP   ) is running 
  Node 34(CP6FEP  ) is disabled 
L6XII   *SEL H=HDLCX25 
L6XII   *DI HANDP 
 PARAMETER         CURRENT   :NETCON   DEFAULT   MINIMUM   MAXIMUM 
 INTLVL            36        36        36        12        60 
 MEM               80        80        90        0         65535 
 IOMEM             48        48        128       0         65535 
 RES               CL        CL        CL 
 ATTR              2000      2000      2000      0         FFFF 
 TYPAHDBFRLMT      30        30        30        1         254 
 LINERRDSCLMT      254       254       255       0         255 
 ERRSND            0         0         0         0         7 
 RCVCQBYTSIZ       8192      8192      8192      0         32000 
 SNDCQBYTSIZ       8192      8192      8192      0         32000 
 MMRINTCHC         0         0         0         0         FFFF 
 IOBUF             7         7         7         1         14 
 LINERRLOGBFRLMT   240       240       240       0         65535 
 X29MLTMR          10        10        10        0         255 
00002
00004
00001
00003
See the following topics for a list and description of NETCON DISPLAY and SET 
command parameters: 
    BOOT_PARAMETERS 
    BOOTINFO_PARAMETERS 
    CHANTBL_PARAMETERS 
    HANDLER_PARAMETERS 
    LCP6_PARAMETERS 
    PSEUDO_PARAMETERS 
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
HOST    *DO DI 
means display the current system status 
HOST    *!LDEV LP09 TITLE='report title',PAGE=100,COPIES=3 
means set up a title and page number for a report destination 
00002
00003
00001
END
Format: 
EN[ABLE] termspec 
Parameters: 
termspec    identifies terminals in the format termid [TO termid].  See HELP 
(NETCON) TERMSPEC_PARAMETER. 
Description: 
The ENABLE command sends a message to the SELECTed FEP to enable specified 
termid(s).  The ENABLE command is used to enable a line or range of lines that 
has not been enabled by means of a CONFIG command, or has been previously 
disabled by means of a DISABLE command.  The ENABLE command allows users to 
log on the line(s). 
The effect of the ENABLE command is immediate. 
00002
00001
Format: 
{E[ND]|[E]X[IT]|Q[UIT]} 
Description: 
The END command, and its synonyms QUIT and EXIT, are used to terminate NETCON 
and return control to IBEX. 
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
HOST    *ERASE ALL 
deletes all output accumulated for all logical devices defined for the session 
or job. 
00002
00003
00001
END
The following describes messages that may be sent to communications and 
operator consoles concerning the status of FEPs. 
  Message                               Meaning 
FEP id - RECOVERY INITIATED           An operator initiated BOOT/DUMP/ 
                                      CRASH of FEP id has been started. 
FEP id IS ACTIVE                      Response when an FEP is 
                                      booted/started successfully. 
FEP id reason - RECOVERY INITIATED    An event initiated BOOT/DUMP 
                                      of FEP id has been started 
FEP id REFUSES BOOT/DUMP - reason     FEP id refuses to be booted or 
                                      dumped; the reason explains why. 
FEP id HALTED BY USER                 Some user has halted FEP id. 
FEP id STOPPED                        Response when a STOP FEP Keyin is 
                                      entered, and the FEP is stopped 
                                      normally. 
FEP id STARTED                        Response when a START FEP Keyin 
                                      is entered, and the FEP starts 
                                      normally. 
where: 
    id    represents the logical FEP number as defined via TIGR or 
    NETCON followed, if appropriate, by the FEP name (enclosed in 
    parentheses) assigned via NETCON. 
    reason    indicates that one of the following FEP failure causes 
    is included, as appropriate, in the message: 
        Timed out                 Bad line number 
        Not listening             Bad message format 
        Software crash            Bad function code 
        Coupler failed            Illegal memory access 
        Bad interrupt 
HELP
HANDPARAMS
HANDPARAMS
The handler parameters are: 
ATTR, BLOCK, ERRSND, HOPCOST, IMPTBLMAX, INTLVL, 
IOBUF, IOMEM, LGNRTRYNUM, LINERRDSCLMT, 
LINERRLOGBFRLMT, LINERRLOGLMT, MAXICQTIME, MEM, MMRINTCHC, 
OCQDBLKSIZ, OTPBFRBYTSIZBIG, OTPBFRBYTSIZSML, RCVCQBYTSIZ, 
RES, SNDCQBYTSIZ, SSNMAX, TYPAHDBFRLMT, UNBLOCK, 
USRPARM, and VDHTRC. 
Enter HELP (NETCON) HANDPARAMS parameter 
for a description of a specific handler parameter. 
For a description of all parameters, enter: ??. 
  Parameter         Description                                 Handler 
ATTR              Default ATTRibute specifies the             ASYNC 
                  hexadecimal value associated with the       BISYNC 
                  RESource parameter.  (See CONFIG_OPTIONS.)  COUPLER 
                  These two parameters select the channels    HDLCX25 
                  that a handler will use.  The ATTR value    UNITREC 
                  must be preceded by a period                User- 
                  (i.e., .xxxx).  The handler defaults          defined 
                  for ATTR are: 
                      ASYNC    - .8000 
                      BISYNC   - .1000 
                      COUPLER  - .0000 
                      HDLCX25  - .2000 
                      UNITREC  - .0000 
                  Unit: - None 
                  Minimum: - .0                   Maximum: - .FFFF 
                  Effect: At boot time 
BLOCK ({ALL|speed1[-speed2]|speed1[,speed2]...}) 
                  The BLOCK values specify the amount of      ASYNC 
                  waiting output characters at which          HDLCX25 
                  blocking is to occur.  The value            User- 
                  specified may apply to all line speeds        defined 
                  (ALL), to a range of speeds or to a list 
                  of speeds.  The values that may be 
                  specified for speed and the default 
                  BLOCK values are as follows: 
                  Speed - Block value   Speed - Block Value 
                     (bps)               (bps) 
                     50 - 500            1050 - 500 
                     75 - 500            1200 - 720 
                    110 - 500            1800 - 1080 
                    134 - 500            2000 - 1080 
                    150 - 500            2400 - 1440 
                    200 - 500            4800 - 2000 
                    300 - 500            9600 - 2000 
                    600 - 500           19200 - 2000 
                  Unit: Characters              Maximum: 65535 
                  Minimum: Current UNBLOCK 
                           value 
                  Effect: Immediate for new logons 
ERRSND            ERRor SeND specifies the error severity     ASYNC 
                  level (0-7) that will cause error           BISYNC 
                  logging.  The default, which is             COUPLER 
                  0, means to log all errors.                 HDLCX25 
                                                              UNITREC 
                  Unit: Severity level          Default: 0    User- 
                  Minimum: 0                    Maximum: 7      defined 
                  Effect: Immediate 
HOPCOST           Quality of service (QOS) penalty            NODEADMN 
                  for a message passing through the           User- 
                  associated node.                              defined 
                  Unit: QOS unit                Default: 10 
                  Minimum: 0                    Maximum: 255 
                  Effect: Immediate 
IMP[TBLMAX]       IMP TaBLe MAXimum specifies the maximum     ASYNC 
                  number of words of memory available for     BISYNC 
                  each window's Imp table.  The minimum       HDLCX25 
                  of 0 will disallow imps.  Otherwise, the    User- 
                  smallest useful limit is approximately        defined 
                  100 (a table with no definition 
                  occupies 92 words).  Each definition 
                  requires 3 words plus the number of 
                  bytes of text it defines (plus 3 bytes 
                  per TEXT keyword after the first TEXT 
                  keyword). 
                  Unit: Words of memory         Default: 1024 
                  Minimum: 0                    Maximum: 32767 
                  Effect:  Immediate 
INTLVL            INTerrupt LeVeL specifies the               ASYNC 
                  level of the interrupt to be                BISYNC 
                  used by the handler.                        COUPLER 
                                                              HDLCX25 
                  Defaults for the LCP-6 Handlers:            UNITREC 
                    ASYNC     - 32                            User- 
                    BISYNC    - 26                              defined 
                    COUPLER   - 50 
                    HDLCX25   - 36 
                    UNITREC   - 30 
                  Unit: Interrupt level         Default: 0 
                  Minimum: 12                   Maximum: 60 
                  Effect: At boot time 
IOBUF             Input Output BUFfer specifies               HDLCX25 
                  the maximum number of buffers               User- 
                  that the HDLCX25 buffer manager               defined 
                  is to maintain before releasing 
                  buffers to the FEP buffer manager. 
                  IOBUF is used to improve HDLCX25 
                  handler performance by tuning 
                  the acquisition and release of 
                  I/O buffers. 
                  Unit: Page                    Default: 7 
                  Minimum: 1                    Maximum: 14 
                  Effect: At boot time 
IOMEM             Input/Output MEMory specifies the           HDLCX25 
                  amount of memory to be used for             User- 
                  input/output buffers.  See                    defined 
                  IO_BUF_FORMULAS for formulas for 
                  establishing input/output buffers. 
                  The default for HDLCX25 is 128. 
                  Unit: Page                    Default: 0 
                  Minimum: 0                    Maximum: 2048, 
                                                but IOMEM plus 
                  Effect: At boot time          MEM cannot 
                                                exceed 2304. 
LGNRTRYNUM        LoGoN ReTRY NUMber specifies                NODEADMN 
                  the number of times to allow a              User- 
                  user to retry his logon string                defined 
                  after the initial attempt failed. 
                  Minimum: 0 indicates that the user 
                  is allowed one attempt to logon. 
                  Unit: Logon attempt 
                  Minimum: 0                    Default: 6 
                  Effect: At boot time          Maximum: 255 
LINERRDSCLMT      LINE ERRor DiSConnect LiMiT specifies       ASYNC 
                  the maximum number of framing and           BISYNC 
                  parity errors, or CLA overruns, to          HDLCX25 
                  permit in one minute.  If this limit        User- 
                  is exceeded, the line is disconnected.        defined 
                  A value of 255 specifies no disconnection 
                  on errors.  This option takes effect 
                  with the next occurrence of the error. 
                  Unit: Errors/minute           Default: 255 
                  Minimum: 0                    Maximum: 255 
                  Effect: Immediate 
LINERRLOGBFRLMT   LINE ERRor LOG BuFfeR specifies the         HDLCX25 
                  maximum amount of buffer space              User- 
                  used by HDLCX25 for queuing line              defined 
                  error entries on each line. 
                  Unit: Words of memory      Default: 240 (@ 10 entries) 
                  Minimum: 0                 Maximum: 2**16-1 
                  Effect:  At boot time 
LINERRLOGLMT      LINE ERRor LOG LiMiT specifies the          ASYNC 
                  maximum number of framing and parity        BISYNC 
                  errors, or CLA overruns, to permit          HDLCX25 
                  before logging the errors.  A value         User- 
                  of 255 specifies not to log errors.           defined 
                  This option takes effect with the 
                  next occurrence of the error. 
                  Default for ASYNC: 255 
                  Default for HDLCX25: 254 
                  Unit: Error 
                  Minimum: 0                    Maximum: 255 
                  Effect: Immediate 
MAXICQTIME        MAXimum Input Circular Queue TIME           COUPLER 
                  specifies the time between interrupts,      User- 
                  FEP to host.                                  defined 
                  Unit: ticks (.133 secs)       Default: 1 
                  Minimum: 1                    Maximum: 120 
MEM               MEMory specifies the amount of memory       ASYNC 
                  to be used for context buffers.  See        BISYNC 
                  IO_BUF_FORMULAS for formulas for            COUPLER 
                  establishing context buffer sizes.          HDLCX25 
                                                              NODEADMN 
                  Defaults for the LCP-6 Handlers:            UNITREC 
                    ASYNC     - 192                           User- 
                    BISYNC    - 80                              defined 
                    COUPLER   - 2 
                    HDLCX25   - 90 
                    NODEADMN  - 50 
                    UNITREC   - 32 
                  Unit: Page                    Default: 0 
                  Minimum: 0                    Maximum: 2048, 
                                                but MEM plus 
                  Effect: At boot time          IOMEM cannot 
                                                exceed 2304. 
MMRINTCHC         MeMoRy INiTialization and CHeCking          ASYNC 
                  specifies various memory pool parameters    BISYNC 
                  in the form of flags combined as a          HDLCX25 
                  4-digit hexadecimal value as follows:       NODEADMN 
                                                              UNITREC 
                  Value  Meaning                              User- 
                  -----  -------                                defined 
                  .8000  specifies that a bitmap is to be 
                         used to help diagnose buffer 
                         management problems, at a small 
                         expense in processing and space 
                         overhead. 
                  .4000  specifies that each buffer is to 
                         be initialized when allocated to 
                         a repeating pattern consisting 
                         of the four ASCII characters 
                         'BUSY' followed by the 
                         8-hexadecimal digit string 
                         .BADaaaaa, where "aaaaa" is the 
                         address of the calling program. 
                         This option is helpful in 
                         determining the cause for lost 
                         memory and in finding problems 
                         due to use of un-initialized 
                         data, since any reference to a 
                         pointer in such an area will 
                         trap immediately. 
                  .2000  specifies that the chains of 
                         free buffers are to be validated 
                         before each attempt to allocate 
                         or release a buffer is made. 
                  .1000  specifies that the chains are to 
                         be validated after each buffer 
                         allocation has been performed. 
                  .0800  specifies that the chains are to 
                         be validated after each buffer 
                         release has been performed. 
                  The flags may be specified in any 
                  combination by OR-ing or adding the 
                  values of the desired ones together. 
                  Any of the flags may be changed at any 
                  time except the "bitmap" one, which is 
                  effective only at boot time. 
                  Unit: -                       Default: .8000 
                  Maximum: .FFFF                Minimum: .0 
                  Effect: Immediate 
OCQDBLKSIZ        Output Circular Queue DeBLocK SIZe          COUPLER 
                  specifies the maximum output queue block    User- 
                  size that can be sent through the L6          defined 
                  coupler (larger values are broken up 
                  into blocks of this size). 
                  Unit: Byte                    Default: 4096 
                  Maximum: 32768                Minimum: 1024 
                  Effect: At boot time 
OTPBFRBYTSIZBIG   OuTPut BuFfeR BYTe SIZe BIG specifies       ASYNC 
                  the asynchronous output buffer size for     User- 
                  big buffers.  (Note that the size of          defined 
                  the buffer allocated is rounded up, 
                  if necessary, to the next power of 2.) 
                  This parameter takes effect 
                  immediately. 
                  Unit: Byte                    Default: 256 
                  Minimum: 32                   Maximum: 1024 
                  Effect: Immediate 
OTPBFRBYTSIZSML   OuTPut BuFfer BYTe SIZe SMalL specifies     ASYNC 
                  the asynchronous output buffer size for     User- 
                  small buffers.  (Note that the size of        defined 
                  the buffer allocated is rounded up, if 
                  necessary, to the next power of 2.) 
                  This parameter takes effect immediately. 
                  Unit: Byte                    Default: 32 
                  Mimimum: 32                   Maximum: 1024 
                  Effect: Immediate 
RCVCQBYTSIZ       ReCeiVe Circular Queue BYTe SIZe specifies  ASYNC 
                  the amount of space to be used for the      BISYNC 
                  Receive Circular Queue for the handler.     COUPLER 
                                                              HDLCX25 
                  Defaults for the LCP-6 Handlers:            NODEADMN 
                    ASYNC     - 4200                          UNITREC 
                    BISYNC    - 4200                          User- 
                    COUPLER   - 8192                            defined 
                    HDLCX25   - 8192 
                    NODEADMN  - 8192 
                    UNITREC   - 4200 
                  Unit: Byte                    Default: 0 
                  Minimum: 4200                 Maximum: 127000* 
                                               *For COUPLER the sum of 
                                                RCVCQBYTSIZ and 
                                                SNDCQBYTSIZ is limited 
                                                to 65534. 
                  Effect: At boot time 
                  See CHANNEL_STATUS. 
RES               REsource is used with the ATTR parameter    ASYNC 
                  to specify the general class of device to   BISYNC 
                  be assigned (i.e., CL for Communication     COUPLER 
                  Line, DK for Diskette, HL for Host Line,    HDLCX25 
                  or UR for Unit Record Device).  (See        UNITREC 
                  CONFIG_OPTIONS.)                            User- 
                  Defaults for the LCP-6 Handlers:              defined 
                    ASYNC     - CL 
                    BISYNC    - CL 
                    COUPLER   - HL 
                    HDLCX25   - CL 
                    UNITREC   - UR 
                  Unit: - 
                  Minimum: -                    Maximum: - 
                  Effect: At boot time 
SNDCQBYTSIZ       SeND Circular Queue BYTe SIZe specifies     ASYNC 
                  the amount of space to be used for the      BISYNC 
                  Send Circular Queue for a handler.          COUPLER 
                                                              HDLCX25 
                  Defaults for the LCP-6 Handlers:            NODEADMN 
                    ASYNC     - 4200                          UNITREC 
                    BISYNC    - 4200                          User- 
                    COUPLER   - 8192                            defined 
                    HDLCX25   - 8192 
                    NODEADMN  - 8192 
                    UNITREC   - 4200 
                  Unit: Byte                    Default: 0 
                  Minimum: 4200                 Maximum: 127000* 
                                               *For COUPLER the sum of 
                                                RCVCQBYTSIZ and 
                                                SNDCQBYTSIZ is limited 
                                                to 65534. 
                  Effect: At boot time 
                  See CHANNEL_STATUS. 
SSNMAX            SeSsion MAXimum specifies the maximum       ASYNC 
                  number of session connections to be         BISYNC 
                  permitted on a single physical device.      HDLCX25 
                                                              User- 
                                                                defined 
                  Unit: Session                 Default: 6 
                  Minimum: 1                    Maximum: 99 
                  Effect: Immediate 
TYPAHDBFRLMT      TYPe AHeaD BuFfeR LiMiT specifies the       ASYNC 
                  number of type-ahead buffers for            BISYNC 
                  asynchronous terminals.  The buffer         HDLCX25 
                  consists of 32 bytes, 26 of which can       User- 
                  contain input characters.  This               defined 
                  parameter takes effect immediately. 
                  Unit: Buffer                  Default: 30 
                  Minimum: 1                    Maximum: 254 
                  Effect: Immediate 
UNBLOCK ({ALL|speed1[-speed2]|speed1[,speed2]...}) 
                  UNBLOCK specifies the unblocking            ASYNC 
                  value for the specified speed.  The         HDLCX25 
                  value specified may apply to all line       User- 
                  speeds (ALL), to a range of speeds, or        defined 
                  to a list of speeds.  See the BLOCK 
                  option for a list of the valid speed 
                  specifications.  The default is 
                  determined by line speed as follows: 
                    Speed      Default 
                    -----      ------- 
                    50-2400    200 
                    >2400      500 
                  Unit: Characters 
                  Minimum: 1                    Maximum: Current 
                  Effect: Immediate                  BLOCK value 
USRPARMn(x)       USeR PARaMeter identifies a                 User- 
                  user-defined parameter for a user-defined     defined 
                  handler.  n identifies the User 
                  Parameter Table (1 or 2) in which 
                  the user parameter is stored.  Each table 
                  contains 8 entries.  x is a value from 
                  1 to 8 that identifies the entry in 
                  the table. 
                  Unit: User defined            Default: 0 
                  Minimum: 0                    Maximum: 65535 
                  Effect: Immediate 
VDHTRC            VDH trace buffer byte size which is used    ASYNC 
                  for tracing messages sent and received by   BISYNC 
                  VDH, and interactions across the virtual    HDLCX25 
                  device interface (VDI) between VDH and      UNITREC 
                  the real device handler.  The default (0)   User- 
                  means no trace buffer is established.         defined 
                  Unit: Byte                    Default: 64 
                  Minimum: 0                    Maximum: 65535 
                  Effect: Immediately for new logons 
X29MLTMR          X29 MuLti-link TiMeR specifies the          HDLCX25 
                  timeout period for unacknowledged           User- 
                  packets.  When n seconds expires the          defined 
                  circuit is reset.  If n=0, the timer is 
                  disabled. 
                  Unit: Seconds                  Default: 10 
                  Minimum: 0                     Maximum: 255 
                  Effect: Immediately for new connections 
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
B 
  BOOT Command - 
      HELP BOOT 
C 
  Channel numbers - 
      HELP TERMSPEC_PARAMETER 
  Channel State - 
      HELP CHANNEL_STATUS 
  Channel Table - 
      HELP LINE_CONFIGURATION 
      HELP CONFIG_OPTIONS ATTR 
      HELP CONFIG_OPTIONS RESOURCE 
  CONFIG Command - 
      HELP CONFIG 
D 
  DATE Command - 
      HELP DATE 
  DEFAULT Command - 
      HELP DEFAULT 
  DEFINE Command - 
      HELP DEFINE 
  DELETE Command - 
      HELP DELETE 
  DIRECTORY Command - 
      HELP DIRECTORY 
  DISABLE Command - 
      HELP DISABLE 
  DISCONNECT Command - 
      HELP DISCONNECT 
  DISPLAY Command - 
      HELP DISPLAY 
  DO Command - 
      HELP DO 
E 
  ENABLE Command - 
      HELP ENABLE 
  END Command - 
      HELP END 
  ENTER Command - 
      HELP ENTER 
  ERASE Command - 
      HELP ERASE 
F 
  FEP Messages - 
      HELP FEP_MESSAGES 
  Files Created by NETCON - 
      HELP RELATED_FILES 
G 
  G_LCP6_E.:LIBRARY file - 
      HELP RESOURCE_DEFAULTS 
H 
  Handlers, standard - 
      HELP DEFAULT PARAMETERS: 
  HDLC line (NETCON) - 
      HELP CONFIG_OPTIONS REENABLE 
  HELP Command - 
      HELP HELP 
I 
  Invoking NETCON - 
      HELP INVOKING_NETCON 
K 
  KILL Command - 
      HELP KILL 
L 
  Line Configuration - 
      HELP LINE_CONFIGURATION 
  logon -   
    automatic (NETCON) - 
      HELP CONFIG_OPTIONS LOGON 
  Logon salutation - 
      HELP CONFIG_OPTIONS SALUTATION 
N 
  NETCON -   
    CONFIG Command - 
      HELP CONFIG FORMAT: 
    DISABLE Command - 
      HELP DISABLE FORMAT: 
    DISCONNECT Command - 
      HELP DISCONNECT FORMAT: 
    ENABLE Command - 
      HELP ENABLE FORMAT: 
    KILL Command - 
      HELP KILL FORMAT: 
    PARTITION Command - 
      HELP PARTITION FORMAT: 
    RETURN Command - 
      HELP RETURN PARAMETERS: 
  :NETCON file - 
      HELP RELATED_FILES 
  Node identification - 
      HELP DEFINE DESCRIPTION: 
O 
  OUTPUT Command - 
      HELP OUTPUT 
P 
  PARTITION Command - 
      HELP PARTITION 
  PRINT Command - 
      HELP PRINT 
  Privileges for Use of NETCON - 
      HELP PRIVILEGES 
R 
  RESET Command - 
      HELP RESET 
  Resource code - 
      HELP CONFIG_OPTIONS RESOURCE 
  RETURN Command - 
      HELP RETURN 
S 
  SELECT Command - 
      HELP SELECT 
  SELECT Command (NETCON) - 
      HELP SELECT FORMAT: 
  SET Command - 
      HELP SET 
  Standard handlers - 
      HELP DEFAULT PARAMETERS: 
T 
  Termspec Parameter - 
      HELP TERMSPEC_PARAMETER 
  timeout -   
    FEP logon - 
      HELP CONFIG_OPTIONS LOGONTIMEOUT 
    FEP read - 
      HELP CONFIG_OPTIONS READTIMEOUT 
U 
  UPDATE Command - 
      HELP UPDATE 
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
NETCON operates in the host CP-6 system as a batch or on-line job.  NETCON 
accepts commands, updates the :NETCON file and/or sends messages to the 
selected FEP. 
The DCBs used by NETCON are: 
o   M$SI for NETCON command input 
o   M$LO for user messages 
When run as an on-line job, NETCON solicits commands with an eight-character, 
blank-filled field that contains either the currently selected node name or 
host.  The prompt terminates with the asterisk (*) character. 
Command lines may be continued to the next line by a semicolon, and options 
are separated by commas.  Comments are bounded by the quotation marks 
("comment"); comments may follow the semicolon. 
  Handler/Parameter    Buffer Size Formula 
ASYNC_MEM            6 pages * no. of terminals 
                     + [if 6EDIT] 6 pages * no. of 6EDIT terminals 
                     + [if forms program] 12 pages * no. of forms 
                       terminals 
BISYNC_MEM           .5 * BLKBYTES from the line's PROFILE / 512 
                     + 5.5 * no. devices 
                     + 1 * input devices 
                     + (NETCON's BLOCK for the line / 256) 
                     * (no. output devices) pages 
                     * 1 for each RBT terminal 
                     + 10 pages * no. 3270 devices 
                     + [if forms program] 12 pages * no. 3270 devices 
HDLCX25_IOMEM        = ( ccb + WINDOW * vc ) * #links * FRAME / 512 
                     ccb is 4 if the communications board is an MLC8, 
                     8 if the communications board is an MLC16, or 
                     either WINDOW or 31 (whichever is smallest) if 
                     the communications board is an SLCC. 
                     WINDOW and FRAME are values from the link profile. 
                     If links have different WINDOW and FRAME sizes, 
                     use IOMEM formula for each link separately and sum 
                     the figures up for total IOMEM. 
                     #links    is the number of X.25 lines to run in 
                     the FEP. 
HDLCX25_MEM          = ( #links * 400 + #vc * 1200 ) / 256 
                     + [if 6EDIT] #x.29_circuits * 6 
                     + [if forms program] #x.29_circuits * 12 
                     + 40 
                     #links    is the number of X.25 lines to run in 
                     the FEP. 
                     #vc    is the number of virtual circuits, including 
                     those that are defined in SUPER to support RFEPs, 
                     and those that may become active on link devices. 
                     (See SUPER - CREATE DEVICE FOR LINK.) 
                     #x.29_circuits    is the number of X.29 
                     connections. 
UNITREC_MEM          No. of devices * (64 + (blocking factor * 4) / 256 
                     The blocking factor is the sum of the BLOCK values 
                     specified for the device channels, 700 by default. 
Format: 
KI[LL] termspec 
Parameters: 
termspec    identifies one or more FEP-connected terminals.  The format of the 
termspec parameter is termid [TO termid].  See HELP (NETCON) 
TERMSPEC_PARAMETER. 
Description: 
The KILL command is used to immediately terminate all activity on a line or 
range of lines on a selected FEP.  If a user is connected, a line drop is 
simulated in the FEP, and the user is disconnected.  If no user is connected, 
the line is immediately disabled.  Users will not be allowed to log on to the 
line until a subsequent ENABLE command is issued. 
The effect of the KILL command is immediate. 
00002
00001
The parameters are:  CMEM, CUSR, DUMP, MMEM, MUSR, QMIN, QUAN, SFILE_DATA, and 
XCONTIME. 
Enter: HELP (NETCON) LCP6PARAMS parameter 
for a description of a specific parameter. 
For a description of all LCP6PARAMS, enter: ??. 
  Parameter   Description 
  CMEM[_mode] 
              Displays the current memory usage by users in the same mode, 
              where mode is one of the following: 
              C - Comgroup connected 
              G - Ghost 
              H - Handler 
              U - User connected 
              If no mode is specified the value displayed is for current 
              memory usage for all modes.  This parameter is not settable. 
  CUSR[_mode] 
              Displays the current number of users in the same mode, where 
              mode is one of the following: 
              C - Comgroup connected 
              G - Ghost 
              H - Handler 
              U - User connected 
              If no mode is specified, the value displayed is the total number 
              of current users in all modes.  The parameter is not settable. 
  DUMP 
              Enables an automatic dump if a remote FEP crashes.  If the value 
              of DUMP is 1 and the remote FEP crashes, a dump is taken and 
              sent to the host.  If the value is 0, no dump is taken. 
              Unit: -                      Default: 1 
              Minimum: 0                   Maximum: 1 
  MMEM[_mode] 
              Specifies the maximum pages of memory that may be allocated at 
              any one time by all users of the same mode, where mode is one of 
              the following: 
              C - Comgroup connected 
              G - Ghost 
              H - Handler 
              U - User connected 
              If no mode is specified, the value is the maximum 
              allocatable memory pages for all modes. 
              Unit: Page                   Default: 61439 
              Minimum: 1                   Maximum: 65535 
  MUSR[_mode] 
              Specifies the maximum number of users allowed on the system by 
              mode, where mode is one of the following: 
              C - Comgroup connected 
              G - Ghost 
              H - Handler 
              U - User connected 
              If no mode is specified, the value is the maximum 
              number of users for all modes. 
              Unit: User                   Default: 20 
              Minimum: 3                   Maximum: 65535 
  QMIN 
              Specifies the minimum quantum time. 
              Unit: ticks(.133 secs)       Default: 4 
              Minimum: 1                   Maximum: <=QUAN 
  QUAN 
              Specifies the default quantum time. 
              Unit: ticks(.133 secs)       Default: 30 
              Minimum: 1                   Maximum: 65535 
  SFILE_DATA 
              Specifies the maximum number of pages that may be used to cache 
              the shared file data. 
              Unit: Page                   Default: 65535 
              Minimum: 0                   Maximum: 65535 
  XCONTIME 
              Specifies the time limit to be imposed for exit control 
              processing. 
              Unit: ticks(.133 secs)       Default: 999 
              Minimum: 5                   Maximum: 65535 
00001
00002
00003
00004
00005
00006
00007
00008
00009
LCP6PARAMS
A Channel Table is created in each FEP.  The Channel Table contains one entry 
for each channel connected to the FEP.  Each entry contains: 
o   flags and parameters that specify how a given channel is to be used.  The 
    parameters and flags can all be defaulted values or the system manager can 
    change them with NETCON CONFIG and DEFAULT commands. 
o   current channel state.  The current state is changed by use of the NETCON 
    processor DISABLE, DISCONNECT, ENABLE, and KILL commands and by external 
    channel use. 
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
The OUTPUT command is used to direct all processor output to a destination. 
OUTPUT with no options redirects output to the original output destination. 
Output can be directed to any valid file name (fid).  If none of ON, TO, OVER, 
or INTO is specified, ON will be assumed. 
00002
00001
See the following topics: 
HELP (NETCON) BOOTINFOPARAMS 
HELP (NETCON) BOOTPARAMS 
HELP (NETCON) CHANTBL_PARAMETERS 
HELP (NETCON) DISPLAY_PARAMETERS 
HELP (NETCON) HANDPARAMS 
HELP (NETCON) LCP6PARAMS 
HELP (NETCON) PSEUDOPARAMS 
HELP (NETCON) SET_PARAMETERS 
HELP (NETCON) TERMSPEC_PARAMETER 
Format: 
PART[ITION] termspec 
Parameters: 
termspec    identifies terminals at the FEP.  The format of termspec is termid 
[TO termid].  See: HELP (NETCON) TERMSPEC_PARAMETER. 
Description: 
The PARTITION command removes the specified termid(s) from system use and 
makes it available for test and diagnostics.  Lines that are currently enabled 
must be KILLed before they can be PARTITIONed. 
The effect of the PARTITION command is immediate. 
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
ldevname[,ldevname]... 
ldevname is a logical device name established through the LDEV command. 
Description: 
PRINT directs that output accumulated for logical devices be sent to 
destination(s) immediately. 
Examples: 
HOST    *PRINT LP01,LP02 
The above example causes the accumulated output associated with logical 
devices LP01 and LP02 to be sent immediately to the associated destinations. 
00002
00003
00001
Use of NETCON requires the NETCON processor privilege. 
The parameters are: NAME and MAXmode 
Enter: HELP (NETCON) PSEUDOPARAMS parameter 
for a description of a specific parameter. 
For a description of all PSEUDOPARAMS, enter: ??. 
  Parameter   Description 
  PSEUDO 
              Specifies a 1 to 8 character alphanumeric name. 
              Effect: At boot time 
  MAX_mode 
              Specifies the maximum number of the resource that may be 
              allocated at any one time by all users of the same mode, where 
              mode is one of the following: 
              C - Comgroup 
              G - Ghost 
              H - Handler 
              U - User connected 
              Effect: Immediate           Default: 0 
              Minimum: 0                  Maximum: 
00002
00001
PSEUDOPARAMS
PSEUDOPARAMS
END
NETCON builds and maintains the :NETCON file.  The :NETCON file contains all 
the configuration information for all FEPs in the network. 
(This information is used by the NETCON, SLUG, FROG and PIGETTE processors.) 
Format: 
RES[ET] termspec [[H[ANDLER] =] handlername] 
Parameters: 
termspec    identifies terminals at the FEP.  The format of termspec is termid 
[TO termid].  See: HELP (NETCON) TERMSPEC_PARAMETER. 
handlername    is the 1-8 character name of the handler whose default record 
is to be used to reset the line configuration.  See the DEFAULT command for a 
list of system defined names. 
Description: 
The RESET command resets the line configuration for the specified termid(s) by 
deleting the current configuration record in :NETCON, and applying a default 
configuration record to the FEP.  If a handler name is specified, that 
handler's DEFAULT record is used; otherwise, a default record (as described in 
HELP topic CHANNEL_TABLE_DEFAULTS) is used.  If the channel being reset 
belongs to a handler other than the one specified in the RESET command, then 
an error will be returned.  The effect of the RESET command is immediate. 
Example: 
L6XII   * CON .2400 READTI=0,LOGON='Miller,Dan',SPEED=19200 
      Line(s) 2400-0-0 to 2400-0-0 Configured 
L6XII   *DI  CON .2400 
Line Configuration for Node# 12(L6XII   ) Channel# .2400-0-0 Terminal id 
Logon:        Miller,Dan 
Profile:      None 
Auto speed:    Off   Speed:       19200 
Echo Logon:    D/C   Flow cntrl:    D/C    Input:         D/C 
Output:        D/C   Send Sal:      D/C    Break Req:     D/C 
Buffer size:    -1   Remote host:  Host    Enable:        D/C 
Re-enable:     D/C   Lgn timeout:    -1    Readtimeout:     0 
TP timeout:     -1   Hard wired:    D/C    Clock:         D/C 
Drop DTR:      D/C   Kill hst dwn:   No    Dsb hst dwn:    No 
Resource:     None   Attribute:   .   0    Block:          -1 
Unblock:        -1   Debug:         D/C    Remote debug:  D/C 
L6XII   * RESET .2400 
      Line(s) 2400-0-0 to 2400-0-0 Reset 
L6XII   * DI CON .2400 
The specified key does not exist in :NETCON.:SYS 
unable to display configuration. 
00002
00003
00001
The following tables list the default attributes assigned if no NETCON line 
configuration options are used to change the resource/attribute association. 
The default attributes listed in these tables correspond to EQUs defined in 
the system file G_LCP6_E.:LIBRARY.  The equate name is formatted: 
    G_ATTR_rescode_attrname 
where 
    rescode    is one of the resource codes:  CL, DK, HL, or UR. 
    attrname    is defined in the column "Default Attribute" in the following 
    tables. 
For example: 
    G_ATTR_UR_LP identifies a unit record line printer. 
    G_ATTR_CL_ASYNC|G_ATTR_CL_RS232 identifies an ASYNC RS232 terminal. 
  Device Id   Name, Characteristics      Resource Code   Default Attribute 
2000        Line Printer, 64           UR              LP 
            characters without VFU 
2001        Line Printer, 64           UR              LP 
            characters with VFU 
2002        Line Printer, 96           UR              LP 
            characters without VFU 
2003        Line Printer, 96           UR              LP 
            characters with VFU 
2004        Serial Printer, 64         UR              LP 
            characters 
2006        Serial Printer, 96         UR              LP 
            characters 
2008        Card Reader, 300 CPM       UR              CR 
            Card Reader, 500 CPM       UR              CR 
            Card Reader, 300/500 CPM   UR              CR 
            Card Reader, 300/500 CPM,  UR              CR 
            with Mark Sense 
2010        Diskette, Single Sided     DK              8IN 
            (8") 
2011        Diskette, Doubled Sided    DK              8IN + 2SIDED 
            (8") 
2017        Diskette, Mini (5-1/4")    DK              MINI 
2031        Line Printer, 64           UR              LP 
            characters with EVFU 
2033        Line Printer, 96           UR              LP 
            characters with EVFU 
2088        Card Reader/Punch, 2111-1A UR              CP 
208A        Card Reader/Punch, 2111-2A UR              CP 
20C4        Line Printer, 95           UR              LP 
            characters with EVFU 
2110        Asynchronous, Current      CL              ASYNC + CURLP 
            Loop 
2118        Asynchronous, RS-232C      CL              ASYNC + RS232 
2120        Auto-Dialer, ACU           CL              ACU 
2138        Synchronous, 301/303,      CL              SYNC + 301 + WIDE 
            Wideband 
2140        Synchronous, HDLC, RS-232C CL              HDLC + RS232 
2158        Synchronous, RS-232C       CL              SYNC + RS232 
2168        Synchronous, DSU/V.35,     CL              SYNC + V35 + WIDE 
            Wideband 
21F2        Current Loop, RS422C       CL              ASYNC + RS422C 
21F6        Synchronous, HDLC,         CL              ASYNC + 301 + 
            301/303, Wideband                          WIDE 
21F7        Synchronous, HDLC,         CL              ASYNC + V35 + 
            DSU/V.35 Wideband                          WIDE 
21F8        Synchronous, HDLC,         CL              ASYNC + MIL188C 
            MIL-188C Wideband                          + WIDE 
2408        6600 Front End Coupler     HL 
  Device ID    Extended ID    Mode     Adapter Type    Default Attribute 
2978         3A00           422DC    HDLC/SYNC       ASYNC 
2978         48xx           SYNC     HDLC/SYNC       SYNC 
2978         49xx           HDLC     HDLC/SYNC       HDLC 
2978         78xx           SYNC     SYNC/ASYNC      SYNC 
2978         7Axx           ASYNC    SYNC/ASYNC      ASYNC 
2978         6800             -      Integrated      SYNC 
                                     RS-232 SYNC 
2978         6A00             -      Integrated      ASYNC 
                                     RS-232 ASYNC 
where xx is the flap ID as follows: 
    xx    Flap Type              Default Attribute 
    --    ---------              ----------------- 
    00    No Flap 
    01    RS-232                 RS232 
    02    RS-422 Broadband       RS422C + WIDE 
    03    RS-422 Medium Speed    RS422C 
    04    Current Loop           CURLP 
    07    30//303                301 + WIDE 
    08    V.35                   V35 + WIDE 
    0A    MIL-188-114            MIL188C 
Format: 
RET[URN] termspec 
Parameters: 
termspec    identifies terminals at the FEP.  The format of termspec is termid 
[TO termid].  See HELP (NETCON) TERMSPEC_PARAMETER. 
Description: 
The RETURN command restores PARTITIONed termid(s) to system use.  The effect 
of the RETURN command is immediate. 
00002
00001
Format: 
SEL[ECT] {N[ODE=]nodeid        } 
         {H[ANDLER=]handlername} 
         {S[TORAGE=]mode       } 
Parameters: 
nodeid    is the 1 to 8 character node name or the node number that defines 
the CP-6 host or the FEP. 
handlername    is the 1 to 8 character name of the handler assigned by the SET 
BOOTINFO command that assigns the handler to the FEP.  See the DEFAULT command 
for a list of system defined names. 
mode    specifies how to apply subsequent CONFIG and SET commands and how to 
display NETCON parameters as follows: 
    FILE  specifies subsequent commands are to be applied to :NETCON, only. 
          No changes are to be made to the selected node until the node is 
          re-booted.  For display of LCP6 and handler parameters, FILE 
          specifies NETCON should not interrogate the FEP for the current 
          parameter values in the FEP. 
    PERM  specifies that subsequent commands are to be applied immediately to 
          the selected node and are to be reflected in the :NETCON file as 
          well.  This is the default. 
    TEMP  specifies that subsequent commands are to be applied immediately to 
          the selected node only; no change is to be made to the :NETCON file. 
Description: 
The SELECT command is used to select a network node or handler so that 
subsequent NETCON processor commands will be applied to the SELECTed node or 
handler. 
The SELECT command is also used to specify if subsequent NETCON processor 
commands will affect the :NETCON file, an active FEP node, or both. 
00002
00001
Format: 
SET BOOT[INFO] [bootlist] 
or 
SET param=value[,param=value]... 
or 
SET PSEUDO=pseudoname [param=value[,param=value]] 
Parameters: 
BOOTINFO    specifies the run units to be used when booting a SELECTed FEP. 
The BOOTINFO identifies the run units, the LCP-6 monitor and the handlers that 
are to be booted at a later time.  This may be via the BOOT command of NETCON, 
an operator BOOT keyin, a boot of a diskette built by the PIGETTE processor, a 
host tape boot or a FEP software recovery.  The SET BOOTINFO command has no 
effect on the current execution of the selected node.  BOOTINFO parameters are 
used when the FEP is booted or a diskette is built by PIGETTE.  bootlist 
consists of one or more of the following: 
    M[ONITOR]={filename[.account]|.account} 
    L[IBRARY]=[.]account 
    H[ANDLER]=hname[(optionlist)] 
bootlist specifications are separated by commas.  If MONITOR, LIBRARY and/or 
HANDLER are specified in the SET BOOTINFO command, any of the three not 
specified default to the values currently defined for the node.  MONITOR and 
LIBRARY can be specified in the command once.  HANDLER can be repeated.  If 
SET BOOT is specified with no bootlist parameters, the user is prompted to 
enter the run unit information described under HELP (NETCON) BOOTINFOPARAMS. 
A carriage return in response to a prompt selects the value currently defined 
for the node except that options for the HANDLER parameter are defaulted as 
described in the BOOTINFOPARAMS topic. 
One or more of the following HANDLER parameter options can be specified in the 
SET BOOTINFO command separated by commas: 
    B[OOTTIME]={YES|NO}    specifies whether the handler is to be included in 
    the boot image (YES), or is to be downloaded after the FEP is booted.  The 
    default is YES. 
    D[EFAULT][={YES|NO}]    specifies whether to set handler parameters back 
    to the defaults.  The default is NO.  If DEFAULT is specified but neither 
    YES nor NO is specified, YES is assumed. 
    F[ID]={filename[.acct]|.acct}    specifies the handler name and account. 
    the default is handlername.:SYS. 
    REMOVE    deletes a currently defined handler. 
param=value    specifies a NETCON boot parameter, handler parameter or LCP-6 
parameter.  The boot parameters specify the sizes of the monitor tables that 
will be built when the FEP is booted.  Setting these parameters has no effect 
on the currently running monitor of the SELECTed FEP.  The boot parameters 
that can be specified are described under HELP (NETCON) BOOTPARAMS.  The 
handler parameters are set for the selected handler of the selected FEP.  The 
handler information that can be specified is described under HELP (NETCON) 
HANDPARAMS.  The LCP-6 parameters are used to tailor the LCP-6 operating 
system to meet the special performance and operational requirements of the 
selected FEP.  The LCP-6 parameters that can be specified are described under 
HELP (NETCON) LCP6PARAMS. 
PSEUDO=pseudoname    identifies the pseudo resource whose limits are to be 
set.  The pseudo resources known to a FEP can be changed only at boot time. 
param=value specifies the number of resources available to users of a FEP 
node.  The SET PSEUDO command parameters are described under HELP (NETCON) 
PSEUDOPARAMS.  If no parameter is specified, all pseudo resource parameters 
default to 0. 
Description: 
The SET command allows the user to set control parameters on a per FEP or per 
handler basis.  In most cases, the default NETCON parameters as shipped in the 
CP-6 system are suitable. 
If BOOTINFO, boot parameters and LCP-6 parameters are set, they take effect 
when the FEP is booted.  Some PSEUDO and handler parameters take effect 
immediately; others take effect when the FEP is booted.  The HANDPARAMS topic 
indicates when a handler parameter takes effect, and the PSEUDOPARAMS topic 
indicates when a PSEUDO parameter takes effect. 
Other commands cannot be chained on the same line as a SET BOOTINFO command. 
00002
00001
DISPLAY_PARAMETERS
    The termspec parameter is used in NETCON commands to identify one or a 
    range of lines.  The lines are identified by a terminal id.  Terminals, 
    controllers, and subdevices on them can be identified via the termspec 
    parameter.  termspec is formatted as: 
        termid [TO termid] 
    where termid is formatted as: 
        {[CHAN=].channelnum[-subnum[-subsubnnum]]} 
        {[CHAN=]termname[-subnum[-subsubnum]]    } 
    channelnum    is a hexadecimal number that is the address of the physical 
    channel corresponding to the terminal.  The period preceding the 
    hexadecimal value is required. 
    termname    is the terminal name as defined via SUPER.  A termname is 
    associated with a channel by setting the logon string equal to the 
    termname in the CONFIG for the channel (e.g., CONFIG .3200 
    LOGON='3270LION').  Thereafter, only the termname should be used to refer 
    to the specified terminal.  termname with no subnum represents the first 
    terminal level. 
    -subnum    is a decimal number that represents the second terminal level 
    (i.e., termname is level 1 and termname-n is level 2). 
    -subsubnum    is a decimal number that represents the third terminal level 
    (i.e., termname is a level 1, termname-n is level 2, and termname-n-m is 
    level 3).  Only three levels can be established. 
    For a termspec range to be valid: 
o   the termids must have the same number of levels. 
o   the termid may differ only in the lowest level component, i.e., TERM-1-2 
    to TERM-2-2 is illegal. 
o   the lowest level component of the second termid must be numerically 
    greater than or equal to the corresponding component of the first termid. 
DATE
Format: 
         [{               [{,C[ONTROL] = hostname                   }]   }] 
         [{NODE =] nodenum[{,L[INK] {= .channelnum|[=](channellist)}}]...}] 
UPDA[TE] [{               [{,N[AME] = nodename                      }]   }] 
         [{               [{,T[YPE] = nodetype                      }]   }] 
Parameters: 
nodenum    is a decimal integer (1-n) that identifies the node that is to be 
updated. 
hostname    is a 1 to 8 character alphanumeric value that identifies the new 
controlling host. 
 .channelnum    is a hexadecimal number that is the address of the physical 
channel.  The period preceding the hexadecimal value is required.  channellist 
is a list of .channelnum values enclosed in parenthesis.  The members of the 
list are separated by commas. 
nodename    is a 1-8 character alphanumeric value that specifies a new node 
name. 
nodetype    is one of the following: 
    DEBUG    specifies a FEP node to be used for debugging purposes.  A node 
    with a type of DEBUG will not reboot when the system comes up.  Only DEBUG 
    nodes should be booted with the NOTIME option.  NOTE:  A DEBUG node cannot 
    be changed to a HOST or ME node. 
    FEP    specifies a FEP node.  NOTE:  A FEP node cannot be changed to a 
    HOST or ME node. 
    HOST    specifies a CP-6 host node.  NOTE:  A HOST node cannot be changed 
    to a FEP, RFEP or DEBUG node. 
    ME    specifies the current CP-6 host.  NOTE:  The ME node cannot be 
    changed to a FEP, RFEP or DEBUG node. 
    RFEP    specifies a remote FEP node.  NOTE:  An RFEP node cannot be 
    changed to a HOST or ME node. 
Description: 
The UPDATE command is used to change node definitions.  Typically, the UPDATE 
command is issued with a node number identifying the node to be updated and 
one or more of the definition options, containing the update information. 
Note the following restrictions: 
o   A host type node (i.e., HOST or ME) cannot be changed to a FEP type node 
    (i.e., FEP RFEP or DEBUG), and vice versa. 
o   If a FEP type node is updated to be an RFEP node: 
    -   The Link definition option must be specified if a physical channel 
        address has not already been assigned to the FEP. 
    -   BOOT INFO is adjusted as follows:  if not present, the HDLCX25 handler 
        is added.  The COUPLER is removed.  BOOTTIME is set to YES in the RFEP 
        boot record for the HDLCX25 and NODEADMN handlers.  Any other handlers 
        have BOOTIME=NO. 
See the DEFINE command for more information on the definition options. 
The UPDATE command can be issued without any options to inform the network 
that node(s) have been added to or deleted from the network.  However, this is 
never necessary:  DEFINE, DELETE and UPDATE all update the network 
automatically. 
00002
00001
END
