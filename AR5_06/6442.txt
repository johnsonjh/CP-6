CP-6 communication management, project and user authorization, and forms 
control functions are implemented through the SUPER processor. 
To obtain more HELP information, see 
HELP (SUPER) TOPICS               Displays topics. 
HELP (SUPER) COMMANDS             Displays a list of SUPER 
                                  commands. 
HELP (SUPER) command PARAM        Displays parameters 
                                  associated 
                                  with a particular command. 
HELP (SUPER) command DESCRIPTION  Displays description 
                                  associated with a 
                                  particular command. 
?                                 Displays next level of 
                                  HELP messages. 
??                                Displays all levels of 
                                  HELP messages. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
ALIGN_SUBOPTIONS
ALIGN_SUBOPTIONS
A list of alignment sub-options and their definitions can be accessed by 
typing a ? or a ??.  To obtain definitions of these individual sub-options, 
type 
HELP (SUPER) ALIGN_SUBOPTS suboption 
where suboption is any of the following: 
ALIGN, ENTRY, REPEATS 
  Suboption    Description 
  AL[IGN][EVERY] [={YES}|{NO}] 
               Indicates if the alignment is to be printed before every file. 
               If YES and NO are omitted, YES is assumed.  The default is NO. 
  EN[TRY] = row,col [, font, strikes, icsh, reps, rinc, cinc] 
               Defines one element of this ALIGNMENT and can be used as many 
               times as needed.  The values for this sub-option can be 
               accessed by typing HELP (SUPER) ENTRY_OPTS.  After the ENTRY 
               sub-option is typed, SUPER prompts with TXT*.  Available 
               responses to this prompt can be accessed by typing HELP (SUPER) 
               ENTRY_TEXT. 
  RE[PEATS] = decimal 
               Specifies the number of times the entire ALIGNMENT image is to 
               be repeated.  If this sub-option is omitted, one is assumed if 
               entries are made and zero if no entries are made. 
00001
00002
00003
ALIGN_SUBOPTIONS
BAN_SUBOPTIONS
BAN_SUBOPTIONS
A list of banner sub-options and their definitions can be accessed by typing a 
? or a ??.  To obtain definitions of these individual sub-options, type 
HELP (SUPER) BAN_SUBOPTS suboption 
where suboption is any of the following: 
CHARGE, ENTRY, REPEATS 
  Suboption    Description 
  CH[ARGE] [={YES}|{NO}] 
               Indicates if the user is to be charged for banner pages.  If 
               YES or NO are omitted, YES is assumed.  The default is NO. 
  EN[TRY] = row,col [, font, strikes, icsh, reps, rinc, cinc] 
               Defines one element of this BANNER and can be used as many 
               times as needed.  The values for this sub-option can be 
               accessed by typing HELP (SUPER) ENTRY_OPTS.  After the ENTRY 
               sub-option is typed, SUPER prompts with TXT*.  Available 
               responses to this prompt can be accessed by typing HELP (SUPER) 
               ENTRY_TEXT. 
  RE[PEATS] = decimal 
               Specifies the number of times the entire BANNER image is to be 
               repeated.  If this sub-option is omitted, one is assumed if 
               entries are made and zero if no entries are made. 
00001
00002
00003
BAN_SUBOPTIONS
The suboptions are: 
ACHARGES, BKACCESS, BLINDACCOUNTING, BUDLIM, ICHARGE, 
MCHARGES, and PCHARGE. 
To see HELP for each, enter: 
HELP (SUPER) BUDGET_SUBOPTS AC, or BK, ... PC. 
To see HELP for all, enter: ??. 
  Suboptions    Description 
  AC[HARGES] = curmon 
                Specifies the current value of this user's accumulated 
                charges.  Ordinarily, it is maintained automatically by the 
                system.  The system manager may adjust the accumulated 
                charges. 
                curmon is the value, in dollars and cents, of the user's 
                current accumulated charges. 
  BK[ACCESS][={Y[ES]|{N[O]}] 
                Permits the system manager to deny access to the system when 
                the user is bankrupt; i.e., accumulated charges (ACHARGES) 
                exceed the maximum allowed charges (MCHARGES).  YES allows the 
                user to logon even if bankrupt.  NO means the user cannot 
                logon while he is bankrupt.  The default is YES. 
  BL[INDACCOUNTING][={Y[ES]|N[O]}] 
                Controls the printing of charge-per-units and intermediate 
                charges on a full accounting summary.  YES specifies that 
                charge-per-unit and intermediate charges should be suppressed 
                when printing a full accounting summary.  NO specifies that 
                charge-per-unit and intermediate charges should be printed on 
                the full accounting summary.  The default is NO. 
  BU[DLIM] = {Y[ES]|N[O]} 
                Specifies whether or not to check the budget limit at the end 
                of every job step.  YES indicates that charges for the user 
                are to be calculated at the end of every job step and the user 
                is logged off if his budget has been exceeded.  NO means do 
                nothing at job step.  The default is NO. 
  IC[HARGE][={Y[ES]|N[O]}] 
                Specifies whether or not individual budget accounting should 
                be done for the user.  YES means do individual budget 
                accounting.  NO means do not do individual budget accounting. 
                The default is YES. 
  MC[HARGES[ = {[sign]monval|NONE} 
                Specifies the maximum dollar amount that this logon ID is 
                allowed to accumulate.  It is a cumulative maximum that holds 
                through multiple logon attempts. 
                monval is specified in dollar and cents (with a decimal point) 
                or just dollars (with no decimal point).  If monval is not 
                preceded by a sign (+ or -), the value specified is an 
                absolute value.  If monval is preceded by a sign, the value 
                specified is added or subtracted from the current or default 
                MCHARGES value, NONE specifies there is no maximum limit on 
                this user.  The default is NONE. 
  PC[HARGE] [={Y[ES]|N[O]}] 
                Specifies whether or not project budget accounting should be 
                done for the user.  This means that any accrual of charges for 
                this user is also charged to the project.  YES means do 
                project budget accounting.  NO means do not do project budget 
                accounting.  The default is YES. 
00001
00002
00003
00004
00005
00006
00007
BUDGET_SUBOPTIONS
A list of CHARSET options and suboptions can be accessed by 
typing a ? or ??.  To obtain definitions of individual options, 
type: HELP (SUPER) CHARSET_OPTS option 
where option is: ATTRIBUTES, DEVICES, or IMAGE 
  Option    Description 
  ATT[RIBUTES]=attribute[,attribute]... 
            Assigns a character set attribute which describes the translation 
            method used for output going to the form.  The values that can be 
            specified are: 
            Attribute Name    Description 
            AP[L]             Indicates that output for this form contains APL 
                              characters. 
            BI[N]             Indicates that binary data can be processed as 
                              output for this form.  (This CHARSET record 
                              cannot be used with the DEVICES suboption TS.) 
            LO[WERCASE]       Specifies that output for this form is to have 
                              uppercase alphabetic characters interpreted as 
                              lowercase characters.  In addition, these 
                              translations are made: 
                                  [     to { 
                                  \     to | 
                                  ]     to } 
                                  tilde to ^ 
            NA[TL]            Specifies that output for forms that use this 
                              charset contains National Language characters as 
                              defined by the system table, NK_NATLTBL. 
            NO[XLATE]         Specifies no manipulation of data is to occur in 
                              output. 
            OV[ERPRINT]       Specifies that overprinting can be processed as 
                              part of output for this form. 
            TR[ANSLGL][={NO|YES}] 
                              Indicates whether transparent characters are to 
                              be passed on to the device.  NO specifies that 
                              transparent writes to symbiont files do not go 
                              through translation or get truncated (the 
                              "transparent" bit is not retained in the output 
                              file).  YES specifies that writes will retain 
                              their length and transparency in the output 
                              symbiont file.  The default is NO.  If TRANSLGL 
                              is specified on the option line but neither YES 
                              or NO is specified, YES is assumed. 
                              Note:  TRANSLGL is only meaningful for 
                              non-IOM-/VDH-connected devices.  If the TRANSLGL 
                              setting specified for a CHARSET differs from the 
                              TRANSLGL setting for the appropriate FORM, the 
                              FORM TRANSLGL setting is used. 
            UP[PERCASE]       Specifies that output is to have all alphabetic 
                              characters as uppercase characters. 
            If no attribute is specified UP is assumed. 
            When the ATTRIBUTE option is specified, all attributes are reset. 
            If an attribute name is specified, that attribute is set to YES, 
            all other attribute names from the list will be set to NO. 
            Only one of the following attributes can be specified, except that 
            both UP and LO can be specified together: 
            APL 
            NATL 
            NOXLATE 
            UP, LO (Precedence is: both, then UP, then LO.) 
  DE[VICES] 
            Specifies the logical devices to be associated with the CHARSET 
            record.  Specifying DEVICES initiates suboptions mode.  The 
            suboptions that can be specified are: 
            EL[SOK][={YES|NO}] 
                                  Indicates whether a form built with this 
                                  CHARSET record is legal (YES) or illegal 
                                  (NO) for ALL devices other than line 
                                  printers and timesharing terminals. 
            LP[OK][={YES|NO}] 
                                  Indicates whether a form built with this 
                                  CHARSET record is legal (YES) or illegal 
                                  (NO) for line printers. 
            LT[YP][={cc|NO}] 
                                  Indicates a legal device type for a form 
                                  built with this CHARSET record.  cc 
                                  specified a two-character device type 
                                  defined by the user (via SUPER).  If NO is 
                                  specified, LTYP is set to blank.  NO is 
                                  assumed if neither cc nor NO is specified. 
            TS[OK][={YES|NO}] 
                                  Indicates whether a form built with this 
                                  CHARSET record is legal (YES) or illegal 
                                  (NO) for timesharing terminals. 
            If any of the device names ELSOK, LPOK, or TSOK is specified, but 
            =YES or =NO is omitted, =YES is assumed. 
  IM[AGE] 
            Initiates suboption mode in which the print chain image is 
            specified.  The print chain image always consists of 240 
            characters.  The image is specified as a matrix consisting of 10 
            rows or sets each of which must contain exactly 24 characters. 
            The sets are numbered from 0 through 9.  At the suboption level, 
            the user specifies: 
            SETn='cccccccccccccccccccccccc' 
            where 
            n    is the set number (0-9) 
            c    is any printable character from the ASCII character set. 
            Exactly 24 characters must be specified. 
00001
00002
00003
CHARSET_OPTIONS
VIRTUAL_CIRCUIT
COMMANDS
A list of SUPER commands and their definitions can be accessed by typing 
HELP (SUPER) COMMUNICATIONS_CMDS    for SUPER communications commands. 
HELP (SUPER) PROJECT_CMDS           for SUPER project authorization 
                                    commands. 
HELP (SUPER) USER_CMDS              for SUPER user authorization 
                                    commands. 
HELP (SUPER) FORM_CMDS              for SUPER line-oriented and graphic 
                                    form commands. 
COMMUNICATIONS_COMMANDS
A list of SUPER communications commands and their definitions can be accessed 
by typing a ? or ??.  To obtain definitions of individual communications 
commands, type 
HELP (SUPER) COMMUNICATIONS_CMDS command 
where command is any of the following: 
CONSOLE, CONTROLLER, DEVICE, TP_DEVICE, DEVICE_FOR_LINE, DEVICE_FOR_LINK, 
LINE, LINK, PROFILE, STATION, TERMINAL, VIRTUAL_CIRCUIT, and WSN. 
  Command Type    Order      Description 
  CONSOLE 
                             The CREATE CONSOLE, DELETE CONSOLE, MODIFY 
                             CONSOLE, and REMOVE CONSOLE commands create, 
                             delete (all), modify, or remove (one) console 
                             definitions.  The LIST command lists the 
                             currently defined console.  The DISPLAY CONSOLE 
                             command displays console definitions. 
  CONTROLLER 
                             The CREATE CONTROLLER, MODIFY CONTROLLER, and 
                             REMOVE CONTROLLER commands create, modify and 
                             remove (one) 3270 or POLLVIP controller 
                             definitions.  The LIST CONTROLLER command lists 
                             the currently defined controllers.  The DISPLAY 
                             CONTROLLER command displays controller 
                             definitions. 
  DEVICE 
                             The CREATE DEVICE, DELETE DEVICE, MODIFY DEVICE, 
                             and REMOVE DEVICE commands create, delete (all), 
                             modify, and remove (one) device definitions.  The 
                             LIST DEVICE command displays the currently 
                             defined devices.  The DISPLAY DEVICE command 
                             displays device definitions. 
  TP_DEVICE 
                             The CREATE TP DEVICE, MODIFY TP DEVICE, and 
                             REMOVE TP DEVICE commands create, modify, and 
                             remove TP devices or TP logons.  The LIST TP 
                             DEVICE command lists the currently defined TP 
                             devices.  The DISPLAY TP_DEVICE command displays 
                             TP device definitions. 
  DEVICE_FOR_LINE 
                             The CREATE DEVICE FOR LINE, MODIFY DEVICE FOR 
                             LINE, and REMOVE DEVICE FOR LINE commands create, 
                             modify, and remove (one) 3270 device definitions. 
                             The LIST DEVICE FOR LINE command lists the 
                             currently defined line device.  The DISPLAY 
                             DEVICE FOR LINE command displays line device 
                             definitions. 
  DEVICE_FOR_LINK 
                             The CREATE DEVICE FOR LINK, MODIFY DEVICE FOR 
                             LINK, and REMOVE DEVICE FOR LINK commands create, 
                             modify, and remove (one) link device definition. 
                             The LIST DEVICE FOR LINK command lists the 
                             currently defined link device.  The DISPLAY 
                             DEVICE FOR LINK command shows link device 
                             definitions. 
  LINE 
                             The CREATE LINE, MODIFY LINE, and REMOVE LINE 
                             commands create, modify, and remove (one) line 
                             definitions for synchronous lines for 3270 type 
                             devices or synchronous lines for VIP 7700/7804 
                             terminals and printers.  The LIST LINE command 
                             lists the currently defined line.  The DISPLAY 
                             LINE command displays line definitions. 
  LINK 
                             The CREATE LINK, MODIFY LINK, and REMOVE LINK 
                             commands create, modify, and remove (one) link 
                             definitions.  The LIST LINK command lists the 
                             currently defined link.  The DISPLAY LINK command 
                             displays link definitions. 
  PROFILE 
                             The CREATE PROFILE, DELETE PROFILE, MODIFY 
                             PROFILE, and REMOVE PROFILE commands create, 
                             delete (all), change, and remove (one) hardware 
                             attributes for a device or terminal.  The LIST 
                             PROFILE command lists the currently defined 
                             profile.  The DISPLAY PROFILE command displays 
                             profile definitions. 
  STATION 
                             The CREATE STATION, and REMOVE STATION commands 
                             create and remove (one) stations.  The LIST 
                             STATION command lists the currently defined 
                             station.  The DISPLAY STATION command displays 
                             station definitions. 
                             The RECONFIGURE STATION LOCAL command removes and 
                             automatically recreates the system-generated 
                             station LOCAL.  The RECONFIGURE STATION sname 
                             command defines IOM-connected devices for sname 
                             (sname must be a TIGR-defined station). 
  TERMINAL 
                             The CREATE TERMINAL, DELETE TERMINAL, MODIFY 
                             TERMINAL, and REMOVE TERMINAL commands create, 
                             delete (all), modify, and remove (one) terminal 
                             definitions.  The LIST TERMINAL command lists the 
                             currently defined terminal.  The DISPLAY TERMINAL 
                             command displays terminal definitions. 
  VIRTUAL_CIRCUIT 
                             The CREATE VIRTUAL CIRCUIT, MODIFY VIRTUAL 
                             CIRCUIT and REMOVE VIRTUAL CIRCUIT commands 
                             create, modify, and remove virtual circuit 
                             definitions.  The LIST VIRTUAL CIRCUIT command 
                             lists the currently defined virtual circuit.  The 
                             DISPLAY VIRTUAL CIRCUIT command displays virtual 
                             circuit defintions. 
  WSN 
                             The CREATE WSN, MODIFY WSN, and REMOVE WSN 
                             commands create, modify, and remove workstation 
                             definitions.  The LIST WSN command lists the 
                             currently defined workstation.  The DISPLAY WSN 
                             command displays workstation definitions. 
00001
00002
00003
00005
00006
00007
00008
00009
00010
00011
00004
00012
00013
A list of communication profile options and their definitions can be accessed 
by typing a ? or ??.  To obtain individual options, type: 
HELP (SUPER) COMMUNICATION_PROFILE_OPTS option 
where option is any of the following: 
BLKBYTES, BLKRECS, COMPRESS, DELAYS, EMCHR, ERRDUPBLK, INTERVAL, IRSCHR, 
LSTRECCTN, MULSTRM, PADSIGNON, PROTYP, RETRYS, RRR, SLC, and SLCALLBLK. 
  Option                       Description                           Device 
BLKB[YTES]=value            Specifies the maximum number of        RBT 
                            bytes per block that may be sent       SYNC 
                            to the terminal.  The default is 400. 
BLKR[ECS]=value             Specifies the maximum number of        RBT 
                            records (0-32767) per block that       SYNC 
                            may be sent to the terminal.  The 
                            default is 400. 
CO[MPRESS]={B[LANKS]|Y[ES]|N[O]|L[INE]} 
                            For HASP only.  BLANKS specifies       SYNC 
                            that repeating blanks will be 
                            compressed.  YES specifies that 
                            all repeating characters will be 
                            compressed, NO that no compression 
                            will be done.  LINE specifies that 
                            compression will be done for all 
                            repeating characters if the line 
                            speed is less than 9600 baud; for 
                            blanks if the line speed is 9600 
                            baud; and not at all if the line 
                            speed is greater than 9600 baud. 
                            The default is LINE. 
DEL[AYS]=value              Specifies the number of delay pads     RBT 
                            (0-511) preceding messages.  The       SYNC 
                            default value, 3, should work 
                            properly unless the equipment being 
                            communicated with is unable to 
                            read fast enough when receiving a 
                            block of data.  Generally, other 
                            multiple purpose computers without 
                            front-end processors (such as CP-V) 
                            fall into this category.  Line 
                            timeouts will occur if the value 
                            for DELAYS is not high enough. 
EM[CHR]=hex                                                        RBTD 
                            For 2780 stations, this option         SYNC 
                            defines the value of the EM (End of 
                            Media) character to be expected in 
                            incoming data and to be used for 
                            outbound data.  The default is '19'X. 
ERR[DUPBLK][={Y[ES]|N[O]}]                                         RBT 
                            For 2780, 3780 and HASP stations, 
                            this option determines whether 
                            duplicate blocks should be sent to 
                            output devices on the station if an 
                            error condition is thought to have 
                            occurred.  NO should only be 
                            specified if the RBT cannot accept 
                            duplicate blocks at all, since re- 
                            transmission of blocks occurs quite 
                            often.  The default is YES. 
INT[ERVAL]=value            For SYNC type profiles that specify    RBT 
                            PROTYP=POLLED.  Specifies the time     SYNC 
                            interval (0-255) in tenths of a 
                            second between general polls of 
                            active controllers.  On an idle 
                            line, this is the maximum time 
                            that will elapse between typing 
                            of a terminal activation key 
                            (ENTER, PF, or PA) and the time 
                            that the data is retrieved from 
                            the device.  Note that making 
                            this value small enough to cause 
                            continuous polling on a high speed 
                            line (9600 baud) will consume a 
                            large portion of the FEP's CPU 
                            power.  A value of 5 or 10 is 
                            recommended.  The default is 10 
                            (1 second). 
IRS[CHR]=hex                                                       RBT 
                            For 3780 stations, this option         SYNC 
                            defines the value IRS (Interchange 
                            Record Separator) character to be 
                            expected in incoming data, and to be 
                            used for outbound data.  The default 
                            is '1E'X. 
LST[RECCTN]={Y[ES]|N[O]}                                           RBT 
                            For 2780 and 3780 stations, this       SYNC 
                            option determines whether or not in- 
                            coming blocks which end in "<record 
                            text> ETB", but not "record text> IRS 
                            ETB", are to be considered as 
                            containing "broken records:", in 
                            which case the partial record from 
                           the block in question will be "cut" 
                           from its block and "pasted" on to the 
                           front of the first record of the next 
                           block from the input device.  The 
                           default is NO. 
MU[LSTRM][={Y[ES]|N[O]}]    YES indicates data for multiple        RBT 
                            devices (e.g., operator console, 
                            line printer) may be included in 
                            the same block.  The default is YES. 
PAD[SIGNON]={Y[ES}|N[O]}                                           RBT 
                            For 2780, 3780 and HASP stations       SYNC 
                            operating in SLAVE mode, this option 
                            specifies whether or not the SIGNON 
                            string sent to remote hosts is to be 
                            extended to 80 characters with 
                            blanks.  The default is YES. 
PROT[YP]={POLLED|2780|3780|HASP} 
                            Indicates the protocol type to         RBT 
                            use with the terminal.  POLLED         SYNC 
                            specifies polled line protocol; 
                            2780 specifies IBM 2780 type 
                            terminal protocol; 3780 specified 
                            IBM 3780 type terminal protocol; 
                            HASP specifies a HASP-protocol 
                            IRBT terminal.  The default is HASP. 
RETR[YS]=value              Specifies the maximum number of        RBT 
                            retries (0-511) to attempt on a        SYNC 
                            line error.  The default is 15. 
RRR={Y[ES]|N[O]}                                                   RBT 
                            For 2780, 3780 and HASP stations,      SYNC 
                            this option specifies whether or not 
                            the CP-6 host should be notified of 
                            the successful transmission of out- 
                            bound data only after a positive 
                            acknowledgement has been received 
                            from the RBT concerning that data. 
                            YES causes the CP-6 FEP to wait for 
                            an ACK or a block of incoming data 
                            from the RBT before sending a 
                            successful completion code to the 
                            CP-6 host, which enhances data 
                            security.  NO causes the CP-6 FEP 
                            to send a successful completion 
                            code to the CP-6 host without 
                            waiting for the positive 
                            acknowledgement, which enhances 
                            data throughput.  The default 
                            is YES. 
SLC={Y[ES]|N[O]}                                                   RBT 
                            For 2780 and 3780 stations, this       SYNC 
                            option specifies whether or not 
                            incoming data for SLAVE stations 
                            will contain device selection bytes, 
                            and whether or not the first block 
                            of outbound data for MASTER stations 
                            should select devices.  The default 
                            is YES. 
SLCALLBLK={Y[ES]|N[O]}                                             RBT 
                            For 2780 and 3780 stations, YES 
                            specifies that all blocks of out- 
                            bound data for MASTER stations 
                            should select devices.  If NO is 
                            specified, the SLC option is 
                            checked.  The default is NO. 
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
COMMUNICATION_PROFILE_OPTIONS
Format: 
{C[REATE]} CON[SOLE] cname [FOR STA[TION] sname] 
{M[ODIFY]} 
or 
D[ELETE] CON[SOLE] 
or 
D[ISPLAY] {[ALL] CON[SOLES] [FOR STA[TION] sname]} [(JCL)] 
          {CON[SOLE] cname [FOR STA[TION] sname] } 
or 
L[IST] {[ALL] CON[SOLES] [FOR STA[TION] sname]} 
       {CON[SOLE] cname [FOR STA[TION] sname] } 
or 
R[EMOVE] CON[SOLE] cname 
Parameters: 
cname    is the 1-8 character name of a console.  If the MODIFY form of the 
command is used and a console does not exist, it is created.  If the LIST or 
DISPLAY form of the command is used, cname can be wildcarded.  If the LIST 
form of the command is used and cname is not specified, all consoles are 
listed. 
sname    is the name of a station (which must exist) with which the console 
will be associated.  If the FOR clause is not specified in the CREATE or 
MODIFY command, the default is LOCAL.  If the FOR clause is not specified in 
the LIST command, all consoles are displayed.  If the LIST or DISPLAY form of 
the command is used, sname can be wildcarded. 
Description: 
The CREATE, DELETE, MODIFY, and REMOVE CONSOLE commands are used to create, 
delete (all), modify, and remove (one) console definitions.  The LIST CONSOLE 
command lists the currently defined consoles.  The DISPLAY CONSOLE command 
shows console definitions. 
Each console created via these commands or as an option of the TERMINAL 
command is assigned a name OCuu where uu is a number from 01 to 99 assigned in 
the order in which consoles for this station are created. 
The LIST CONSOLE command lists console names.  Including cname in the LIST 
CONSOLE command is useful when wildcarding is used or to verify the existence 
of a console definition. 
The DISPLAY CONSOLE command shows a columnized display of the options for 
selected consoles (or all consoles if the ALL option is specified), prefaced 
by a header consisting of the console information as entered in a CREATE or 
MODIFY CONSOLE command.  The JCL option causes the command keyword CREATE to 
be written at the beginning of each console definition and the END keyword to 
be automatically inserted where it is needed. 
The REMOVE CONSOLE command is used to delete one console definition.  The 
DELETE CONSOLE command will remove all console definitions (except 
IOM-connected ones), and should be used with caution.  SUPER attempts to 
protect users from inadvertently deleting all consoles by requiring 
confirmation before a DELETE CONSOLE command is executed.  When the command 
DELETE CONSOLE is issued, SUPER prompts: 
Delete all CONSOLES  ? 
The value YES$ must be supplied or the deletion request is cancelled. 
SUPER prompts for options when it encounters a CREATE or MODIFY CONSOLE 
command.  The options are listed under HELP (SUPER) CONSOLE_OPTS. 
00002
00001
SUPER prompts for options when it encounters a CREATE or MODIFY CONSOLE 
command.  Some console attribute options (such as SYSTEM and ADMIN) specify 
YES, NO, DISPLAY or KEYIN.  DISPLAY allows receipt and display of information, 
KEYIN allows changes, YES means both DISPLAY and KEYIN, NO means neither 
DISPLAY nor KEYIN.  To see all the options, enter ??.  For information about a 
specific option, enter: 
HELP (SUPER) CONSOLE_OPTS option 
where option is: 
ADMIN, CMD, COMMUNICATION, DEVICE, MAXPRIO, PADMIN, PASSWORD, 
PROFILE, SLAVE, SYSTEM, TP, UADMIN, or WSN. 
  Option    Description 
  ADMIN = {YES|NO|DISPLAY|KEYIN} 
            Specifies whether or not this console can display and control 
            running users and jobs in the batch queue associated with its WSN. 
            The default is DISPLAY. 
  CMD = {NONE|string} 
            Specifies an initial keyin to be automatically performed for this 
            console when it logs on.  The default is NONE. 
  CO[MMUNICATION] = {YES|NO|DISPLAY|KEYIN} 
            Specifies whether or not this console can display and control FEPs 
            and communication devices at the line level.  COM = KEYIN is only 
            legal for LOCAL consoles.  The default is NO. 
  DE[VICE] = {YES|NO|DISPLAY|KEYIN} 
            Specifies whether or not this console can display and control 
            devices and symbiont output associated with a terminal or station. 
            The default is YES. 
  MA[XPRIO] = value 
            Specifies the maximum priority (0-14) to which a job in the batch 
            queue can be raised.  A priority 0 job will be queued but not 
            executed.  Used with consoles assigned SYSTEM or PADMIN attributes 
            only.  The default is 7. 
  PAD[MIN] = {YES|NO} 
            Is a shorthand way to describe the ADMIN attributes.  YES is 
            identical to ADMIN = YES, NO turns off the ADMIN = KEYIN 
            attribute. 
  PA[SSWORD] = {NONE|password} 
            Specifies the 1-8 character logon password for the console.  Any 
            printable character can be used in the password value.  The 
            default is NONE. 
  PR[OFILE] = {NONE|pname} 
            Specifies the default profile for this console.  If pname is 
            specified, the identified profile must have been defined.  The 
            default is NONE, which means the handler default is used. 
  SL[AVE] = {Y[ES]|N[O]} 
            Specifies whether this console treats the CP-6 system itself as a 
            console.  All "keyins" (data items received on this path from the 
            remote site) are simply displayed on COMMUNICATION and SYSTEM 
            consoles.  This console attribute is usually used when running a 
            CP-6 system as a master IRBT to another CP-6 system or when 
            defining the CP-6 system to be a slave IRBT to a non-CP-6 system 
            which requires the remote station (e.g., the CP-6 system) to be a 
            slave.  If SLAVE is specified, no other console attribute is 
            legal.  The default is NO. 
  SY[STEM] = {YES|NO|DISPLAY|KEYIN} 
            Specifies whether or not this console shall have full system 
            control powers.  SYSTEM = YES or KEYIN is only legal on LOCAL 
            consoles.  SYSTEM consoles incorporate all the other attributes. 
            The default is NO. 
  TP = {YES|NO|DISPLAY|KEYIN} 
            Specifies that this console may be used to communicate with an 
            instance of TP.  KEYIN specifies that the console can issue TP 
            commands to any specified instance.  DISPLAY specifies that TP 
            abort messages will be displayed on the console.  NO is the 
            default. 
  UA[DMIN] = {YES|NO} 
            Is a shorthand way to describe the ADMIN = DISPLAY attribute.  YES 
            is equivalent to ADMIN = DISPLAY, NO turns off the ADMIN display 
            attribute. 
  WSN = wname 
            Specifies a 1-8 character name of the workstation(s) controlled by 
            this console.  The last character may be '?', in which case all 
            workstations with names that match up to the '?' are those 
            controlled.  For example, WSN = ABC?  means that ABC, ABCD, ABCQ, 
            etc. are controlled.  The default is sname, as described above 
            under parameters. 
00001
00002
00003
00004
00005
00007
00006
00007
00008
00009
00010
00011
00012
00013
CONSOLE_OPTIONS
Format: 
{C[REATE]} 
{M[ODIFY]} CONT[ROLLER] ctnum FOR LINE lname 
{R[EMOVE]} 
or 
D[ISPLAY] {[ALL] CON[TROLLERS] [FOR LINE lname]} [(JCL)] 
          {CON[TROLLER] ctnum [FOR LINE lname] } 
or 
L[IST] {[ALL] CON[TROLLERS] [FOR LINE lname]} 
       {CON[TROLLER] ctnum [FOR LINE lname] } 
Parameters: 
ctnum    specifies the poll address (0-31) of the controller.  IF MODIFY is 
specified and a controller does not exist, it is created.  If the LIST or 
DISPLAY form of the command is used, ctnum can be wildcarded. 
lname    specifies the name of the line with which the controller will be 
associated.  lname consists of 1-8 alphanumeric characters and can include the 
special characters ':', '$', '*'.  If the LIST or DISPLAY form of the command 
is used, lname can be wildcarded. 
Description: 
The CREATE, MODIFY and REMOVE CONTROLLER commands create, modify, and remove 
(one) 3270 or polled VIP controller definitions.  The LIST CONTROLLER command 
lists the currently defined controllers.  The DISPLAY CONTROLLER command 
displays controller definitions.  A CONTROLLER is a description of the 
attributes of a 3270 or polled VIP controller.  (A polled VIP controller is 
one defined for a line whose profile is RBT with a PROTYP of HIP. 
SUPER prompts for the options below when it encounters a CREATE, MODIFY, or 
DISPLAY CONTROLLER command. 
00002
00001
A list of CONTROLLER command options and their definitions can be accessed by 
typing a ? or ??.  To access individual options, type: 
HELP (SUPER) CONTROLLER_OPTS option 
where option is any of the following: 
COLUMNS, ROWS, or TYPE 
  Option    Description 
  C[OLUMNS] = decimal 
            Specifies the number of columns (40-255) on the screen.  The 
            default is 80. 
  R[OWS] = decimal 
            Specifies the number of rows (12-255) on the screen.  The default 
            is 24. 
  T[YPE] = {2780|3271|3274|3275|3276|7700|7804} 
            Specifies the type of controller.  3271 and 3274 are treated 
            identically.  3276 (the default) causes an ERASE WRITE ALTERNATE 
            command to be sent, which puts the devices into large-screen mode. 
The LIST CONTROLLER command lists the poll number (only) of selected or, if 
the ALL option is specified instead of a controller poll number, all 
controllers.  Including ctnum in the LIST CONTROLLER command is useful when 
wildcarding is used or to verify the existence of a controller definition. 
The DISPLAY CONTROLLER command lists a columnized display of the options for 
selected controllers (or all controllers if the ALL option is specified), 
prefaced by a header consisting of the controller information as entered in a 
CREATE or MODIFY CONTROLLER command.  The controller name can be wildcarded. 
The JCL option causes the command keyword CREATE to be written at the 
beginning of the header and the keyword END to be inserted where needed. 
00001
00002
00003
CONTROLLER_OPTIONS
Format: 
C[REATE] [.]account1, name1 [FROM {[.]account2, name2}] 
                            [     {DEFAULT           }] 
Parameters: 
account1, name1    is the logon ID.  This combination must be entered to gain 
access to the CP-6 system.  The account is limited to 8 characters, the name 
to 12.  The valid character set consists of alphanumeric characters plus the 
characters $ and :. 
FROM account2, name2    indicates that each item not explicitly specified at 
the option level is to be set to the value of the corresponding item of the 
authorization record identified by this logon ID. 
FROM DEFAULT    indicates that each item not explicitly specified at the 
option level is to be set to the value of the corresponding item of the 
default authorization record.  (The default record may be initialized by 
substituting the keyword DEFAULT for the account-name logon ID, i.e., CREATE 
DEFAULT.  Use of the DEFAULT authorization permits the definition of many 
users with a minimum of effort.) 
If FROM is not specified, FROM DEFAULT is assumed. 
Description: 
This command invokes the user authorization mode of SUPER.  Options that may 
be entered in this mode can be accessed by typing HELP (SUPER) USER_OPTS. 
00002
00001
Format: 
{C[REATE]} CHAR[SET] charsetname 
{M[ODIFY]} 
Parameters: 
charsetname    is the one-to-eight character name of the CHARSET record to be 
created or modified.  The charsetname can be a combination of alphabetic 
characters, numeric characters and the special characters; colon (:), dollar 
sign ($), and asterisk (*). 
Description: 
The CREATE/MODIFY CHARSET command is used to define a CHARSET record.  SUPER 
requests options with the prompt OPT* when it encounters a CREATE or MODIFY 
CHARSET command.  There are three CHARSET options, one that identifies each of 
the three parts of a CHARSET record: 
AT[TRIBUTES] 
DE[VICES] 
IM[AGE] 
When ATTRIBUTES is specified, it is followed by an attribute list.  When 
either DEVICES or IMAGE is specified, SUPER prompts for suboptions with the 
prompt 'SUB*'.  Entering a blank line or 'END' returns the user from 'SUB*' to 
'OPT*', and from 'OPT*' to 'CMD*'.  Multiple devices can be chained at the 
suboption level by linking them with semicolons; but, each IMAGE entry must be 
entered on a separate line. 
See: HELP (SUPER) CHARSET_OPTS for a summary of the options. 
00002
00001
CREATE_COMMANDS
See the following topics: 
HELP (SUPER) CONSOLE, CONTROLLER, CREATE, CREATE_CHARSET, CREATE_FORM, 
CREATE_FORM_GRAPHICS, CREATE_PSEUDO, CREATE_PROJECT, CREATE_USER, DEVICE, 
DEVICE_FOR_LINE, DEVICE_FOR_LINK, LINE, LINK, PROFILE, STATION, TERMINAL, 
VIRTUAL_CIRCUIT, WSN. 
Format: 
{C[REATE]} FOR[M] formname [FROM formname2] 
{M[ODIFY]} 
Parameters: 
formname    is the one-to-six character name of the form to be created or 
modified.  The formname can be a combination of alphabetic characters, numeric 
characters, and the special characters:  colon (:), dollar sign ($) and 
asterisk (*). 
formname2    is the name of an existing form to be used to obtain the option's 
default setting.  If the FROM clause is not specified, the default for CREATE 
is from STDLP. 
Description: 
The CREATE/MODIFY FORM command is used to construct a line-oriented form or 
modify an existing form.  SUPER requests options with the prompt 'OPT*' when 
it encounters a CREATE or MODIFY FORM command.  All options default to the 
value in the formname2 record.  To access these options, type HELP (SUPER) 
FORM_OPTS. 
If the BANNER or ALIGNMENT options are entered, SUPER prompts with 'SUB*', and 
the user may enter options listed under HELP (SUPER) BAN_SUBOPTS or HELP 
(SUPER) ALIGN_SUBOPTS.  Note that specifying the BANNER or ALIGNMENT options 
removes the entire banner or alignment image: the image must be recreated. 
The values for the ENTRY sub-option of the BANNER and ALIGNMENT options are 
available by typing HELP (SUPER) ENTRY_OPTS.  After the ENTRY sub-option is 
typed, SUPER prompts with: 'TXT*'.  The responses to the prompt are available 
by typing HELP (SUPER) ENTRY_TEXT.  Entering a blank line returns the user 
from 'TXT*' to 'SUB*', from 'SUB*' to 'OPT*', from 'OPT*' to 'CMD*'. 
Line-oriented forms are deleted, listed, displayed, and removed using the 
DELETE FORMS, LIST FORM, DISPLAY FORM, and REMOVE FORM commands. 
Usage Note: 
The total length of the form definition is subject to the following 
restrictions: 
  FIXED + ACCESS + ACCOUNT + BANNER > 700 words 
and 
  FIXED + ACCESS + ACCOUNT + BANNER + ALIGNMENT + SETUP > 1024 words 
00002
00001
00003
Format: 
{C[REATE]} FOR[M] formname [FROM formname2] [(]GR[APHICS][)] 
{M[ODIFY]} 
Parameters: 
formname    is the one-to-six character name of the graphic form to be created 
or modified.  The formname can be a combination of alphabetic characters, 
numeric characters, and the special characters:  colon (:), dollar sign ($) 
and asterisk (*). 
FROM formname2    names an existing graphic form to be used to obtain the 
option's default settings.  If the FROM phrase is not specified, the keyword 
GRAPHICS must be specified and the default for CREATE is from STDGR.  If the 
FROM phrase is specified, the form name must be a graphic form and the keyword 
GRAPHICS may be omitted. 
GRAPHICS    specifies that the form is a graphic form.  This keyword need only 
be specified for a CREATE FORM if the FROM phrase is not specified; GRAPHICS 
is never required with the MODIFY FORM command. 
Description: 
The CREATE/MODIFY FORM GRAPHICS command is used to construct a graphic form or 
modify an existing form.  SUPER requests options with the prompt 'OPT*' when 
it encounters a CREATE or MODIFY FORM GRAPHICS command.  All options default 
to the value in the formname2 record.  To access these options, type HELP 
(SUPER) GRAPHICS_FORM_OPTS. 
If the ALIGNMENT or BANNER options are entered, SUPER prompts with 'SUB*', and 
the user may enter options listed under HELP (SUPER) GRAPHICS_BAN_SUBOPTS or 
GRAPHICS_ALIGN_SUBOPTS.  Note that specifying the BANNER or ALIGNMENT options 
removes the entire banner or alignment image: the image must be recreated. 
The values for the ENTRY sub-option of the BANNER and ALIGNMENT options are 
available by typing HELP (SUPER) GRAPHICS_ENTRY_OPTS.  After the ENTRY 
sub-option is typed, SUPER prompts with: 'TXT*'.  The responses to the prompt 
are available by typing HELP (SUPER) ENTRY_TEXT.  Entering a blank line 
returns the user from 'TXT*' to 'SUB*', from 'SUB*' to 'OPT*', and from 'OPT*' 
to 'CMD*'. 
Graphic forms are deleted, displayed, listed and removed using the DELETE 
FORM, LIST FORM, DISPLAY FORM, and REMOVE FORM commands. 
Usage Note: 
The total length of the form definition is subject to the following 
restrictions: 
  FIXED + ACCESS + ACCOUNT + BANNER < 700 words 
and 
  FIXED + ACCESS + ACCOUNT + BANNER + ALIGNMENT + SETUP < 1024 words 
00002
00001
00003
Format: 
C[REATE] PROJ[ECT] [.]account1, name1 [FROM [.]account2, name2] 
Parameters: 
account1, name1    is the logon ID for the project administrator of the 
project being created.  The account is limited to 8 characters, the name to 
12.  The valid character set consists of the alphanumeric characters plus the 
characters $ and :. 
FROM account2, name2    indicates that each item not explicitly specified at 
the option level is to be set to the value of the corresponding item in the 
project authorization record identified by this logon ID. 
Description: 
This command invokes the project authorization mode of SUPER.  A list of 
options that may be entered in this mode may be accessed by typing HELP 
(SUPER) PROJECT_OPTS. 
00002
00001
Format: 
{C[REATE]} PS[EUDO] formname [FOR formname2] 
{M[ODIFY]} 
Parameters: 
formname    is the one-to-six character name of the pseudo form to be created 
or modified.  The formname can be a combination of alphabetic characters, 
numeric characters and the special characters:  colon (:), dollar sign ($) and 
asterisk (*). 
formname2    is the name of an existing form to be used to obtain the option's 
default settings; formname2 also defines the alignment and setup information 
needed for the pseudo form.  If the FOR clause is not specified, the default 
for CREATE is STDLP. 
Description: 
The CREATE/MODIFY PSEUDO command is used to define a pseudo form.  Pseudo 
forms can be defined for line-oriented forms and for graphic forms.  For both 
line-oriented and graphic forms, pseudo forms can be used to allow an 
installation to define one type of paper to be many forms, and not have to 
perform a 'FORM' keyin to change the form.  This allows the same paper to be 
used with different banners and account lists.  In addition, for line-oriented 
forms, a pseudo form allows the same FORM to be used for different VFU images 
and margins, and, for graphic forms, a pseudo form can be used to define a 
media size that differs from the physical size definition of the device. 
SUPER requests options with the prompt 'OPT*' when it encounters a CREATE or 
MODIFY PSEUDO command.  All options default to the value in the formname2 
record.  For line-oriented forms, any of the FORM options under HELP (SUPER) 
FORM_OPTS can then be entered, except for the following:  ALIGNMENT, CHARSET, 
LPI, and SETUP. 
For graphic forms, any of the FORM options under HELP (SUPER) 
GRAPHICS_FORM_OPTS can then be entered, except for the following:  ALIGNMENT, 
CHARSET, DEVICE, and SETUP. 
Pseudo forms are deleted, listed, displayed and removed using the DELETE FORM, 
DISPLAY FORM, LIST FORM and REMOVE FORM commands. 
00002
00001
CREATE
A list of cursor profile options and their definitions can be accessed by 
typing a ? or ??.  To access individual options, type: 
HELP (SUPER) CURSOR_PROFILE_OPTS option 
where option is any of the following: 
AUTONL, AUTOTABCLM, AWIDTH, BLANKERASES, CRISNL, CUB_CHR, CUD_CHR, CUF_CHR, 
CUP_ALG, CUP_BIS, CUP_CHR, CUP_CLMFRS, CUP_CMP, CUU_CHR, DCH_CHR, DEVICEBS, 
DEVICECR, DEVICELF, DEVPOSOPTS, DEVSCROLL, DLTLIN_CHR, DSPHEIGHT, ED0_CHR, 
ED2_CHR, EL0_CHR, ENDMSGLIN_CHR, EWALT, EXTSRD_CHR, FF_FLUSH, FF_INCCR, 
FRMFED_CHR, HEIGHT, ICH_CHR, ICHRQRDCH, ILNRQRDLIN, INPUT, INSERTMODE, 
INSLIN_CHR, LFISNL, LIMBOCLM, MSGLIN, OPDTAB, PROGDTAB, RGNSCROLL, and 
RSTINSMOD_CHR. 
  Option                       Description                           Device 
AUTONL[={Y[ES]|N[O]}]       YES specifies that after the           ASYNC 
                            terminal prints (or spaces) in         POLLVIP 
                            its right margin column (AWIDTH), 
                            it will automatically effect a 
                            CR/LF.  NO means the cursor either 
                            stays in the right margin column 
                            or goes to a non-displayable 
                            column just to the right margin 
                            column. 
AUTOT[ABCLM]=value          Specifies the initial cursor           ASYNC 
                            position (0-255) to use when a         POLLVIP 
                            read a new record request occurs.      3270 
                            A value of 0 to 1 specifies that 
                            the input data is to begin 
                            immediately after the prompt. 
AW[IDTH]=value              Specifies the number of printable      ASYNC 
                            columns (0 to 508) in the terminal.    POLLVIP 
                            The default is 80 for ASYNC,           RBTD 
                            POLLVIP, RBTD, and 3270, but 132       URP 
                            URP.  A value of 255 is the same as    3270 
                            DC.  (See the PWIDTH option under 
                            OPERATIONAL_PROFILE_OPTIONS.) 
BLA[NKERASES][=Y[ES]|N[O]|D[C]}] 
                            YES means that a blank (space)         ASYNC 
                            character displayed on the             POLLVIP 
                            terminal in a position occupied        3270 
                            by another character erases the 
                            previous character.  NO means 
                            that the previous character is 
                            unchanged. 
CR[ISNL][={Y[ES]|N[O]|D[C]}] 
                            YES specifies that when the            ASYNC 
                            terminal is sent a CR character,       POLLVIP 
                            it will perform a new-line 
                            carriage return and line feed.  NO 
                            means that CR does not cause the 
                            new line function.  If CRISNL=YES 
                            is specified, DEVICECR=YES must 
                            not be specified. 
CUB[_CHR]=hex_list          Specifies the characters that          ASYNC 
                            cause the cursor to move back          POLLVIP 
                            one column. 
CUD[_CHR]=hex_list          Specifies the characters that          ASYNC 
                            cause the cursor to move down          POLLVIP 
                            one line. 
CUF[_CHR]=hex_list          Specifies the characters that          ASYNC 
                            cause the cursor to move forward       POLLVIP 
                            one column. 
CUP_A[LG]={0|ANS|1|TBL|2}   Establishes the cursor position-       ASYNC 
                            ing algorithm as follows:              POLLVIP 
                            Values    Meaning 
                            0         Used as a reset value. 
                            ANS       Specifies the ANS X3.64 
                                      CUP. 
                            TBL       Specifies a table-driven 
                                      algorithm as defined by 
                                      the CUP_BIS, CUP_CLMFRS 
                                      CUP_CMP and CUP_CHR 
                                      options. 
CUP_B[IS]={value|hex|NONE}  Establishes the CUP bias to be         ASYNC 
                            added to the column and line           POLLVIP 
                            numbers.  This value can be 
                            expressed as a decimal number 
                            (0-255) or a hexadecimal number. 
                            The default is zero. 
CUP_CH[R]=hex_list          Specifies the characters that          ASYNC 
                            introduce the cursor position          POLLVIP 
                            sequence. 
CUP_CL[MFRS][={Y[ES]|N[O]}] Determines whether column (YES)        ASYNC 
                            or line (NO) is sent first.  The       POLLVIP 
                            default is NO. 
CUP_CM[P][={Y[ES]|N[O]}]    Determines whether line and column     ASYNC 
                            values are to be complemented or       POLLVIP 
                            not.  The default is NO. 
CUU[_CHR]=hex_list          Specifies the characters that          ASYNC 
                            cause the cursor to move up one        POLLVIP 
                            line. 
DCH[_CHR]=hex_list          Specifies the character sequence       ASYNC 
                            that deletes the character under       POLLVIP 
                            the cursor by sliding the rest 
                            of the current line one character 
                            to the left (see ICH_CHR). 
DEVICEB[S][={Y[ES]|N[O]|C[D]}] 
                            YES indicates that a BS character      ASYNC 
                            sent to the terminal causes a          POLLVIP 
                            backspace.  NO specifies that a BS 
                            character be processed normally, 
                            which may or may not cause a 
                            backspace.  The default is YES. 
DEVICEC[R][={Y[ES]|N[O]|D[C}}] 
                            YES specifies the terminal will        ASYNC 
                            perform only the normal CR function    POLLVIP 
                            if sent a CR (e.g., it would not 
                            also perform the line feed function, 
                            yielding a new-line).  NO means 
                            that CR has some other or no effect. 
                            The default is YES. 
DEVICEL[F][={Y[ES]|N[O]|D[C]}] 
                            YES specifies the terminal will        ASYNC 
                            perform only the normal LF function    POLLVIP 
                            if sent a LF (e.g., it will not 
                            also perform the carriage return 
                            function, yielding a new-line). 
                            NO means that LF has some other 
                            or no effect.  The default is YES. 
DEVP[OSOPTS][={Y[ES]|N[O]|D[C]}] 
                            Indicates whether or not the           ASYNC 
                            terminal combines contiguous           POLLVIP 
                            horizontal positioning requests 
                            into a single internal operation. 
                            YES implies that if a tab to 
                            column 10 followed by a backspace 
                            were sent to the terminal, the 
                            carriage would go directly to 
                            column 9.  The default is NO. 
DEVS[CROLL][={Y[ES]|N[O]|D[C]}] 
                            YES specifies that the terminal is     ASYNC 
                            self-scrolling and should only be      POLLVIP 
                            specified for CRT devices.  This       3270 
                            means that it rolls old lines off 
                            its screen as new ones are added 
                            at the bottom.  NO means that 
                            lines are overwritten when the 
                            screen is filled or the device is 
                            not a CRT.  The default is NO. 
DLTL[IN_CHR]=hex_list       Specifies the character sequence       ASYNC 
                            that creates a blank line at the       POLLVIP 
                            bottom of the screen by pulling 
                            all lines below the current one 
                            up one line. 
DSPH[EIGHT]={value|D[C]}    Specifies the number (0-255) of        ASYNC 
                            displayable lines on a screen.         POLLVIP 
                            Used only for screen-type 
                            terminals and only if DSPHEIGHT 
                            is less than HEIGHT.  DSPHEIGHT 
                            causes the default scrolling 
                            operation of the terminal to use 
                            the bottom DSPHEIGHT lines 
                            so that direct cursor positioning 
                            can be used.  The remaining 
                            terminal lines function as a 
                            capture buffer.  If 
                            DSPHEIGHT=0, DSPHEIGHT=HEIGHT 
                            is assumed.  The default is DC. 
                            A value of 255 is the same as DC. 
ED0[_CHR]=hex_list          Specifies the characters that          ASYNC 
                            determine how to perform erasures      POLLVIP 
                            from the current cursor position 
                            through the end of the display. 
ED2[_CHR]=hex_list          Specifies the characters that          ASYNC 
                            cause the entire display to be         POLLVIP 
                            erased. 
EL0[_CHR]=hex_list          Specifies the characters that          ASYNC 
                            determine how to perform erasures 
                            from the current cursor position       POLLVIP 
                            through the end of the line. 
ENDM[SGLIN_CHR]=hex_list    Specifies the character sequence       ASYNC 
                            that repositions the cursor to the     POLLVIP 
                            position at which a MSGLIN_CHR 
                            was sent. 
EW[ALT][={Y[ES]|N[O]}]      YES specifies that an                  ASYNC 
                            ERASE-WRITE-ALTERNATE command is       POLLVIP 
                            sent to the device to initiate the 
                            large-screen mode.  The default is 
                            NO. 
EXTSRD[_CHR]=hex_list       Specifies the character sequence       ASYNC 
                            needed to exit an SRD (window)         POLLVIP 
                            to go to a different SRD.  Typically, 
                            this option is used only to exit an 
                            SRD being used by a graphics program, 
                            and is the sequence that restores 
                            the terminal to alphanumeric mode 
                            (from graphics mode).  This sequence 
                            is only sent if M$TRMCTL EXBEXTSRD 
                            = YES. 
FF_FL[USH]=[={Y[ES]|N[O]|D[C]}] 
                            Specifies how to complete the          ASYNC 
                            display of buffered data for           POLLVIP 
                            a device.  YES specifies that 
                            the device needs to have a 
                            form-feed operation performed 
                            to complete the display of 
                            any data still buffered in the 
                            device.  NO specifies that a 
                            new-line operation is 
                            sufficient.  The default is 
                            DC. 
FF_IN[CCR][= {YES|NO|DC}]                                          ASYNC 
                            YES specifies that the form-feed       POLLVIP 
                            function for this terminal also 
                            positions to the left margin.  NO 
                            specifies that it positions only 
                            vertically.  The default is DC. 
FRMFED[_CHR]=hex_list       Specifies the characters that          ASYNC 
                            cause the cursor or device to          POLLVIP 
                            skip to the first line after 
                            the perforation. 
                            For ASYNC printers the applicable 
                            timing for the form feed is: 
                            (TMNALG_PRM6 * MOVEMENT-IN-LINES) + 
                            TMNALG_PRM7.  See 
                            TIMING_PROFILE_OPTIONS. 
HE[IGHT]={value|D[C]}       Indicates the number of lines          ASYNC 
                            (0-999) on the screen of a             POLLVIP 
                            screen-type terminal.  Height is       3270 
                            0 for non-screen-type terminals. 
                            The default is zero for ASYNC; but 
                            24 for POLLVIP and 3270.  HEIGHT=0 
                            implies no overstriking. 
ICH[_CHR]=hex_list          Specifies the character sequence       ASYNC 
                            that either 1) inserts a blank 
                            space at the cursor position, 
                            pushing the remaining characters 
                            on the same line to the right 
                            (see DCH_CHR), or, if 
                            RSTINSMOD_CHR is also specified, 
                            2) sets a mode that causes any 
                            character to be similarly inserted 
                            (see DCH_CHR and RSTINSMOD_CHR). 
ICHR[QRDCH][={Y[ES]|N[O]}]  Specifies whether the device will      ASYNC 
                            balk if a character insert is 
                            attempted when a character is 
                            present in the rightmost column 
                            of the line.  The default is NO. 
ILNR[QRDLIN][={Y[ES]|N[O]}] Specifies whether the device will      ASYNC 
                            balk if a line insert is attempted     POLLVIP 
                            when any characters are present on 
                            the bottom line of the screen. 
                            The default is NO. 
INPUT[={Y[ES]|N[O]|D[C]}]   Specifies whether or not the           ASYNC 
                            terminal or device is capable          POLLVIP 
                            of transmitting input.  The default    RBTD 
                            is YES for ASYNC, POLLVIP, URP and     URP 
                            3270, but NO for RBTD.                 3270 
INSE[RTMODE][={Y[ES]|N[O]|D[C]} 
                            Specifies whether insert mode is       ASYNC 
                            to be enabled or not.  The 
                            default is DC. 
INSL[IN_CHR]=hex_list       Specifies the character sequence       ASYNC 
                            that creates a blank line at the       POLLVIP 
                            current character position by 
                            pushing down the current line and 
                            those below. 
LF[ISNL][={Y[ES]|N[O]|D[C]}] 
                            YES specifies that when the            ASYNC 
                            terminal is sent a LF character        POLLVIP 
                            it will do a new-line carriage         RBTD 
                            return and line feed.  NO specifies 
                            that LF does not cause the new 
                            line function.  If LFISNL=YES is 
                            specified, then DEVICELF=YES 
                            must not be specified. 
LIMBOCLM[={Y[ES|N[O]|D[C]}] YES specifies that after the           ASYNC 
                            terminal prints (or spaces) in its     POLLVIP 
                            right margin column (usually 80 or 
                            132), the cursor remains on the 
                            current line, such that a backspace 
                            operation returns to (or stays) in 
                            the rightmost column.  NO specifies 
                            that a backspace after printing in 
                            the rightmost column positions to 
                            the left of the rightmost column. 
                            Applicable only if AUTONL=NO.  The 
                            default is DC. 
MSGL[IN_CHR]=hex_list       Specifies the character sequence       ASYNC 
                            that positions into a message          POLLVIP 
                            line, if one exists on the ter- 
                            minal.  This option should not be 
                            specified unless ENDMSGLIN_CHR is 
                            specified also. 
OP[DTAB][={Y[ES]|N[O]|D[C]}] 
                            YES specifies that the terminal        ASYNC 
                            has device tabs that can be set        POLLVIP 
                            by the operator.  NO specifies 
                            that they are programmatic or 
                            nonexistent and is the default. 
                            This option is not currently 
                            implemented. 
PROG[DTAB][={Y[ES]|N[O]|D[C]}] 
                            YES indicates that the terminal        ASYNC 
                            device tabs are programmatic.  NO      POLLVIP 
                            indicates that the terminal device 
                            tabs are manual and is the default. 
                            This option is not currently 
                            implemented. 
RGNSCROLL[={Y[ES]|N[O]}]    Specifies whether or not region        ASYNC 
                            scrolling is to be used.  The default  POLLVIP 
                            is NO.  If the terminal conforms to 
                            DEC implementation for scrolling regions 
                            (i.e., accepts "ESC [ lt ; lb r" 
                            to define the (only) scrolling region to 
                            be the lines contained by and including 
                            lt and lb, with lt <lb and the top line of 
                            the screen is numbered 1) then setting 
                            RGNSCROLL=YES and the following SUPER options 
                            causes regions to be used instead of 
                            INSLIN/DLTLIN for scrolling partial screens: 
                            INSLIN_CHR=the sequence to use at lt to 
                            scroll (reverse index) 
                            DLTLIN_CHR=the sequence to use at lb to 
                            scroll (index - usually LF) 
RSTINS[MOD_CHR]=hex_list    Specifies the character sequence       ASYNC 
                            that resets insert mode set by 
                            ICH_CHR.  Note that the specification 
                            of RSTINSMOD_CHR affects the 
                            meaning of ICH_CHR. 
00001
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
00023
00024
00025
00026
00027
00028
00029
00030
00029
00030
00031
00032
00033
00034
00033
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
CURSOR_PROFILE_OPTIONS
CREATE_CHARSET
CREATE_FORM
CREATE_FORM_GRAPHICS
CREATE_PROJECT
CREATE_PSEUDO
DISPLAY
DELETE_USERS
Format: 
DEL[ETE] CHAR[SET] 
Description: 
The DELETE CHARSET command is used to delete ALL CHARSET records and rebuild 
the CP-6 supplied ones in the :FORM file. 
00001
DELETE_COMMANDS
See the following topics: 
HELP (SUPER) CONSOLE, DELETE_CHARSET, DELETE_FORMS, DELETE_USERS, DEVICE, 
PROFILE, TERMINAL. 
Format: 
DEL[ETE] F[ORMS] 
Description 
The DELETE FORMS command is used to delete ALL forms and rebuild the three 
initial forms (STDLP, STDGR and STD**) in the :FORM file. 
SUPER attempts to protect users from inadvertently deleting all forms by 
requiring confirmation before a DELETE FORMS command is executed.  When the 
command DELETE FORMS is issued, SUPER prompts: 
    Delete all FORMS  ? 
The value YES$ must be supplied or the deletion request is cancelled. 
00001
Format: 
DEL[ETE] U[SERS] 
Description: 
This command deletes all user authorizations and rebuilds the default users. 
Care should be taken when using this command. 
SUPER protects administrators from inadvertently deleting all users by 
requiring confirmation before a DELETE USERS command is executed.  When the 
command DELETE USERS is issued, SUPER prompts: 
    Delete all USERS   ? 
The value YES$ must be supplied or the deletion request is cancelled. 
00001
DELETE_CHARSET
DELETE_FORMS
Format: 
C[REATE] {DEV[ICE] dname [FOR STATION sname]} 
         {TP [DEV[ICE]] id                  } 
or 
D[ELETE] DEV[ICE] 
or 
          {[ALL] DEV[ICES] [FOR STA[TION] sname]      } 
D[ISPLAY] {[use] DEV[ICE] dname [FOR STA[TION] sname] } [(JCL)] 
          {TP [DEV[ICE]] account[,uname]              } 
or 
       {[ALL] DEV[ICES] [FOR STA[TION] sname]      } 
L[IST] {[use] DEV[ICE] dname [FOR STA[TION] sname] } 
       {TP [DEV[ICE]] account[,uname]              } 
or 
M[ODIFY] {DEV[ICE] dname [FOR STATION sname]} 
         {TP [DEV[ICE]] id                  } 
or 
R[EMOVE] {DEV[ICE] dname               } 
         {TP [DEV[ICE]] account[,uname]} 
For more information on DEVICE commands, please see the 
topics DEVICE_FOR_LINK and DEVICE_FOR_LINE. 
Parameters: 
dname    is the 1-8 character name of the device.  If the MODIFY form of the 
command is used and a device does not exist, it is created.  If the LIST 
command is entered without dname, all devices are listed.  If the LIST or 
DISPLAY form of the command is used, dname can be wildcarded. 
sname    is the 1-8 character name of a station with which the device will be 
associated.  If the FOR clause is not specified in the CREATE or MODIFY 
command, the default is LOCAL.  If sname is omitted in the LIST command, 
devices for all STATIONs are listed.  If the LIST or DISPLAY form of the 
command is used, sname can be wildcarded. 
id    can be either: 
    dname 
    account,uname 
dname    same as above. 
account,uname    account is the 1-8 character account, and uname is the 1-12 
character station name (sname) (See Description, below.)  If uname is 
specified as more than 8 characters, the value will truncate to 8 characters 
for SUPER purposes (i.e., as the sname value), and a warning diagnostic will 
be issued by SUPER.  However, the full value will be entered as the key in the 
:HLP file entry for the TP device. 
use    is CG, IN[SYM], OUT[SYM], RES[OURCE], or TP.  Use specifies the type of 
device to be listed or displayed.  If "use" is not specified, all five types 
of devices will be listed or displayed. 
Description: 
The CREATE, DELETE, MODIFY, and REMOVE DEVICE commands are used to create, 
delete (all), modify, and remove (one) device definitions.  The LIST DEVICE 
command is used to list the currently defined devices.  The DISPLAY DEVICE 
command is used to show device definitions. 
Asynchronous devices which connect like timesharing terminals but are used as 
peripherals (e.g., an on-line plotter, a 1200 baud keyboard display used as a 
symbiont printer) are assigned names of the form dduu.  dd is from the TYPE 
option and uu is an incrementing number (01-99) within the TYPE and station. 
Comgroups and TP stations are assigned names of the form CG nntttt, where nn 
is from the TYPE option and tttt is a four digit decimal number. 
The LIST [use] DEVICE command lists device names.  Including dname in the LIST 
DEVICE command is useful when wildcarding is used or to verify the existence 
of a device definition. 
The DISPLAY [use] DEVICE command lists a columnized display of the options for 
selected devices (or all devices if the ALL option is specified), prefaced by 
a header consisting of device information as entered in a CREATE or MODIFY 
command.  The JCL option causes the command keyword CREATE to be written in 
front of each listed DEVICE definition and the keyword END to be inserted as 
needed. 
The REMOVE DEVICE command is used to delete one device definition.  The DELETE 
DEVICE command will delete all device definitions (except IOM-connected ones), 
and should be used with caution.  SUPER attempts to protect users from 
inadvertently deleting all devices by requiring confirmation before a DELETE 
DEVICE command is executed.  When the command DELETE DEVICE is issued, SUPER 
prompts: 
Delete all DEVICES   ? 
The value YES$ must be supplied or the deletion request is cancelled. 
SUPER prompts for options when it encounters a CREATE or MODIFY DEVICE 
command. 
The effect of including the keyword TP in a CREATE, MODIFY, LIST, DISPLAY or 
REMOVE DEVICE command is to perform an automatic USE=TP (see HELP (SUPER) 
DEVICE_OPTIONS).  If TP is specified, the keyword DEVICE is assumed; its 
specification becomes optional. 
When TP is specified, either a device or a TP logon may be specified in the 
CREATE and MODIFY forms of the DEVICE command.  The format: 
    {CREATE|MODIFY} TP [DEVICE] dname 
specifies the 8 character blank-filled key that will be stored as a device key 
(i.e., with an asterisk appended) in the :HLP file.  The format: 
    {CREATE|MODIFY} TP [DEVICE] account,uname 
specifies the TP logon to be stored in the :HLP file.  The effect of including 
uname with the TP keyword is to perform an automatic USE=TP and an automatic 
SNAME=uname, also. 
For more information on how to create TP stations, refer to the CP-6 TP 
Administrator Guide (CE50). 
For the DEVICE command options, see: HELP (SUPER) DEVICE_OPTIONS. 
00002
00001
SUPER profile device attribute options are divided into the following types: 
  CURSOR CONTROL OPTIONS 
  FIELD CONTROL OPTIONS 
  MISCELLANEOUS OPTIONS 
  TIMING OPTIONS 
See the topic PROFILE_OPTION_SUMMARY for a listing of all PROFILE 
options.  That summary includes, for each option, a pointer to the 
OPTIONS topic that contains option syntax and description.  The 
profile option topics can be accessed directly by entering: 
  HELP (SUPER) topic 
where topic is one of the following: 
  CURSOR_PROFILE_OPTIONS 
  FIELD_PROFILE_OPTIONS 
  MISC_PROFILE_OPTIONS 
  TIMING_PROFILE_OPTIONS 
See PROFILE_OPTIONS for a complete listing of profile option topics. 
Format: 
{C[REATE]} 
{M[ODIFY]} DEV[ICE] dnum FOR LINE lname CONT[ROLLER] ctnum 
{R[EMOVE]} 
or 
D[ISPLAY] {[ALL] DEV[ICES] [FOR LINE lname] [CONT[ROLLER] ctnum]} [(JCL)] 
          {DEV[ICES] dnum [FOR LINE lname] [CONT[ROLLER] ctnum] } 
or 
L[IST] {[ALL] DEV[ICES] [FOR LINE lname] [CONT[ROLLER] ctnum]} 
       {DEV[ICE] dnum [FOR LINE lname] [CONT[ROLLER] ctnum]  } 
Parameters: 
dnum    specifies the device number (0-31) for the device to be created, 
modified or removed.  If MODIFY is specified and a device does not exist, it 
is created.  If the LIST or DISPLAY form of the command is used, dnum can be 
wildcarded 
lname    specifies the name of the line with which the device will be 
associated (see CREATE LINE).  lname consists of 1-8 alphanumeric characters 
and can include the special characters ':', '$', '*'.  If the LIST or DISPLAY 
form of the command is used, lname can be wildcarded. 
ctnum    specifies the number of the controller (0-31) with which the device 
will be associated.  If the LIST or DISPLAY form of the command is used, ctnum 
can be wildcarded. 
Description: 
The CREATE, MODIFY and REMOVE DEVICE FOR LINE commands create, modify, and 
remove 3270 device definitions.  The LIST DEVICE FOR LINE command lists the 
currently defined 3270 devices.  The DISPLAY DEVICE FOR LINE command displays 
3270 device definitions.  SUPER prompts for options when it encounters a 
CREATE or MODIFY DEVICE FOR LINE command.  The options are described in HELP 
(SUPER) DEVICE_FOR_LINE_OPTS. 
The LIST DEVICE FOR LINE command lists device numbers for a line.  Including 
dnum in the LIST DEVICE command is useful when wildcarding is used or to 
verify the existence of a device definition. 
The DISPLAY DEVICE FOR LINE command shows a columnized display of the options 
for selected devices (or all devices for a line if the ALL option is 
specified), prefaced by a header consisting of the device information as 
entered in a CREATE or MODIFY DEVICE FOR LINE command.  The JCL option causes 
the command keyword CREATE to be written at the beginning of each listed 
device definition and the keyword END to be inserted where needed. 
00002
00001
A list of DEVICE FOR LINE command options and their definitions can be 
accessed by typing a ? or ??.  To access individual options, type: 
HELP (SUPER) DEVICE_FOR_LINE_OPTS option 
where option is any of the following: 
COLUMNS, ROWS, or TYPE 
  Option    Description 
  C[OLUMNS] = dec 
            Specifies the number of columns (40-255) on the screen.  The 
            default is 80. 
  R[OWS] = dec 
            Specifies the number of rows (12-255) on the screen.  The default 
            is 24. 
  T[YPE] = {3275|3277|3278|3279|3284|3286|3287|3288|3289|7700|7804} 
            Specifies the type of device.  If 3278 or 3279 is specified, an 
            ERASE WRITE ALTERNATE command is sent to the device, initiating 
            the large-screen mode.  7799 and 7804 identify polled VIP devices. 
            The default is 3278. 
00001
00002
00003
DEVICE_FOR_LINE_OPTIONS
Format: 
{C[REATE]} 
{M[ODIFY]} DEVICE dname FOR LINK link-name 
{R[EMOVE]} 
or 
D[ISPLAY] {[ALL] DEV[ICES] [FOR LINK link-name]} [(JCL)] 
          {DEV[ICE] dname [FOR LINK link-name] } 
or 
L[IST] {[ALL] DEV[ICES] [FOR LINK link-name]} 
       {DEV[ICE] dname [FOR LINK link-name] } 
Parameters: 
dname    specifies the 1-8 character device name.  If the LIST or DISPLAY form 
of the command is used, dname can be wildcarded. 
link-name    specifies the 1-8 character name of the link.  If the LIST or 
DISPLAY form of the command is used, link-name can be wildcarded. 
Description: 
The CREATE, MODIFY and REMOVE DEVICE FOR LINK commands create, modify, and 
remove (one) link device definition.  The LIST DEVICE FOR LINK command lists 
the currently defined link devices.  The DISPLAY DEVICE FOR LINK command shows 
link device definitions. 
SUPER prompts for options when it encounters a CREATE or MODIFY DEVICE FOR 
LINK command.  The options are described in Table 19-6.  in HELP (SUPER) 
DEVICE_FOR_LINK_OPTS. 
The LIST DEVICE FOR LINK command lists link device names.  Including link-name 
in the LIST DEVICE FOR LINK command is useful when wildcarding is used or to 
verify the existence of a link definition. 
The DISPLAY DEVICE FOR LINK command lists a columnized display of the options 
for selected link devices (or all link devices if the ALL option is 
specified), prefaced by a header consisting of the link device information as 
entered in a CREATE or MODIFY DEVICE FOR LINK command.  The JCL option causes 
the command keyword CREATE to be written at the beginning of each link device 
definition and the END keyword to be inserted where appropriate. 
00002
00001
A list of DEVICE FOR LINK command options and their definitions can be 
accessed by typing a ? or ??.  To access individual options, type: 
HELP (SUPER) DEVICE_FOR_LINK_OPTS option 
where option is any of the following: 
CIRCUITS, PROTOCOL_ID, SUBADDRESSS. 
  Option    Description 
  CIRCUITS= dec 
            Specifies the maximum number of outgoing virtual circuits (1-4095) 
            that can be opened by host applications on the link.  The default 
            is 0. 
  PROTOCOL_ID = {dec|.hex_string} 
            Specifies that VCs, identified by a protocol id (expressed as a 
            decimal number (in the range 1-255) or a hex2 string, are to be 
            routed to host applications.  The default is 0. 
  SUB[ADDRESS] = dec 
            Specifies that VCs identified by a subaddress value (dec) in the 
            called address field, are to be routed to host applications.  The 
            range for dec is 0-99.  The default is 0. 
00001
00002
00003
DEVICE_FOR_LINK_OPTIONS
A list of DEVICE command options and their definition can be 
accessed by typing a ? or ??.  For individual options, type: 
HELP (SUPER) DEVICE_OPTS option 
where option is any of the following: 
PROFILE, PASSWORD, USE, CMD_CG, COMGROUP_CG, NOCG_CG, SNAME_CG, USER_CG, 
DEFPRIO_IN, MAXPRIO_IN, NCACCT_IN, NCFID_IN, NOCK_IN, 
NCTL_IN, TYPE_IN, WSN_IN, FORM_OUT, TYPE_OUT, 
UPLOCKED_OUT, ATTR_RESOURCE, AUACCOUNT_RESOURCE, MODE_RESOURCE, 
RNAME_RESOURCE, TYPE_RESOURCE, CMD_TP, INSTANCE_TP, MCT_TP, NOCG_TP, 
PRIORITY_TP, or SNAME_TP. 
Note:  _SUFFIX specifies the usage code. 
  Option    Description 
  PR[OFILE]=pname 
            Specifies the 1-8 character default profile for this device.  Any 
            printable character can be included in the profile name.  If pname 
            is specified, the identified profile must have been defined.  The 
            default is NONE, which means the handler default is used. 
  PA[SSWORD] = {NONE|password} 
            Specifies the 1-8 character logon password for the device.  Any 
            printable character can be included in the password value.  The 
            default is NONE. 
  USE = {CG|IN[SYM]|OUT[SYM]|RES[OURCE]|TP} 
            Specifies whether this is a comgroup (CG), an input (INSYM) or 
            output (OUTSYM) symbiont device, a resource device (RESOURCE), or 
            a TP station (TP).  This option is required and determines what 
            subsequent options are legal. 
      CMD = {string|NONE} 
            Specifies a 1-80 byte string to be passed to the administrative 
            user of the comgroup when this device connects.  NONE specifies 
            that no string is to be passed.  The default is NONE.  This option 
            is legal if USE=CG. 
      COMGROUP = fid 
            Specifies the comgroup to which this terminal is to be attached; 
            fid must be a legal comgroup fid.  If the comgroup is in public 
            storage, PSN should not be specified.  This option is required if 
            USE=CG. 
      NOCG = {OK|REJECT|INFORM} 
            Specifies what action is to be taken when the device connects and 
            the comgroup is not open or when the device is connected when the 
            comgroup closes.  OK means simply to keep the device connected. 
            REJECT means to reject the device's logon or disconnect it. 
            INFORM means to keep the device connected, but inform it that it 
            cannot currently operate.  The default is OK.  This option is 
            legal if USE=CG. 
      SNAME = sname 
            Specifies the name this device will have on the comgroup.  If this 
            is a CREATE DEVICE command, the default is the device name.  If it 
            is the DEVICE option of the CREATE TERMINAL command, the system 
            will generate a unique name by default.  Only one device of a 
            given name may be connected to a particular comgroup at a time. 
            This option is legal if USE=CG. 
      USERn = value 
            Specifies for n a value to be passed to the administrative user of 
            the comgroup when this device connects.  n = 1, 2, 3, or 4.  value 
            may be a one to 11 integer decimal number or an octal number.  The 
            value is passed as a 36 bit value.  The default for value is 0. 
            This option is legal if USE=CG. 
      DE[FPRIO] = p 
            Specifies an integer value from 0-15 that is the default priority 
            assigned to jobs submitted from this device if PRIO is not 
            specified on the JOB command.  The default is to use the default 
            for the job's account.  This option is legal if USE=IN. 
      MA[XPRIO] = p 
            Specifies an integer value from 0-15 that is the maximum priority 
            that may be specified for a job submitted from this device.  The 
            default is to use the default for the job's account.  This option 
            is legal if USE=IN. 
      NCA[CCT] = acct 
            Specifies the 1-8 character intrinsic NCTL account for this 
            device.  See the discussion of NCTL for details.  The default is 
            :NCTL.  This option is legal if USE=IN. 
      NCF[ID] = fid 
            Specifies the device's intrinsic NCTL fid for NCTL files.  This 
            option may be used for devices which are incapable of submitting 
            an '!NCTL' card, to establish the destination fid for their 
            non-control streams.  A ? may be specified at the end of the fid. 
            The ? will be replaced by an 11-digit decimal UTS value.  The 
            length of the filename (including the trailing ?) must not exceed 
            21 characters or the substitution will not be performed and the 
            NCTL M$OPEN will fail.  See the discussion of NCTL for details. 
            This option is legal if USE=IN. 
      NCOK ={Y[ES]|N[O]} 
            Specifies whether (YES) or not (NO) this control device may submit 
            NCTL files.  See the discussion of NCTL for details.  This option 
            is meaningful only if NCTL = NO.  The default is YES.  This option 
            is legal if USE=IN. 
      NCTL = {Y[ES]|N[O]} 
            Specifies whether (YES) or not (NO) the device is a non-control 
            (NCTL) device.  The default is NO.  This option is legal if 
            USE=IN.  For more information, type: HELP (SUPER) NCTL_DEVICE 
      TYP[E] = dd 
            Specifies what type of device is being created.  The value for dd 
            can be any two alphabetic characters except the following:  AP, 
            CP, CG, DP, FT, GR, JE, JF, LO, LP, LT, ME, MT NO, SY and UC.  The 
            conventional type CR for card reader can be used.  This option is 
            required if USE=IN. 
      WSN = wname 
            Specifies the 1-8 character name of the default workstation to be 
            associated automatically with the device.  This option is legal if 
            USE=IN. 
      FOR[M] = fname 
            Specifies the form assumed mounted on the device when it is 
            connected.  The default is STDLP if TYP=LP, and STD** for all 
            other types.  The form must exist.  Note:  If the output stream is 
            directed to a CP type device (for example, when output is sent 
            from JE to CR), a form that contains no banner should be used. 
            The default form contains a banner which is usually unintelligible 
            to the receiving end and may cause undesirable results.  This 
            option is legal if USE=OUT. 
      TYP[E] = dd 
            Specifies what type of device is being created.  The value for dd 
            can be any two alphabetic characters except the following:  AP, 
            CP, CG, DP, FT, JF, LO, LT, ME, MT, NO, SY and UC.  The 
            conventional types CP for card punch, LP for line printer and LZ 
            for laser printer can be used.  This option is required if 
            USE=OUT. 
      UPL[OCKED] = {Y[ES]|N[O]} 
            Specifies whether the device will be in the locked state when 
            connected.  If UPLOCKED=YES, no output will be written to the 
            device until it is unlocked through an operator keyin.  The 
            default is NO.  This option is legal if USE=OUT. 
      TYP[E] = dd 
            Specifies what type of device is being created.  The conventional 
            type CL for communication line and LP for line printer can be 
            used.  This option is required if USE=RESOURCE. 
      ATTR = {YES|NO} 
            Specifies the attributes of a resource device. ATTR is selected 
            from the following, and the option may be repeated for as many 
            different attributes as are applicable. 
            ATTR            Description 
            ----            ----------- 
            B300            300 baud 
            B1200           1200 baud 
            B2400           2400 baud 
            HAYES           Hayes protocol 
            TCPIP           TCP/IP resource 
            TCP             TCP access is allowed 
            PRIVILEGE       Connection to privileged TCP/IP port allowed 
            IP              Not currently used 
            X28             X.28 circuit 
            RFU1...RFU11    Available for site-specific use and future 
                            expansion. 
            These options are legal if USE=RESOURCE and TYPE=CL. 
      AUACCOUNT = account 
            Specifies a 1-8 character account that is permitted to act as the 
            AU of the resource set.  account can be wildcarded, but only a 
            single ? character can be used.  This option must be specified if 
            the MODE for the resource is INCOMING.  It is optional if the MODE 
            for the resource is either FIXED or OUTGOING.  This option is 
            legal if USE=RESOURCE and TYPE=CL. 
      MODE = {FIXED|INCOMING|OUTGOING} 
            Describes the resource's mode as follows. 
            FIXED describes a single facility, like an ASYNC modem, which is 
            usually controlled by a single host user at a time. 
            INCOMING describes the possible appearance of some number of 
            incoming "lines" whose existence is to be reported to the attached 
            host user (if any), so that it can then connect to them 
            individually. 
            OUTGOING describes the availability of some number of "lines" that 
            can be created as needed when so requested by host users.  For 
            example, outgoing X.28 circuits are defined as OUTGOING. 
            This option is legal if USE=RESOURCE and TYPE=CL. 
      RNAME = name 
            Specifies a name that a user can reference to request a specific 
            resource.  For example, RNAME can be used to distinguish between 
            otherwise identical X.28 facilities on different links.  This 
            option is legal if USE=RESOURCE and TYPE=CL. 
      CMD = {NONE|string} 
            Specifies a command to TPA to be executed when the device is 
            initially connected.  The command may be 1 to 80 bytes long.  The 
            default is NONE.  This option is legal if USE=TP. 
      INSTANCE = [[DP]#psn.] name 
            Specifies the transaction processing instance to which the device 
            is to be connected.  This option is required.  This option is 
            legal if USE=TP. 
      MCT = {YES|COMMANDS|NO} 
            Specifies whether this is a master control terminal (YES), may 
            enter master control terminal commands (COMMANDS), or has no 
            master control privileges (NO).  The default is NO.  This option 
            is legal if USE=TP. 
      NOCG = {OK|REJECT|INFORM} 
            Specifies what action is to be taken when device connects and the 
            TP instance is not running or the TP instance stops running while 
            the device is connected.  OK means simply to keep the device 
            connected until the instance starts (or restarts).  REJECT means 
            to reject the device logon or disconnect it.  INFORM means to keep 
            the device connected, but inform it that it cannot currently 
            operate.  The default is OK.  This option is legal if USE=TP. 
      PRIORITY = n 
            Specifies the priority of messages from this device, from 1 to 
            511.  The default is 1.  This option is legal if USE=TP. 
      SNAME = sname 
            Specifies the name by which this device will be known to 
            transaction processing.  Only one device of a given name may be 
            attached to an instance of TP at a time.  The default is the 
            device name if this is a CREATE DEVICE command, or a system 
            generated unique name if this is the DEVICE option of a CREATE 
            TERMINAL command.  Use of the SNAME option in the latter case is 
            highly recommended.  This option is legal if USE=TP. 
00021
00022
00025
00004
00025
00005
00009
00017
00026
00010
00027
00023
00012
00011
00012
00013
00014
00006
00028
00002
00001
00029
00001
00024
00007
00030
00015
00018
00020
00019
00003
00008
00016
DEVICE_OPTIONS
The following lists the DEVNUM mnemonics and their associated options. 
Mnemonic       Hex          Hex         Hex 
DEVNUM         DEVNUM       SDNUM       DEVCTL 
2780LP            3 
2780CR            6 
2780CP            4 
3780LP           11 
3780CR            0 
3780CP           12 
HASPOC           91          92            40 
HASPLP           94                       800 
HASPCR           93                         1 
HASPCP           95                         1 
HASPLP2          A4                       400 
HASPLP3          B4                       200 
IBMCR            93                       800 
DEVNUM_MNEMONICS_OPTIONS
The attributes of devices can be set by escape sequences, which requires that 
unprintable characters be sent through the CP-6 banner-building code.  Banners 
with unprintable characters can be created from XEQ files only and must be 
created using font "0".  See the Usage Note in the description of the CREATE 
and MODIFY CHARSET commands description for more information on using the CP-6 
Editor to build XEQ files that contain unprintable pass-through characters. 
Format: 
          [[.]account, name] 
D[ISPLAY] [DEFAULT         ] [(JCL)] 
          [ALL USERS       ] 
Parameters: 
account, name    specifies a user account.  The account is limited to 8 
characters, the name to 12.  The valid character set consists of alphanumeric 
characters plus the characters $ and :.  Note that wildcarding is allowed for 
account and name (e.g., D[ISPLAY] ?HOST). 
DEFAULT    indicates the default user authorization record is to be displayed. 
ALL USERS    requests display of information for all users in the current 
project, or, all users if projects are not used. 
JCL    requests that the listing be formatted to include SUPER commands 
(MAKEME and MAKEME RESET, where appropriate, and the CREATE command), and the 
END keyword at appropriate places in the listing.  (See Description.) 
Description: 
This command displays various items of a user's authorization.  If USERS is 
specified, the listing will include information for all users in the current 
project. 
If a user logon is specified but the JCL option is not, SUPER will prompt for 
options to be displayed.  The options that can be specified are the keyword 
ALL or any of the following: 
    *S[_ACCOUNTING]           FEMA[CCTMEM]              N[ATIVEL] 
    AC[CESS]                  FEMF[PRG]                 O[NLINE] 
    ACCOU[NT_OWNER]           FEMI[NTS]                 OU[TPUTPRIO] 
    ALT[ERABLE]               FEMME[MORY]               PA[SSWORD] 
    BAN[NER]                  FEMTI[ME]                 PPRIV[ILEGE] 
    BA[TCH]                   FEP*S[_ACCOUNTING]        PRIO[B] 
    BA[TNUM]                  FEPP[RIV]                 PRIV[ILEGE] 
    BI[LLING]                 FEPR[IV]                  PRO[FILE] 
    BU[DGET]                  FEPS[EUDO]                PS[EUDO] 
    CP[ROC]                   FERE[SOURCES]             QU[AN] 
    EX[PIRE]                  FEU[SER]                  RE[SOURCE] 
    FA[CCOUNT]                FORC[E_SETUP]             SER[VICES] 
    FE                        G[HOST]                   SET[UP] 
    FEBI[LLING]               HS[ET]                    ST[EPACCNT] 
    FECG                      KEY                       TI[ME] 
    FECX[TMEM]                L[AST] [CPROC]            TP 
    FEDB[ACCN]                LASTLOG[ON]               W[SN] 
    FEG[HOST]                 MA[XENQ] 
    FEH[ANDLER]               ME[MORY] 
These options are described in HELP (SUPER) USER_OPTS. 
The account or name values can be wildcarded. 
DISPLAY options can be specified one per line or in the format: 
    option[;option] 
Listing of the selected DISPLAY will begin after the END keyword or an empty 
input line is entered.  If a specific authorization is not requested, all 
currently defined logon IDs will be displayed. 
The JCL option is specified to extract one or more user definitions usually to 
be directed to a file (via the OUTPUT command) for submission as a XEQ file. 
Specifying the JCL option causes the command keyword CREATE to be written at 
the beginning of each user definition.  If the project administrator needs to 
be at a higher level to perform the creation (see Project Administration, 
above), the MAKEME and MAKEME RESET commands will be inserted at the beginning 
and the end of the listing.  SUPER definition files must include the END 
keyword at appropriate places to simulate suboption and option prompting 
responses.  The JCL option also causes the END keywords to be inserted 
automatically where they are needed. 
00002
00001
DISPLAY
Format: 
D[ISPLAY] {[ALL] CHAR[SETS]   } [(JCL)] 
          {CHARSET charsetname} 
Parameters: 
ALL CHARSETS    requests display of all CHARSET records in the :FORM file. 
charsetname    is the name of the charset to be DISPLAYed.  The charsetname 
can be a combination of alphabetic characters, numeric characters and the 
characters:  colon (:), dollar sign ($) and asterisk (*).  The charsetname can 
be wildcarded with the ? character. 
JCL    requests that the listing be formatted to include the SUPER CREATE 
command and the END option at appropriate places in the listing.  (See 
Description.) 
Description: 
The DISPLAY CHARSET command is used to display the contents of all or selected 
CHARSET records.  The command qualifies CHARSET definitions for listing. 
If the DISPLAY ALL CHARSET command is used, all CHARSET records in the :FORMS 
file will be listed. 
If the DISPLAY CHARSET charsetname command is used, the definitions of all 
CHARSET records qualifying for the charsetname are listed.  This listing is 
useful when wildcarding is used in charsetname. 
The JCL option is specified to extract one or more CHARSET definitions usually 
to be directed to a file (via the OUTPUT command described in this section) 
for submission as a job file. 
Specifying the JCL option causes the command keyword CREATE to be written at 
the beginning of each CHARSET definition.  SUPER definition files must include 
the END keyword at appropriate places to simulate suboption and option 
prompting responses.  The JCL option also causes the END keyword to be 
inserted automatically where it is needed. 
00002
00001
DISPLAY_COMMANDS
See the following topics: 
HELP (SUPER) CONSOLE, CONTROLLER, DEVICE, DEVICE_FOR_LINE, DEVICE_FOR_LINK, 
DISPLAY, DISPLAY_CHARSET, DISPLAY_FORM, DISPLAY_PROJECT, DISPLAY_PSEUDO, 
DISPLAY_USERS, LINE, LINK, PROFILE, TERMINAL, VIRTUAL_CIRCUIT, WSN 
Format: 
D[ISPLAY] {[ALL] FORM[S]} [(JCL)] 
          {FORM formname} 
Parameters: 
ALL FORMS    requests display of all forms in the :FORM file. 
formname    is the name of the form to be DISPLAYed.  The formname can be a 
combination of alphabetic characters, numeric characters and the characters: 
colon (:), dollar sign ($) and asterisk (*).  The formname can be wildcarded 
with the ?  character. 
JCL    requests that the listing be formatted to include the SUPER CREATE 
command and the END option at appropriate places in the listing.  (See 
Description.) 
Description: 
The DISPLAY FORM command is used to display the contents of all or selected 
line-oriented, graphic and pseudo form records.  The command qualifies FORM 
definitions for display. 
If the DISPLAY ALL FORMS command is used, all form definitions -- 
line-oriented, graphic and pseudo -- will be displayed. 
If the DISPLAY FORM formname command is used and the JCL option is not 
specified, SUPER requests display options with the prompt 'OPT*'.  The option 
ALL specifies that the complete form definition be shown for the selected 
form.  Specification of other options limits the record information displayed 
to the specified options.  Any of the FORM record display options in HELP 
(SUPER) LISTFORM_OPTS can be entered for the identified line-oriented, graphic 
or pseudo form record. 
If a formname is specified in the DISPLAY FORM command but no options are 
specified, the definitions of all forms qualifying for the formname are 
listed.  This listing is useful when wildcarding is used in formname. 
The JCL option is specified to extract one or more form definitions usually to 
be directed to a file (via the OUTPUT command described in this section) for 
submission as a job file. 
Specifying the JCL option causes the command keyword CREATE to be written at 
the beginning of each form definition.  SUPER definition files must include 
the END keyword at appropriate places to simulate suboption and option 
prompting responses.  The JCL option also causes the END keyword to be 
inserted automatically where it is needed. 
00002
00001
Format: 
D[ISPLAY] {[ALL] FORMSET[S]} [(JCL)] 
          {FORM formsetname} 
Parameters: 
ALL FORMSETS    requests display of all forms in the :FORM file. 
formsetname    is the name of the form to be DISPLAYed.  The formsetname can 
be a combination of alphabetic characters, numeric characters and the 
characters:  colon (:), dollar sign ($) and asterisk (*).  The formsetname can 
be wildcarded with the ? character. 
JCL    requests that the listing be formatted to include the SUPER CREATE 
command and the END option at appropriate places in the listing.  (See 
Description.) 
Description: 
The DISPLAY FORMSET command is used to display the contents of a base form 
followed by a listing of any PSEUDO forms that have been built upon the 
specified base form.  The command qualifies FORMSETS for display. 
If the DISPLAY ALL FORMSETS command is used, all form definitions and their 
pseudo forms will be displayed. 
If the DISPLAY FORMSETS formname command is used and the JCL option is not 
specified, SUPER requests display options with the prompt 'OPT*'.  The option 
ALL specifies that the complete form definition be listed for the selected 
form.  Specification of other options limits the record information displayed 
to the specified options.  Any of the FORM record display options in HELP 
(SUPER) LISTFORM_OPTS can be entered for the identified formset. 
If a formsetname is specified in the DISPLAY FORM command but no options are 
specified, the definitions of all forms qualifying for the formsetname are 
listed.  This listing is useful when wildcarding is used in formsetname. 
The JCL option is specified to extract one or more formset definitions usually 
to be directed to a file (via the OUTPUT command described in this section) 
for submission as a job file. 
Specifying the JCL option causes the command keyword CREATE to be written at 
the beginning of each formset definition.  SUPER definition files must include 
the END keyword at appropriate places to simulate option and suboption 
prompting responses.  The JCL option also causes the END keyword to be 
inserted automatically where it is needed. 
If the ALIGNMENT or BANNER options are entered, SUPER prompts with 'SUB*'. 
Then the user may enter the options listed below. 
  Suboption    Description 
  AL[IGN][EVERY] [={YES}|{NO}] 
               Indicates if the alignment is to be printed before every file. 
               If YES and NO are omitted, YES is assumed.  (Legal only for 
               ALIGNMENT images.)  The default is NO. 
  CH[ARGE] [={YES}|{NO}] 
               Indicates if the user is to be charged for banner pages.  If 
               YES or NO are omitted, YES is assumed.  (Legal only for 
               BANNER.)  The default is NO. 
  EN[TRY] = row,col [, font, strikes, icsh, reps, rinc, cinc] 
               Defines one element of this BANNER or ALIGNMENT and can be used 
               as many times as needed.  The values for this sub-option can be 
               accessed by typing HELP (SUPER) ENTRY_FORMOPTS.  After the 
               ENTRY sub-option is typed, SUPER prompts with TXT*.  Available 
               responses to this prompt can be accessed by typing HELP (SUPER) 
               ENTRY_TEXT. 
  RE[PEATS] = decimal 
               Specifies the number of times the entire BANNER or ALIGNMENT 
               image is to be repeated.  If this sub-option is omitted, one is 
               assumed if entries are made and zero if no entries are made. 
00003
00004
00002
00005
00001
00006
Format: 
          {[ALL] PROJ[ECTS]           } 
D[ISPLAY] {DEFAULT[P]                 } [(JCL)] 
          {PROJ[ECT] [.]account, name]} 
Parameters: 
account, name    specifies a logon ID.  The account is limited to 8 
characters, the name to 12.  The valid character set consists of alphanumeric 
characters plus the characters $ and :.  Note that wildcarding is allowed for 
account and name (e.g., D[ISPLAY] ?HOST). 
DEFAULTP    indicates the system's project default record. 
ALL PROJECTS    requests display of information for all projects under 
management of the system manager or project administrator. 
JCL    requests that the listing be formatted to include SUPER commands 
(MAKEME and MAKEME RESET, where appropriate, and the CREATE command), and the 
END keyword at appropriate places in the listing.  (See Description.) 
Description: 
This command displays various items of a project's authorization.  If ALL 
PROJECTS is specified, the listing will include information for all projects 
managed by the project administrator, or all projects, if the requestor is the 
system manager. 
If a project logon id is specified but the JCL is not, SUPER will prompt for 
options to be displayed.  The options that can be specified are the keyword 
ALL or any of the CREATE/MODIFY PROJECT options (see HELP (SUPER) 
PROJECT_OPTS).  Only options may be specified, not sub-options. 
The account or name values can be wildcarded. 
DISPLAY options can be specified one per line or in the format: 
    option[;option] 
Listing of the selected DISPLAY will begin after the END keyword or an empty 
input line is entered.  If a specific authorization is not requested, all 
currently defined projects will be displayed. 
Project administrators list their own user authorizations by using the command 
in the following format: 
    CMD*DISPLAY PROJECT account, name 
    PROJ*ADMIN 
    OPT*ALL 
    PROJ*END 
Project administrators list the default record for the project by using the 
command in the following format: 
    CMD*DISPLAY PROJECT account, name 
    PROJ*DEFAULT 
    OPT*ALL 
    PROJ*END 
(Note that for the ADMINISTRATOR and DEFAULT options, SUPER will prompt for 
user authorization options to be displayed so long as the JCL option is not 
specified, as is done for the DISPLAY (user) command.) 
The JCL option is specified to extract one or more project definitions usually 
to be directed to a file (via the OUTPUT command) for submission as a XEQ 
file. 
Specifying the JCL option causes the command keyword CREATE to be written at 
the beginning of each project definition.  If the project administrator needs 
to be at a higher level to perform the creation (see Project Administration, 
above), the MAKEME and MAKEME RESET commands will be inserted at the beginning 
and the end of the listing.  SUPER definition files must include the END 
keyword at appropriate places to simulate option prompting responses.  The JCL 
option also causes the END keywords to be inserted automatically where they 
are needed. 
00002
00001
DISPLAY
DISPLAY_CHARSETS
DISPLAY_FORMS
DISPLAY_FORMSETS
DISPLAY_PROJECT
A list of ENTRY options can be accessed by typing a ? or ??.  To obtain 
definitions of individual ENTRY options, type 
HELP (SUPER) ENTRY_FORMOPTS option 
where option is any of the following: 
cinc, col, font, icsh, reps, rinc, row, strikes 
  Value    Description 
  cinc 
           The amount to increment the column for each repeat.  The default is 
           zero. 
  col 
           The column where this element is to begin printing. 
  font 
           The type font to be used (0=standard typing, 1-3=block-print fonts; 
           1 includes lower case.)  The default is zero. 
  icsh 
           Specifies inter-character spacing.  The defaults are zero for font 
           0 and one for fonts 1-3. 
  reps 
           The number of times this element is to be repeated.  The default is 
           1. 
  rinc 
           The amount to increment the row after each repeat.  The default is 
           zero.  This means there are to be no extra lines after a line is 
           printed.  The height of each ENTRY is the number of lines PER FONT 
           + rinc. 
  row 
           The row where this element is to begin printing. 
  strikes 
           The number of times this element is to be printed.  The default is 
           1. 
00001
00002
00003
00004
00005
00006
00007
00008
ENTRY_FORMOPTIONS
A list of ENTRY options can be accessed by typing a ? or ??.  To obtain 
definitions of individual ENTRY options, type 
HELP (SUPER) ENTRY_OPTS option 
where option is any of the following: 
cinc, col, font, icsh, reps, rinc, row, strikes 
  Value    Description 
  cinc 
           The amount to increment the column for each repeat.  The default is 
           zero. 
  col 
           The column where this element is to begin printing. 
  font 
           The type font to be used (0=standard typing, 1-3=block-print fonts; 
           1 includes lower case.)  The default is zero. 
  icsh 
           Specifies inter-character spacing.  The defaults are zero for font 
           0 and one for fonts 1-3. 
  reps 
           The number of times this element is to be repeated.  The default is 
           1. 
  rinc 
           The amount to increment the row after each repeat.  The default is 
           zero.  This means there are to be no extra lines after a line is 
           printed.  The height of each ENTRY is the number of lines PER FONT 
           + rinc. 
  row 
           The row where this element is to begin printing. 
  strikes 
           The number of times this element is to be printed.  The default is 
           1. 
00001
00002
00003
00004
00005
00006
00007
00008
ENTRY_OPTIONS
A list of responses to the SUPER prompt of TXT* can be accessed by typing a ? 
or a ??.  To obtain definitions of individual responses, type 
HELP (SUPER) ENTRY_TEXT response 
where response may be any of the following: 
ACCN, Any, BANNER, DATE, FORM, JOBNAME, LOGO, n, REGISTEREDNAME, SALUTE, 
SITENAME, SUBFILE, SYSID, TIME, UNAME, VERSION, WOD, WOO 
  Typed Entry    Description 
  %AC[CN] 
                 The account name for the user (legal for BANNER only). 
  Any 
                 Any text line not starting with '%' (legal for both BANNER 
                 and ALIGNMENT).  The text line is printed just as it is 
                 entered. 
  %{BANNER|BANNERTEXT} i 
                 A reference to a banner text field that is extracted from a 
                 record in the user's *S file.  The value of i is 1 to 9 
                 inclusive (legal for BANNER only). 
  %DA[TE] 
                 The current date (legal for BANNER only). 
  %FO[RM] 
                 The formname (legal for BANNER only). 
  %JO[BNAME] 
                 The name specified on the user's job card (legal for BANNER 
                 only). 
  %LO[GO] 
                 The standard CP-6 logo (legal for both BANNER and ALIGNMENT). 
                 For line-oriented forms, the ENTRY options 'font' and 'icsh' 
                 are ignored. 
  %n 
                 Any single character repeated across the entire line (legal 
                 for BANNER and ALIGNMENT). 
  %RE[GISTEREDNAME] 
                 A 21-character (including the comma) field that contains the 
                 user's account (8 characters) and name (12 characters) 
                 formatted as follows: 
                   account,username 
                 The registered name field is stored as bannertext 0 in the 
                 user's *S record.  This field is built at logon and during a 
                 reset of the bannertext (via the IBEX command LET).  (Legal 
                 for BANNER only.) 
  %SA[LUTE] 
                 The standard system salutation (legal for BANNER only). 
  %SI[TENAME] 
                 The site name (legal for BANNER only). 
  %SU[BFILE] 
                 The subfile number of this printout (legal for BANNER only). 
  %SY[SID] 
                 The user sysid for the output being printed (legal for BANNER 
                 only). 
  %TI[ME] 
                 The current time (legal for BANNER only). 
  %UN[AME] 
                 The user name for the user (legal for BANNER only). 
  %VE[RSION] 
                 The system version (legal for BANNER only). 
  %WOD 
                 The output's workstation of destination (legal for BANNER 
                 only). 
  %WOO 
                 The user's workstation of origin (legal for BANNER only). 
00001
00002
00003
00004
00005
00006
00007
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
00008
A list for field profile options and their definitions can be accessed by 
typing a ? or ??.  To access individual options, type: 
HELP (SUPER) FIELD_PROFILE_OPTS option 
where option is any of the following: 
ATRSCRNPOS, DAQINP_CHR, DAQPRT_CHR, DCHMOVFLD, DCLFLD_ALG, DCLFRM_CHR, 
DLTALLFLDS_CHR, DLTFLD_CHR, ED0DLTFLD, ED2DLTFLD, ED0_CHR, ED2_CHR, EDITOVR, 
ELODLTFLD, ENDDCLFRM_CHR, ERASEFLD_CHR, FLDTRM, FRSCLMFLD, INSERTMODE, 
MAXATRS, RESTORE_DFLTSCRN_CHR, SGRDCRINT_CHR, SGRFSTBLN_CHR, SGRHDN_CHR, 
SGRINCDAQ, SGRINCINT_CHR, SGRINTRO_CHR, SGRRVRVID_CHR, SGRSLWBLN_CHR, 
SGRUNDSCR_CHR, SGR_ALG, and SPCDLTFLD. 
  Option                       Description                           Device 
AT[RSCRNPOS][=Y[ES]|N[O]|D[C]}] 
                            Specifying YES indicates that the      ASYNC 
                            attribute byte itself takes up a       POLLVIP 
                            position on the display.  The 
                            default is NO. 
DAQINP_[CHR]=hex                                                   POLLVIP 
                            Specifies the character that allows 
                            the data in a field to be modifiable. 
                            The default is X'55'.  The option 
                            SGRINCDAQ must be set for this option 
                            to take effect. 
DAQPRT[_CHR]=hex                                                   POLLVIP 
                            Specifies the character that 
                            protects the data in a field from 
                            operator access.  The default is 
                            X'50'.  The option SGRINCDAQ must be 
                            set for this option to take effect. 
DCHM[OVFLD][={Y[ES]|N[O]|D[C]}] 
                            YES specifies that the local           ASYNC 
                            character-editing functions 
                            (insert- and delete-character) 
                            cause fields to the right of 
                            their invocation to slide along 
                            with the data contained in them. 
                            NO specifies that such fields remain 
                            stationary on the screen.  YES 
                            causes the use of such functions 
                            to be disabled if a field 
                            position begins or ends to the 
                            right of the editing position. 
                            The default is DC. 
DCLFL[D_ALG]={ANS|NONE|1|2|3} 
                            This item indicates which of           ASYNC 
                            these algorithms should be used        POLLVIP 
                            to declare fields on this device: 
                            {ANS|1}  This terminal follows all 
                                     ANSII X3.64 conventions. 
                            NONE    Indicates that fields cannot 
                                    be declared.  NONE is the 
                                    default. 
                            2       Send DCLFRM_CHR 
                                    position to start of field; 
                                    execute SGR_ALG.  If no field 
                                    immediately follows the 
                                    position following the last 
                                    character in the field, then 
                                    send RESTORE_CR and ENDDCLFRM_CHR 
                            3       Visual attributes on the 
                                    device depend not on the 
                                    position on the screen, but on 
                                    the state of the terminal when 
                                    the characters are sent.  Thus: 
                                    Send DCLFRM_CHR; 
                                    execute SGR_ALG; 
                                    send character or accept 
                                    input; send RESTORE_CHR; 
                                    send ENDDCLFRM_CHR 
DCLFR[M_CHR]=hex_list       Some devices must be in a certain     ASYNC 
                            mode to declare fields.  This         POLLVIP 
                            sequence places the terminal in a 
                            declare field mode if one exists. 
DLTA[LLFLDS_CHR]=hex_list   Character string erases all           ASYNC 
                            characters and deletes all            POLLVIP 
                            attributes from the display. 
DLTF[LD_CHR]=hex_list       Character string erases the field      ASYNC 
                            located at the current cursor          POLLVIP 
                            position and deletes all its 
                            associated attribute bytes. 
                            Note:  The front end simulates 
                            protected fields and does not 
                            invoke the terminal's protection 
                            capabilities.  The terminal is 
                            always in an asynchronous (character 
                            by character) transmission mode. 
                            To perform this operation properly 
                            it will probably be necessary to 
                            place the terminal in some sort 
                            of block transfer mode, issue the 
                            proper sequence to erase the input 
                            fields and then issue another 
                            sequence to place the terminal 
                            back in a character by character 
                            transfer mode. 
ED0D[LTFLD][={Y[ES]|N[O]}]  Specifies whether ED0_CHR removes      ASYNC 
                            all field definitions in the           POLLVIP 
                            erased area.  The default is NO. 
ED2D[LTFLD][={Y[ES]|N[O]}]  Specifies whether ED2_CHR removes      ASYNC 
                            all field definitions.  The default    POLLVIP 
                            is NO. 
ED0[_CHR]=hex_list          Specifies the characters that          ASYNC 
                            determine how to perform erasures      POLLVIP 
                            from the current cursor position 
                            through the end of the display. 
ED2[_CHR]=hex_list          Specifies the characters that          ASYNC 
                            cause the entire display to be         POLLVIP 
                            erased. 
EDI[TOVR][={Y[ES]|N[O]}]    For CRT devices, YES specifies         ASYNC 
                            that visual fidelity is to be          POLLVIP 
                            maintained while using input 
                            editing to insert or delete char- 
                            acters.  Visual fidelity means 
                            the image on the screen matches 
                            the input record.  NO specifies 
                            that upspacing and backslashes 
                            will be displayed to indicate 
                            character insertions and 
                            deletions. 
                            The default is NO.  For ASYNC 
                            devices do not specify YES unless 
                            all of the following is true: 
                                BLANKERASES = YES 
                                CUU or CUP was specified 
                                CUB or CUP was specified 
                                CUF or CUP was specified 
                                CUD or CUP was specified 
                            For hardcopy devices, YES specifies 
                            that character-delete input 
                            operations (e.g., depressing the 
                            DEL key) should overstrike the 
                            deleted character with a \ 
                            (backslash).  NO specifies that the 
                            \ should simply be displayed. 
EL0D[LTFLD][={Y[ES]|N[O]}]  Specifies whether EL0_CHR removes      ASYNC 
                            all field definitions in the           POLLVIP 
                            erased area.  The default is NO. 
ENDD[CLFRM_CHR]=hex_list    If a DCLFRM_CHR exists, this           ASYNC 
                            character sequence is needed to        POLLVIP 
                            place the terminal back into its 
                            default mode. 
ERASE[FLD_CHR]=hex_list     Character string erases the field      ASYNC 
                            located by the current cursor          POLLVIP 
                            position.  See the DLTFLD option. 
FL[DTRM]={L[INE]|P[AGE]|D[C]} 
                            LINE specifies that fields are         ASYNC 
                            terminated automatically by the        POLLVIP 
                            terminal at the end of a line. 
                            PAGE specifies that fields do 
                            not terminate at the end of a 
                            line.  Default is DC. 
FRSC[LMFLD][={Y[ES]|N[O]}]  Specifies whether there will           ASYNC 
                            always be a field in column 1          POLLVIP 
                            of each line.  FRSCLMFLD=YES 
                            implies that RESTORE_DFLSCRN_CHR 
                            will be used instead of 
                            DLTFLD_CHR to delete a field 
                            definition in column 1.  The 
                            default is NO. 
INSE[RTMODE][={Y[ES]|N[O]|D[C]}] 
                            Specifies whether insert mode is       ASYNC 
                            to be enabled or not.  The 
                            default is DC. 
MA[XATRS]={value|D[C]}      The maximum number (0-255) of field    ASYNC 
                            attribute declarations allowable       POLLVIP 
                            on a single line on this device. 
                            The default is DC.  A value of 255 
                            is the same as DC. 
RES[TORE_DFLTSCRN_CHR]=hex_list 
                            This character sequence follows        ASYNC 
                            the declaration of a field and         POLLVIP 
                            turns the terminal back to its 
                            default mode.  For example, if a 
                            field has been declared to be 
                            high-intensity blinking this 
                            character sequence restores the 
                            display to normal intensity. 
SGRD[CRINT_CHR]=hex         Character follows SGRINTRO_CHR         ASYNC 
                            and causes a field to be decreased     POLLVIP 
                            in intensity.  The default is X'00'. 
SGRF[STBLN_CHR]=hex         Character follows SGRINTRO_CHR         ASYNC 
                            and causes a field to blink            POLLVIP 
                            quickly.  The default is X'00'. 
SGRH[DN_CHR]=hex            Character follows SGRINTRO_CHR and     ASYNC 
                            causes a field to be hidden from       POLLVIP 
                            view.  If this value is zero the 
                            front end will simulate hidden 
                            fields by sending blanks instead 
                            of printing characters.  The default 
                            is X'00'. 
SGRINCD[AQ][={Y[ES]|N[O]}                                          POLLVIP 
                            Specifies whether or not the 
                            sequence established by the DAQINP 
                            or DAQPRT options is to be sent for 
                            unprotected or protected fields.  The 
                            default is NO. 
SGRINCI[NT_CHR]=hex         Character follows SGRINTRO_CHR         ASYNC 
                            and causes an increased intensity      POLLVIP 
                            field.  The default is X'00'. 
SGRINT[RO_CHR]=hex_list     This character sequence introduces     ASYNC 
                            (precedes) another character from      POLLVIP 
                            the set of SGR CHRs (SGRUNDSCR_CHR, 
                            SGRINCINT_CHR etc.) and begins a 
                            graphic attribute declaration. 
SGRR[VRVID_CHR]=hex         Character follows SGRINTRO_CHR         ASYNC 
                            and causes a field to be displayed     POLLVIP 
                            in reverse video.  The default is 
                            X'00'. 
SGRS[LWBLN_CHR]=hex         Character follows SGRINTRO_CHR         ASYNC 
                            and causes a field to blink 
                            slowly.  The default is X'00'. 
SGRU[NDSCR_CHR]=hex         Character follows SGRINTRO_CHR         ASYNC 
                            and causes a field to be               POLLVIP 
                            underscored.  The default is X'00'. 
SGR_[ALG]={NONE|ANS|1|2|3} 
                            This item determines which of four     ASYNC 
                            algorithms will be used to declare     POLLVIP 
                            graphic rendition attributes on the 
                            target device. 
                            {1|ANS}  This terminal conforms to the 
                                     ANSII X3.64 standard. 
                            2        The following sequence is sent 
                                     for each attribute in the field: 
                                       (SGRINTRO_CHR)(SGR_CHR) 
                                     Where SGR_CHR is one of the 
                                     set of attribute specifier 
                                     characters such as 
                                     SGRSLWBLN_CHR. 
                            3        One attribute declaration 
                                     sequence is sent for the entire 
                                     field in the following form: 
                                       (SGRINTRO_CHR)(SGR_CHR) 
                                     In this case, SGR_CHR is 
                                     formed by ORing together 
                                     the bit patterns for each 
                                     attribute specifier char- 
                                     acter needed by the field 
                                     declaration.  NONE is the 
                                     default. 
SPCD[LTFLD][={Y[ES]|N[O]}]           Specifies whether a space        ASYNC 
                                     character removes a field        POLLVIP 
                                     definition.  The default is NO. 
00001
00002
00003
00004
00005
00006
00007
00008
00014
00011
00009
00011
00012
00010
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
00031
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
FIELD_PROFILE_OPTIONS
FORM_COMMANDS
A list of SUPER form commands and their definitions can be accessed by typing 
a ? or a ??.  To obtain definitions of individual form commands, type 
HELP (SUPER) FORM_CMDS command 
where command is any of the following: 
CREATE_CHARSET, CREATE_FORM, CREATE_FORM_GRAPHICS, CREATE_PSEUDO, 
DELETE_CHARSET, DELETE_FORM, DISPLAY_CHARSETS, DISPLAY_FORMS, 
DISPLAY_FORMSETS, LIST_CHARSETS, LIST_FORMS, LIST_FORMSETS, MODIFY_CHARSET, 
MODIFY_FORM, MODIFY_FORM_GRAPHICS, MODIFY_PSEUDO, OUTPUT, REMOVE_CHARSET, 
REMOVE_FORM. 
  Command    Description 
  CREATE CHARSET 
             Constructs a CHARSET record. 
  CREATE FORM 
             Constructs a line-oriented form. 
  CREATE FORM GRAPHICS 
             Constructs a graphic form. 
  CREATE PSEUDO 
             Constructs a pseudo form. 
  DELETE CHARSET 
             Deletes all CHARSET records and rebuilds the CP-6 supplied ones. 
  DELETE FORM 
             Deletes all forms and rebuilds the three initial form definitions 
             (STDLP, STDGR and STD**). 
  DISPLAY CHARSETS 
             Displays one or all CHARSET records contained in the :FORM file. 
  DISPLAY FORMS 
             Displays one line-oriented form, one graphic form, one pseudo 
             form or all forms contained in the :FORM file. 
  DISPLAY FORMSETS 
             Displays one or all base form definition(s) and associated pseudo 
             forms. 
  LIST CHARSETS 
             Lists the names of character sets defined in the :FORM file. 
  LIST FORMS 
             Lists the names of forms defined in the :FORM file. 
  LIST FORMSETS 
             Lists the names of base forms in the :FORM file and the names of 
             their associated pseudo forms. 
  MODIFY CHARSET 
             Modifies an existing CHARSET record. 
  MODIFY FORM 
             Modifies an existing line-oriented form. 
  MODIFY FORM GRAPHICS 
             Modifies an existing graphic form. 
  MODIFY PSEUDO 
             Modifies an existing pseudo form. 
  OUTPUT 
             Directs processor output to a destination. 
  REMOVE CHARSET 
             Removes a CHARSET record from the :FORM file 
  REMOVE FORM 
             Removes a line-oriented form, a graphic form or a pseudo-form 
             from the :FORM file. 
00010
00001
00002
00003
00004
00001
00002
00003
00004
00009
00005
00006
00007
00008
00009
00005
00006
00008
00009
00010
00011
00012
00010
00011
00012
00013
00014
00015
00016
00013
00014
00015
00016
00017
00018
00019
00018
00019
A list of SUPER form options can be accessed by typing a ? or a ??.  To obtain 
definitions of individual form options, type 
HELP (SUPER) FORM_OPTS option 
where option is any of the following: 
ACCESS, ACCOUNT, ALIGNMENT, BANNER, CHARSET, FIRSTLINE, LENGTH, LIMBO, LPI, 
REMOVE_ALIGNMENT, REMOVE_BANNER, SETUP, TRANSLGL, VFUIM, WIDTH 
  Option    Description 
  ACCE[SS] [A[DD]|R[EMOVE]] = tname[, tname] ... 
            Sets the access list of terminal names (which may be wildcarded) 
            that can use this line-oriented form.  ADD supplies additional 
            tnames to the list.  REMOVE deletes tnames from the list. 
  ACCO[UNT] [A[DD]|R[EMOVE]] = account[, account] ... 
            Sets the access list of accounts that can use this line-oriented 
            form.  If no account is specified, any account can use this form. 
            ADD supplies additional accounts to the list.  REMOVE deletes 
            accounts from the list. 
  AL[IGNMENT] 
            Defines the alignment image for this line-oriented form.  SUPER 
            requests sub-options with the prompt SUB*.  An alignment image can 
            be built anywhere on a physical page.  However, building it in the 
            first and/or limbo areas will produce unpredictable results (i.e., 
            output can be formatted incorrectly).  To access these 
            sub-options, type HELP (SUPER) ALIGN_SUBOPTS. 
  BA[NNER] 
            Defines the banner image for this line-oriented form.  SUPER 
            requests sub-options with the prompt SUB*.  To access these 
            sub-options, type HELP (SUPER) BAN_SUBOPTS. 
  CH[ARSET]|CHAI[N] = charsetname 
            Copies the logical devices, attributes and print chain image from 
            the specified CHARSET record into this form definition. 
  FI[RSTLINE] = decimal 
            Specifies the height (0-254) of blank area between the beginning 
            of the page and the first legal print line.  Also, the number of 
            the first legal print line. 
  LE[NGTH] = decimal 
            Specifies the number (0-254) of printable lines per page. 
            (FIRSTLINE+LENGTH+LIMBO= total lines per page.)  (Note: Forms to 
            be used on unit record devices must have a form length no less 
            than 12 and no greater than 144). 
  LI[MBO] = decimal 
            Specifies the number (0-254) of blank lines between the last legal 
            print line and the bottom of the page. 
  LPI = decimal 
            Specifies the number of lines per inch.  Enter 6 or 8. 
  R[EMOVE] A[LIGNMENT] 
            Removes the alignment image from the form. 
  R[EMOVE] B[ANNER] 
            Removes the banner image from the form. 
  SE[TUP] 
            Indicates that an operator message of setup information is to be 
            defined.  SUPER prompts with 'TXT*' and 82 lines of 72 characters 
            each can be entered.  A blank line ends the entry.  If all 82 
            lines are entered, SUPER responds with: 
                SETUP BUFFER FULL,RETURNING TO 
                'OPT*' LEVEL. 
  TR[ANSLGL][={NO|YES}] 
            Indicates whether transparent characters are to be passed on to 
            the device.  NO specifies that transparent writes to symbiont 
            files do not go through translation or get truncated (the 
            "transparent" bit is not retained in the output file).  YES 
            specifies that writes will retain their length and transparency in 
            the output symbiont file.  The default is NO.  If TRANSLGL is 
            specified on the option line but neither YES or NO is specified, 
            YES is assumed. 
            Note:  TRANSLGL is only meaningful for non-IOM-/VDH-connected 
            devices.  If the TRANSLGL setting specified for a CHARSET differs 
            from the TRANSLGL setting for the appropriate FORM, the FORM 
            TRANSLGL setting is used. 
  VF[UIM] 
            Indicates that the VFU image is to be defined for this form. 
            SUPER prompts for sub-options with SUB* and the operator enters 
            image definitions of the form CH[AN]decimal=decimal[, decimal] ... 
            (For example, an entry of 'CHAN5=2,10' means a channel 5 "punch" 
            for lines 2 and 10.) 
            Note: Only channels 1-12 and lines 1-144 can be specified. 
  WI[DTH] = decimal 
            Specifies the maximum number (0-508) of characters to be written 
            per line on the form. 
00001
00002
00003
00004
00005
00005
00006
00007
00008
00009
00010
00011
00010
00011
00012
00013
00014
00015
FORM_OPTIONS
ARC                    E[ND]                  PRI[NT] 
ARE[A_FILL]            END_OF_F[IELD]         PUR[PLE] 
ASSIGN_I[NPUT]         END_OF_L[INE]          RAY 
ASSIGN_O[UTPUT]        END[_OF_PAGE]          REC[ALL] 
ATTE[NTION]            ENT[ER]                RECT[ANGLE] 
ATTRIBUTE_OF[F]        ERASE_A[LL]            RED 
ATTRIBUTE_ON           ERASE_EOF              REDR[AW] 
AUX                    ERASE_EOP              RES[ET] 
AUX_O[N]               EXE[CUTE]              RESET_I[NSERT_MODE] 
AUX_S[END]             EXI[T]                 ROL[L] 
BACK_T[AB]             E_AUX                  RTA[RROW] 
BLA[CK]                Fn (n=0-25)            RUBB[ER_BAND] 
BLI[NK]                FIL[L]                 SCA[LE] 
BLU[E]                 FOR[MS]                SCROLL_SEG_D[OWN] 
BRE[AK]                FORM_M[ODE]            SCROLL_SEG_U[P] 
CAL[C_MODE]            GOTO_R[IGHT_MARGIN]    SEN[D] 
CHAN[GE]               GRE[EN]                SET 
CHAR[ACTER_MODE]       HE[LP]                 SFn (n=0-25) 
CIR[CLE]               HOM[E]                 SIZ[E] 
CLE[AR]                IDR[IS]                SPAREn[PATCHSPACE](n=0-23) 
CLEAR_E[NTRY]          INCREMENT_X[_BAR]      SUn (n=0-24) 
CLEAR_T[O_RT_MARGIN]   INCREMENT_Y[_BAR]      S_D[NARROW] 
COL[OR_SWAP]           INC_V[ECTOR]           S_L[TARROW] 
CON[CAT_VECTOR]        INI[T]                 S_R[TARROW] 
COP[Y]                 INSERT_C[HARACTER]     S_U[PARROW] 
CRE[ATE]               INSERT_L[INE]          TAB_CLEAR_1 
CURS[OR_ON]            INSERT_M[ODE]          TAB_CLEAR_A[LL] 
CURV[E]                INSERT_MODE_EOL        TAB_S[ET] 
C_D[NARROW]            INSERT_MODE_EOP        TER[MINAL] 
C_E[ND]                LIN[E]                 TES[T] 
C_H[OME]               LOC[AL]                TEST_T[ONE] 
C_L[TARROW]            LTA[RROW]              TEXT_M[ODE] 
C_PGD[N]               Mn (n=1-2)             THA[W] 
C_PGU[P]               MEM[ORY_LOCK]          TRA[NSMIT] 
C_R[TARROW]            MON[ITOR]              TRI[ANGLE] 
C_U[PARROW]            MOV[E_X_Y]             TUR[QUOISE] 
DEF[INE]               OTHER_X[MIT]           UFn (n=0-24) 
DELETE_CHAR[ACTER]     OVE[RLAY]              UPA[RROW] 
DELETE_CHAR_EOL        PAn (n=1-4)            VEC[TOR] 
DELETE_CHAR_EOP        PAN[_X_Y]              VER[TICAL_WIDTH] 
DELETE_L[INE]          PFn (n=0-25)           VIE[W] 
DELETE_MODE_EOL        PGD[N]                 WHI[TE] 
DELETE_MODE_EOP        PGU[P]                 WIN[DOW] 
DNA[ARROW]             PLO[T]                 XMI[T] 
DOS                    PLOT_M[ODE]            YEL[LOW] 
DOT                    POL[YGON] 
Key Labeling Convention Recommendations 
--------------------------------------- 
If the key has writing on it that does not obviously define a single ASCII 
character, use that name or a spelling variant thereof in the table (for 
example, CLEAR, RESET, and INIT). 
Otherwise, if the key sends the character sequence that performs some terminal 
function whose name is in the list, use that name.  For example, BACK_TAB on a 
VIP (which is a <CNTL_TAB>). 
Otherwise (no name on the key, no local functions), use UFn for keys that 
don't use shift, SUn for ones that do. 
A list of graphics alignment sub-options and their definitions can be accessed 
by typing a ? or a ??.  To obtain definitions of these individual sub-options, 
type 
HELP (SUPER) GRAPHICS_ALIGN_SUBOPTS suboption 
where suboptions is any of the following: 
ALIGN, ENTRY, REPEATS 
  Suboptions    Description 
  AL[IGN][EVERY] [={YES}|{ NO}] 
                Indicates if the alignment is to be printed before every file. 
                If YES and NO are omitted, YES is assumed.  The default is NO. 
  EN[TRY]=xloc,yloc[,zloc,rotation,charwide,charhght,charsp] 
                Defines one element of this ALIGNMENT and can be used as many 
                times as needed.  The values for this sub-option can be 
                accessed by typing HELP (SUPER) GRAPHICS_ENTRY_OPTS.  After 
                the ENTRY sub-option is typed, SUPER prompts with TXT*. 
                Available responses to this prompt can be accessed by typing 
                HELP (SUPER) ENTRY_TEXT. 
  RE[PEATS] = decimal 
                Specifies the number of times the entire ALIGNMENT image is to 
                be repeated.  If this sub-option is omitted, one is assumed if 
                entries are made and zero if no entries are made. 
00001
00002
00003
GRAPHICS_ALIGN_SUBOPTIONS
GRAPHICS_BAN_SUBOPTIONS
A list of graphic banner sub-options and their definitions can be accessed by 
typing a ? or a ??.  To obtain definitions of these individual sub-options, 
type 
HELP (SUPER) GRAPHICS_BAN_SUBOPTS suboption 
where suboptions is any of the following: 
CHARGE, ENTRY, REPEATS 
  Suboptions    Description 
  CH[ARGE] [={YES}|{NO}] 
                Indicates if the user is to be charged for banner pages.  If 
                YES or NO are omitted, YES is assumed.  The default is NO. 
  EN[TRY]=xloc,yloc[,zloc,rotation,charwide,charhght,charsp] 
                Defines one element of this BANNER or ALIGNMENT and can be 
                used as many times as needed.  The values for this sub-option 
                can be accessed by typing HELP (SUPER) GRAPHICS_ENTRY_OPTS. 
                After the ENTRY sub-option is typed, SUPER prompts with TXT*. 
                Available responses to this prompt can be accessed by typing 
                HELP (SUPER) ENTRY_TEXT. 
  RE[PEATS] = decimal 
                Specifies the number of times the entire BANNER image is to be 
                repeated.  If this sub-option is omitted, one is assumed if 
                entries are made and zero if no entries are made. 
00001
00002
00003
GRAPHICS_BAN_SUBOPTIONS
A list of graphic ENTRY options can be accessed by typing a ? or ??.  To 
obtain definitions of individual ENTRY options, type 
HELP (SUPER) GRAPHICS_ENTRY_OPTS option 
where option is any of the following: 
charhght, charsp, charwide, rotation, xloc, yloc, zloc 
  Value    Description 
  charhght 
           The height, specified as a percent of Normalized Device Coordinate 
           (NDC) space of the character in the entry.  A value between 0 and 
           100 (inclusive) can be specified.  The default is 1. 
  charsp 
           The space, specified as a percent of Normalized Device Coordinate 
           (NDC) space, between the characters in the entry.  A value between 
           0 and 100 (inclusive) can be specified.  The default is 0. 
  charwide 
           The width, specified as a percent of Normalized Device Coordinate 
           (NDC) space, between the characters in the entry.  A value between 
           0 and 100 (inclusive) can be specified.  The default is 1. 
  rotation 
           The character orientation for an entry.  The value specified 
           indicates the display direction to the top of the characters as 
           follows: 
                            90 
                             | 
                             | 
                   180  <----o---->  0 
                             | 
                             | 
                             v 
                            270 
           where the circle indicates the base of the character and the 
           numbers represent the direction to the top of the character.  (90 
           indicates a standard (straight up and down) character.)  Only the 
           following values may be specified: 0, 90, 180, 270.  The default is 
           90. 
  xloc 
           The starting X (length) location for the display of the entry 
           specified as a percent of Normalized Device Coordinate (NDC) space. 
           A value between 0 and 100 (inclusive) must be specified. 
  yloc 
           The starting Y (width) location for the display of the entry 
           specified as a percent of Normalized Device Coordinate (NDC) space. 
           A value between 0 and 100 (inclusive) must be specified. 
  zloc 
           The starting Z (height) location for the display of the entry 
           specified as a percent of Normalized Device Coordinate (NDC) space. 
           A value between 0 and 100 (inclusive) may be specified.  The 
           default is 0. 
00001
00002
00003
00004
00005
00006
00007
GRAPHICS_ENTRY_OPTIONS
A list of SUPER form options can be accessed by typing a ? or a ??.  To obtain 
definitions of individual form options, type 
HELP (SUPER) GRAPHICS_FORM_OPTS option 
where option is any of the following: 
ACCESS, ACCOUNT, ALIGNMENT, BANNER, CHARSET, DEVICE, REMOVE_ALIGNMENT, 
REMOVE_BANNER, SETUP, XOFFSET, XSIZE, YOFFSET, YSIZE, ZOFFSET, ZSIZE 
  Option    Description 
  ACCE[SS] [A[DD]|R[EMOVE]] = tname[, tname] ... 
            Sets the access list of terminal names (which may be wildcarded) 
            that can use this graphic form.  ADD supplies additional tnames to 
            the list.  REMOVE deletes tnames from the list. 
  ACCO[UNT] [A[DD]|R[EMOVE]] = account[, account] ... 
            Sets the access list of accounts that can use this graphic form. 
            If no account is specified, any account can use this form.  ADD 
            supplies additional accounts to the list.  REMOVE deletes accounts 
            from the list. 
  AL[IGNMENT] 
            Defines the alignment image for this graphic form.  SUPER requests 
            sub-options with the prompt 'SUB*'.  To access these sub-options, 
            type HELP (SUPER) GRAPHICS_ALIGN_SUBOPTS. 
  BA[NNER] 
            Defines the banner image for this graphic form.  SUPER requests 
            sub-options with the prompt 'SUB*'.  To access these sub-options, 
            type HELP (SUPER) GRAPHICS_BAN_SUBOPTS. 
  CH[ARSET]|CHAI[N] = charsetname 
            Copies the logical device types (i.e., ELSOK, LPOK, LTYP, and 
            TSOK) from the specified CHARSET record into this graphic form 
            definition. 
  DE[VICE LIMITS] parameter = value 
            Sets the specified user-manageable SET DEVICE LIMITS parameter to 
            the desired value.  The first ten parameters of the graphic 
            instruction SET DEVICE LIMITS are reserved for system use.  The 
            second ten parameters are available to the knowledgeable user (who 
            must have appropriately modified the device handler to utilize 
            these values).  Values are assigned to the parameters through this 
            graphic FORM option.  The parameter field is assigned a value from 
            0 to 9, which identifies the user-manageable parameter 
            (0=10,1=11,...9=19).  The value field contains a value 0 < value < 
            65535 that is passed to the graphics device driver. 
  R[EMOVE] A[LIGNMENT] 
            Removes the alignment image from the graphic form. 
  R[EMOVE] B[ANNER] 
            Removes the banner image from the graphic form. 
  SE[TUP] 
            Indicates that an operator message of setup information is to be 
            defined.  SUPER prompts with 'TXT*' and 82 lines of 72 characters 
            each can be entered.  A blank line ends the entry.  If all 82 
            lines are entered, SUPER responds with: 
               SETUP BUFFER FULL,RETURNING TO 
               'OPT*' LEVEL. 
  XO[FFSET][=value] 
            Specifies in tenths of millimeters the X coordinate (length) 
            offset from the 0,0,0 (origin) location for the device.  0 < value 
            < 65535.  The default is 0. 
  XS[IZE][=value] 
            Specifies in tenths of millimeters the X coordinate (length 
            dimension) of the plotting area.  0 < value < 65535.  The default 
            is 0. 
  YO[FFSET][=value] 
            Specifies in tenths of millimeters the Y coordinate (width) offset 
            from the 0,0,0 (origin) location for the device.  0 < value < 
            65535.  The default is 0. 
  YS[IZE][=value] 
            Specifies in tenths of millimeters the Y coordinate (width 
            dimension) of the plotting area.  0 < value < 65535.  The default 
            is 0. 
  ZO[FFSET][=value] 
            Specifies in tenths of millimeters the Z coordinate (height) 
            offset from the 0,0,0 (origin) location for the device.  0 < value 
            < 65535.  The default is 0. 
  ZS[IZE][=value] 
            Specifies in tenths of millimeters the Z coordinate (height 
            dimension) of the plotting area.  0 < value < 65535.  The default 
            is 0. 
00001
00002
00003
00004
00005
00005
00006
00007
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
GRAPHICS_FORM_OPTIONS
  Option                       Description                           Device 
A list of graphics profile options and their definitions can be 
accessed by typing a ? or ??. 
To obtains individual options, type: 
HELP (SUPER) GRAPHICS_PROFILE_OPTS option 
where option is any of the following: 
GR_BATCHMODE, GR_BKGRNDCOLOR, GR_BKGRNDTYPE, GR_CHSIZECOUNT, GR_CHSIZESUPPORT, 
GR_COLRACTION, GR_COLRMODEL, GR_COLRTABSIZE, GR_COLRTABTLYPE, GR_DEPTHULSE, 
GR_DEVTYPE, GR_DIMLEVEL, GR_EDGETYPE, GR_ESCAPE, GR_FONTLCOUNT, GR_FPRG, 
GR_GLBLCOLORS, GR_GLBLINTENSITIES, GR_HEIGHTUSE, GR_HIDDENLEVEL, 
GR_HIGHLTSUPPORT, GR_IMAGETRANS, GR_INTNACTION, GR_INTNSUPPORT, 
GR_INTNTABSIZE, GR_LINESTYLEHWCOUNT, GR_LINESTYLESWCOUNT, GR_LINEWCOUNT, 
GR_LINEWSUPPORT, GR_MARKERHWCOUNT, GR_MARKERSWCOUNT, GR_MAXCHSIZE, 
GR_MAXLINEWIDTH, GR_MAXPICK, GR_MINCHSIZE, GR_MINLINEWIDTH, GR_NDCDCHARS, 
GR_NDCDCURRENT, GR_NDCDSPACE, GR_NDCHCHARS, GR_NDCHCURRENT, GR_NDCHSPACE, 
GR_NDCWCHARS, GR_NDCWCURRENT, GR_NDCWSPACE, GR_OUTLEVEL, GR_PENHWCOUNT, 
GR_PENSWCOUNT, GR_PIXELTYPE, GR_POLYGONFILL, GR_VIEWSURFACE, GR_VIEWTYPE, 
GR_WIDTHUSE, GR_XPIXMAX, GR_XSPACE, GR_YPIXMAX, GR_YSPACE, and 
GR_ZSPACE. 
GR_BATCH[MODE]=value        Specifies the strategy (1-4) used      GRAPHICS 
                            by the device driver for batching 
                            of updates as follows: 
                                    1 - defer-nothing 
                                    2 - defer-deletion 
                                    3 - defer-retained 
                                    4 - defer-all 
                            The default is 1. 
GR_BKGRNDC[OLOR]=value      Specifies the background color         GRAPHICS 
                            (1-2) of the device and its view 
                            surface as follows: 
                                    1 - black 
                                    2 - white 
                            The default is 1. 
GR_BKGRNDT[YPE]=value       Specifies the background type          GRAPHICS 
                            (1-2) of the device as follows: 
                                    1 - fixed 
                                    2 - variable 
                            The default is 2. 
GR_CHSIZEC[OUNT]=value      Specifies a count (1-32767) of the     GRAPHICS 
                            number of different hardware 
                            character sizes available from 
                            the device.  The default is 
                            32767. 
GR_CHSIZES[UPPORT]=value    Specifies the type of support          GRAPHICS 
                            (0-3) given to the GR_CHSIZECOUNT 
                            count as follows: 
                                    0 - no support for any 
                                        charsize 
                                    1 - hardware support 
                                    2 - software support 
                                    3 - both hardware and 
                                        software support 
                            The default is 1. 
GR_COLRA[CTION]=value       Specifies the type of color            GRAPHICS 
                            action (0-2) this device and 
                            driver support as follows: 
                                    0 - none 
                                    1 - sequential 
                                    2 - retroactive 
                            The default is 2. 
GR_COLRM[ODEL]=value        Specifies the model (1-2) used         GRAPHICS 
                            by the device as follows: 
                                    1 - HLS 
                                    2 - RGB 
                            The default is 2. 
GR_COLRTABS[IZE]=value      Specifies the maximum number           GRAPHICS 
                            (0-32767) of entries possible 
                            in this device or driver color 
                            index table.  The default is 
                            32767. 
GR_COLRTABT[YPE]=value      Specifies the type (1-4) of color      GRAPHICS 
                            table available as follows: 
                                    1 - fixed 
                                    2 - dynamic 
                                    3 - direct color 
                                    4 - fixed dynamic 
                            The default is 4. 
GR_DEPTHU[SE]=value         Specifies the depth in centimeters     GRAPHICS 
                            (0-999999) of the usable display. 
                            The default is 999999. 
GR_DEV[TYPE]=value          Specifies the device type (0-1) as     GRAPHICS 
                            follows: 
                                    0 - pseudo or file 
                                    1 - real or display surface 
                            The default is 0. 
GR_DIM[LEVEL]=value         Specifies the dimension level (2-3)    GRAPHICS 
                            supported by this device and device 
                            driver as follows: 
                                    2 - 2 dimensional 
                                    3 - 3 dimensional 
                            The default is 3. 
GR_EDGE[TYPE]=value         Specifies the type of edges (0-3)      GRAPHICS 
                            supported by the device and the 
                            device driver. 
                                    0 - none (generally 
                                        not used) 
                                    1 - interior only 
                                    2 - solid only (as in a 
                                        vector generator) 
                                    3 - both interior and 
                                        solid 
                            The default is 0. 
GR_ESC[APE] x = {H[ARDWARE]|S[OFTWARE]|U[NSUPPORTED] 
                            Defines an escape function and         GRAPHICS 
                            specifies whether the escape 
                            function is supported in the actual 
                            hardware (HARDWARE) or is simulated 
                            in the software (SOFTWARE). 
                            UNSUPPORTED deletes an escape 
                            function.  The value of x can be 
                            0-32767.  Up to 63 escape functions 
                            can be supported at any one time. 
                            The escape functions are maintained 
                            in sorted ascending order in the 
                            graphics profile record.  The 
                            following GR_ESCAPE options have 
                            default values: 
                                GR_ESCAPE      Default 
                                    1          HARDWARE 
                                    2          HARDWARE 
                                    3          SOFTWARE 
                                    4          SOFTWARE 
GR_FONT[COUNT]=value        Specifies a count (1-32767) of the     GRAPHICS 
                            number of different fonts supported 
                            by the device and its driver.  The 
                            default is 32767. 
GR_FPRG=fid                 Specifies the 1 to 64 character        GRAPHICS 
                            graphics handler run unit fid. 
                            The default is nil.  The GDDR 
                            fid will be a part of the profile 
                            header record. 
GR_GLBLCO[LORS]=value       Specifies the maximum number           GRAPHICS 
                            (1-999999999) of colors that 
                            this device can generate.  The 
                            default is 999999999. 
GR_GLBLIN[TENSITIES]=value  Specifies the maximum number           GRAPHICS 
                            (1-999999999) of different levels 
                            of intensity this device and driver 
                            support.  The  default is 999999999. 
GR_HEIGHTU[SE]=value        Specifies the height in centimeters    GRAPHICS 
                            (0-999999) of the usable display. 
                            The default is 999999. 
GR_HID[DENLEVEL]=value      Specifies the level (0-3) of hid-      GRAPHICS 
                            den surface or hidden line removal 
                            supported by the device or the 
                            device driver as follows: 
                                    0 - none 
                                    1 - temporal 
                                    2 - explicit 
                                    3 - full 
                            The default is 3. 
GR_HIGHLTS[UPPORT]=value    Specifies the type of support          GRAPHICS 
                            (0-3) given to the highlighting 
                            primitive attribute as follows: 
                                    0 - no support for any 
                                        highlighting 
                                    1 - hardware support 
                                    2 - software support 
                                    3 - both hardware and 
                                        software support 
                            The default is 1.  Any highlight- 
                            ing support is valid only if 
                            GR_OUTLEVEL is not basic. 
GR_IMA[GETRANS]=value       Specifies the level of hardware        GRAPHICS 
                            support (0-3) for image 
                            transformations. 
                            value = 0 - none 
                                    1 - a 
                                    2 - b 
                                    3 - c 
                            The default is 0.  This bit 
                            setting has meaning only if the 
                            GR_OUTLEVEL is not basic. 
GR_INTNACT[ION]=value       Specifies the type of intensity        GRAPHICS 
                            action (0-2) this device and 
                            driver support as follows: 
                                    0 - none 
                                    1 - sequential 
                                    2 - retroactive 
                            The default is 2. 
GR_INTNSUP[PORT]=value      Specifies the type of support          GRAPHICS 
                            (0-3) given to the intensity 
                            count above as follows: 
                                    0 - no support for any 
                                        intensity 
                                    1 - hardware support 
                                    2 - software support 
                                    3 - both hardware and 
                                        software support 
                            The default is 1. 
GR_INTNTAB[SIZE]=value      Specifies the maximum number           GRAPHICS 
                            (0-32767) of entries possible 
                            in this device or driver's 
                            intensity index table.  The 
                            default is 32767. 
GR_LINESTYLEH[WCOUNT]=value 
                            Specifies a count (1-9) of the         GRAPHICS 
                            number of different hardware line 
                            styles supported by the device and 
                            its driver.  The different styles 
                            refer to solid, dashed, and dotted. 
                            The default is 9. 
GR_LINESTYLES[WCOUNT]=value 
                            Specifies a count (0-9990) of          GRAPHICS 
                            different software line styles 
                            supported by the device and its 
                            driver.  The different styles 
                            refer to solid, dashed, and 
                            dotted.  The default is 9990. 
GR_LINEWC[OUNT]=value       Specifies a count (1-32767) of         GRAPHICS 
                            the number of different line 
                            widths supported by the device 
                            and its driver.  The default 
                            is 32767. 
GR_LINEWS[UPPORT]=value     Specifies the type of support          GRAPHICS 
                            (0-3) for the various line widths 
                            as follows: 
                                    0 - no support for any 
                                        line width 
                                    1 - hardware support 
                                    2 - software support 
                                    3 - both hardware and 
                                        software support 
                            The default is 1. 
GR_MARKERH[WCOUNT]=value    Specifies a count (0-32767) of         GRAPHICS 
                            the different hardware marker 
                            symbols supported by the device 
                            and its driver.  The default 
                            is 32767. 
GR_MARKERS[WCOUNT]=value    Specifies a count (0-32767) of         GRAPHICS 
                            the number of different software 
                            marker symbols supported by the 
                            device and its driver.  The default 
                            is 32767. 
GR_MAXCH[SIZE]=value        Specifies the maximum character        GRAPHICS 
                            size in NDC coordinates (0-32767). 
                            The default is 327 (one percent). 
                            (The value is taken as a percentage 
                            of NDC space, where 0 represents 
                            0% and 32767 represents 100%.) 
GR_MAXLINE[WIDTH]=value     Specifies the maximum line width       GRAPHICS 
                            in NDC coordinates (0-32767). 
                            The default is 327 (one percent). 
                            (The value is taken as a percentage 
                            of NDC space, where 0 represents 
                            0% and 32767 represents 100%.) 
GR_MAXP[ICK]=value          Specifies the maximum number           GRAPHICS 
                            (0-32767) of pick id's supported 
                            by this device.  The default is 
                            32767. 
GR_MINCH[SIZE]=value        Specifies the minimum character        GRAPHICS 
                            size (0-32767) in NDC coordinates. 
                            The default is 1.  The value is 
                            taken as a percentage of NDC 
                            space, where 0 represents 0% and 
                            32767 represents 100%.) 
GR_MINLINE[WIDTH]=value     Specifies the minimum line width       GRAPHICS 
                            in NDC coordinates (0-32767). 
                            The default is 1.  (The value is 
                            taken as a percentage of NDC space, 
                            where 0 represents 0% and 32767 
                            represents 100%.) 
GR_NDCDCH[ARS]=value        Specifies the depth of NDC space       GRAPHICS 
                            in addressable character 
                            positions (0-999999999).  The 
                            default is 999999999. 
GR_NDCDCUR[RENT]=value      Specifies the depth of NDC space       GRAPHICS 
                            (0-32767 which, means 
                            0.0<=value<=1.0).  The 
                            default is 32767. 
GR_NDCDSP[ACE]=value        Specifies the depth of NDC space       GRAPHICS 
                            in addressable units 
                            (0-999999999).  The default is 
                            999999999. 
GR_NDCHCH[ARS]=value        Specifies the height of NDC space      GRAPHICS 
                            in addressable character positions 
                            (0-999999999).  The default is 
                            999999999. 
GR_NDCHCUR[RENT]=value      Specifies the height of NDC space      GRAPHICS 
                            (0-32767, which means 
                            0.0<=value<=1.0).  The default 
                            is 32767. 
GR_NDCHSP[ACE]=value        Specifies the height of NDC space      GRAPHICS 
                            in addressable units (0-999999999). 
                            The default is 999999999. 
GR_NDCWCH[ARS]=value        Specifies the width of NDC space       GRAPHICS 
                            in addressable character positions 
                            (0-999999999).  The default is 
                            999999999. 
GR_NDCWCUR[RENT]=value      Specifies the width of NDC space       GRAPHICS 
                            (0-32767, which means 0.0<=value 
                            <=1.0).  The default is 32767. 
GR_NDCWSP[ACE]=value        Specifies the width of NDC space       GRAPHICS 
                            in addressable units (0-999999999). 
                            The default is 999999999. 
GR_OUT[LEVEL]=value         Specifies the highest output           GRAPHICS 
                            level (1-5) supported by the 
                            device driver as follows: 
                            value = 1 - basic 
                                    2 - buffered 
                                    3 - dynamic a 
                                    4 - dynamic b 
                                    5 - dynamic c 
                            The default is 1. 
GR_PENH[WCOUNT]=value       Specifies a count (0-32767) of the     GRAPHICS 
                            number of different hardware pens 
                            supported by the device and its 
                            driver.  Pen refers to a collection 
                            of Line Index, Line Style, Line 
                            Width, and Text Index.  The default 
                            is 32767. 
GR_PENS[WCOUNT]=value       Specifies a count (0-32767) of the     GRAPHICS 
                            number of different software pens 
                            supported by the device and its 
                            driver.  Pen refers to a collection 
                            of Line Index, Line Style, Line 
                            Width, and Text Index.  The default 
                            is 32767. 
GR_PIX[ELTYPE]=value        Specifies the availability of          GRAPHICS 
                            pixel addressing functions (1-3) 
                            as follows: 
                                    1 - read/write functions 
                                        available 
                                    2 - functions not available 
                                    3 - write functions only 
                                        available 
                            The default is 1. 
GR_POLY[GONFILL] {PAT[TERNED]|PLA[IN]|SHA[DED]}=value              GRAPHICS 
                            PAT[TERNED]    specifies the 
                            maximum number of edges that can 
                            be supported with a patterned 
                            type of polygon fill. 
                            PLA[IN]    specifies the maximum 
                            number of edges that can be 
                            supported with a plain type of 
                            polygon fill. 
                            SHA[DED]    specifies the maximum 
                            number of edges that can be 
                            supported with a shaded type of 
                            polygon fill. 
                            The value for value is 0-32767. 
                            The default is 32767 for all 
                            three types. 
GR_VIEWSURF[ACE]=value      Specifies the initialized view         GRAPHICS 
                            surface (0-32767) about which an 
                            inquiry of device characteristics 
                            has been made.  The default is 0. 
GR_VIEWTY[PE]=value         Specifies the type of view surface     GRAPHICS 
                            (0-3) as follows: 
                                    0 - character only 
                                    1 - vector only 
                                    2 - intensity only 
                                    3 - color 
                            The default is 3. 
GR_WIDTHU[SE]=value         Specifies the width in centi-          GRAPHICS 
                            meters (0-999999) of usable 
                            display.  The default is 
                            999999. 
GR_XPIX[MAX]=value          Specifies the maximum size             GRAPHICS 
                            (0-65535) in the X direction of 
                            the pixel array.  The default is 
                            65535. 
GR_XSP[ACE]=value           Specifies the addressable units        GRAPHICS 
                            (0-4095) of the view surface in 
                            X per centimeters.  The default 
                            is 4095. 
GR_YPIX[MAX]=value          Specifies the maximum size             GRAPHICS 
                            (0-32767) in the Y direction of 
                            the pixel array.  The default is 
                            32767. 
GR_YSP[ACE]=value           Specifies the addressable units        GRAPHICS 
                            (0-4095) of the view surface in 
                            Y per centimeters.  The default 
                            is 4095. 
GR_ZSP[ACE]=value           Specifies the addressable units        GRAPHICS 
                            (0-4095) of the view surface in 
                            Z per centimeters.  The default 
                            is 4095. 
00022
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
00017
00018
00019
00020
00021
00021
00022
00023
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
GRAPHICS_PROFILE_OPTIONS
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
  accounting - 
      HELP USER_OPTIONS *S_ACCOUNTING 
  ADMIN console option - 
      HELP CONSOLE_OPTIONS ADMIN 
  ASYNC Profiles - 
      HELP PROFILE DESCRIPTION: 
B 
  Banner field - 
      HELP USER_OPTIONS BANNERTEXT 
  BUDGET option (SUPER) - 
      HELP USER_OPTIONS CPROC 
C 
  Chain images - 
      HELP CHARSET_OPTIONS IMAGE 
  CHARSET - 
      HELP CREATE_CHARSET FORMAT: 
  Comgroup - 
      HELP DEVICE_OPTIONS COMGROUP_CG 
  COMMUNICATION console option - 
      HELP CONSOLE_OPTIONS COMMUNICATION 
  CONSOLE Commands - 
      HELP CONSOLE 
  console, terminal - 
      HELP TERMINAL_OPTIONS CONSOLE 
  CONTROLLER Commands - 
      HELP CONTROLLER 
  controller type - 
      HELP CONTROLLER_OPTIONS TYPE 
  CPU time for user - 
      HELP USER_OPTIONS TIME 
  CREATE and MODIFY CHARSET Commands - 
      HELP CREATE_CHARSET 
  CREATE and MODIFY FORM Commands - 
      HELP CREATE_FORM 
  CREATE and MODIFY FORM GRAPHICS Commands - 
      HELP CREATE_FORM_GRAPHICS 
  CREATE and MODIFY PSEUDO Commands - 
      HELP CREATE_PSEUDO 
  CREATE CHARSET Command (SUPER) - 
      HELP CREATE_CHARSET FORMAT: 
  CREATE Command - 
      HELP CREATE 
  CREATE command (SUPER) - 
      HELP CREATE FORMAT: 
  CREATE CONSOLE command (SUPER) - 
      HELP CONSOLE FORMAT: 
  CREATE CONTROLLER command (SUPER) - 
      HELP CONTROLLER FORMAT: 
  CREATE DEVICE command (SUPER) - 
      HELP DEVICE FORMAT: 
  CREATE DEVICE FOR LINE command (SUPER) - 
      HELP DEVICE_FOR_LINE FORMAT: 
  CREATE LINE command (SUPER) - 
      HELP LINE FORMAT: 
  CREATE LINK command (SUPER) - 
      HELP LINK FORMAT: 
  CREATE PROFILE command (SUPER) - 
      HELP PROFILE FORMAT: 
  CREATE PROJECT Command - 
      HELP CREATE_PROJECT 
  CREATE PSEUDO command (SUPER) - 
      HELP CREATE_PSEUDO FORMAT: 
  CREATE STATION command (SUPER) - 
      HELP STATION FORMAT: 
  CREATE TERMINAL command (SUPER) - 
      HELP TERMINAL FORMAT: 
  CREATE VIRTUAL CIRCUIT command (SUPER) - 
      HELP VIRTUAL_CIRCUIT FORMAT: 
  CREATE WSN command (SUPER) - 
      HELP WSN FORMAT: 
D 
  Default priority for device - 
      HELP DEVICE_OPTIONS DEFPRIO_IN 
  DELETE CHARSET Command - 
      HELP DELETE_CHARSET 
  DELETE CHARSET command (SUPER) - 
      HELP DELETE_CHARSET FORMAT: 
  DELETE Command - 
      HELP DELETE_USERS 
  DELETE command (SUPER) - 
      HELP DELETE_USERS FORMAT: 
  DELETE CONSOLE command (SUPER) - 
      HELP CONSOLE FORMAT: 
  DELETE DEVICE command (SUPER) - 
      HELP DEVICE FORMAT: 
  DELETE FORM command (SUPER) - 
      HELP DELETE_FORMS FORMAT: 
  DELETE FORMS Command - 
      HELP DELETE_FORMS 
  DELETE PROFILE command (SUPER) - 
      HELP PROFILE FORMAT: 
  DELETE TERMINAL command (SUPER) - 
      HELP TERMINAL FORMAT: 
  DEVICE Commands - 
      HELP DEVICE 
  DEVICE console option - 
      HELP CONSOLE_OPTIONS DEVICE 
  DEVICE FOR LINE Commands - 
      HELP DEVICE_FOR_LINE 
  DEVICE FOR LINK Commands - 
      HELP DEVICE_FOR_LINK_COMMAND 
  Device for terminal - 
      HELP TERMINAL_OPTIONS DEVICE 
  Device type - 
      HELP DEVICE_OPTIONS TYPE_OUT 
      HELP DEVICE_OPTIONS TYPE_RESOURCE 
  Device type (3270) - 
      HELP DEVICE_FOR_LINE_OPTIONS TYPE 
  DEVICE_ATTRIBUTE_OPTIONS - 
      HELP DEVICE_ATTRIBUTE_OPTIONS 
  DISPLAY ALL CONSOLE command (SUPER) - 
      HELP CONSOLE FORMAT: 
  DISPLAY CHARSETS Command - 
      HELP DISPLAY_CHARSETS 
  DISPLAY CHARSETS command (SUPER) - 
      HELP DISPLAY_CHARSETS FORMAT: 
  DISPLAY Command - 
      HELP DISPLAY 
  DISPLAY Command (SUPER) - 
      HELP DISPLAY FORMAT: 
  DISPLAY FORMS Command - 
      HELP DISPLAY_FORMS 
  DISPLAY FORMSETS Command - 
      HELP DISPLAY_FORMSETS 
  DISPLAY FORMSETS command (SUPER) - 
      HELP DISPLAY_FORMSETS FORMAT: 
  DISPLAY PROJECT Command - 
      HELP DISPLAY_PROJECT 
F 
  File management account - 
      HELP USER_OPTIONS FACCOUNT 
  file retention for user - 
      HELP USER_OPTIONS EXPIRE 
  Files Created by SUPER - 
      HELP RELATED_FILES 
  form - 
      HELP CREATE_FORM DESCRIPTION: 
      HELP CREATE_FORM_GRAPHICS DESCRIPTION: 
  :FORM file - 
      HELP RELATED_FILES 
  Form for device - 
      HELP DEVICE_OPTIONS FORM_OUT 
  form, default - 
      HELP WSN_OPTIONS DFORM 
  Forms management - 
      HELP SAMPLE_SUPER_RUNS_FOR_USER_AUTHORIZATION 
H 
  :HLP file - 
      HELP RELATED_FILES 
I 
  Instance of TP - 
      HELP DEVICE_OPTIONS INSTANCE_TP 
  Invoking SUPER - 
      HELP INVOKING_SUPER 
L 
  LINE Commands - 
      HELP LINE 
  LINK Commands - 
      HELP LINK 
  LIST ALL CONSOLE command (SUPER) - 
      HELP CONSOLE FORMAT: 
  LIST CHARSET Command - 
      HELP LIST_CHARSET 
  LIST CHARSET Command (SUPER) - 
      HELP LIST_CHARSET FORMAT: 
  LIST Command - 
      HELP LIST 
  LIST Command (SUPER) - 
      HELP LIST FORMAT: 
  LIST CONTROLLER command (SUPER) - 
      HELP CONTROLLER FORMAT: 
  LIST DEVICE command (SUPER) - 
      HELP DEVICE FORMAT: 
  LIST FORM Command - 
      HELP LIST_FORM 
  LIST FORM Command (SUPER) - 
      HELP LIST_FORM FORMAT: 
  LIST FORMSETS Command - 
      HELP LIST_FORMSETS 
  LIST LINE command (SUPER) - 
      HELP LINE FORMAT: 
  LIST LINK command (SUPER) - 
      HELP LINK FORMAT: 
  LIST PROFILE command (SUPER) - 
      HELP PROFILE FORMAT: 
  LIST PROJECT Command - 
      HELP LIST_PROJECT 
  LIST PROJECT command (SUPER) - 
      HELP LIST_PROJECT FORMAT: 
  LIST STATION command (SUPER) - 
      HELP STATION FORMAT: 
  LIST TERMINAL command (SUPER) - 
      HELP TERMINAL FORMAT: 
  LIST VIRTUAL CIRCUIT command (SUPER) - 
      HELP VIRTUAL_CIRCUIT FORMAT: 
  LIST WSN command (SUPER) - 
      HELP WSN FORMAT: 
M 
  MAKEME Command - 
      HELP MAKEME 
  MAKEME command (SUPER) - 
      HELP MAKEME FORMAT: 
  Master Control Terminal (MCT) - 
      HELP DEVICE_OPTIONS MCT_TP 
  MAXPRIO for console - 
      HELP CONSOLE_OPTIONS MAXPRIO 
  MAXPRIO for device - 
      HELP DEVICE_OPTIONS MAXPRIO_IN 
  MODIFY Command - 
      HELP MODIFY 
  MODIFY command (SUPER) - 
      HELP MODIFY FORMAT: 
  MODIFY CONSOLE command (SUPER) - 
      HELP CONSOLE FORMAT: 
  MODIFY CONTROLLER command (SUPER) - 
      HELP CONTROLLER FORMAT: 
  MODIFY DEVICE command (SUPER) - 
      HELP DEVICE FORMAT: 
  MODIFY DEVICE FOR LINE command (SUPER) - 
      HELP DEVICE_FOR_LINE FORMAT: 
  MODIFY LINE command (SUPER) - 
      HELP LINE FORMAT: 
  MODIFY LINK command (SUPER) - 
      HELP LINK FORMAT: 
  MODIFY PROFILE command (SUPER) - 
      HELP PROFILE FORMAT: 
  MODIFY PROJECT Command - 
      HELP MODIFY_PROJECT 
  MODIFY PROJECT command (SUPER) - 
      HELP MODIFY_PROJECT FORMAT: 
  MODIFY PSEUDO command (SUPER) - 
      HELP CREATE_PSEUDO FORMAT: 
  MODIFY TERMINAL command (SUPER) - 
      HELP TERMINAL FORMAT: 
  MODIFY VIRTUAL CIRCUIT command (SUPER) - 
      HELP VIRTUAL_CIRCUIT FORMAT: 
  MODIFY WSN command (SUPER) - 
      HELP WSN FORMAT: 
N 
  NCTL option - 
      HELP DEVICE_OPTIONS NCTL_IN 
  Non-Control (NCTL) Devices - 
      HELP NCTL_DEVICES 
  Non-control files - 
      HELP NCTL_DEVICES 
      HELP DEVICE_OPTIONS NCTL_IN 
P 
  PADMIN console option - 
      HELP CONSOLE_OPTIONS PADMIN 
  Password for console - 
      HELP CONSOLE_OPTIONS PASSWORD 
  Password for device - 
      HELP DEVICE_OPTIONS PASSWORD 
  Password, terminal logon - 
      HELP TERMINAL_OPTIONS PASSWORD 
  Print chain images - 
      HELP CHARSET_OPTIONS IMAGE 
  PRIVILEGE - 
      HELP USER_OPTIONS PRIVILEGE 
  Privileges for Use of SUPER - 
      HELP PRIVILEGES 
  :PRO file - 
      HELP RELATED_FILES 
  PROFILE Commands - 
      HELP PROFILE 
  Profile for console - 
      HELP CONSOLE_OPTIONS PROFILE 
  Profile for device - 
      HELP DEVICE_OPTIONS PROFILE 
  PROFILE for line - 
      HELP LINE DESCRIPTION: 
  Profile for link - 
      HELP LINK_OPTIONS PROFILE 
  Profile for RBT - 
      HELP TERMINAL_OPTIONS PROFILE 
  Profile names - 
      HELP PROFILE DESCRIPTION: 
  profile, logon - 
      HELP USER_OPTIONS PROFILE 
  3270 Profiles - 
      HELP PROFILE DESCRIPTION: 
  PROFILE_OPTIONS - 
      HELP PROFILE_OPTIONS 
  :PROJ file - 
      HELP RELATED_FILES 
  pseudo form - 
      HELP CREATE_PSEUDO DESCRIPTION: 
  pseudo resource - 
      HELP USER_OPTIONS PSEUDO 
R 
  RBT Device Profiles - 
      HELP PROFILE DESCRIPTION: 
  RBT Line Profiles - 
      HELP PROFILE DESCRIPTION: 
  RECONFIGURE STATION LOCAL - 
      HELP STATION DESCRIPTION: 
  RECONFIGURE STATION LOCAL - 
      HELP WSN DESCRIPTION: 
  REMOVE CHARSET Command - 
      HELP REMOVE_CHARSET 
  REMOVE CHARSET Command (SUPER) - 
      HELP REMOVE_CHARSET FORMAT: 
  REMOVE Command - 
      HELP REMOVE 
  REMOVE command (SUPER) - 
      HELP REMOVE FORMAT: 
  REMOVE CONSOLE command (SUPER) - 
      HELP CONSOLE FORMAT: 
  REMOVE CONTROLLER command (SUPER) - 
      HELP CONTROLLER FORMAT: 
  REMOVE DEVICE command (SUPER) - 
      HELP DEVICE FORMAT: 
  REMOVE DEVICE FOR LINE command (SUPER) - 
      HELP DEVICE_FOR_LINE FORMAT: 
  REMOVE FORM Command - 
      HELP REMOVE_FORM 
  REMOVE FORM command (SUPER) - 
      HELP REMOVE_FORM FORMAT: 
  REMOVE LINE command (SUPER) - 
      HELP LINE FORMAT: 
  REMOVE LINK command (SUPER) - 
      HELP LINK FORMAT: 
  REMOVE PROFILE command (SUPER) - 
      HELP PROFILE FORMAT: 
  REMOVE PROJECT Command - 
      HELP REMOVE_PROJECT 
  REMOVE PROJECT command (SUPER) - 
      HELP REMOVE_PROJECT FORMAT: 
  REMOVE STATION command (SUPER) - 
      HELP STATION FORMAT: 
  REMOVE TERMINAL command (SUPER) - 
      HELP TERMINAL FORMAT: 
  REMOVE VIRTUAL CIRCUIT command (SUPER) - 
      HELP VIRTUAL_CIRCUIT FORMAT: 
  REMOVE WSN command (SUPER) - 
      HELP WSN FORMAT: 
  resources for user - 
      HELP USER_OPTIONS RESOURCES 
S 
  SLAVE console option - 
      HELP CONSOLE_OPTIONS SLAVE 
  Special Device Handling In Banners - 
      HELP DEV_HANDLING_BANNERS 
  STATION Commands - 
      HELP STATION 
  step accounting - 
      HELP USER_OPTIONS STEPACCNT 
  SUPER -   
    CONSOLE Command - 
      HELP CONSOLE FORMAT: 
    CONTROLLER Command - 
      HELP CONTROLLER FORMAT: 
    CREATE CHARSET Command - 
      HELP CREATE_CHARSET FORMAT: 
    CREATE Command - 
      HELP CREATE FORMAT: 
    CREATE CONSOLE Command - 
      HELP CONSOLE FORMAT: 
    CREATE CONTROLLER Command - 
      HELP CONTROLLER FORMAT: 
    CREATE DEVICE Command - 
      HELP DEVICE FORMAT: 
    CREATE DEVICE FOR LINE Command - 
      HELP DEVICE_FOR_LINE FORMAT: 
    CREATE LINE Command - 
      HELP LINE FORMAT: 
    CREATE LINK Command - 
      HELP LINK FORMAT: 
    CREATE PROFILE Command - 
      HELP PROFILE FORMAT: 
    CREATE PROJECT Command - 
      HELP CREATE_PROJECT FORMAT: 
    CREATE PSEUDO Command - 
      HELP CREATE_PSEUDO FORMAT: 
    CREATE STATION Command - 
      HELP STATION FORMAT: 
    CREATE TERMINAL Command - 
      HELP TERMINAL FORMAT: 
    CREATE VIRTUAL CIRCUIT Command - 
      HELP VIRTUAL_CIRCUIT FORMAT: 
    CREATE WSN Command - 
      HELP WSN FORMAT: 
    DELETE CHARSET command - 
      HELP DELETE_CHARSET FORMAT: 
    DELETE CONSOLE Command - 
      HELP CONSOLE FORMAT: 
    DELETE DEVICE Command - 
      HELP DEVICE FORMAT: 
    DELETE FORM Command - 
      HELP DELETE_FORMS FORMAT: 
    DELETE TERMINAL Command - 
      HELP TERMINAL FORMAT: 
    DEVICE Command - 
      HELP DEVICE FORMAT: 
    DEVICE FOR LINE Command - 
      HELP DEVICE_FOR_LINE FORMAT: 
    DISPLAY ALL CONSOLE command (SUPER) - 
      HELP CONSOLE FORMAT: 
    DISPLAY CHARSETS Command - 
      HELP DISPLAY_CHARSETS FORMAT: 
    DISPLAY FORMSETS Command - 
      HELP DISPLAY_FORMSETS FORMAT: 
    LINE Command - 
      HELP LINE FORMAT: 
    LINK Command - 
      HELP LINK FORMAT: 
    LIST ALL CONSOLE Command - 
      HELP CONSOLE FORMAT: 
    LIST CHARSET command - 
      HELP LIST_CHARSET FORMAT: 
    LIST CONTROLLER Command - 
      HELP CONTROLLER FORMAT: 
    LIST DEVICE Command - 
      HELP DEVICE FORMAT: 
    LIST FORM Command - 
      HELP LIST_FORM FORMAT: 
    LIST LINE Command - 
      HELP LINE FORMAT: 
    LIST LINK Command - 
      HELP LINK FORMAT: 
    LIST PROFILE Command - 
      HELP PROFILE FORMAT: 
    LIST PROJECT Command - 
      HELP LIST_PROJECT FORMAT: 
    LIST STATION Command - 
      HELP STATION FORMAT: 
    LIST TERMINAL Command - 
      HELP TERMINAL FORMAT: 
    LIST VIRTUAL CIRCUIT Command - 
      HELP VIRTUAL_CIRCUIT FORMAT: 
    LIST WSN Command - 
      HELP WSN FORMAT: 
    MAKEME Command - 
      HELP MAKEME FORMAT: 
    MODIFY Command - 
      HELP MODIFY FORMAT: 
    MODIFY CONSOLE Command - 
      HELP CONSOLE FORMAT: 
    MODIFY CONTROLLER Command - 
      HELP CONTROLLER FORMAT: 
    MODIFY DEVICE Command - 
      HELP DEVICE FORMAT: 
    MODIFY DEVICE FOR LINE Command - 
      HELP DEVICE_FOR_LINE FORMAT: 
    MODIFY LINE Command - 
      HELP LINE FORMAT: 
    MODIFY LINK Command - 
      HELP LINK FORMAT: 
    MODIFY PROFILE Command - 
      HELP PROFILE FORMAT: 
    MODIFY PROJECT Command - 
      HELP MODIFY_PROJECT FORMAT: 
    MODIFY PSEUDO Command - 
      HELP CREATE_PSEUDO FORMAT: 
    MODIFY TERMINAL Command - 
      HELP TERMINAL FORMAT: 
    MODIFY VIRTUAL CIRCUIT Command - 
      HELP VIRTUAL_CIRCUIT FORMAT: 
    MODIFY WSN Command - 
      HELP WSN FORMAT: 
    OUTPUT Command - 
      HELP DIRECTING_SUPER'S_OUTPUT 
      HELP DIRECTING_SUPER'S_OUTPUT 
      HELP DIRECTING_SUPER'S_OUTPUT 
      HELP OUTPUT FORMAT: 
    PROFILE Command - 
      HELP PROFILE FORMAT: 
    RECONFIGURE STATION LOCAL Command - 
      HELP WSN DESCRIPTION: 
    REMOVE CHARSET command - 
      HELP REMOVE_CHARSET FORMAT: 
    REMOVE Command - 
      HELP REMOVE FORMAT: 
    REMOVE CONSOLE Command - 
      HELP CONSOLE FORMAT: 
    REMOVE CONTROLLER Command - 
      HELP CONTROLLER FORMAT: 
    REMOVE DEVICE Command - 
      HELP DEVICE FORMAT: 
    REMOVE DEVICE FOR LINE Command - 
      HELP DEVICE_FOR_LINE FORMAT: 
    REMOVE FORM Command - 
      HELP REMOVE_FORM FORMAT: 
    REMOVE LINE Command - 
      HELP LINE FORMAT: 
    REMOVE LINK Command - 
      HELP LINK FORMAT: 
    REMOVE PROFILE Command - 
      HELP PROFILE FORMAT: 
    REMOVE PROJECT Command - 
      HELP REMOVE_PROJECT FORMAT: 
    REMOVE STATION Command - 
      HELP STATION FORMAT: 
    REMOVE TERMINAL Command - 
      HELP TERMINAL FORMAT: 
    REMOVE VIRTUAL CIRCUIT Command - 
      HELP VIRTUAL_CIRCUIT FORMAT: 
    REMOVE WSN Command - 
      HELP WSN FORMAT: 
    STATION Command - 
      HELP STATION FORMAT: 
    TERMINAL Command - 
      HELP TERMINAL FORMAT: 
    TIE Command - 
      HELP TIE FORMAT: 
    TIE PROJECT Command - 
      HELP TIE_PROJECT FORMAT: 
    UNTIE Command - 
      HELP UNTIE FORMAT: 
    UNTIE PROJECT Command - 
      HELP UNTIE_PROJECT FORMAT: 
    VIRTUAL CIRCUIT Command - 
      HELP VIRTUAL_CIRCUIT FORMAT: 
    WORKSTATION - 
      HELP WSN FORMAT: 
  SUPER,DELETE PROFILE command - 
      HELP PROFILE FORMAT: 
  System administration - 
      HELP TIMING_PROFILE_OPTIONS TMNALG_PRM8 
  SYSTEM console option - 
      HELP CONSOLE_OPTIONS SYSTEM 
T 
  TERMINAL Commands - 
      HELP TERMINAL 
  TIE Command - 
      HELP TIE 
  TIE command (SUPER) - 
      HELP TIE FORMAT: 
  TIE PROJECT Command - 
      HELP TIE_PROJECT 
  TIE PROJECT command (SUPER) - 
      HELP TIE_PROJECT FORMAT: 
  TP console option - 
      HELP CONSOLE_OPTIONS TP 
U 
  UADMIN console option - 
      HELP CONSOLE_OPTIONS UADMIN 
  UNTIE Command - 
      HELP UNTIE 
  UNTIE command (SUPER) - 
      HELP UNTIE FORMAT: 
  UNTIE PROJECT Command - 
      HELP UNTIE_PROJECT 
  UNTIE PROJECT command (SUPER) - 
      HELP UNTIE_PROJECT FORMAT: 
  URP Profiles - 
      HELP PROFILE DESCRIPTION: 
  User keys - 
      HELP USER_OPTIONS KEY 
  User password - 
      HELP USER_OPTIONS PASSWORD 
  :USERS file - 
      HELP RELATED_FILES 
V 
  VIRTUAL CIRCUIT Commands - 
      HELP VIRTUAL_CIRCUIT 
W 
  WSN Commands - 
      HELP WSN 
  WSN console option - 
      HELP CONSOLE_OPTIONS WSN 
  :WSN file - 
      HELP RELATED_FILES 
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
SUPER is normally run as an on-line job.  It is invoked by the command !SUPER. 
The DCBs used by SUPER are: 
o   M$SI for input 
o   M$LO for normal output 
o   M$DO for error messages 
o   M$UC for issuing prompts 
o   and the following DCBs used to read and write records in the files 
    created/maintained by SUPER:  M$FORM, M$HLP, M$PRO, M$PROJ, M$USER, and 
    M$WSN. 
In on-line mode, SUPER issues three levels of prompts.  SUPER prompts: 
o   for commands, with the prompt CMD* 
o   for options, with the prompt OPT* 
o   for suboptions, with the prompt SUB* 
The next prompting level (down) is initiated automatically.  The previous 
prompting level (up) is returned to by responding to a prompt with END or a 
carriage return (CR).  END in response to a command level prompt terminates 
SUPER processing. 
If SUPER is run in batch mode, the user must anticipate level changes and exit 
properly from each level before entering a higher-level option or command.  In 
batch mode, at least one blank must precede the carriage return to exit to a 
higher level. 
Format: 
{C[REATE]} LINE lname PROFILE=pname [SLAVE={Y[ES]|N[O]}] 
{M[ODIFY]} 
or 
D[ISPLAY] {[ALL] LINE[S]} [(JCL)] 
          {LINE lname   } 
or 
L[IST] {[ALL] LINE[S]} 
       {LINE lname   } 
or 
R[EMOVE] LINE lname 
Parameters: 
lname    specifies the 1-8 character name of the line to be created, modified, 
removed or listed.  If MODIFY is specified and the line does not exist, it is 
created.  If the LIST or DISPLAY form of the command is used, lname can be 
wildcarded. 
Description: 
The CREATE, MODIFY and REMOVE LINE commands create, modify, and remove (one) 
line definition.  A LINE defines either synchronous lines for a 3270 type 
device or synchronous lines for VIP7700, VIP7814 terminals and printers.  The 
LIST LINE command lists the currently defined lines.  The DISPLAY LINE command 
shows line definitions. 
The LIST LINE command lists line names.  Including lname in the LIST LINE 
command is useful when wildcarding is used or to verify the existence of a 
line definition. 
The DISPLAY LINE command shows a columnized display of the options for 
selected lines (or all lines if the ALL option is specified), prefaced by a 
header consisting of the line information as entered in a CREATE or MODIFY 
LINE command.  Note that PROTOCOL values are always displayed as decimal 
values.  The JCL option causes the command keyword CREATE to be written at the 
beginning of each line definition and the END keyword to be inserted where 
needed. 
SUPER prompts for options when it encounters a CREATE or MODIFY LINE command. 
00002
00001
    A list of LINE command options and their definitions is shown below. 
        PR[OFILE] = pname    specifies the profile for the line. 
        This option must be specified and pname must be defined as a line type 
        profile. 
        The profile type determines the line type.  If pname is a 
        3270 profile, a 3270 line is defined.  A line is defined as 
        a polled VIP line by assigning a polled VIP profile.    
        SLAVE = {Y[ES]|N[O]}    specifies that the CP-6 system is to send the 
        initial bid and possibly the logon string for the line.  This option 
        is valid only for PROTYP=HASP.  It is ignored for PROTYP=3780 or 
        2680.  The default is NO. 
Format: 
{C[REATE]} 
{M[ODIFY]} LINK link-name 
{R[EMOVE]} 
or 
D[ISPLAY] {[ALL] LINK[S] } [(JCL)] 
          {LINK link-name} 
or 
L[IST] {[ALL] LINK[S] } 
       {LINK link-name} 
Parameters: 
link-name    specifies the 1-8 character name of the link to be created, 
modified, removed, displayed or listed.  If MODIFY is specified and the link 
does not exist, it is created.  If the LIST or DISPLAY form of the command is 
used, link-name can be wildcarded. 
Description: 
The CREATE, MODIFY, and REMOVE LINK commands create, modify, and remove (one) 
link definitions.  The LIST LINK command lists current links.  The DISPLAY 
LINK command shows LINK definitions.  A LINK is a physical communication line 
using the HDLC protocol.  A link connects a CP-6 node to a public data network 
(PDN) or to another CP-6 node. 
SUPER prompts for an options when it encounters a CREATE or MODIFY LINK 
command.  The options that can be specified are listed in HELP (SUPER) 
LINK_OPTS. 
The LIST LINK command lists link names.  Including link-name in the LIST LINK 
command is useful when wildcarding is used or to verify the existence of a 
link definition. 
The DISPLAY LINK command shows a columnized display of the options for 
selected links (or all links if the ALL option is specified), prefaced by a 
header consisting of the link information as entered in a CREATE or MODIFY 
LINK command.  The JCL option causes the command keyword CREATE to be written 
at the beginning of each link definition and the END keyword to be inserted 
where needed. 
Usage Note: 
If all virtual circuits (incoming and outgoing) on a link use the same 
profile, the profile need not be specified (via the PROFILE option) when 
creating the virtual circuits.  The profile identified via the DEFAULT VIR CIR 
PRO option in the LINK command for the virtual circuits will be used.  If no 
pname is specified via this option, $VIRCIR will be used. 
In CP-6, by default, incoming and outgoing channels share the entire range of 
LCNs (1-4095).  The need to change HIC, HOC, LIC and LOC values will arise 
when the CP-6 default cannot be used on the connected-to network.  When 
changing these values be aware that each decimal value is interpreted as a 
4-bit field followed by an 8-bit field.  The first field, the 4 most 
significant bits, contains a value between 0-15 that represents the logical 
channel group number (LCGN) for the channel.  The second field, the remaining 
8 bits, contains a value between 0 and 255, which represents the logical 
channel number (LCN). 
The following examples illustrate changing these values. For this example, 
assume that the linked to public network is PSS. 
Assume PSS has the following view of the channel structure: 
    -------------------------------+ LIC    (.1) 
                                   | 
                                   | 
    -------------------------------+ HIC    (.7F) 
    / / / / /  gap  / / / / / / / /| 
    / / / / / / / / / / / / / / / /| 
    -------------------------------+ LOC    (.600) 
                                   | 
                                   | 
    -------------------------------+ HOC    (.67F) 
In this case, the LIC, HIC, LOC and HOC parameters can be set to cause an 
exact match between the PSS view and the CP-6 view of the channel structure. 
Now, suppose the PSS view of the structure includes gaps and a Bothways area. 
In this view: 
o   Incoming (always) starts at 200 hex (LCGN=2). 
o   Bothways starts at 400 hex (LCGN=4). 
o   Outgoing is (actually stops) at 600 hex (LCGN=6). 
The PSS view of this structure can be: 
    0 
    -------------------------------+ 
                                   | 
       Permanent VC                | 
                                   | 
    -------------------------------+ 
    / / / / /  gap / / / / / / / / | 
    -------------------------------+  LIC              (.200) 
                                   | 
                                   | 
    -------------------------------+  HIC              (.300) 
    / / / / /  gap / / / / / / / / | 
    -------------------------------+  Low Bothways     (.400) 
                                   | 
                                   | 
    -------------------------------+  High Bothways    (.500) 
    / / / / /  gap / / / / / / / / | 
    -------------------------------+  LOC              (.600) 
                                   | 
                                   | 
    -------------------------------+  HOC              (.FFF) 
    4095 
In CP-6, the structure can actually look as follows: 
o   LIC = 200 hex 
o   HIC = 500 hex 
o   LOC = 600 hex 
o   HOC > LOC. 
    0 
    -------------------------------+ 
       Permanent VC                | 
    -------------------------------+ LIC    (.200) 
                                   | 
    ...............................+        (.400) \ PSS's Bothways is 
    -------------------------------+ HIC    (.500) / covered here. 
    / / / / /  gap / / / / / / / / | 
    -------------------------------+ LOC    (.600) 
                                   | 
                                   | 
    -------------------------------+ HOC    (.FFF) 
    4095 
Note that the two structures do not match exactly.  In effect, the PSS 
Bothways range is covered by the CP-6 incoming range. 
But this causes no problems.  Because the outgoing range is FFF - 600 hex, 
there will be more than enough growth space for any single FEP.  In effect, 
all the Bothways channels are given to PSS for incoming calls and PSS can 
handle the gap (if it exists) between the incoming and the Bothways range. 
00002
00001
00003
A list of LINK command options and their definitions can be accessed by typing 
a ? or ??.  To access individual options, type:    HELP (SUPER) LINK_OPTS 
option 
where option is:  ADDRESS, DEFAULT, DESTINATION, HIC, HOC, LIC, LOC, MODE 
PROFILE, QOS 
  Option    Description 
  A[DDRESS] = n 
            Specifies the address inserted in the "calling address" field of 
            outgoing call packets.  n is 1-14 decimal digits. 
  DEF[AULT] VIR CIR PRO=pname 
            Specifies the name of an already defined virtual circuit profile. 
            This profile will be used for any circuits that do not have a 
            virtual circuit profile associated with them.  The only way to 
            associate a profile with a virtual circuit is through the 
            CREATE/MODIFY VIRTUAL CIRCUIT command, which is only used for RFEP 
            virtual circuits.  This option provides a way to assign a profile 
            to other outgoing and all incoming virtual circuits. 
  DEST[INATION]=n 
            Specifies the network (X.121) address that this link connects to. 
            n is 1-14 decimal digits. 
  HIC=n 
            Specifies the highest incoming channel (1-4095).  The default is 
            4095. 
  HOC=n 
            Specifies the highest outgoing channel (1-4095).  The default is 
            4095. 
  LIC=n 
            Specifies the lowest incoming channel (1-4095).  The default is 1. 
  LOC=n 
            Specifies the lowest outgoing channel (1-4095).  The default is 1. 
  MODE={DTE|DCE} 
            Determines the command and response addresses for frames, and 
            affects logical channel number assignment and the outcome of a 
            call collision.  If a connection involves a PDN, DTE should be 
            specified.  If no PDN is involved, one end must specify DTE, and 
            the other end must specify DCE.  The default is DTE. 
  PR[OFILE]=pname 
            Specifies a previously defined LINK profile for this link.  If 
            pname is specified, the identified profile must have been defined 
            and must be defined as a LINK profile.  If no profile is 
            specified, the profile defaults to $LINK. 
  QOS=n 
            Specifies the Quality Of Service level requested for the link. 
            These levels are assigned to establish a link quality metric.  n 
            is a value between 2 and 255.  The default is 2. 
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
LINK_OPTIONS
A list of options and their definitions for creating or modifying a LINK 
profile can be accessed by typing a ? or ??.  To access individual options, 
type: 
HELP (SUPER) LINK_PROFILE_OPTS option 
where option is any of the following: 
CALLS, CHARGE_INFORMATION, CIRCUITS, DATA_TIMEOUT, EXTENDED_SEQUENCE, 
FAST_SELECT, FRAME, IDLE_TIMEOUT, MAXIMUM_WINDOW, MODE, RESPONSE_DELAY, 
RESTART_RETRIES, RESTART_TIMEOUT, RETRANSMISSION, REVERSE, TIMEOUT, and 
WINDOW. 
  Option                       Description                           Device 
CA[LLS]={NONE|X25|X29|ALL} 
                            Specifies the usage of a link for      LINK 
                            incoming calls.  NONE indicates 
                            that no incoming calls are allowed. 
                            X25 indicates that all incoming 
                            calls except X29 calls are allowed. 
                            X29 indicates that only X29 calls 
                            are allowed.  ALL is a combination 
                            of X25 and X29.  The default is ALL. 
CHA[RGE] INFO[RMATION][={Y[ES]|N[O]}                               LINK 
                            Specifies whether or not charging 
                            information is to be requested 
                            for incoming calls.  This option 
                            is meaningful only when connected 
                            to a public data network (PDN). 
CIR[CUITS]=value            Specifies a value (1-255) that         LINK 
                            is the maximum number of virtual 
                            circuits that may be operational 
                            at one time on a link.  The default 
                            is 255. 
 
DATA TIME[OUT]=value                                               VIRCIR 
                            Specifies the number of seconds 
                            (0-255) that can elapse before a 
                            packet acknowledgement must be 
                            received for each data packet.  If 
                            this time expires for a data packet, 
                            the circuit is reset and all 
                            unacknowledged data packets will be 
                            retransmitted.  A value of 0 means 
                            there is no timeout value.  The 
                            default is 0. 
EXT[ENDED] SEQ[UENCE]={Y[ES]|N[O]}                                 LINK 
                            If YES is specified, MAXIMUM 
                            WINDOW and RESPONSE DELAY sizes 
                            of up to 127 and FRAME sizes of 
                            2048 and 4096 are legal.  If this 
                            option is set to NO, the maximum 
                            size for MAXIMUM WINDOW and 
                            RESPONSE DELAY is 7 and the 
                            maximum FRAME size is 1024.  The 
                            default is NO. 
FAS[T] SEL[ECT] ACC[EPT]={Y[ES]|N[O]}                              LINK 
                            Specifies whether or not fast select 
                            calls are accepted on this link. 
                            The default is YES. 
FR[AME]={128|256|512|1024}  Specifies the maximum number of        LINK 
                            data bytes that an X.25 information 
                            frame can contain.  The default 
                            is 1024.  2048 and 4096 can only be 
                            specified if the EXT SEQ option is set 
                            to YES. 
IDL[E] TIME[OUT]=value                                             LINK 
                            Specifies a number of seconds 
                            (0-255) to wait before polling 
                            to ensure that the link is 
                            operational.  The default is 4. 
MAX[IMUM] WIN[DOW]=value    Specifies the maximum send window      LINK 
                            (2-7) on incoming calls for circuits 
                            on this link.  When making or 
                            receiving calls, if the send window 
                            size parameter exceeds this value, 
                            this value is used.  The default 
                            is 7. 
MODE={DTE|DCE}              Determines the command and response    LINK 
                            addresses for frames, and affects 
                            logical channel number assignment 
                            and the outcome of a call collision. 
                            If a connection involves a PDN, DTE 
                            should be specified.  If no PDN 
                            is involved, one end must specify 
                            DTE, and the other end must specify 
                            DCE.  The default is DTE. 
RESP[ONSE] DEL[AY]=value    Specifies the number (0-7) of          LINK 
                            unacknowledged information frames 
                            that should be received before an 
                            explicit acknowledgement frame is 
                            generated.  A value of 0 indicates 
                            that explicit acknowledgement 
                            frames should only be generated 
                            in response to received commands 
                            with the poll bit set.  The 
                            default is 1. 
RESTART RETR[IES]=value                                            LINK 
                            Specifies the number of times 
                            (0-99) to send a restart packet if 
                            a restart confirmation was not 
                            received in the number of seconds 
                            specified in RESTART TIMEOUT.  A 
                            disconnect frame procedure is 
                            initiated to take down the link if 
                            the RESTART RETRIES value is 
                            exceeded.  A value of 0 means do 
                            not retry sending the restart 
                            packet.  The default is 1. 
RESTART TIM[EOUT]=value                                            LINK 
          Specifies the number of seconds (0-999) that can 
          elapse before a restart confirmation must be 
          received for each restart packet.  If this time 
          expires for a restart packet, the timer is reset 
          RESTART RETRIES times.  A value of 0 means there 
          is no timeout value.  The default is 0. 
RET[RANSMISSION]=value      Specifies the number of retrans-       LINK 
                            missions (0-255) that should be 
                            done before moving to an alterna- 
                            tive action.  This is CCITT para- 
                            meter N2.  A value of 0 indicates 
                            an infinite number of retransmissions 
                            should be done.  The default is 20. 
REV[ERSE][={Y[ES]|N[O]}]    Specifies whether or not to accept     LINK 
                            incoming calls that specify reverse 
                            charges.  The default is YES. 
TIME[OUT]=value             The time interval in seconds           LINK 
                            (1-255) that should expire after 
                            transmission of a frame before 
                            corrective action should be 
                            taken because a response was 
                            not received.  This is CCITT 
                            parameter T1.  The default is 3. 
WI[NDOW]=value              Specifies the frame transmit window    LINK 
                            size (1-7).  This is CCITT parameter 
                            K.  The default is 7. 
00001
00002
00002
00003
00004
00004
00005
00005
00006
00006
00007
00008
00008
00009
00009
00010
00011
00011
00012
00013
00012
00013
00014
00015
00016
00017
LINK_PROFILE_OPTIONS
Format: 
L[IST] {[.]account, name} 
       {ALL USERS       } 
Parameters: 
account, name    specifies a user account.  The account is limited to 8 
characters, the name to 12.  The valid character set consists of alphanumeric 
characters plus the characters $ and :.  Note that wildcarding is allowed for 
account and name (e.g., L[IST] ?HOST). 
ALL USERS    requests a listing of all accounts in the current project or all 
accounts. 
Description: 
This command displays user logon ids.  If the requestor is a project 
administrator, LIST ALL USERS requests a listing of all user logon ids in the 
current project.  If the requestor is the system manager, LIST ALL USERS 
requests a listing of all user logon ids in the current project, or on the 
system if the current project is the system manager logon id. 
If account,user is specified in the LIST command, the names of all qualifying 
user accounts are listed.  This listing can be useful when wildcarding is used 
to identify accounts.  LIST [.]account,user can also be used to verify the 
existence of a logon id in a project. 
00002
00001
LISTFORM_OPTIONS
A list of LIST FORM display options and their definitions can be accessed by 
typing a ? or ??.  To access individual options, type: 
HELP (SUPER) LISTFORM_OPT option 
where option is any of the following: 
ACCESS, ALIGN, ALL, BANNER, HEADER, PSEUDO, SETUP, or VFU. 
  Option    FORM and FORMSET Record Information Listed 
  AC[CESS] 
            The names of terminals that can use the form. 
  AL[IGN] 
            The settings for the ALIGN, ENTRY, and REPEATS fields. 
  ALL 
            All the record contents. 
  BA[NNER] 
            The settings for the CHARGE, ENTRY, and REPEATS fields. 
  HE[ADER] 
            For line-oriented forms, the settings for the following record 
            fields:  the CHARSET, CHARSET record DEVICES fields, FIRSTLINE, 
            LENGTH, LIMBO, LPI and WIDTH. 
            For graphic forms, the settings for the following record fields: 
            X-, Y-, and Z-SIZE; X-, Y- and Z-OFFSET; CHARSET, the CHARSET 
            record DEVICE fields, and device limit values. 
  PS[EUDO] 
            The names of any pseudos of the form being listed. 
  SE[TUP] 
            The operator setup information message. 
  VF[U] 
            For line-oriented forms, the VFU image. 
00001
00002
00003
00004
00005
00006
00007
00008
LIST
Format: 
L[IST] {[ALL] CHAR[SETS]     } 
       {CHAR[SET] charsetname} 
Parameters: 
charsetname    is the one to eight character name of the CHARSET record to be 
LISTed.  If omitted, all CHARSET records are listed.  The charsetname can be a 
combination of alphabetic characters, numeric characters and the special 
characters: colon (:), dollar sign ($), and asterisk (*), charsetname can be 
wildcarded with the ? character. 
Description: 
The LIST CHARSET command is used to list the name of one or all CHARSET 
records contained in the :FORM file. 
If charsetname is not specified in the LIST CHARSET command, the names of all 
CHARSETS in the :FORM file are listed. 
If charsetname is specified in the LIST CHARSET command, the names of all 
CHARSETS qualifying for the charsetname are listed.  This listing is useful 
when wildcarding is used in charset name or to verify the existence of a 
character set. 
00002
00001
LIST_COMMANDS
See the following topics: 
HELP (SUPER) CONSOLE, CONTROLLER, DEVICE, DEVICE_FOR_LINE, DEVICE_FOR_LINK, 
LINE, LINK, LIST, LIST_CHARSET, LIST_FORM, LIST_PROJECT, LIST_USERS, PROFILE, 
STATION, TERMINAL, VIRTUAL_CIRCUIT, WSN. 
Format: 
L[IST] {[ALL] FORM[S]} 
       {FORM formname} 
Parameters: 
ALL FORMS    requests listing of all forms in the :FORM file. 
formname    is the name of the form to be LISTed.  The formname can be a 
combination of alphabetic characters, numeric characters and the special 
characters:  colon (:), dollar sign ($) and asterisk (*).  The formname can be 
wildcarded with the ? character. 
Description: 
The LIST FORM command is used to list the names of forms. 
If formname is not specified in the LIST FORM command, the names of all forms 
in the :FORM file are listed. 
If formname is specified in the LIST FORM command, the names of all forms 
qualifying for the formname are listed.  This listing is useful when 
wildcarding is used in formname or to verify the existence of a form. 
00002
00001
Format: 
L[IST] {[ALL] FORMSET[S]   } 
       {FORMSET formsetname} 
Parameters: 
ALL FORMSETS    requests display of all base forms in the :FORM file and their 
associated pseudo forms. 
formsetname    is the name of the form to be DISPLAYed.  The formsetname can 
be a combination of alphabetic characters, numeric characters and the 
characters:  colon (:), dollar sign ($) and asterisk (*).  The formsetname can 
be wildcarded with the ? character. 
Description: 
The LIST FORMSET command is used to list the names of all base forms and their 
associated pseudo forms.  If formset name is not specified in the LIST FORMSET 
command, the names of all forms in the :FORM file and their associated pseudo 
forms are listed. 
If formsetname is specified in the LIST FORMSET command, the names of all base 
forms qualifying for the formsetname and the associated pseudo forms are 
listed. 
00002
00001
Format: 
L[IST] {[ALL] PROJ[ECTS]           } 
       {PROJ[ECT] [.]account, name}} 
Parameters: 
ALL PROJECTS    requests listing of all projects in :PROJ. 
account, name    the logon ID for the project administrator of the project(s) 
being listed.  The account is limited to 8 characters; the name to 12.  The 
valid character set consists of the alphanumeric characters plus the 
characters $ and :.  Note that wildcarding is allowed for account and name 
(e.g., LIST PROJ ?HOST, ABC?). 
Description: 
This command will list the logon ids in the project or all projects 
appropriate for the requestor.  If the project id is not specified in the LIST 
PROJECT command, the ids of all projects in the :PROJ file are listed. If a 
logon id is specified, the ids of only those projects associated with the 
logon id are specified.  This latter listing is useful when wildcarding is 
used or to verify the existence of a project. 
00002
00001
LIST
LIST_CHARSET
LIST_FORM
LIST_FORMSETS
LIST_PROJECT
Format: 
MAKE[ME] [{R[ESET]|P[ROJECT]|[.]account, name}] 
Parameters: 
RESET    specifies the running account,name. 
PROJECT    makes a project administrator with the SUPERAUTH privilege a 
project administrator rather than a system manager.  A project administrator 
with the SUPERAUTH privilege is considered a system manager when first 
entering SUPER. 
account, name    specifies the new project.  The account is limited to 8 
characters, the name to 12.  The valid character set consists of the 
alphanumeric characters plus the characters $ and :. 
Description: 
This command associates with the user, attributes and constraints of a project 
that is lower in the project hierarchy. This association permits creation of 
additional sub-projects or user logons.  A system manager or project 
administrator performs this command in order to enter SUPER commands on behalf 
of a subordinate project administrator.  A system manager may issue a MAKEME 
command with any project, but a project administrator may only specify a 
project that is below him in the project hierarchy. 
MAKEME RESET is used if a previous MAKEME command set the running user at a 
lower project level.  The MAKEME RESET command resets the running user to the 
own user's highest level in the project hierarchy. 
MAKEME specified alone displays the project of which the user is currently 
project administrator. 
Example: 
CMD*MAKEME HOST,REICHART 
This command makes the user the project administrator of the project 
HOST,REICHART. 
CMD*MAKEME PROJECT 
This command makes a project administrator with SUPERAUTH a project 
administrator rather than a system manager. 
CMD*MAKEME RESET 
This command re-establishes the user as the system manager at the system level 
or the project administrator, depending on the user's privileges. 
CMD*MAKEME 
Project:  HOST,REICHART 
This command causes SUPER to display the project of which the user is 
currently project administrator. 
00002
00003
00001
A list of miscellaneous profile options and their definitions can be accessed 
by typing a ? or ??.  To access individual options, type: 
HELP (SUPER) MISC_PROFILE_OPTS option 
where option is any of the following: 
BIN, BLANKERASES, CHARSETNAME, DEVSCROLL, DSPHEIGHT, DVCFLWCTRALG, 
DVCOTPBFRSIZ, FF_FLUSH, FF_INCCR, FUNCTION_KEY, HEIGHT, INPUT, 
LOWERCASEPRINTS, MICROFPL, OUTPUT, PARITY, PRINTTYPE, SETUP_CHR, SPCBFRPRT, 
SPEED, TRUOVRPRT, and TTYTYPE. 
  Option                       Description                           Device 
BI[N][={Y[ES]|N[O]|D[C]}]   Indicates whether or not binary        ASYNC 
                            output to this device is legal.        POLLVIP 
                            This does not apply to timesharing     RBTD 
                            terminals.  The default is NO for      URP 
                            ASYNC, POLLVIP, and URP; but DC for 
                            RBTD. 
BLA[NKERASES][=Y[ES]|N[O]|D[C]}] 
                            YES means that a blank (space)         ASYNC 
                            character displayed on the             POLLVIP 
                            terminal in a position occupied        3270 
                            by another character erases the 
                            previous character.  NO means 
                            that the previous character is 
                            unchanged.  The default is YES. 
CH[ARSETNAME]=cname         Specifies the name of the terminal     ASYNC 
                            character set; that is, how the        POLLVIP 
                            characters sent to and received        RBTD 
                            from the terminal are translated       URP 
                            from/into ASCII as follows.  The       3270 
                            defaults are: 
                            cname     Description 
                            -----     ----------- 
                            ASC64     ASYNC 
                            ASC95     POLLVIP, RBTD, URP 
                            blank     3270 
                            cname     Description 
                            -----     ----------- 
                            APLBF     APL bit-paired               ASYNC 
                                      translation.  Lowercase      POLLVIP 
                                      ASCII characters are 
                                      printed as underscored 
                                      uppercase characters. 
                            APLBP     APL bit-paired               ASYNC 
                                      translation.  Lowercase      POLLVIP 
                                      ASCII characters are 
                                      printed as uppercase 
                                      characters on output. 
                            APLTF     APL typewriter-paired        ASYNC 
                                      translation.  Lowercase      POLLVIP 
                                      ASCII characters are 
                                      printed as underscored 
                                      uppercase characters on 
                                      output. 
                            APLTP     APL typewriter-paired        ASYNC 
                                      translation.  Lowercase      POLLVIP 
                                      ASCII characters are 
                                      printed as uppercase 
                                      characters on output. 
          ASC8I       8-bit ASCII.  Like ASCII-95, but          ASYNC 
                      passes 8-bit characters (X'00' through    POLLVIP 
                      X'FF') through on input rather than 
                      stripping the parity bit. 
          ASC8        8-bit ASCII.  Like ASC8I, but             ASYNC 
                      passes 8-bit characters (X'80' through    POLLVIP 
                      X'FF') through unchanged rather than 
                      as "#". 
                            ASC64     ASCII-64 translation         ASYNC 
                                      (the default for ASYNC       POLLVIP 
                                      device).                     URP 
                            ASC64B    ASCII-64 variant             ASYNC 
                                      translation for              POLLVIP 
                                      Teletype Model 35.  This 
                                      table interprets Altmode 
                                      (X'7E', tilde) as escape 
                                      on input. 
                            ASC64C    ASCII-64 variant             ASYNC 
                                      translation for              POLLVIP 
                                      Teletype Model 33, 
                                      Xerox 7015, Hazeltine 
                                      2000, etc.  This table 
                                      exchanges NOT (tilde) 
                                      and OR (vertical line) 
                                      in CP-6 system with right 
                                      bracket and left bracket 
                                      at the terminal.  It also 
                                      interprets Altmode 
                                      (X'7E', tilde) as escape 
                                      on input. 
                            ASC95     ASCII-95 translation (the    ASYNC 
                                      default for RBTD, POLLVIP    POLLVIP 
                                      and URP).                    RBTD 
                                                                   URP 
                            ASC95M    ASCII-95 variant             ASYNC 
                                      translation for CDI1203      POLLVIP 
                                      Miniterms operating in 
                                      STD mode.  Converts the 
                                      character generated by 
                                      the ESC key (without 
                                      CTRL) to an ESC. 
                            EBC[{I|O}] EBCDIC input is             RBTD 
                                      translated to CP-6 
                                      ASCII and ASCII to EBCDIC 
                                      input/output translation. 
                            HIS[{I|O}] Bull (e.g., GCOS MOD400)     RBTD 
                                      EBCDIC to CP-6 ASCII and 
                                      ASCII to EBCDIC input/ 
                                      output translation. 
                            NONE      No translation to or from    RBTD 
                                      CP-6 ASCII will be performed. 
                            XDS[{I|O}] Xerox-extended EBCDIC to     RBTD 
                                      CP-6 ASCII and ASCII to 
                                      EBCDIC input/output 
                                      translation. 
                            SDS7012   CP-6 ASCII operator          RBTD 
                                      console output is 
                                      translated to an 
                                      uppercase EBCDIC 
                                      subset; this should be 
                                      specified for Xerox 
                                      model 7012 operator 
                                      consoles. 
                            3270      For pre-IBM 3276 type        3270 
                                      device (limited 
                                      character set).  Same 
                                      as 3276LIM with differences: 
                            EBCDIC            ASCII 
                            right-paren  <--  right-brace 
                            left-paren   <--  left-brace 
                            pound-sign   <--  accent-grave 
                            pound-sign   <--  backslash 
                            3276EUR     Same as 3276STD except for 3270 
                                        the following differences 
                                        needed by European sites: 
                            EBCDIC                 ASCII 
                            cent-sign        <-->  dollar-sign 
                            solid-bar        <-->  pound-sign 
                            backslash        <-->  ampersand 
                            ampersand        <-->  backslash 
                            pound-sign       <-->  left-bracket 
                            dollar-sign      <-->  exclamation pt. 
                            exclamation pt.  <-->  left-bracket 
                            3276LIM   Same as 3276STD except        3270 
                                      useful for data-entry 
                                      keyboards that doe not have 
                                      all keys, or for others that 
                                      prefer a more obvious EBCDIC- 
                                      ASCII translation at the 
                                      expense of not being able 
                                      to enter or display square 
                                      brackets: 
                            EBCDIC                ASCII 
                            not-sign        <--> tilde 
                            solid-vert-line <--> broken-vert-line 
                            cent-sign       <--> vert arrow 
                            left-paren      <--  left-bracket 
                            right-paren     <--  right-bracket 
                            broken-vert-line --> broken-vert-line 
                                      Note:  not all transla- 
                                      tions hold for both input 
                                      and output.  The arrows 
                                      indicate the direction 
                                      of translation. 
                            3276STD   Standard EBCDIC-ASCII        3270 
                                      translation with all 
                                      characters that can be 
                                      displayed by the 3276 type 
                                      devices.  The following 
                                      translation is used for 
                                      those characters not in 
                                      both sets: 
                            EBCDIC               ASCII 
                            not-sign        <--> vertical-arrow 
                            cent-sign       <--> left-bracket 
                            solid-vert-line <--> right-bracket 
                            field-mark      <--> escape 
DEVS[CROLL][={Y[ES]|N[O]|D[C]}] 
                            YES specifies that the terminal is     ASYNC 
                            self-scrolling and should only be      POLLVIP 
                            specified for CRT devices.  This       3270 
                            means that it rolls old lines off 
                            its screen as new ones are added 
                            at the bottom.  NO means that 
                            lines are overwritten when the 
                            screen is filled or the device is 
                            not a CRT.  The default is NO. 
DSPH[EIGHT] = {value|DC}    Specifies the number (0-254) of        ASYNC 
                            displayable lines on a screen.         POLLVIP 
                            Used only for screen-type 
                            terminals and only if DSPHEIGHT 
                            is less than HEIGHT.  DSPHEIGHT 
                            causes the default scrolling 
                            operation of the terminal to use 
                            the bottom DSPHEIGHT lines 
                            so that direct cursor positioning 
                            can be used.  The remaining 
                            terminal lines function as a 
                            capture buffer.  If 
                            DSPHEIGHT=0, DSPHEIGHT=HEIGHT 
                            is assumed.  The default is 
                            DC.  A value of 255 is the same 
                            as DC. 
DVCFLW[CTRALG]={0|NONE|ENQ[ACK]|1|ETX[ACK]|2|DC1[DC3]|3|D[C]} 
                            Determines flow of data to a           ASYNC 
                            device with an internal output 
                            buffer.  The following values 
                            can be assigned: 
                            Value       Meaning 
                            {0|NONE}    Used as reset value. 
                            {1|ENQACK}  The computer sends ENQ; 
                                        the device responds 
                                        with an ACK. 
                            {2|ETXACK}  The computer sends 
                                        ETX; the device responds 
                                        with an ACK. 
                            {3|DC1DC3}  The device sends a DC1 
                                        to resume output and a 
                                        DC3 to halt output. 
DVCOTPB[FRSIZ]=value        Specifies the size (in bytes) of       ASYNC 
                            the output buffer internal to the      POLLVIP 
                            device.  The range of 0-4096.  The     3270 
                            default is 0. 
FF_FL[USH]=[={Y[ES]|N[O]|D[C]}] 
                            Specifies how to complete the          ASYNC 
                            display of buffered data for           POLLVIP 
                            a device.  YES specifies that 
                            the device needs to have a 
                            form-feed operation performed 
                            to complete the display of 
                            any data still buffered in the 
                            device.  NO specifies that a 
                            new-line operation is 
                            sufficient.  The default is 
                            DC, which means the current 
                            option is not changed. 
FF_IN[CCR][= {YES|NO|DC}]                                          ASYNC 
                           YES specifies that the form-feed        POLLVIP 
                           function for this terminal also posi- 
                           tions to the left margin.  NO 
                           specifies that it positions only 
                           vertically.  The default is DC. 
FUNC[TION_KEY]              Associates labels with function        ASYNC 
                            key character sequences                POLLVIP 
                            transmitted to the CP-6 system 
                            as a result of depressing a 
                            terminal key.  Most commonly, 
                            this option is used to define 
                            labels that will be used by 
                            the IMP processor to customize 
                            key functions that include 
                            multiple character sequences 
                            (see the CP-6 Programmer 
                            Reference, CE40). It can also 
                            be used to define single 
                            character definitions; that is 
                            to change multiple character 
                            sequences to a single 
                            character or change a single 
                            character.  Specifying this 
                            option initiates suboption 
                            mode in which function key 
                            character sequences and their 
                            associated labels are defined, 
                            changed and removed.  The format 
                            of a function key label/character 
                            sequence entry is: 
                            label=[introchar1, [introchar2,] 
                            [mod,]] identifier 
                            label    is one of the function key 
                            names listed in FUNCTION_KEY_LABELS. 
                            The special label IGNORE indicates 
                            that a particular character or 
                            character sequence is to be 
                            ignored when received from the 
                            terminal.  (See Example 1, below.) 
                            introchar    is the first or first 
                            and second (hex) characters in the 
                            sequence. 
                            mod    is one or two decimal 
                            digits (each one, 0 to 9) as 
                            contained in the character 
                            sequence.  As with IMP, a total of 
                            two different intro sequences is 
                            permitted for each profile. 
                            identifier    is the (hex) character 
                            in the sequence that identifies the 
                            function. 
                            Note:  If two function key definitions 
                            are identical except one has no 
                            modifier, SUPER supplies a modifier of 
                            0 for that definition. 
                            A function key entry for a profile 
                            is deleted at the suboption level 
                            by specifying REMOVE label.  All 
                            functions key entries for a profile 
                            can be deleted by specifying REMOVE 
                            ALL. 
                            Examples: 
                            1.  Each function key on a Beehive 
                            DM20 terminal generates the 
                            following character sequence: 
                            STX,ESC,'char',ETX 
                            char is a single character that 
                            varies from key to key.  The 
                            following needs to be specified 
                            to define the F1 label: 
                            IGNORE=ETX 
                            F1=STX,ESC,'char' 
                            (The special label IGNORE is 
                            used because the identifier 
                            (char) is not the last 
                            character of the sequence.) 
                            2.  The F20 function key on a DEC 
                            VT200 terminal generates the 
                            following character sequence: 
                            ESC,'[',3,4,'~' 
                            The following needs to be specified 
                            to define the F20 label: 
                            F20=ESC,'[',34,'~' 
                            F19 on a DEC VT200 generates the 
                            following character sequence: 
                            ESC,'[',3,3,'~' 
                            If F20 is defined, F19 does not 
                            have to be defined because 
                            the mod value for F19 is 33 
                            and for F20 is 34 (and there 
                            is the following numeric 
                            descending relationships: 
                            the labels are 20 and 19 and 
                            the modifiers are 34 and 33). 
                            Other function keys with 
                            corresponding relationships 
                            also need not be defined.  When 
                            defining a sequence with numeric 
                            values for the mod portion of 
                            the character sequence, only 
                            the last number in the sequence 
                            needs to be defined.  When the 
                            sequence is the same except for 
                            the mod portion of the character 
                            sequence, other key functions 
                            with mod values in strict 
                            descending numeric sequence 
                            are defined automatically. 
                            The program WOCKY in the X 
                            account can be used to display 
                            the character sequence trans- 
                            mitted to the CP-6 system when 
                            a function key is depressed on 
                            a terminal. 
HE[IGHT]={value|DC}         Indicates the number of lines          ASYNC 
                            (0-999) on the screen of a screen-     POLLVIP 
                            type terminal.  Height is 0 for        3270 
                            non-screen-type terminals.  The 
                            default is zero.  HEIGHT=0 
                            implies no overstriking.  A value 
                            of 255 is the same as DC. 
INPUT[={Y[ES]|N[O]|D[C]}]   Specifies whether or not the           ASYNC 
                            terminal or device is capable of       POLLVIP 
                            transmitting input.  The default       RBTD 
                            is YES for ASYNC, URP, and 3270,       URP 
                            but NO for RBTD.                       3270 
LOWERCASEP[RINTS][={Y[ES]|N[O]|D[C]}] 
                            YES indicates that the terminal        ASYNC 
                            or device is capable of printing       POLLVIP 
                            (displaying) lowercase letters.        RBT 
                            NO indicates that the terminal         URP 
                            cannot print lowercase letters         3270 
                            and is the default. 
MIC[ROFPL][={Y[ES]|N[O]|DC}                                        ASYNC 
                            Specifies whether or not FPL 
                            programs run by a user will be 
                            executed on the user's microcomputer 
                            instead of being downloaded into the 
                            CP-6 FEP through which the user's 
                            connection is established.  This 
                            option is only available to users of 
                            IBM PC/XT/AT (and compatible micro- 
                            computers running the CP-6 PC Terminal 
                            Facility (PCT) emulator program.  For 
                            more information, refer to the CP-6 
                            Forms Processing Language (FPL) 
                            Reference Manual (CE51) and the PC 
                            Terminal Facility Reference Manual 
                            (HA15).  The default is NO. 
OUTPUT[={Y[ES]|N[O]|D[C]}]  Specifies whether or not the           ASYNC 
                            terminal is capable of receiving       POLLVIP 
                            output.  The default is YES for        RBTD 
                            ASYNC, URP, and 3270, but NO for       URP 
                            RBTD.                                  3270 
PARITY={NONE|ODD|EVEN|ONE|ZERO|D[C]} 
                            Specifies the type of character        ASYNC 
                            parity at the terminal.  Parity        POLLVIP 
                            is checked on input if 
                            PARITYCHECK=YES, PARITY=NONE is 
                            not specified, and the associated 
                            M$READ does not specify 
                            transparent input.  Parity is 
                            generated on output if PARITY=NONE 
                            is not specified and the 
                            associated M$WRITE does not 
                            specify transparent output.  The 
                            type of parity may be set to ODD 
                            (odd parity), EVEN (even parity), 
                            ZERO (parity bit always reset), 
                            or ONE (parity bit always set). 
                            The default is DC. 
PRINTT[YPE][={Y[ES]|N[O]|D[C]}] 
                            YES specifies that the terminal        ASYNC 
                            prints on a form or screen such        POLLVIP 
                            that vertical positioning is           RBTD 
                            sensible.  NO specifies that the       URP 
                            terminal produces records only         3270 
                            and vertical positioning is 
                            meaningless.  The default is YES for 
                            ASYNC, URP, and 3270, but NO for RBTD. 
SETUP[_CHR]=hex_list        Specifies the character string to      ASYNC 
                            be sent transparently to the           POLLVIP 
                            device whenever this profile is 
                            invoked. 
SPC[BFRPRT][={Y[ES]|N[O]|D[C]}] 
                            If SPCBFRPRT=NO then any VFC will      RBTD 
                            be translated such that all paper 
                            motion will follow print (e.g., 
                            space 4 and print VFCs will be 
                            translated into write a blank 
                            line and space 4 followed by 
                            write the read data and do not 
                            space).  When SPCBFRPRT=NO, 
                            functionality is identical to 
                            SRCB=X on CP-V.  If SPCBFRPRT=YES, 
                            then no special VFC translation 
                            is done.  SPCBFRPRT=YES is the 
                            CP-V equivalent of SRCB=P.  The 
                            default is DC. 
SPE[ED]={50|75|110|134.5|150|200|300|600|1050|1200|1800|2000| 
         2400|4800|9600|19200|D[C]} 
                            Indicates the actual line speed        ASYNC 
                            of the terminal.  The default is 
                            DC. 
TRUO[VRPRT][={Y[ES]|N[O]|D[C]}] 
                            YES specifies that the terminal        ASYNC 
                            performs overprinting.  NO             POLLVIP 
                            specifies that the terminal is         RBTD 
                            not capable of overprinting.  The      URP 
                            default is YES for ASYNC and 3270,     3270 
                            NO for RBTD, and DC for URP. 
                            Currently, used only by the APL 
                            processor to determine whether a 
                            terminal can backspace and overprint 
                            in response to a backspace character. 
TT[YTYPE][={Y[ES]|N[O]|D[C]}] 
                            YES specifies that the terminal        ASYNC 
                            is capable of displaying what it       POLLVIP 
                            transmits.  YES is usually             RBTD 
                            specified for a device such as a       3270 
                            keyboard printer or a CRT.  NO 
                            specifies that input is not 
                            displayed.  The default is YES for 
                            ASYNC, POLLVIP and 3270, but NO for 
                            RBTD. 
00001
00002
00003
00004
00005
00006
00007
00009
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
MISC_PROFILE_OPTIONS
Format: 
M[ODIFY] [.]account1, name1 [FROM {[.]account2, name2}] 
                            [     {DEFAULT           }] 
Parameters: 
account1, name1    is the logon ID.  This combination must be entered to gain 
access to the CP-6 system.  The account is limited to 8 characters, the name 
to 12.  The valid character set consists of alphanumeric characters plus the 
characters $ and :.  Note that wildcarding is allowed for account1 and name1 
(e.g., M[ODIFY] ?HOST, 102?). 
account2, name2    indicates that each item not explicitly specified at the 
option level is to be set to the value of the corresponding item of the 
authorization record identified by this logon ID. 
DEFAULT    indicates that each item not explicitly specified at the option 
level is to be set to the value of the corresponding item of the default user 
authorization record. 
Description: 
This command alters an existing user authorization.  The options which may be 
altered can be accessed by typing HELP (SUPER) USER_OPTS. 
00002
00001
CREATE_CHARSET
MODIFY_COMMANDS
See the following topics: 
HELP (SUPER) CONSOLE, CONTROLLER, DEVICE, DEVICE_FOR_LINE, DEVICE_FOR_LINK, 
LINE, LINK, MODIFY, MODIFY_CHARSET, MODIFY_FORM, MODIFY_FORM_GRAPHICS, 
MODIFY_PROJECT, MODIFY_PSEUDO, MODIFY_USER, PROFILE, TERMINAL, 
VIRTUAL_CIRCUIT, WSN. 
CREATE_FORM
CREATE_FORM_GRAPHICS
Format: 
Form 1: 
M[ODIFY] PROJ[ECT] [.]account1, name1 [FROM [.]account2, name2] 
Form 2: 
M[ODIFY] [.]account3, name3 TO PROJ[ECT] [FA[CCOUNT] [=facctlist]] 
Form 3: 
M[ODIFY] PROJ[ECT] [.]account1, name1 TO USER 
Parameters: 
account1, name1    is the logon ID for the project administrator of the 
project being modified.  The account is limited to 8 characters, the name to 
12.  The valid character set consist of the alphanumeric characters plus the 
characters $ and :. 
FROM account2, name2    indicates that each item not explicitly specified at 
the option level is to be set to the value of the corresponding item in the 
project authorization record identified by this logon ID. 
account3, name3    identifies a user logon. 
facctlist    is a list of file management accounts, of the form 
[[DP]#psn.]acct, that are associated with the user and are to be included in 
the project.  If FACCOUNT is specified, but a list of accounts is not given, 
SUPER assumes the account is the specified account on the home packset. 
Description: 
The first form of the command invokes the project authorization mode of SUPER 
and allows modification of options for an existing project.  Wildcarding is 
allowed in this form of the MODIFY PROJECT command. 
If wildcarding is used, all projects (users and administrators) and all other 
logon users meeting the wildcard criteria qualify for change.  The command 
sequence: 
    MAKEME HOST,REICHART 
    MODIFY ?,? 
qualifies for modification all logon users and all project users and project 
administrators within the project HOST,REICHART. 
The second form of the command modifies a logon user to be a project and 
invokes the project authorization mode of SUPER.  Options that may be altered 
in this mode are available by typing HELP (SUPER) PROJECT_OPTS. 
The third form of the command modifies a project to be a user and invokes the 
user authorization mode of SUPER.  Options that may be altered in this mode 
are available by typing HELP (SUPER) PROJECT_OPTS. 
00002
00001
CREATE_PSEUDO
MODIFY
CREATE_CHARSET
CREATE_FORM
CREATE_FORM_GRAPHICS
MODIFY_PROJECT
CREATE_PSEUDO
Input symbiont devices are divided into two classes, control and non-control 
(NCTL).  A device is defined as a NCTL device via the SUPER DEVICE command 
option NCTL.  Non-control devices may only submit non-control files (NCTL 
files); that is, they may not submit !JOB-type job streams.  All control 
devices may submit control files (beginning with !JOB).  For control devices, 
the DEVICE command NCOK option indicates whether (YES) or not (NO) it is legal 
to submit NCTL files as well. 
The NCTL device must: 
o   Get INSYM's attention by issuing a "break" (i.e., an ESC-B, ESC-ALT-B, or 
    BREAK) before the first record of a file can be transmitted. 
o   Ignore the default comgroup device prompt (!). 
A non-control file is terminated by an appropriate end-of-file indicator from 
the device.  One means of supplying this end-of-file is to transmit an ESC-F. 
Another is a record containing '!FIN ' as the first five characters.  Note 
that "FIN" must be followed by a blank.  Such a record is referred to as a 
"FIN card." 
A non-control file may be started by a record containing '!NCTL ' as the first 
six characters.  Such a record is referred to as an "NCTL card."  In the case 
of NCTL devices, this card is optional.  For control devices, an NCTL file 
must begin with an NCTL card, since this distinguishes the file from a control 
file (signalled by !JOB). 
Within an NCTL file, ANY card (including !JOB and !NCTL) except the FIN card 
is considered part of the file.  Thus an NCTL file containing many !JOB cards 
may be submitted as a single non-control stream. 
NCTL files have two possible types of destinations:  disk files and symbiont 
output.  Examples of these two types are 'filename.account' and 'device@wsn'. 
The specifications and options pertinent to these two types will be discussed 
separately. 
For disk files, only CONSECUTIVE files are permitted.  If the named 
consecutive file exists, then the NCTL stream is appended to the end of the 
existing file.  Otherwise a new file is created.  For a given NCTL file 
destined for disk, two pieces of information are required, the filename and 
the account. 
First, each device possesses an intrinsic NCTL account (see the NACCT option 
above).  This account is used for the account of the destination disk file if 
one is not specified.  Next, for each NCTL stream, a fid is supplied.  This 
may originate from the NCTL card of the stream itself, i.e., "!NCTL fid" or 
from the device's intrinsic NCTL fid.  This latter fid is established by the 
NCFID option (see above) and may be changed by the NCTL keyin (see the CP-6 
Operations Reference Manual, CE34) from an operator console.  If the NCTL card 
bears a fid then this overrides that specified by the NCTL keyin, otherwise 
the keyin fid is used.  In either case, the fid may take the form "filename" 
in which case the implicit account is the NCTL account of the device, or the 
form "filename.acct" in which case the destination account is "acct".  In this 
latter case, the device's NCTL account (default :NCTL) MUST be authorized for 
write/create access to "filename.acct".  A ? may be specified at the end of 
the fid.  The ? will be replaced by an 11-digit decimal UTS value.  The length 
of the filename (including the trailing ?) must not exceed 21 characters or 
the substitution will not be performed and the NCTL M$OPEN will fail.  Note: 
A file created by the NCTL card has an expiration date equal to the creation 
date, i.e., it never expires. 
For streams destined as symbiont output, again a fid is required, and is 
obtained from the NCTL card, or the device's intrinsic fid in the same way as 
for disk files.  The fid may take the form "dev@[(form)]" or 
"dev@wsn[(form)]".  In the former case the destination is dev@dwsn where dwsn 
is the wsn associated with the device's TERMINAL or STATION.  In the latter 
case the destination is dev@wsn.  In either case (form) is optional and causes 
the specified form to be associated with the output. 
NCTL_DEVICES
A list of operational profile options and their definitions can be accessed by 
typing a ? or ??.  To access individual options, type: 
HELP (SUPER) OPERATIONAL_PROFILE_OPTS option 
where option is any of the following: 
ABSGRPRND, ACTONTRN, APLLCNRM, AUTOCURSOR, AUTOTABCLM, CURSORREAD, DISPINPUT, 
EDITOVR, FCNTBL, FIRSTLINE, FRMFED_CHR, FULLDUXPAPERTAPE, HALFDUXPAPERTAPE, 
HPA_ALG, HSCROLL, KEEPTYPAHD, LENGTH, LIMBO, LOCALECHO, LOWERCASE, MSGHALT, 
MSGLINE, NOOPTMIZ, OUTPUTDISCARD, PAGEHALT, PARITYCHECK, PARKCURSOR, 
PRINTHALT, PWIDTH, RELPAGE, RETYPOVR, SCROLL, SENDBKSPACE, SIMPERF, SINPUTSZ, 
SPACEINSERT, TABRELATIVE, TABS, TABSIM, TRUNCATE, UPPERCASE, WORDWRAPCLM, and 
WRAPPAGE. 
  Option                       Description                           Device 
{A[BSGRPRND]_EM[PHASIS]}    Defines the graphic rendition          ASYNC 
{A[BSGRPRND]_ER[ROR]   }    (visual attributes) for this           POLLVIP 
{A[BSGRPRND]_H[IDDEN]  }    device.  List represents one or        3270 
{A[BSGRPRND]_I[NPUT]   }    more of the following: 
{A[BSGRPRND]_N[ULL]    } 
{A[BSGRPRND]_O[UTPUT]  }      INCINT - Increased intensity 
{A[BSGRPRND]_W[ARNING] }      HDN    - Hidden 
                              DCRINT - Decreased intensity 
  = list                      UNDSCR - Underscore 
                              SLWBLN - Slow blink 
                              FSTBLN - Fast blink 
                              RVRVID - Reverse video 
                              NONE 
                            For 3270 the only list items 
                            that may be specified are HDN, 
                            DCRINT, and INCINT; for time- 
                            sharing mode only the options 
                            A_INPUT and A_OUTPUT are 
                            applicable. 
AC[TONTRN][={Y[ES]|N[O]|D[C]}] 
                            YES specifies that the activation      ASYNC 
                            characters (EOM) are to apply to       POLLVIP 
                            transparent reads to the terminal. 
                            NO specifies that activation on 
                            byte count will be performed. 
                            The default is NO. 
APLL[CNRM][={Y[ES]|N[O]|D[C]}] 
                            YES specifies that if lowercase        ASYNC 
                            characters are sent to the             POLLVIP 
                            terminal while it is in APL mode, 
                            they are printed as uppercase. 
                            NO specifies that they are to 
                            be uppercase underscored.  The 
                            default is YES 
AUTOC[URSOR][= {YES|NO|DC}]                                        ASYNC 
                            YES specifies that the cursor is to    POLLVIP 
                            move automatically from a non-reading  3270 
                            session when a read starts and is not 
                            completed by type-ahead.  The cursor 
                            is moved to the newly reading 
                            session.  NO specifies that the 
                            cursor is to be moved only via the 
                            keyboard or M$TRMPRG with 
                            CURSORHERE=YES.  The default is DC. 
AUTOT[ABCLM]={value|D[C]}   Specifies the initial cursor           ASYNC 
                            position (0-254) to use when a         POLLVIP 
                            read a new record request occurs.      3270 
                            A value of 0 to 1 specifies that 
                            the input data is to begin 
                            immediately after the prompt. 
CURSORR[EAD][= {Y[ES]|N[O]|D[C]}]                                  ASYNC 
                            YES specifies that the "change         POLLVIP 
                            sessions" input function (usually      3270 
                            <ESC> <.>) is to access only 
                            sessions for which a read is 
                            pending.  If NO is specified, or 
                            if there are no reading sessions, 
                            all sessions are accessible.  The 
                            default is DC. 
DI[SPINPUT][={Y[ES]|N[O]|D[C]}] 
                            Specifies whether or not the           ASYNC 
                            system is to display input             POLLVIP 
                            characters on the terminal.  The       3270 
                            default is YES. 
EDI[TOVR][={Y[ES]|N[O]|D[C}}] 
                            For CRT devices, YES specifies         ASYNC 
                            that visual fidelity is to be          POLLVIP 
                            maintained while using input           3270 
                            editing to insert or delete char- 
                            acters.  Visual fidelity means 
                            the image on the screen matches 
                            the input record.  NO specifies 
                            that upspacing and backslashes 
                            will be displayed to indicate 
                            character insertions and deletions. 
                            The default is NO.  For ASYNC 
                            DEVICES do not specify YES unless 
                            all of the following is true: 
                                BLANKERASES = YES 
                                CUU or CUP was specified 
                                CUB or CUP was specified 
                                CUF or CUP was specified 
                                CUD or CUP was specified 
                            For hardcopy devices, YES specifies 
                            that character-delete input opera- 
                            tions (e.g., depressing the DEL 
                            key) should overstrike the deleted 
                            character with a \ (backslash). 
                            NO specifies that the \ should 
                            be displayed. 
FC[NTBL]={CP5|CP5S1|CP5S2|FRM1|SE1|SE2|NO|NONE} 
                            Specifies the name of a table          ASYNC 
                            that tells the terminal handler        POLLVIP 
                            how to interpret control 
                            functions.  CP5 identifies the 
                            full input function table and is 
                            the default.  CP5S1 and CP5S2 
                            identify subset tables.  FRM1 
                            identifies forms functions. 
                            SE1 identifies screen editor 
                            read/write functions.  SE2 identifies 
                            screen editor read-only functions.  A 
                            value of NONE specifies do not change 
                            the current setting, and is the default. 
                            NO 
                            Escape       Special      Numeric 
                            Characters   Characters   Escapes 
                            None         None         None 
                            CP5 
                            Escape              Special      Numeric 
                            Characters          Characters   Escapes 
                            CR     A-Y          BS     EM    HT   M 
                            DC2    $            CAN    ETB   C    R-T 
                            DC4    '            CR     FF    D    ^ (caret) 
                            DEL    (            DC1    HT    H    . 
                            EOT    )            DC2    LF    I 
                            ESC    -            DC3    NAK 
                            ETB    ^ (caret)    DEL 
                            HT     * 
                            LF     : 
                            SOH    < 
                            STX    > 
                            VT     . 
                            CP5S1 
                            Escape              Special      Numeric 
                            Characters          Characters   Escapes 
                            CR     D-O          BS     EM    HT   M 
                            DC2    Q-R          CAN    ETB   C    R-T 
                            DC4    U-Y          CR     FF    D    ^ (caret) 
                            DEL    $            DC2    HT    H    . 
                            EOT    '            DEL    LF    I 
                            ESC    - 
                            ETB    ^ (caret) 
                            HT     * 
                            LF     : 
                            SOH    < 
                            STX    > 
                            VT     . 
                            A-B 
                            CP5S2 
                            Escape              Special      Numeric 
                            Characters          Characters   Escapes 
                            CR     N            BS     ETB   HT  R-T 
                            DC2    Q            CAN    FF    C   ^ (caret) 
                            DC4    R            CR     HT    D   . 
                            DEL    V            DC2    LF    I 
                            EOT    X            DEL 
                            ETB    ' 
                            HT     ^ (caret) 
                            LF     * 
                            VT     : 
                            D      < 
                            F      > 
                            G      . 
                            I-K 
                            FRM1 
                            Escape        Special      Numeric 
                            Characters    Characters   Escapes 
                            CR     R      BS     EM    I 
                            DC2    U      CAN    ETB   R 
                            DEL    V      CR     HT    S 
                            EOT    X      DC2    LF    T 
                            ESC    Y      DEL    NAK   . 
                            ETB    i 
                            LF     ' 
                            STX    ( 
                            VT     ) 
                            A      - 
                            B      * 
                            D      : 
                            G-K    < 
                            M-O    > 
                            Q      . 
                            SE1 
                            Escape              Special      Numeric 
                            Characters          Characters   Escapes 
                            BS     V            BS     EM    HT   M 
                            CR     X            CAN    ETB   LF   P 
                            DC2    Y            CR     HT    A-E  R-T 
                            DEL    '            DC2    LF    H    ^ (caret) 
                            EOT    (            DEL          I    . 
                            ESC    ) 
                            FF     ^ (caret) 
                            HT     - 
                            STX    * 
                            VT     : 
                            A-D    < 
                            G-K    > 
                            M-R    . 
                            U 
                            SE2 
                            Escape              Numeric 
                            Characters          Escapes 
                            STX    A-D          HT   R-T 
                            DC2    G-J          A-E  ^ (caret) 
                            HT     N,Q,R        H    . 
                            CR     V            I 
                            ESC    Y            M 
                            <      > 
                            -      * 
                            .      ^ (caret) 
FI[RSTLINE]={value|DC}      Specifies the height (0-333) of the    ASYNC 
                            area which is to be left blank         POLLVIP 
                            between the beginning of the page or   RBTD 
                            screen and the first legal print       URP 
                            line.  It can also be considered       3270 
                            as the number of the first legal 
                            print line.  For URP device, 
                            FIRSTLINE must be 0 or 255.  The 
                            default is zero.  A value of 255 
                            is the same as DC. 
FRMFED[_CHR][={Y[ES]|N[O]}]                                        3270 
                            Specifies whether or not the FF 
                            character will cause a printer page 
                            eject.  The default is NO. 
FU[LLDUXPAPERTAPE][={Y[ES]|N[O]|D[C]}] 
                            YES specifies that terminal input      ASYNC 
                            is handled via the following 
                            paper tape conventions: 
                            1.  If DISPINPUT=YES, DC3 
                                (X-OFF) and DC1 (X-ON) 
                                characters are sent to the 
                                terminal so that the input 
                                does not overflow available 
                                buffering space. 
                            2.  A DEL character on input is 
                                ignored. 
                            3.  An LF character received as 
                                the first character of an 
                                input message is ignored 
                                when M$READ is using the 
                                default activation character 
                                set. 
                            NO specifies normal processing 
                            of terminal input. 
HA[LFDUXPAPERTAPE][={Y[ES]|N[O]|D[C]}] 
                            YES specifies that full duplex        ASYNC 
                            paper tape conventions are to 
                            be followed and that absolutely 
                            no characters are to be sent to 
                            the terminal for either input 
                            or echoing.  NO specifies normal 
                            processing of terminal input and 
                            is the default. 
HPA_ALG={O|ANS|CHA|DBL|NEC} Establishes the horizontal position   ASYNC 
                            absolute (HPA) algorithm as follows:  POLLVIP 
                            0   - Used as a reset value.  This 
                                  is also the default. 
                            ANS - Specifies the ANS X3.64 HPA. 
                            CHA - Specifies the ANS X3.64 CHA. 
                            DBL - Specifies a Diablo 
                            1620-compatible algorithm. 
                            NEC - Specifies a NEC 
                            5520-compatible algorithm. 
HSCR[OLL][={Y[ES]|N[O]|D[C]}] 
                            Specifies whether horizontal          ASYNC 
                            scrolling mode is to be enabled. 
                            The default is DC. 
KEEP[TYPAHD][= {Y[ES]|N[O]|D[C]}]                                  ASYNC 
                            YES specifies that a session change    POLLVIP 
                            as a result of the AUTOCURSOR          3270 
                            parameter is to move any type-ahead 
                            from the old session to the new one 
                            for use as input to the new session. 
                            NO specifies that the type-ahead is 
                            to remain with the previous session. 
                            The default is DC. 
LE[NGTH]={value|D[C]}       Specifies the number of printable      ASYNC 
                            lines on the page (0-555).  A          POLLVIP 
                            value of zero specifies that the       RBTD 
                            form is to be treated as one           URP 
                            continuous page.  The default is       3270 
                            zero for ASYNC, POLLVIP, RBTD, and 
                            3270, but 66 for URP.  A value of 
                            255 is the same as DC. 
LI[MBO]={value=D[C]}        Specifies the number of lines (0-444)  ASYNC 
                            to be left blank between the last      POLLVIP 
                            legal print line and the bottom        RBTD 
                            of the page or screen.  For a          URP 
                            URP device, LIMBO must be 0 or         3270 
                            255.  The default is zero.  A 
                            value of 255 is the same as DC. 
LOCALECHO[={Y[ES]|N[O]|D[C]}] 
                            YES indicates that any characters      ASYNC 
                            received by the CP-6 system from       POLLVIP 
                            this terminal have already been 
                            displayed on the terminal.  This 
                            option is especially useful for 
                            very slow connections (such as a 
                            packet network) where the normal 
                            CP-6 echo mechanism becomes 
                            distracting.  NO specifies normal 
                            processing.  The default is DC. 
LOWERCASE[={Y[ES]|N[O]|D[C}}] 
                            Specifies whether or not to send       ASYNC 
                            uppercase alphabetic characters        POLLVIP 
                            input from the terminal to the         3270 
                            user program as lowercase letters. 
                            In addition, these translations 
                            are made: 
                                [     to  { 
                                \     to  | 
                                ]     to  } 
                                tilde to  ^ 
                            NO specifies normal processing of 
                            the above terminal characters and 
                            is the default. 
MSGH[ALT][={Y[ES]|N[O]|D[C]} 
                            Specifies whether output is to be      ASYNC 
                            halted after displaying an             POLLVIP 
                            operator message until the 
                            user enters the customary 
                            continuation response.  The 
                            default is DC. 
MSGLINE[={Y[ES]|N[O]|D[C]}] 
                            Specifies whether operator messages    ASYNC 
                            will be displayed on the message       POLLVIP 
                            line.  This option is meaningful 
                            only if both MSGLIN_CHR and 
                            ENDMSGLIN_CHR have been specified. 
                            The default is DC. 
NOO[PTMIZ][={Y[ES]|N[O]|D[C}}] 
                            YES specifies that carriage            ASYNC 
                            positioning optimization is not to     POLLVIP 
                            be done.  This option is useful 
                            when writing to minicomputers and 
                            paper tape punches.  NO specifies 
                            that data is to be written as 
                            efficiently as possible.  The 
                            default is DC. 
OUTPUTD[ISCARD][={Y[ES]|N[O]|D[C]}] 
                            YES specifies that output is not       ASYNC 
                            sent to the terminal.  NO              POLLVIP 
                            specifies normal processing of         3270 
                            output.  Issuing an M$READ monitor 
                            service request that is not 
                            satisfied by type-ahead resets 
                            OUTPUTDISCARD. 
PAG[EHALT][={Y[ES]|N[O]|D[C]}] 
                            YES specifies that when the end        ASYNC 
                            of a page is reached, output is        POLLVIP 
                            halted until the user types a          3270 
                            carriage return.  NO specifies 
                            that output continues in this 
                            situation.  The default is NO for 
                            ASYNC; but YES for POLLVIP and 3270. 
                            For 3270, it is recommended that 
                            this option be used for 
                            timesharing.  It is difficult to 
                            type any input (PA or PF) when 
                            data is being sent to the device; 
                            PAGEHALT provides convenient 
                            breakpoints.  Use of this option 
                            together with PRINTHALT is 
                            especially helpful when using the 
                            pagewrap scrolling technique since 
                            the screen is never cleared and a 
                            new attribute character is never 
                            inserted. 
PARITYC[HECK][={Y[ES]|N[O]D[C]}] 
                            Specifies whether or not               ASYNC 
                            characters input from the terminal     POLLVIP 
                            are to be checked for proper 
                            parity.  If YES is specified, a 
                            character with bad parity is 
                            echoed as a bell and pound 
                            sign (#).  A parity error code is 
                            reported on the M$READ monitor 
                            service.  The default is DC. 
PARK[CURSOR][= {YES|NO|DC}]                                        ASYNC 
                            YES specifies, for video display       POLLVIP 
                            terminals, that the cursor is to be    3270 
                            moved to the window's home position 
                            when activation occurs in forms or 
                            screen-editing mode.  NO specifies 
                            that the cursor is not moved in 
                            those situations.  The default is DC. 
PRINTH[ALT][={Y[ES]|N[O]|D[C]}] 
                            YES specifies that if the terminal     ASYNC 
                            is being halted at the end of each     POLLVIP 
                            page of output, a message (CR TO       3270 
                            GO or ENTER TO GO) is to be printed 
                            to prompt the user to continue the 
                            output.  NO specifies that the 
                            message will not be printed.  The 
                            default is NO for ASYNC; but YES 
                            for POLLVIP and 3270. 
                            For 3270, it is recommended that 
                            this option be used for timesharing. 
                            It is difficult to type any input 
                            (PA or PF) when data is being sent 
                            to the device.  PRINTHALT is useful 
                            because it is desirable to 
                            maintain a protected attribute 
                            character on the screen at all 
                            times.  PRINTHALT effectively 
                            pre-empts the last line to 
                            provide a place for the 
                            attribute character.  Use of 
                            this option together with 
                            PAGEHALT is especially helpful 
                            when using the pagewrap scrolling 
                            technique since the screen is 
                            never cleared and a new attribute 
                            character is never inserted. 
PW[IDTH]={value|D[C]}       Specifies the platen width, which is   ASYNC 
                            the number of characters (0-508) to    POLLVIP 
                            be written per line.  PWIDTH may be    RBTD 
                            less than or equal to AWIDTH.          URP 
                            PWIDTH determines where folding of     3270 
                            the print image occurs.  (The 
                            platen is the backing against 
                            which the printing mechanism 
                            strikes to produce an impression.) 
                            (See the AWIDTH option under 
                            CURSOR_PROFILE_OPTIONS.)  The 
                            default is 80 for ASYNC, POLLVIP, 
                            RBTD and 3270, but 132 for URP. 
RELP[AGE][={Y[ES]|N[O]|D[C]}] 
                            YES specifies that if the terminal     ASYNC 
                            is being halted at the end of each     POLLVIP 
                            page of output, that the page 
                            boundary will be relative to the 
                            last read that halted the 
                            terminal.  The default is NO. 
RETY[POVR][={Y[ES]|N[O]|D[C]}] 
                            YES specifies that retypes are to      ASYNC 
                            overprint the line being retyped.      POLLVIP 
                            YES should always be specified for     3270 
                            3270 keyboard display devices.  NO 
                            specifies that they are to be 
                            printed on the next line.  The 
                            default is NO for ASYNC; but YES 
                            for POLLVIP and 3270. 
SC[ROLL][={Y[ES]|N[O]|D[C]}] 
                            YES specifies that the terminal is     ASYNC 
                            to be scrolled; that is, treated       POLLVIP 
                            as though the media is a 
                            continuous form.  NO specifies 
                            that when a page is filled, a 
                            screen erase is sent and a new 
                            page started.  NO should always be 
                            specified for IBM 3270 type 
                            display devices. 
SE[NDBKSPACE][={Y[ES]|N[O]|D[C}}] 
                            YES specifies that when the user       ASYNC 
                            backspaces over a character and 
                            overstrikes it, the original 
                            character -- a backspace -- and 
                            the overstriking character are 
                            returned to the program.  NO 
                            specifies that, in this situation, 
                            only the overstriking character 
                            is sent.  The default is NO. 
SIM[PERF][={Y[ES]|N[O]|D[C]}] 
                            YES specifies that underscores         ASYNC 
                            should be printed where the            POLLVIP 
                            perforation would normally occur       3270 
                            on the terminal form.  This 
                            option gives the appearance of 
                            perforated forms on terminals 
                            with continuous form paper. 
SIN[PUTSZ]={value|D[C]}     Specifies the minimum length of        ASYNC 
                            lines typed (0-255) which are to be    POLLVIP 
                            remembered by the system for reuse.    3270 
                            Zero specifies that all lines are 
                            saved.  A value of 255 is the same 
                            as DC.  The default is DC. 
SPA[CEINSERT][={Y[ES]|N[O]|D[C]}] 
                            YES specifies that horizontal tab      ASYNC 
                            characters input from the terminal     POLLVIP 
                            are to be replaced by an               URP 
                            appropriate number of blanks based     3270 
                            on user input tab stop settings. 
                            NO specifies that horizontal tab 
                            characters are to be placed in the 
                            buffer unchanged.  The default is 
                            YES. 
TABR[ELATIVE][={Y[ES]|N[O]|D[C]}] 
                            YES specifies that on input and        ASYNC 
                            input echoing, user tab stops          POLLVIP 
                            are relative to the column where       3270 
                            input was prompted.  NO specifies 
                            that user tab stops are relative 
                            to column 1.  The default is DC. 
TABS=value[, value] ...     Specifies the column positions         ASYNC 
                            where device tab stops are to          POLLVIP 
                            be placed.  The default is zero        3270 
                            (not currently implemented). 
TABSI[M][={Y[ES]|N[O]|D[C]}] 
                            Specifies positioning of              ASYNC 
                            horizontal tabs.  YES positions        RBTD 
                            cursor to the next logical output      URP 
                            tab stop.  If tab stops are not 
                            set, each tab character is 
                            replaced by a single blank.  NO 
                            specifies that horizontal tab 
                            characters are sent to the 
                            terminal unchanged.  The default 
                            is YES. 
Type ?? for more options. 
TRUN[CATE][={Y[ES]|N[O]|D[C]}] 
                            YES specifies that output lines        ASYNC 
                            which exceed the platen width          POLLVIP 
                            will be truncated to fit on one        URP 
                            line.  NO specifies that such          3270 
                            lines will wrap to the next line. 
                            The default is DC. 
UP[PERCASE][={Y[ES]|N[O]|D[C]}] 
                            Specifies whether or not to send       ASYNC 
                            lowercase alphabetic characters        POLLVIP 
                            input from the terminal to the         3270 
                            user program as uppercase letters. 
                            NO specifies normal processing of 
                            lowercase input.  The default is DC. 
                            For 3270, UPPERCASE is turned on 
                            in all supplied profiles.  IBM 
                            3270-type devices have no caps 
                            lock key, only a shift lock.  For 
                            timesharing, it is convenient to 
                            have all lowercase characters 
                            shifted to uppercase.  FIELDMARK-U 
                            may be used to toggle this. 
WORD[WRAPCLM]={value|D[C]}  Specifies the maximum length           ASYNC 
                            (0-255) of lines containing blanks     POLLVIP 
                            that will be returned to the           3270 
                            reading program.  If a longer 
                            line is entered, the characters 
                            past the space before WORDWRAPCLM 
                            are saved for use in the next read 
                            operation.  0 disables this 
                            facility.  The default is DC. 
                            The value 255 is the same as DC. 
WRAPPAGE[={Y[ES]|N[O]|D[C]}] 
                            YES specifies that for CRTs with       ASYNC 
                            SCROLL=NO, the screen is to be         POLLVIP 
                            erased one line at a time, such        3270 
                            that the line below the cursor 
                            is always blank.  NO specifies 
                            that the entire screen is to be 
                            erased after using the bottom 
                            line.  The default is DC. 
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
OPERATIONAL_PROFILE_OPTIONS
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
A list of PACKSET suboptions and their definitions can be accessed by typing a 
? or ??.  To access individual suboptions, type: 
HELP (SUPER) PACKSET_SUBOPTS suboption 
where suboption is any of the following: 
ACCOUNTS, ATTRIBUTES, GRANULES, SKELETON 
  Suboption    Description 
  AC[COUNTS] = decimal 
               Specifies the maximum number of file management accounts that 
               can be created for the project on this packset.  The decimal 
               value is the maximum number of file management accounts that 
               can be created on this packset for the project.  The default is 
               0. 
  AT[TRIBUTES] 
               Indicates that the system manager wishes to enter the 
               sub-option mode to specify the default file usage attributes 
               for file management accounts created on this packset by the 
               project administrator.  Once the ATTRIBUTES sub-option mode is 
               specified, any of the attribute options used with the PIG 
               CREATE or MODIFY command can be entered.  A blank line ends the 
               entry.  If the ATTRIBUTES option is not specified, the default 
               file attributes for the packset will be used when creating a 
               file management account for the project. 
  G[RANULES] = decimal 
               Specifies the maximum number of granules that can be used by 
               the project on this packset.  The decimal value is the maximum 
               number of granules.  The default is 0. 
  S[KELETON] = skeleton 
               Specifies an account name skeleton for file management accounts 
               created on this packset (e.g., ?HOST).  skeleton consists of 1 
               to 8 characters.  The valid character set consists of the 
               alphanumeric characters plus the characters $, :, and ?.  No 
               more than two question marks can be included in the skeleton 
               account name.  The default is '?'. 
00001
00002
00003
00004
PACKSET_SUBOPTIONS
For communications management, the user must have the appropriate PPRIV 
authorization.  That is, the user must have the PPRIV SUPER privilege or an 
appropriate combination of the SUPERAUTH, SUPERD, SUPERFORM and SUPERWSN 
privileges.  See HELP (SUPER) USER_OPTS PPRIVILEGE. 
Format: 
{C[REATE]} PRO[FILE] pname1 {devtype    } 
{M[ODIFY]}                  {FROM pname2} 
or 
D[ELETE] PRO[FILE] 
or 
R[EMOVE] PRO[FILE] pname1 
or 
D[ISPLAY] {[ALL] PRO[FILE[S]  } 
          {PRO[FILE] {devtype}} [(JCL)] 
          {          {pname  }} 
or 
L[IST] {[ALL] PRO[FILE[S]  } 
       {PRO[FILE] {devtype}} 
       {          {pname  }} 
Parameters: 
pname1    specifies a profile name.  If the MODIFY form of the command is used 
and a profile does not exist, it is created.  If the LIST or DISPLAY form of 
the command is used, pname can be wildcarded. 
devtype    specifies one of the following device types: 
3270              Used for IBM 3270-type terminals. 
ASYNC             Used for asynchronous terminals. 
LINK              Used for X.25 communication links. 
P[OLLED] V[IP]    Used for synchronous VIP7700 and VIP7814 terminals 
                  and printers. 
RBT|SYNC          Used for IRBT and RBT terminals, and 3270 and polled VIP 
                  lines.  (SYNC can be used as a synonym for RBT.) 
RBTD              Used for RBT devices. 
URP               Used for FEP-connected 
                  unit record peripherals (line printers, card 
                  readers or card punches). 
VIRTUAL CIRCUIT   Used for X.25 virtual circuits. 
The MODIFY PROFILE command verifies the specified device type against the 
device type of pname1. 
pname2    specifies an existing profile name.  The default profiles for each 
type are not changeable.  The default profile name for a device type is of the 
form $devtype; for example, $ASYNC for ASYNC device type, $RBT for RBT and 
SYNC device types.  Current profiles may be listed with the IBEX DI PROFILE 
command, or with the SUPER LIST PROFILE devtype command for the desired device 
type. 
Description: 
The CREATE, DELETE, MODIFY and REMOVE PROFILE commands create, delete (all), 
modify, and remove (one) profile.  The LIST PROFILE command lists the 
currently defined profiles.  The DISPLAY PROFILE command shows profile 
definitions. 
SUPER maintains profiles in the file :PRO.:SYS.  One ASYNC profile named TTY 
is automatically generated when the file is created.  If a user logs on and a 
profile is not associated with the account, the default for the VDH handler 
profile is assigned.  The preselected options of this profile are such that 
essentially any ASYNC terminal can operate using this profile.  It is also a 
good base for creating additional TTY-like profiles. 
SUPER commands that may be used to create profiles for a wide variety of 
common terminals and devices are included with the system release materials. 
While the list of these profiles is constantly growing, typing DISPLAY 
PROFILES at the IBEX level lists the names of those currently available.  Note 
that procedures established in the CP-6 Software Release Bulletin must be 
followed to create these profiles.  Enter HELP (SUPER) PROFILE_TYPES for more 
specific HELP. 
When CREATE, MODIFY or DISPLAY PROFILE is entered, SUPER prompts for options 
(OPT*) to which the user can respond with any of the PROFILE options.  See: 
HELP (SUPER) PROFILE_OPTION_SUMMARY.  Further details on graphics, link, and 
virtual circuit profile options can be obtained by entering: 
HELP (SUPER) GRAPHICS_PROFILE_OPTIONS, 
HELP (SUPER) LINK_PROFILE_OPTIONS, 
HELP (SUPER) VIRCIR_PROFILE_OPTIONS. 
For further information on ASYNC, RBT, RBTD, SYNC, URP, and 3270 options, see 
the CP-6 Systems Support Reference Manual, Volumes I & II (HA20 & HA21). 
While all options should be correctly specified for the most efficient use of 
the device, the options described below are particularly important for correct 
system operation: 
Option                Types              Remarks 
BLKBYTES              RBT                Specifies the number of bytes 
                                         per block. 
BLKRECS               RBT                Specifies the number of 
                                         records per block. 
DEVNUM                RBTD               Specifies how to address the 
                                         device. 
INPUT, OUTPUT         ASYNC, RBTD        Specifies the possible data 
                                         flow. 
LOWERCASEPRINTS       ASYNC, RBTD*,      Specifies whether lower case 
                      URP                characters are printable and 
                                         appears to users as 
                                         DCB.ATTR.LOWERCASE. 
LPTYPE, TTYTYPE       RBTD*              Used to establish DCB.DDEV. 
PROTYP                RBT                Specifies the terminal 
                                         protocol. 
PWIDTH                ASYNC, URP         Specifies the paper width and 
                                         appears to users in 
                                         DCB.WIDTH. 
*Also important for ASYNC profiles for devices used as printers, etc. 
Note:  When building profiles, significant effort can be saved by starting the 
profile definition with the appropriate default profile, since most parameters 
for a general class of devices will have the same values.  Examples can be 
found in the following profile fids. 
Device            Default Profile Name       Profile fid 
ASYNC CRT         DFLCRT                     KA$PRF.SUPPORT 
ASYNC hard-copy   DFLHC                      KA$PRF.SUPPORT 
3270 Display      3270D                      KZ$3270PRO.SUPPORT 
3270 Printer      3270P                      KZ$3270PRO.SUPPORT 
The LIST PROFILE command lists the name of selected device-type profiles or 
other types of profiles.  Including pname in the LIST PROFILE command is 
useful when wildcarding is used or to verify the existence of a profile 
definition. 
The DISPLAY PROFILE command shows a columnized display of the options for 
selected profiles (or all profiles if the ALL option is specified), prefaced 
by a header consisting of the profile information as entered in a CREATE or 
MODIFY PROFILE command.  The JCL option causes the command keyword CREATE to 
be written at the beginning of each profile definition and the END keyword to 
be inserted where needed. 
The REMOVE PROFILE command is used to remove one profile.  The DELETE PROFILE 
command will remove all profiles (except system-built ones), and should be 
used with caution.  SUPER attempts to protect users from inadvertently 
deleting all profiles by requiring confirmation before a DELETE PROFILE 
command is executed.  When the command DELETE PROFILE is issued, SUPER 
prompts: 
Delete all PROFILES  ? 
The value YES$ must be supplied or the deletion request is cancelled. 
When DISPLAY PROFILE is entered, SUPER prompts for options (OPT*).  The user 
can respond with:  any option listed under HELP (SUPER) 
PROFILE_OPTION_SUMMARY, or ALL, which lists all options for the specified 
profile or device type, or carriage return, which lists all profile names 
associated with the specified device type. 
UP[PERCASE][={Y[ES]|N[O]|D[C]}]                                 ASYNC 
          Specifies whether or not to send lowercase            POLLVIP 
          alphabetic characters input from the terminal to      3270 
          the user program as uppercase letters.  NO 
          specifies normal processing of lowercase input. 
          The default is DC. 
          For 3270, UPPERCASE is turned on in all supplied 
          profiles.  IBM 3270-type devices have no caps 
          lock key, only a shift lock.  For timesharing, it 
          is convenient to have all lowercase characters 
          shifted to uppercase.  FIELDMARK-U may be used to 
          toggle this. 
WI[NDOW]=value                                                  LINK 
          Specifies the frame transmit window size.  This is 
          CCITT parameter K.  The size that can be specified 
          depends on the value of the EXT SEQ option.  If EXT 
          SEQ=NO, the value is in the range 1-7.  If EXT 
          SEQ=YES, the value is in the range 1-127.  The 
          default is 7. 
WORD[WRAPCLM]={value|D[C]}                                      ASYNC 
          Specifies the maximum length (0-255) of lines         POLLVIP 
          containing blanks that will be returned to the        3270 
          reading program.  If a longer line is entered, 
          the characters past the space before WORDWRAPCLM 
          are saved for use in the next read operation. 
          0 disables this facility.  The default is DC. 
WRAPPAGE[={Y[ES]|N[O]|D[C]}]                                    ASYNC 
          YES specifies that for CRTs with SCROLL=NO, the       POLLVIP 
          screen is to be erased one line at a time, such       3270 
          that the line below the cursor is always blank. 
          NO specifies that the entire screen is to be 
          erased after using the bottom line.  The default 
          is DC. 
00002
00001
Profile options are divided into the following types: 
  COMMUNICATIONS OPTIONS 
  DEVICE ATTRIBUTE OPTIONS 
  GRAPHICS OPTIONS 
  LINK OPTIONS 
  OPERATIONAL OPTIONS 
  VIRTUAL CIRCUIT OPTIONS 
Device attribute options are further divided into the following 
types: 
  CURSOR CONTROL OPTIONS 
  FIELD CONTROL OPTIONS 
  MISCELLANEOUS OPTIONS 
  TIMING OPTIONS 
See the topic PROFILE_OPTION_SUMMARY for a listing of all PROFILE 
options.  That summary includes, for each option, a pointer to the 
OPTIONS topic that contains option syntax and description.  The 
profile option topics can be accessed directly by entering: 
  HELP (SUPER) topic 
where topic is one of the following: 
  COMMUNICATION_PROFILE_OPTIONS 
  CURSOR_PROFILE_OPTIONS 
  FIELD_PROFILE_OPTIONS 
  GRAPHICS_PROFILE_OPTIONS 
  LINK_PROFILE_OPTIONS 
  MISC_PROFILE_OPTIONS 
  OPERATIONAL_PROFILE_OPTIONS 
  TIMING_PROFILE_OPTIONS 
  VIRCIR_PROFILE_OPTIONS 
A list of profile options can be accessed by typing a ? or ??.  For individual 
options, type: 
HELP (SUPER) PROFILE_OPT_SUMMARY option 
where option is a combination of options found in the HELP topics listed 
below. 
For more information on specific options see the following topics: 
HELP (SUPER) COMMUNICATION_PROFILE_OPTIONS 
HELP (SUPER) CURSOR_PROFILE_OPTIONS 
HELP (SUPER) FIELD_PROFILE_OPTIONS 
HELP (SUPER) GRAPHICS_PROFILE_OPTIONS 
HELP (SUPER) LINK_PROFILE_OPTIONS 
HELP (SUPER) MISC_PROFILE_OPTIONS 
HELP (SUPER) OPERATIONAL_PROFILE_OPTIONS 
HELP (SUPER) TIMING_PROFILE_OPTIONS 
HELP (SUPER) VIRCIR_PROFILE_OPTIONS 
  Option                       Device      Profile Option Topic 
{A[BSGRPRND]_EM[PHASIS]}    ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
{A[BSGRPRND]_ER[ROR]   }    POLLVIP, 
{A[BSGRPRND]_H[IDDEN]  }    3270 
{A[BSGRPRND]_I[NPUT]   }=list 
{A[BSGRPRND]_N[ULL]    } 
{A[BSGRPRND]_O[UTPUT]  } 
{A[BSGRPRND]_W[ARNING] } 
AC[TONTRN][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP, 
                            3270 
APLL[CNRM][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP 
AT[RSCRNPOS][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      FIELD_PROFILE_OPTIONS 
                            POLLVIP 
AUTOC[URSOR][={Y[ES]|N[O]|DC}] 
                            ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP, 
                            3270 
AUTONL[={Y[ES]|N[O]|D[C]}]  ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
AUTOT[ABCLM]={value|D[C]}   ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP, 
                            3270 
AW[IDTH]={value|D[C]}       ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP, 
                            RBTD,URP, 
                            3270 
BI[N][={Y[ES]|N[O]|D[C]}]   ASYNC,      MISC_PROFILE_OPTIONS 
                            POLLVIP, 
                            RBTD,URP 
BLA[NKERASES][=Y[ES]|N[O]|D[C]}] 
                            ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP,    MISC_PROFILE_OPTIONS 
                            3270 
BLKB[YTES]=value            RBT,SYNC    COMMUNICATION_PROFILE_OPTIONS 
BLKR[ECS]=value             RBT,SYNC    COMMUNICATION_PROFILE_OPTIONS 
BS_TIM=real                 ASYNC,      TIMING_PROFILE_OPTIONS 
                            POLLVIP 
CALL DEL[AYS]=value         VIRCIR      VIRTUAL_CIRCUIT_OPTIONS 
CALL RETR[IES]=value        VIRCIR      VIRTUAL_CIRCUIT_OPTIONS 
CALL TIME[OUT]=value        VIRCIR      VIRTUAL_CIRCUIT_OPTIONS 
CA[LLS]={NONE|X25|X29|ALL}  LINK        LINK_PROFILE_OPTIONS 
CHA[RGE] INFO[RMATION][={Y[ES]|N[O]}] 
                            LINK        LINK_PROFILE_OPTIONS 
CHA[RGE] INFO[RMATION][={Y[ES]|N[O]}] 
                            VIRCIR      VIRTUAL_CIRCUIT_OPTIONS 
CH[ARSETNAME]=cname         ASYNC,      MISC_PROFILE_OPTIONS 
                            POLLVIP, 
                            RBTD,URP, 
                            3270 
CIR[CUITS]=value            LINK        LINK_PROFILE_OPTIONS 
CLEAR RETR[IES]=value       VIRCIR      VIRTUAL_CIRCUIT_OPTIONS 
CLEAR TIME[OUT]=value       VIRCIR      VIRTUAL_CIRCUIT_OPTIONS 
CO[MPRESS]={B[LANKS]|Y[ES]|N[O]|L[INE]} 
                            RBT,SYNC    COMMUNICATION_PROFILE_OPTIONS 
CR[ISNL][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
CUB[_CHR]=hex_list          ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
CUD[_CHR]=hex_list          ASYNC,     CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
CUF[_CHR]=hex_list          ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
CUP_A[LG]={0|ANS|1|TBL|2}   ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
CUP_B[IS]={value|hex|NONE}  ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
CUP_CH[R]=hex_list          ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
CUP_CL[MFRS][={Y[ES]|N[O]}] 
                            ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
CURSORR[EAD][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP, 
                            3270 
CUP_CM[P][={Y[ES]|N[O]}]    ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
CUU[_CHR]=hex_list          ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
DAQINP_[CHR]=hex            POLLVIP     FIELD_PROFILE_OPTIONS 
DAQPRT[_CHR]=hex            POLLVIP     FIELD_PROFILE_OPTIONS 
DATA TIME[OUT]=value        VIRCIR      VIRTUAL_CIRCUIT_OPTIONS 
DCH[_CHR]=hex_list          ASYNC       CURSOR_PROFILE_OPTIONS 
DCHM[OVFLD][={Y[ES]|N[O]|D[C]}] 
                            ASYNC       FIELD_PROFILE_OPTIONS 
DCLFL[D_ALG]={ANS|NONE|1|2|3} 
                            ASYNC,      FIELD_PROFILE_OPTIONS 
                            POLLVIP 
DCLFR[M_CHR]=hex_list       ASYNC,      FIELD_PROFILE_OPTIONS 
                            POLLVIP 
DEL[AYS]=value              RBT,SYNC    COMMUNICATION_PROFILE_OPTIONS 
DEVICEB[S][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
DEVICEC[R][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
DEVICEL[F][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
DEVP[OSOPTS][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
DEVS[CROLL][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP,    MISC_PROFILE_OPTIONS 
                            3270 
DI[SPINPUT][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP, 
                            3270 
DLTA[LLFLDS_CHR]=hex_list   ASYNC,      FIELD_PROFILE_OPTIONS 
                            POLLVIP 
DLTF[LD_CHR]=hex_list       ASYNC,      FIELD_PROFILE_OPTIONS 
                            POLLVIP 
DLTL[IN_CHR]=hex_list       ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
DSPH[EIGHT]={value|D[C]}    ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
DVCFLW[CTRALG]={0|NONE|ENQ[ACK]|1|ETX[ACK]|2|DC1[DC3]|D[C]} 
                            ASYNC       MISC_PROFILE_OPTIONS 
                                        TIMING_PROFILE_OPTIONS 
DVCOTPB[FRSIZ]=value        ASYNC,      MISC_PROFILE_OPTIONS 
                            POLLVIP,    TIMING_PROFILE_OPTIONS 
                            3270 
ED0D[LTFLD][={Y[ES]|N[O]}]  ASYNC,      FIELD_PROFILE_OPTIONS 
                            POLLVIP 
ED2D[LTFLD][={Y[ES]|N[O]}]  ASYNC,      FIELD_PROFILE_OPTIONS 
                            POLLVIP 
ED0[_CHR]=hex_list          ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
ED2[_CHR]=hex_list          ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
EDI[TOVR][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP 
EL0D[LTFLD][={Y[ES]|N[O]}]  ASYNC,      FIELD_PROFILE_OPTIONS 
                            POLLVIP 
EL0[_CHR]=hex_list          ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
EM[CHR]=hex                 RBT, SYNC   COMMUNICATION_PROFILE_OPTIONS 
ENDD[CLFRM_CHR]=hex_list    ASYNC,      FIELD_PROFILE_OPTIONS 
                            POLLVIP 
ENDM[SGLIN_CHR]=hex_list    ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
ERASE[FLD_CHR]=hex_list     ASYNC,      FIELD_PROFILE_OPTIONS 
                            POLLVIP 
ERR[DUPBLK][={Y[ES]|N[O]}]  RBT, SYNC   COMMUNICATION_PROFILE_OPTIONS 
ERSTIM=real                 ASYNC,      TIMING_PROFILE_OPTIONS 
                            POLLVIP 
EW[ALT][={Y[ES]|N[O]|DC}]   ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
EXT[ENDED] SEQ[UENCE]={Y[ES]|N[O]} 
                            LINK        LINK_PROFILE_OPTIONS 
EXT[ENDED] SEQ[UENCE]={Y[ES]|N[O]} 
                            VIRCIR      VIRCIR_PROFILE_OPTIONS 
EXTSRD[_CHR]=hex_list       ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
FAS[T] SEL[ECT] ACC[EPT]={Y[ES]|N[O]} 
                            LINK        LINK_PROFILE_OPTIONS 
FC[NTBL]={CP5|CP5S1|CP5S2|FRM1|SE1|SE2|NO|NONE} 
                            ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP, 
                            3270 
FF_FL[USH]=[{Y[ES]|N[O]|D[C]}] 
                            ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP     MISC_PROFILE_OPTIONS 
FF_IN[CCR][={YES|NO|DC}     ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP     MISC_PROFILE_OPTIONS 
FI[RSTLINE]={value|D[C]}    ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP, 
                            RBTD,URP, 
                            3270 
FL[DTRM]={L[INE]|P[AGE]|D[C]} 
                            ASYNC,      FIELD_PROFILE_OPTIONS 
                            POLLVIP 
FR[AME]={128|256|512|1024|2048|4096} 
                            LINK        LINK_PROFILE_OPTIONS 
FRMFED[_CHR]=hex_list       ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
FRMFED[_CHR][={Y[ES]|N[O]}] 3270        OPERATIONAL_PROFILE_OPTIONS 
FRSC[LMFLD][={Y[ES]|N[O]}]  ASYNC,      FIELD_PROFILE_OPTIONS 
                            POLLVIP 
FU[LLDUXPAPERTAPE][={Y[ES]|N[O]|D[C]}] 
                            ASYNC       OPERATIONAL_PROFILE_OPTIONS 
FUNCT[ION_KEY]              ASYNC,      MISC_PROFILE_OPTIONS 
                            POLLVIP 
GR_BATCH[MODE]=value                    GRAPHICS_PROFILE_OPTIONS 
GR_BKGRNDC[OLOR]=value                  GRAPHICS_PROFILE_OPTIONS 
GR_BKGRNDT[YPE]=value                   GRAPHICS_PROFILE_OPTIONS 
GR_CHSIZEC[OUNT]=value                  GRAPHICS_PROFILE_OPTIONS 
GR_CHSIZES[UPPORT]=value                GRAPHICS_PROFILE_OPTIONS 
GR_COLRA[CTION]=value                   GRAPHICS_PROFILE_OPTIONS 
GR_COLRM[ODEL]=value                    GRAPHICS_PROFILE_OPTIONS 
GR_COLRTABS[IZE]=value                  GRAPHICS_PROFILE_OPTIONS 
GR_COLRTABT[YPE]=value                  GRAPHICS_PROFILE_OPTIONS 
GR_DEPTHU[SE]=value                     GRAPHICS_PROFILE_OPTIONS 
GR_DEV[TYPE]=value                      GRAPHICS_PROFILE_OPTIONS 
GR_DIM[LEVEL]=value                     GRAPHICS_PROFILE_OPTIONS 
GR_EDGE[TYPE]=value                     GRAPHICS_PROFILE_OPTIONS 
GR_ESC[APE] x = {H[ARDWARE]|S[OFTWARE]|U[NSUPPORTED]} 
                                        GRAPHICS_PROFILE_OPTIONS 
GR_FONT[COUNT]=value                    GRAPHICS_PROFILE_OPTIONS 
GR_FPRG=value                           GRAPHICS_PROFILE_OPTIONS 
GR_GLBLCO[LORS]=value                   GRAPHICS_PROFILE_OPTIONS 
GR_GLBLIN[TENSITIES]=value              GRAPHICS_PROFILE_OPTIONS 
GR_HEIGHTU[SE]=value                    GRAPHICS_PROFILE_OPTIONS 
GR_HID[DENLEVEL]=value                  GRAPHICS_PROFILE_OPTIONS 
GR_HIGHLTS[UPPORT]=value                GRAPHICS_PROFILE_OPTIONS 
GR_IMA[GETRANS]=value                   GRAPHICS_PROFILE_OPTIONS 
GR_INTNACT[ION]=value                   GRAPHICS_PROFILE_OPTIONS 
GR_INTNSUP[PORT]=value                  GRAPHICS_PROFILE_OPTIONS 
GR_INTNTAB[SIZE]=value                  GRAPHICS_PROFILE_OPTIONS 
GR_LINESTYLEH[WCOUNT]=value             GRAPHICS_PROFILE_OPTIONS 
GR_LINESTYLES[WCOUNT]=value             GRAPHICS_PROFILE_OPTIONS 
GR_LINEWC[OUNT]=value                   GRAPHICS_PROFILE_OPTIONS 
GR_LINEWS[UPPORT]=value                 GRAPHICS_PROFILE_OPTIONS 
GR_MARKERH[WCOUNT]=value                GRAPHICS_PROFILE_OPTIONS 
GR_MARKERS[WCOUNT]=value                GRAPHICS_PROFILE_OPTIONS 
GR_MAXCH[SIZE]=value                    GRAPHICS_PROFILE_OPTIONS 
GR_MAXLINE[WIDTH]=value                 GRAPHICS_PROFILE_OPTIONS 
GR_MAXP[ICK]=value                      GRAPHICS_PROFILE_OPTIONS 
GR_MINCH[SIZE]=value                    GRAPHICS_PROFILE_OPTIONS 
GR_MINLINE[WIDTH]=value                 GRAPHICS_PROFILE_OPTIONS 
GR_NDCDCH[ARS]=value                    GRAPHICS_PROFILE_OPTIONS 
GR_NDCDCUR[RENT]=value                  GRAPHICS_PROFILE_OPTIONS 
GR_NDCDSP[ACE]=value                    GRAPHICS_PROFILE_OPTIONS 
GR_NDCHCH[ARS]=value                    GRAPHICS_PROFILE_OPTIONS 
GR_NDCHCUR[RENT]=value                  GRAPHICS_PROFILE_OPTIONS 
GR_NDCHSP[ACE]=value                    GRAPHICS_PROFILE_OPTIONS 
GR_NDCWCH[ARS]=value                    GRAPHICS_PROFILE_OPTIONS 
GR_NDCWCUR[RENT]=value                  GRAPHICS_PROFILE_OPTIONS 
GR_NDCWSP[ACE]=value                    GRAPHICS_PROFILE_OPTIONS 
GR_OUT[LEVEL]=value                     GRAPHICS_PROFILE_OPTIONS 
GR_PENH[WCOUNT]=value                   GRAPHICS_PROFILE_OPTIONS 
GR_PENS[WCOUNT]=value                   GRAPHICS_PROFILE_OPTIONS 
GR_PIX[ELTYPE]=value                    GRAPHICS_PROFILE_OPTIONS 
GR_POLY[GONFILL]{PAT[TERNED]|PLA[IN]| 
   SHA[DED]}=value                      GRAPHICS_PROFILE_OPTIONS 
GR_VIEWSURF[ACE]=value                  GRAPHICS_PROFILE_OPTIONS 
GR_VIEWTY[PE]=value                     GRAPHICS_PROFILE_OPTIONS 
GR_WIDTHU[SE]=value                     GRAPHICS_PROFILE_OPTIONS 
GR_XPIX[MAX]=value                      GRAPHICS_PROFILE_OPTIONS 
GR_XSP[ACE]=value                       GRAPHICS_PROFILE_OPTIONS 
GR_YPIX[MAX]=value                      GRAPHICS_PROFILE_OPTIONS 
GR_YSP[ACE]=value                       GRAPHICS_PROFILE_OPTIONS 
GR_ZSP[ACE]=value                       GRAPHICS_PROFILE_OPTIONS 
HA[LFDUXPAPERTAPE][={Y[ES]|N[O]|D[C]}] 
                            ASYNC       OPERATIONAL_PROFILE_OPTIONS 
HE[IGHT]={value|D[C]}       ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP,    MISC_PROFILE_OPTIONS 
                            3270 
HPA_ALG={0|ANS|CHA|DBL|NEC} ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP 
HSCR[OLL][={Y[ES]|N[O]|D[C]}] 
                            ASYNC       OPERATIONAL_PROFILE_OPTIONS 
ICH[_CHR]=hex_list          ASYNC       CURSOR_PROFILE_OPTIONS 
ICHR[QRDCH][={Y[ES]|N[O]}]  ASYNC       CURSOR_PROFILE_OPTIONS 
IDL[E] TIME[OUT]=value      LINK        LINK_PROFILE_OPTIONS 
IDL[E] TIME[OUT]=value      VIRCIR      VIRCIR_PROFILE_OPTIONS 
ILNR[QRDLIN][={Y[ES]|N[O]}] ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
INPUT[={YES}|N[O]|D[C]}]    ASYNC,      MISC_PROFILE_OPTIONS 
                            POLLVIP, 
                            RBTD,URP, 
                            3270 
INSE[RTMODE][={Y[ES]|N[O]|D[C]}] 
                            ASYNC       OPERATIONAL_PROFILE_OPTIONS 
INSL[IN_CHR]=hex_list       ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
INT[ERRUPT] TIME[OUT]=value             VIRCIR_PROFILE_OPTIONS 
INT[ERVAL]=value            RBT,SYNC    COMMUNICATION_PROFILE_OPTIONS 
IRS[CHR]=hex                RBT,SYNC    COMMUNICATION_PROFILE_OPTIONS 
KEEP[TYPAHD][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP, 
                            3270 
LE[NGTH]={value|D[C]}       ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP, 
                            RBTD,URP, 
                            3270 
LF[ISNL][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP, 
                            RBTD 
LI[MBO]={value|D[C]}        ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP, 
                            RBTD,URP, 
                            3270 
LIMBOCLM[={Y[ES|N[O]|D[C]}] ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
LOCALECHO[={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP 
LOWERCASE[={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP, 
                            3270 
LOWERCASEP[RINTS][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      MISC_PROFILE_OPTIONS 
                            POLLVIP, 
                            RBT,URP, 
                            3270 
LST[RECCTN]={Y[ES]|N[O]}    RBT,SYNC    COMMUNICATION_PROFILE_OPTIONS 
MA[XATRS]={value|D[C]}      ASYNC,      FIELD_PROFILE_OPTIONS 
                            POLLVIP 
MAX[IMUM] WIN[DOW]=value                LINK_PROFILE_OPTIONS 
ENTER ? TO CONTINUE 
MAXV[IRCIR]=value                       VIRCIR_PROFILE_OPTIONS 
MIC[ROFPL][={Y[ES]|N[O]|DC}  ASYNC      MISC_PROFILE_OPTIONS 
MINV[IRCIR]=value                       VIRCIR_PROFILE_OPTIONS 
MODE={DTE|DCE}                          LINK_PROFILE_OPTIONS 
MSGH[ALT][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP, 
                            3270 
MSGLINE[={Y[ES]|N[O]|D[C]}] ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP 
MSGL[IN_CHR]=hex_list       ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
MU[LSTRM][={Y[ES]|N[O]}]    RBT,SYNC    COMMUNICATION_PROFILE_OPTIONS 
NOO[PTMIZ][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP 
OP[DTAB][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
OUTPUT[={Y[ES]|N[O]|D[C]}]  ASYNC,      MISC_PROFILE_OPTIONS 
                            POLLVIP, 
                            RBTD,URP, 
                            3270 
OUTPUTD[ISCARD][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP, 
                            3270 
PAD[SIGNON]={Y[ES]|N[O]}    RBT,SYNC    COMMUNICATION_PROFILE_OPTIONS 
PAG[EHALT][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP, 
                            3270 
PARITY={NONE|ODD|EVEN|ONE|ZERO|D[C]} 
                            ASYNC,      MISC_PROFILE_OPTIONS 
                            POLLVIP 
PARITYC[HECK][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP 
PARK[CURSOR][={Y[ES]|N[O]|D[C]}] 
PRINTH[ALT][={Y[ES]|N[O]DC}] 
                            ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP, 
                            3270 
PRINTT[YPE][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      MISC_PROFILE_OPTIONS 
                            POLLVIP, 
                            RBTD,URP, 
                            3270 
PROG[DTAB][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
PROT[YP]={POLLED|2780|3780|HASP|HIP} 
                            RBT,SYNC    COMMUNICATION_PROFILE_OPTIONS 
PW[IDTH]={value|D[C]}       ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP, 
                            RBTD,URP, 
                            3270 
REC[EIVE] SIZ[E]={128|256|512|1024|2048|4096} 
                            VIRCIR      VIRCIR_PROFILE_OPTIONS 
REC[EIVE] THR[OUGHPUT]={NONE|75|150|300|600| 
    1200|2400|4800|9600|19200|48000}    VIRCIR_PROFILE_OPTIONS 
REC[EIVE] WIN[DOW]=value                VIRCIR_PROFILE_OPTIONS 
RELP[AGE][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP 
RESET RETR[IES]=value       VIRCIR      VIRCIR_PROFILE_OPTIONS 
RESET TIME[OUT]=value       VIRCIR      VIRCIR_PROFILE_OPTIONS 
RES[POND TO] COM[PLETE][={YES|NO}]      VIRCIR_PROFILE_OPTIONS 
RESP[ONSE] DEL[AY]=value                LINK_PROFILE_OPTIONS 
RESP[ONSE] DEL[AY]=value                VIRCIR_PROFILE_OPTIONS 
RES[PONSE] TI[MER]=value                VIRCIR_PROFILE_OPTIONS 
RESTART RETR[IES]=value     LINK        LINK_PROFILE_OPTIONS 
RESTART TIME[OUT]=value     LINK        LINK_PROFILE_OPTIONS 
RES[TORE_DFLTSCRN_CHR]=hex_list 
                            ASYNC,      FIELD_PROFILE_OPTIONS 
                            POLLVIP 
RET[RANSMISSION]=value                  LINK_PROFILE_OPTIONS 
RETR[YS]=value              RBT,SYNC    COMMUNICATION_PROFILE_OPTIONS 
RETY[POVR][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP, 
                            3270 
REV[ERSE][={Y[ES]|N[O]}]                LINK_PROFILE_OPTIONS 
RE[VERSE][={Y[ES]|N[O]}]                VIRCIR_PROFILE_OPTIONS 
RGNSCROLL[={Y[ES]|N[O]}]    ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP 
RRR={Y[ES]|N[O]}            RBT,SYNC    COMMUNICATION_PROFILE_OPTIONS 
RSTINS[MOD_CHR]=hex_list    ASYNC       CURSOR_PROFILE_OPTIONS 
SC[ROLL][={Y[ES]|N[O]|D[C]}] 
                            ASYNC       OPERATIONAL_PROFILE_OPTIONS 
SE[NDBKSPACE][={Y[ES]|N[O]|D[C]}] 
                            ASYNC       OPERATIONAL_PROFILE_OPTIONS 
SEN[D] SIZ[E]={128|256|512|1024|2048|4096} 
                            VIRCIR      VIRCIR_PROFILE_OPTIONSTN10 
SEN[D] THR[OUGHPUT]={NONE|75|150|300|600| 
   1200|2400|4800|9600|19200|48000}     VIRCIR_PROFILE_OPTIONS 
SEN[D] WIN[DOW]=value                   VIRCIR_PROFILE_OPTIONS 
SETUP[_CHR]=hex_list        ASYNC,      MISC_PROFILE_OPTIONS 
                            POLLVIP 
SGRD[CRINT_CHR]=hex         ASYNC,      FIELD_PROFILE_OPTIONS 
                            POLLVIP 
SGRINCD[AQ][={Y[ES]|N[O]}]  POLLVIP     FIELD_PROFILE_OPTIONS 
SGRF[STBLN_CHR]=hex         ASYNC,      FIELD_PROFILE_OPTIONS 
                            POLLVIP 
SGRH[DN_CHR]=hex            ASYNC,      FIELD_PROFILE_OPTIONS 
                            POLLVIP 
SGRINCI[NT_CHR]=hex         ASYNC,      FIELD_PROFILE_OPTIONS 
                            POLLVIP 
SGRINT[RO_CHR]=hex_list     ASYNC,      FIELD_PROFILE_OPTIONS 
                            POLLVIP 
SGRR[VRVID_CHR]=hex         ASYNC,      FIELD_PROFILE_OPTIONS 
                            POLLVIP 
SGRS[LWBLN_CHR]=hex         ASYNC,     FIELD_PROFILE_OPTIONS 
                            POLLVIP 
SGRU[NDSCR_CHR]=hex         ASYNC,      FIELD_PROFILE_OPTIONS 
                            POLLVIP 
SGR_[ALG]={NONE|ANS|1|2|3}  ASYNC,      FIELD_PROFILE_OPTIONS 
                            POLLVIP 
SIM[PERF][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP, 
                            3270 
SIN[PUTSZ]={value|D[C]}     ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP, 
                            3270 
SIO[PT][={Y[ES]|N[O]}]      ASYNC,      CURSOR_PROFILE_OPTIONS 
                            POLLVIP, 
                            3270 
SLC={Y[ES]|N[O]}            RBT,SYNC    COMMUNICATION_PROFILE_OPTIONS 
SLCALLBLK={Y[ES]|N[O]}      RBT,SYNC    COMMUNICATION_PROFILE_OPTIONS 
SPA[CEINSERT][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP, 
                            URP,3270 
SPC[BFRPRT][={Y[ES]|N[O]|D[C]}] 
                            RBTD        MISC_PROFILE_OPTIONS 
SPCD[LTFLD][={Y[ES]|N[O]}]  ASYNC,      FIELD_PROFILE_OPTIONS 
                            POLLVIP 
SPE[ED]={50|75|110|134.5|150|200|300|600| 
   1050|1200|1800|2000|2400|4800|9600|19200|D[C]} 
                            ASYNC       MISC_PROFILE_OPTIONS 
TABR[ELATIVE][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP, 
                            3270 
TABS=value[, value] ...     ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP, 
                            URP 
TABSI[M][={Y[ES]|N[O]|DC}]  RBTD,URP,   OPERATIONAL_PROFILE_OPTIONS 
                            3270 
TIMAFTCT[RFNC]=real         ASYNC,      TIMING_PROFILE_OPTIONS 
                            POLLVIP 
TIME[OUT]=value                         LINK_PROFILE_OPTIONS 
TMNALG_AFTCR=value          ASYNC,      TIMING_PROFILE_OPTIONS 
                            POLLVIP 
TMNALG_AFTCUP=value         ASYNC,      TIMING_PROFILE_OPTIONS 
                            POLLVIP 
TMNALG_AFTHPA=value         ASYNC,      TIMING_PROFILE_OPTIONS 
                            POLLVIP 
TMNALG_AFTHT=value          ASYNC,      TIMING_PROFILE_OPTIONS 
                            POLLVIP 
TMNALG_AFTLF=value          ASYNC,      TIMING_PROFILE_OPTIONS 
                            POLLVIP 
TMNALG_BFRCR=value          ASYNC,      TIMING_PROFILE_OPTIONS 
                            POLLVIP 
TMNALG_BFRLF=value          ASYNC,      TIMING_PROFILE_OPTIONS 
                            POLLVIP 
TMNALG_FILCHR=hex           ASYNC,      TIMING_PROFILE_OPTIONS 
                            POLLVIP 
TMNALG_PRM1=real            ASYNC,      TIMING_PROFILE_OPTIONS 
                            POLLVIP 
TMNALG_PRM2=real            ASYNC,      TIMING_PROFILE_OPTIONS 
                            POLLVIP 
TMNALG_PRM3=real            ASYNC,      TIMING_PROFILE_OPTIONS 
                            POLLVIP 
TMNALG_PRM4=real            ASYNC,      TIMING_PROFILE_OPTIONS 
                            POLLVIP 
TMNALG_PRM5=real            ASYNC,      TIMING_PROFILE_OPTIONS 
                            POLLVIP 
TMNALG_PRM6=real            ASYNC,      TIMING_PROFILE_OPTIONS 
                            POLLVIP 
TMNALG_PRM7=real            ASYNC,      TIMING_PROFILE_OPTIONS 
                            POLLVIP 
TMNALG_PRM8=real            ASYNC,      TIMING_PROFILE_OPTIONS 
                            POLLVIP 
TRA[NSIT] DEL[AY]=value     VIRCIR      VIRCIR_PROFILE_OPTIONS 
TRUN[CATE][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP, 
                            URP,3270 
TRUO[VRPRT][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      MISC_PROFILE_OPTIONS 
                            POLLVIP, 
                            RBTD,URP, 
                            3270 
TT[YTYPE][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      MISC_PROFILE_OPTIONS 
                            POLLVIP, 
                            RBTD,3270 
TY[PE]={P[RIMARY]|S[ECONDARY}           VIRCIR_PROFILE_OPTIONS 
UP[PERCASE][={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP, 
                            3270 
WI[NDOW]=value                          LINK_PROFILE_OPTIONS 
WORD[WRAPCLM]={value|D[C]}  ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP, 
                            3270 
WRAPPAGE[={Y[ES]|N[O]|D[C]}] 
                            ASYNC,      OPERATIONAL_PROFILE_OPTIONS 
                            POLLVIP, 
                            3270 
00001
00002
00218
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
00017
00014
00015
00017
00016
00014
00015
00016
00019
00018
00018
00019
00020
00021
00022
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
00033
00032
00034
00035
00036
00037
00037
00038
00039
00038
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
00051
00054
00052
00054
00055
00053
00055
00056
00058
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
00066
00067
00068
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
00132
00133
00134
00135
00136
00137
00138
00139
00140
00142
00141
00141
00143
00143
00144
00145
00146
00147
00149
00148
00149
00148
00150
00151
00152
00153
00154
00155
00156
00157
00158
00158
00159
00160
00161
00162
00161
00163
00164
00165
00166
00168
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
00184
00185
00186
00187
00195
00190
00191
00188
00189
00188
00189
00190
00191
00192
00193
00194
00193
00194
00192
00195
00196
00197
00196
00197
00198
00199
00200
00201
00202
00203
00204
00206
00205
00206
00207
00207
00205
00208
00209
00211
00212
00210
00213
00214
00215
00216
00217
00218
00219
00220
00221
00222
00223
00224
00225
00226
00227
00228
00229
00230
00231
00232
00233
00234
00234
00235
00236
00237
00238
00239
00240
00241
00242
PROFILE_OPTION_SUMMARY
The documented profile types are divided into the following categories: 
ASYNC, 3270, RBT_LINE, RBT_DEVICE and URP.  Enter HELP (SUPER) PROFILE_TYPES 
category to list documented profile types by profile category.  To list all 
the available profile types, enter ??. 
  Profile Name        Terminal Description 
ASYNC Profiles 
$$ASYNC             Default graphics device profile 
DFLCRT              Default CRT 
DFLHC               Default hardcopy 
DFLPRF              Default profile (before logon) 
GRAPHICFILE         Default graphicfile graphics record 
TTY                 Default, very basic and slow 
ADDS25              ADDS (Regent) 25 
ADDS60              ADDS (Regent) 60 
ADDS60TP            ADDS (Regent) 60, without EL0 
ADDS200             ADDS (Regent) 200 
ADDS580             ADDS (Consul) 580 
ADDS980             ADDS (Consul) 980 
ADDSVPA1            ADDS Viewpoint Model A1 
ADDSVPA2            ADDS Viewpoint Model A2 
ADDSVPA3            ADDS Viewpoint Model A3 
ANNAMB              Ann Arbor Ambassador 
APLLISW             Apple Lisa Workshop 
BEEDM20             Beehive DM20 
CDI1203             Computer Devices Inc 1203 (Miniterm) 
CDI1203S            Computer Devices Inc 1203S (Miniterm) 
CDI1205             Computer Devices Inc 1205 (Miniterm) with narrow platen 
CDI1205W            Computer Devices Inc 1205 (Miniterm) with wide platen 
CDI2200             Computer Devices Inc 2200 (Miniterm) with narrow platen 
CDI2200H            Computer Devices Inc 2200 (Miniterm) at high-speed 
                      (>1200 baud) 
CDI2200W            Computer Devices Inc 2200 (Miniterm) with wide platen 
CDI2200HW           Computer Devices Inc 2200 (Miniterm) >1200 baud, 
                      wide platen 
CTR6300             Centronics 6300 
DBL1550             Diablo 1550 
DBL1610             Diablo 1610 
DBL1620             Diablo 1620 
DBL1641             Diablo 1641 
DECDS120            Digital Equipment LA36 with Datasouth 120 
DECLA120            Digital Equipment LA120 
DECLA34             Digital Equipment LA34 
DECLA36             Digital Equipment LA36 
DECLA36SD           Digital Equipment LA36 with SUPERDEC board 
DECVT50             Digital Equipment VT50 
DECVT52             Digital Equipment VT52 
DECVT52W            Digital Equipment VT-1xx in VT52 mode, wide 
DECVT100            Digital Equipment VT100 
DECVT100A           Digital Equipment VT100, Application Keypad 
DECVT100W           Digital Equipment VT100, wide 
DECVT100WA          Digital Equipment VT100, Application Keypad, wide 
DECVT125            Digital Equipment VT125 
DECVT131            Digital Equipment VT131T 
DECVT131A           Digital Equipment VT131T, Application Keypad 
DECVT131W           Digital Equipment VT131T, wide 
DECVT131WA          Digital Equipment VT131, Application Keypad, wide 
DECVT200            Digital Equipment VT200 
DECVT200A           Digital Equipment VT200, Application Keypad 
DECVT200W           Digital Equipment VT200, wide 
DECVT200WA          Digital Equipment VT200T, Application Keypad, wide 
DECVT220            Digital Equipment VT220 
DECVT241            DEC's color graphics CRT 
DECVT241A           Digital Equipment VT241, Application Keypad 
DECVT241W           Digital Equipment VT241, wide 
DECVT241WA          Digital Equipment VT241, Application Keypad, wide 
DKU7102             CII Bull DKU 7102 
DTM1520             Datamedia Elite 1520A 
DTP8200             Datapoint 8200 
DY4VGT100H          DY-4 Systems VGT-100H in DEC VT-100 mode 
DY4VGT100HT         DY-4 Systems VGT-100H in TEKM mode, vsn 2.2 PROMs 
EPSPX8-8            Epson PX-8, 8 line window 
EPSPX8-40           Epson PX-8, 40 line window 
GETN300             GE Terminet 300 
GT100               General Terminal GT 100 
GT400               General Terminal GT 400 
GT400TP             General Terminal GT 400 for TP 
HIDMP29             Houston Instruments DMP-29 
HP2645              Hewlett Packard 2645 
HP7475A             Hewlett Packard 7475H 
HP7475ADEC          Hewlett Packard 7475A on DECVT-1xx or VT-2xx 
HP9845              Hewlett Packard 9845 
HTH14               Heath H14 printer 
HTH19               Heath H19 
HTH19A              Heath H19 (ANS mode) 
HTH89               Heath H89 
HZL1000             Hazeltine 1000 
HZL1500             Hazeltine 1500 
HZL1520             Hazeltine 1520 
HZL2000             Hazeltine 2000 
HZL2000P            Hazeltine 2000 Printer 
HZLMOD1             Hazeltine Modular 1 
Type ? for more profile types. 
IBM3101-1X          IBM 3101-1X 
IBM3101-2X          IBM 3101-2X 
IBMPC-H89           IBM Personal Computer in Heath H89 mode 
INFI100             Infoton I-100 
INFI400             Infoton I-400 
INFSTL              Infoton Satellite 
INFVST              Infoton Vistar 
INTI                Intertec Intertube I 
INTII               Intertec Intertube II 
INTSII              Interstate Superbrain II 
LBRF50              Liberty Electronics Freedom 50 
LBRF100             Liberty Electronics Freedom 100 
LSIADM3A            Lear Siegler Inc ADM 3A 
LSIADM5             Lear Siegler Inc ADM 5 
LSIADM31            Lear Siegler Inc ADM 31 
MCRACTIV            Microterm ACT-IV 
NEC5510             NEC 5510 (Spinwriter) 
NEC5515             NEC 5515 (Spinwriter) 
NEC5520             NEC 5520 (Spinwriter) 
NEC5525             NEC 5525 (Spinwriter) 
NECPC8201A          NEC PC-8201A 
PCTX364             PCT Terminal emulator / X3.64 mode. 
PCTX364GR           PCT Terminal emulator / X3.64 mode with graphics 
PCTV7800            PCT Terminal emulator / VIP7800-style 
PCTV7800GR          PCT Terminal emulator / VIP7800 with graphics 
PCTV7800INV         PCT emulator / VIP7800 with Inverse Video 
PE550               Perkins Elmer 550 
PRT300              Printronix 300 
PRU1002             Bull PRU1002 
PRU1003             Bull PRU1003 
PRU1005             Bull PRU1005 
QMS1200             Quality Microsystems 1200 Laserprinter 
QUMEVT101           Qume VT-101 
SDS420              SDS (Scientific Data Systems) 420 
SMTP                Simple Mail Transfer Protocol 
SNRKTM380           Synertek KTM 3/80 
SOROC120            Soroc 120 
Enter ? for more profile names. 
TEK4010             Tektronix 4010 
TEK4010L            Tektronix 4010, Long, narrow 
TEK4013             Tektronix 4013 
TEK4013L            Tektronix 4013, long, narrow 
TEK4023             Tektronix 4023 
TEK4024             Tektronix 4024 
TEK4025             Tektronix 4025 
TEK4027             Tektronix 4027 
TEK4105             Tektronix 4105 in ANS X3.64 mode 
TEK4107             Tektronix 4107 in ANS X3.64 mode 
TEK4112A            Tektronix 4112A 
TEK4112AA           Tektronix 4112A, APL mode 
TEK4112B            Tektronix 4112B in ANS 3.64 mode 
TI725               Texas Instruments 725 
TI733               Texas Instruments 733 
TI743               Texas Instruments 743 
TI745               Texas Instruments 745 
TI783               Texas Instruments 783 
TI785               Texas Instruments 785 
TI787               Texas Instruments 787 
TI810               Texas Instruments 810 
TI820               Texas Instruments 820 
TI855WP             Texas Instruments 855 printer, WP mode 
TLR1000             Telray 1000 
TLR3300             Telray 3300 
TRS80M1             Radio Shack TRS-80 Model 1 
TRS80M2             Radio Shack TRS-80 Model 2 
TRS80M2VT           Radio Shack TRS-80 Model 2, TRSDOS-II, Videotex 
TRS80M16            Radio Shack TRS-80 Model 16, TRSDOS-16 
TRS80M16X           Radio Shack TRS-80 Model 16 Console, Xenix (UNIX) 
TRS80M100           Radio Shack TRS-80 Model 100 
TTY33               Teletype Model 33 
TTY35               Teletype Model 35 
TTY37               Teletype Model 37 
TTY43               Teletype Model 43 
TVI910P             Televideo TVI-910 PLUS 
TVI910PA            Televideo TVI-910 PLUS with fields 
TVI912A             Televideo TVI-912A 
TVI912C             Televideo TVI-912C 
TVI912N             Televideo TVI-912 with AUTONL disable 
TVI920              Televideo TVI-920 
TVI950              Televideo TVI-950 
TWU1002             Bull TWU1002 
TWU1003             Bull TWU1003 
TWU1005             Bull TWU1005 
TWU9101             Bull TWU9101 
TWU9104             Bull TWU9104 
TWU9106             Bull TWU9106 
UNIXVT100           Unix DEC VT-100 Emulator 
VC303A              Vogler Craig VC303A 
VC403A              Vogler Craig VC403A 
VC404               Vogler Craig VC404 
VC414H              Vogler Craig VC414H 
VERPLP100           Verticom PLP 100 
VERPLP100W          Verticom PLP 100, wide 
VIP7100             Bull VIP 7100 
VIP7105             Bull VIP 7105 
VIP7200             Bull VIP 7200 
VIP7201             Bull VIP 7201 
VIP7205             Bull VIP 7205 
VIP7301             Bull VIP 7301 
VIP7801             Bull VIP 7801 
VIP7802             Bull VIP 7802 
VIP7813             Bull VIP 7813 
VIP7814             Bull VIP 7814 
VIP7801L            Bull VIP 7801 with 72-line option 
VIP7802L            Bull VIP 7802 with 72-line option 
VIP7813L            Bull VIP 7813 with 72-line option 
VIP7814L            Bull VIP 7814 with 72-line option 
VIP7814AP           Bull VIP7814 w/attached printer 
XRX850              Xerox 850 
XRX1760             Xerox 1760 
XRX7015             Xerox 7015 
ZENZ19              Zenith Z19 
ZENZ29              Zenith Z29 
ZENZ89              Zenith Z89 
ZENZ90              Zenith Z90 
ZENZ100             Zenith Z100 
3270 Profiles 
MULDRP              IBM 3270 Line (not device or controller) 
3270D               IBM 3270 Display default 
3277-1              IBM 3277 Model 1 
3277-2              IBM 3277 Model 2 
3278-1              IBM 3278/3276 Model 1 
3278-2              IBM 3278/3276 Model 2 
3278-2L             IBM 3278/3276 Model 2 with data-entry keyboard 
3278-3              IBM 3278/3276 Model 3 
3278-4              IBM 3278/3276 Model 4 
3278-5              IBM 3278 Model 5 
3270P               IBM 328x basic printer, 66 lines/page, with form-feed 
3270PC              IBM 328x basic printer, no page length (continuous) 
RBT Line Profiles 
STDHASP             Standard HASP line 
STD3780             Standard 3780 line 
STD2780             Standard 2780 line 
RBT Device Profiles 
IRBTCR              Standard HASP card reader profile 
IRBTLP              Standard HASP line printer profile 
IRBTCP              Standard HASP card punch profile 
IRBTOC              Standard HASP operator console profile 
XDSCR               Xerox HASP card reader profile 
XDSLP               Xerox HASP line printer profile 
XDSCP               Xerox HASP card punch profile 
SIGMAOC             Old style KSR-35 Sigma operator console 
3780CR              All IBM 3780-type card reader streams 
3780CP              All IBM 3780-type card punch streams 
3780LP              All IBM 3780-type printer streams 
2780CR              All IBM 2780-type card reader streams 
2780CP              All IBM 2780-type card punch streams 
2780LP              All IBM 2780-type line printer streams 
URP Profiles 
PRU9117             PRU9117 and PRU9617 Line Printer with 132 columns 
                    with PRB1600 upper/lowercase print band 
PRU9118             PRU9118 and PRU9618 Line Printer with 132 columns 
                    with PRB2600 upper/lowercase print band 
PRU9619             PRU9619 Line Printer with 136 columns with EVFU ASC95 
PRU9627             PRU9627 Line Printer with 132 columns with EVFU ASC95 
PRU9109             PRU9109 and PRU9609 Line Printer with 132 columns 
PRF9118             PRU9118 and PRU9618 Line Printer with 136 columns 
                    (option PRF9118 or PRF9618) 
PRF9627             PRU9627 Line Printer with 132 columns with EVFU ASC64 
CRU9111             CRU9111 and CRU9611 Card Reader 
PCU9101             PCU9101 Card Punch 
00004
00001
00006
00005
00007
PROJECT_COMMANDS
A list of SUPER project authorization commands and their definitions can be 
accessed by typing a ? or a ?? after this message.  To obtain definitions of 
individual project authorization commands, type 
HELP (SUPER) PROJECT_CMDS command 
where command is any of the following: 
CREATE_PROJECT, LIST_PROJECT, MAKEME, MODIFY_PROJECT REMOVE_PROJECT, TIE, 
TIE_PROJECT, UNTIE, UNTIE_PROJECT 
  Command    Description 
  CREATE PROJECT 
             Creates a project and enters the project authorization mode of 
             SUPER. 
  DISPLAY PROJECT 
             Displays the various items of a project's authorization. 
  LIST PROJECT 
             Lists one or all of the logon ids for projects managed by a 
             project administrator or lists one or all project logon ids for 
             the system manager. 
  MAKEME 
             Allows a system manager or project administrator to perform SUPER 
             commands on behalf of a subordinate project administrator. 
  MODIFY PROJECT 
             Enters the project authorization mode to allow modification of an 
             existing project. 
  REMOVE PROJECT 
             Removes an existing project. 
  TIE 
             Attaches a logon user and any specified file management accounts 
             to an existing project. 
  TIE PROJECT 
             Attaches one project to another as a sub-project. 
  UNTIE 
             Removes a logon user and the associated file management accounts 
             from an existing project. 
  UNTIE PROJECT 
             Removes a specified sub-project from a project. 
00001
00001
00002
00002
00003
00003
00004
00005
00005
00006
00006
00007
00008
00008
00009
00010
00010
A list of project options can be accessed by typing a ? or a ?? after this 
message.  To obtain definitions of individual options, type 
HELP (SUPER) PROJECT_OPTS option 
where option is any of the following: 
ACCOUNTS, ACHARGES, ADMINISTRATOR, DEFAULT, MCHARGES, PACKSET, PROJECTS, 
REMOVE_PACKSET 
  Option    Description 
  AC[COUNTS] = decimal 
            Specifies the maximum number of logon accounts that can be 
            authorized in the project.  The decimal value specified is the 
            maximum number of logon accounts that can be authorized in the 
            project.  If ACCOUNTS is not specified, the default is 0. 
  ACH[ARGES] = curmon 
            Specifies the accumulated charges for a project.  curmon is the 
            value, in dollars and cents, of the project's current accumulated 
            charges (for example, ACH=2560.88). 
  AD[MINISTRATOR] 
            Defines the logon account for the project administrator of the 
            project.  Specifying this option causes SUPER to enter the user 
            authorization mode.  Any of the user authorization options can 
            then be specified.  A list of these options and their definitions 
            can be accessed by typing HELP (SUPER) USER_OPTS.  If the 
            ADMINISTRATOR option is not specified, the project administrator 
            will be defined from the default project authorization record. 
  DE[FAULT] 
            Defines the default record (which specifies all the options that a 
            user can have) for users created in this project by the project 
            administrator.  Specifying this option causes SUPER to enter the 
            user authorization option mode.  Any of the user authorization 
            options, with the exception of the FACCOUNT option, can then be 
            specified.  A list of these options and their definitions can be 
            accessed by typing HELP (SUPER) USER_OPTS.  The record built by 
            these options will serve as the default record for users created 
            by the project administrator, in place of the global DEFAULT 
            record.  Also, no user in the project may be authorized privileges 
            or limits by the project administrator that exceed those specified 
            for this default record.  If the DEFAULT option is not specified, 
            then the default will be defined from the default project 
            authorization record. 
  MC[HARGES[ = {[sign]monval|NONE} 
            Specifies the maximum dollar amount that this logon ID is allowed 
            to accumulate.  It is a cumulative maximum that holds through 
            multiple logon attempts. 
            monval is specified in dollar and cents (with a decimal point) or 
            just dollars (with no decimal point).  If monval is not preceded 
            by a sign (+ or -), the value specified is an absolute value.  If 
            monval is preceded by a sign, the value specified is added or 
            subtracted from the current or default MCHARGES value, NONE 
            specifies there is no maximum limit on this user.  The default is 
            NONE. 
  PA[CKSET] = [DP#]setname 
            Specifies a packset for the project's file management accounts. 
            setname is the 1-6 character packset name.  At least one PACKSET 
            option must be specified to define the default home packset for 
            users in the project (i.e., for the packset specified on the HSET 
            option for the default record).  Multiple PACKSET options are 
            allowed. 
            The PACKSET option mode will then be entered and any of the 
            suboptions described under HELP (SUPER) PACKSET_SUBOPTS may be 
            specified. 
  PROJ[ECTS] = decimal 
            Specifies the maximum number of subprojects a project may contain. 
            The decimal value is the maximum number of projects that can be 
            created.  The default is 0. 
  R[EMOVE] PA[CKSET] = [DP#]psn 
            Removes the specified packset from a project. 
00001
00002
00003
00004
00005
00006
00007
00008
00008
PROJECT_OPTIONS
REMOVE
STATION
SUPER creates several files in :SYS; these files are :FORM, :HLP, :PRO, :PROJ, 
:USERS and :WSN. 
Note: These files always appear to be busy, and are therefore not saved via 
EFT.  Instead, these files can be backed up on tape using the PCL processor. 
For instance, to save :USERS.:SYS, use 
    C :USERS.:SYS(SHARE) TO LT#SAVE/:USERS 
and to restore that file, use 
    C LT#SAVE/:USERS INTO :USERS.:SYS(SHARE) 
Format: 
R[EMOVE] [.]account, name [(FA[CCOUNT])] 
Parameters: 
account, name    specifies a user account.  The account is limited to 8 
characters, the name to 12.  The valid character set consists of alphanumeric 
characters plus the characters $ and :.  Wildcarding is also allowed (e.g., 
R[EMOVE] DCR?, ?REICHART). 
FACCOUNT    requests deletion of the specified file management account. 
Description: 
This command removes an existing user authorization and optionally removes the 
file management account specified by account.  If files exist in the specified 
file management account, the PIG processor will prompt whether granules are to 
be removed.  If the response is Y (for YES), the file management account will 
be removed when the next RECONSTRUCT is performed as part of packset 
maintenance. 
CAUTION:  Be advised that a REMOVE command of the form: 
    REMOVE ?,? 
removes all users without a request for conformation. 
00002
00001
Format: 
R[EMOVE] CHAR[SET] charsetname 
Parameters: 
charsetname    is the one to eight character name of the CHARSET record to be 
REMOVEd.  The charsetname can be a combination of alphabetic characters, 
numeric characters and the special characters: colon (:), dollar sign ($), and 
asterisk (*). 
Description: 
The REMOVE CHARSET command is used to remove the specified CHARSET record from 
the :FORM file. 
00002
00001
REMOVE_COMMANDS
See the following topics: 
HELP (SUPER) CONSOLE, CONTROLLER, DEVICE, DEVICE_FOR_LINE, DEVICE_FOR_LINK, 
LINE, LINK, PROFILE, REMOVE, REMOVE_CHARSET, REMOVE_FORM, REMOVE_PROJECT, 
REMOVE_USER, STATION, TERMINAL, VIRTUAL_CIRCUIT, WSN. 
Format: 
R[EMOVE] FOR[M] formname 
Parameters: 
formname    is the name of the form to be REMOVEd.  The formname can be a 
combination of alphabetic characters, numeric characters and the special 
characters:  colon (:), dollar sign ($) and asterisk (*).  The formname can be 
wildcarded with the ? character. 
Description 
The REMOVE FORM command is used to remove one or a group of line-oriented, 
graphic or pseudo form records from the :FORM file. 
Be advised that a REMOVE FORM command of the form: 
    REMOVE FORM ? 
removes all forms without a request for confirmation.  The three 
system-maintained forms STDLP, STDGR and STD** are rebuilt. 
00002
00001
Format: 
R[EMOVE] PROJ[ECT] [.]account, name [(FA[CCOUNT])] 
Parameters: 
account, name    is the logon ID for the project administrator of the project 
being removed.  The account is limited to 8 characters, the name to 12.  The 
valid character set consists of the alphanumeric characters plus the 
characters $ and :.  Note that wildcarding is allowed (e.g., REMOVE PROJECT 
?HOST ). 
FACCOUNT    specifies that the file management accounts for the project are to 
be deleted. 
Description: 
This command deletes an existing project. 
00002
00001
REMOVE
REMOVE_CHARSET
REMOVE_FORM
REMOVE_PROJECT
Format: 
{C[REATE]} STA[TION] sname 
{R[EMOVE]} 
or 
D[ISPLAY] {[ALL] STA[TIONS]} [(JCL)] 
          {STA[TION] sname } 
or 
L[IST] {[ALL] STA[TIONS]} 
       {STA[TION] sname } 
or 
RECON[FIGURE] STAT[ION] {sname} 
                        {LOCAL} 
Parameters: 
sname    is the 1-8 character name of the station to be created or removed. 
If station sname exists on a CREATE, the command is ignored.  When a station 
is removed, all associated devices, consoles and WSNs are also removed.  If 
sname is not specified on the LIST or DISPLAY command, all stations and 
terminals are listed or displayed.  If the LIST or DISPLAY form of the command 
is used, sname can be wildcarded. 
Description: 
The CREATE STATION and REMOVE STATION commands are used to create and remove 
stations which serve to associate devices, consoles and workstations.  The 
LIST STATION command lists currently defined stations and the DISPLAY STATION 
command shows station definitions. 
SUPER maintains stations in the file :HLP.:SYS.  One station named LOCAL is 
automatically generated when the file is created, to allow the WSN LOCAL to 
describe central site devices.  If the WSN option is used in TIGR, (see HELP 
(TIGR) CONSOLE) other stations are generated to describe sets of central site 
devices. 
The LIST STATION command lists the name data for selected stations.  Including 
sname in the LIST STATION command is useful when wildcarding is used or to 
verify the existence of a station definition. 
The DISPLAY STATION command shows a columnized display of the options for 
selected stations (or all stations if the ALL option is specified), prefaced 
by a header consisting of the station information as entered in a CREATE or 
MODIFY STATION command.  The JCL option causes the command keyword CREATE to 
be written at the beginning of each station definition and the END keyword is 
inserted where needed. 
The RECONFIGURE STATION LOCAL command recreates the central site station LOCAL 
and central site workstation LOCAL.  RECONFIGURE STATION LOCAL is used to 
reconfigure the central site station and workstation without having to 
reconfigure the entire system. 
RECONFIGURE STATION sname defines the IOM-connected devices for the specified 
station if it is a TIGR-defined station.  When the RECONFIGURE STATION sname 
command is issued, all consoles and devices that are not IOM-connected and 
belong to this station must be redefined. 
When the RECONFIGURE STATION command is issued, reconfiguration must be 
confirmed (via YES$).  For example: 
   CMD*RECON STAT LOCAL 
   Reconfiguration station LOCAL will remove STATION and WSN LOCAL and 
   then rebuild them with only the IOM connected devices.  Are you sure 
   you want to do this? 
   Go For It?  YES$ 
     Station LOCAL removed. 
    WSN LOCAL removed. 
    (The removed consoles and devices are listed.) 
   Station LOCAL has been recreated. 
   WSN LOCAL has been recreated from the new STATION LOCAL. 
00002
00001
TIE
Format: 
C[REATE] TERM[INAL] tname type [FOR STAT[ION] sname] 
or 
M[ODIFY] TERM[INAL] tname [type] [FOR STAT[ION] sname] 
or 
R[EMOVE] TERM[INAL] tname [FOR STAT[ION] sname] 
or 
D[ELETE] TERM[INAL] 
or 
D[ISPLAY] {[ALL] TER[MINALS] [FOR STA[TION] sname]} [(JCL)] 
          {TER[MINAL] tname [FOR STA[TION] sname] } 
or 
L[IST] {[ALL] TER[MINALS] [FOR STA[TION] sname]} 
       {TER[MINAL] tname [FOR STA[TION] sname] } 
Parameters: 
tname    is the 1-8 character name of the terminal to be created, modified or 
removed.  If the MODIFY form of the command is used and a terminal does not 
exist, it is created.  If tname and the FOR clause are not specified in a LIST 
TERMINAL command, all terminals are listed.  If tname is not specified but the 
FOR clause is specified in a LIST TERMINAL command, all terminals for the 
specified station are listed.  If the LIST or DISPLAY form of the command is 
used, tname can be wildcarded. 
type    is one of the following values that specifies the type of terminal 
being described: 
    IRBT 
    2780 
    3780 
sname    is the 1-8 character name of a station with which the terminal will 
be associated.  If the FOR clause is not specified in the CREATE or MODIFY 
command, the default is LOCAL.  If the LIST or DISPLAY form of the command is 
used, sname can be wildcarded. 
Description: 
The CREATE and MODIFY TERMINAL commands are used to create and modify terminal 
definitions.  The LIST TERMINAL command is used to list currently defined 
terminals and the DISPLAY TERMINAL command is used to show terminal 
definitions. 
The LIST TERMINAL command lists the name data for terminals.  Including tname 
in the LIST TERMINAL command is useful when wildcarding is used or to verify 
the existence of a terminal definition. 
The DISPLAY TERMINAL command shows a columnized display of the options for 
selected terminals (or all terminals if the ALL option is specified), prefaced 
by a header consisting of the terminal information as entered in a CREATE or 
MODIFY TERMINAL command.  The JCL option causes the command keyword CREATE to 
be written at the beginning of each terminal definition and the keyword END to 
be inserted where needed. 
The REMOVE TERMINAL command is used to remove one terminal definition.  The 
DELETE TERMINAL command is used to delete all terminal definitions (except 
system-built ones), and should be used with caution.  SUPER attempts to 
protect users from inadvertently deleting all terminals by requiring 
confirmation before a DELETE TERMINAL command is executed.  When the command 
DELETE TERMINAL is issued, SUPER prompts: 
    Delete all TERMINALS ? 
The value YES$ must be supplied or the deletion request is cancelled. 
SUPER prompts for options when it encounters a CREATE or MODIFY TERMINAL 
command.  The options are listed in HELP (SUPER) TERMINAL_OPTS. 
00002
00001
A list of TERMINAL command options and their definitions can be accessed by 
typing a ? or ??.  To access individual options, type: 
HELP (SUPER) TERMINAL_OPTS option 
where option is any of the following: 
CONSOLE, DEVCTL, DEVICE, DEVNUM, GJOB, MODIFY, PASSWORD, PROFILE, REMOTE, 
SDNUM, SLAVE 
  Option    Description 
  CO[NSOLE] 
            Causes SUPER to prompt for suboptions describing a console built 
            into the terminal.  Multiple console options are allowed.  See the 
            CREATE CONSOLE command for a description of the suboptions.  If a 
            value for the PROFILE suboption is not specified, the default for 
            a console is type OC (e.g., IRBTOC) and the PASSWORD option is 
            illegal. 
  DEVC[TL]=hex 
            The hexadecimal value is a constant specifying the susbit value 
            for a HASP device.  hex is a quoted string of up to 4 hex 
            characters (16 bits of data).  The default is based on the 
            terminal type concatenated with the device type.  If one of the 
            special DEVNUM mnemonics is specified, DEVCTL and DEVNUM will be 
            set at the same time.  If a DEVNUM mnemonic is specified after a 
            DEVCTL value has been supplied, the DEVCTL option will be 
            overridden (see DEVNUM_OPTS). 
  DE[VICE] 
            Causes SUPER to prompt for suboptions describing a device (e.g., 
            LP, CP) built into the terminal.  Multiple device commands are 
            allowed.  See the CREATE DEVICE command for a description of the 
            suboptions.  One of these, TYPE=dd, defines the type of device 
            such that PROFILE defaults to (terminal) "typedd" (e.g., IRBTLP or 
            2780CP) for USE = IN or OUT.  For USE = CG, RESOURCE, or TP, 
            PROFILE must be specified.  It is highly recommended that the 
            SNAME option be specified in these cases.  The DEVICE suboption 
            PASSWORD cannot be specified. 
  DEVN[UM]={2780LP|2780CR|2780CP|3780LP|3780CR|3780CP|HASPOC|HASPLP| 
  HASPCR|HASPCP|HASPLP2|HASPLP3|IBMCR|hex} 
            DEVNUM is the device number of an RBTD device.  It may be entered 
            as a two-character hex number or as an alphanumeric mnemonic from 
            the list shown above.  If it is entered as a mnemonic, the 
            mnemonic is translated by the CP-6 system into a hex value as 
            shown in DEVNUM_OPS.  If the device is an IRB, the hex value of 
            DEVNUM is equivalent to the HASP IRBT RCB4 (record control byte) 
            for the device.  Entry of certain mnemonics for DEVNUM will also 
            cause the CP-6 system to set values for the SDNUM and DEVCTL 
            options.  See DEVNUM_OPS.  The default is based on the terminal 
            type concatenated with the device type. 
  GJOB = {NONE|name, account[ , password] CMD = 'command'} 
            Specifies the ghost job that is to be started when the terminal 
            connects or that the current ghost job is to be removed. 
            NONE specifies that the current GJOB definition is to be removed. 
            name, account[, password] specifies that a ghost job is to be 
            started when the terminal connects and specifies the user logon of 
            the ghost job. 
            command specifies the IBEX command executed when the ghost job 
            starts. 
  M[ODIFY] dduu 
            Causes SUPER to prompt for suboptions to modify a defined console 
            or device.  This option is only useful with the MODIFY TERMINAL 
            command.  The dd parameter specifies the type of device discussed 
            under DEVICE above (and is specified as OC for consoles), and uu 
            is the unit number of the device assigned sequentially when the 
            device or console is defined.  Thus, the first console is OC01, 
            the second is OC02, and so on. 
  PA[SSWORD] = {NONE|password} 
            Specifies this terminal's logon password.  The default is NONE. 
  PR[OFILE] = pname 
            Specifies the default RBT profile for this terminal as a whole. 
            If pname is specified, it must be defined, and defined as a RBT 
            terminal profile.  If no PROFILE is specified, the default used 
            depends on the type of terminal as follows: 
            Terminal Type      Default Profile Used 
            -------------      -------------------- 
            IRBT               STDHASP (Standard HASP) 
            2780               STD2780 
            3780               STD3780 
  R[EMOTE] L[OGON] S[TRING][={NONE|text}] 
            This option must be the last option on an input line.  'text' is a 
            character string which will be sent to a remote master site in 
            order to identify the CP-6 system as a HASP terminal.  The default 
            is NONE. 
  SD[NUM]=hex 
            The hexadecimal value is a constant or hexadecimal 4 character 
            quoted string (up to 16 bits).  This value specifies the HASP 
            record control byte for operator-console input if DEVNUM has 
            specified the value for output to an operator console. 
  SLAVE[={Y[ES]|N[O]}] 
            YES specifies that the CP-6 system is to send the initial bid and 
            possibly the logon string for the line.  This option is valid only 
            for PROTYP=HASP.  It is ignored for PROTYP=3780 or 2780.  The 
            default is NO. 
00001
00003
00002
00003
00004
00005
00006
00007
00008
00009
00009
00010
00011
TERMINAL_OPTIONS
Format: 
T[IE] [.]account1, name1 TO [.]account2, name2 [FA[CCOUNT][=facctlist]] 
Parameters: 
account1, name1    identifies a user logon.  The account is limited to 8 
characters, the name to 12.  The valid character set consists of the 
alphanumeric characters plus the characters $ and :. 
account2, name2    identifies an existing project. 
facctlist    is a list of file management accounts, of the form 
[[DP]#psn.]acct, that are associated with the user and are to be included in 
the project.  If FACCOUNT is specified, but a list of accounts is not given, 
SUPER assumes the account is the specified account on the home packset. 
Description: 
This command attaches a logon user, and any specified file management 
accounts, to an existing project. 
00002
00001
Format: 
T[IE] PROJ[ECT] [.]account1, name1 TO [.]account2, name2 
Parameters: 
account1, name1    identifies an existing project that is to become a 
sub-project.  The account is limited to 8 characters, the name to 12.  The 
valid character set consists of the alphanumeric characters plus the 
characters $ and :. 
account2, name2    identifies an existing project. 
Description: 
This command attaches one project to another project as a sub-project. 
00002
00001
A list of timing profile options and their definitions can be accessed by 
typing a ? or ??.  To access individual options, type: 
HELP (SUPER) TIMING_PROFILE_OPTS option 
where option is any of the following: 
BS_TIM, DVCFLWCTRALG, DVCOTPBFRSIZ, ERSTIM, TIMAFTCTRFNC, TMNALG_AFTCUP, 
TMNALG_AFTCR, TMNALG_AFTHPA, TMNALG_AFTHT, TMNALG_AFTLF, TMNALG_BFRCR, 
TMNALG_BFRLF, TMNALG_FILCHR, TMNALG_PRM1, TMNALG_PRM2, TMNALG_PRM3, 
TMNALG_PRM4, TMNALG_PRM5, TMNALG_PRM6, TMNALG_PRM7, and TMNALG_PRM8. 
  Option                       Description                           Device 
BS_TIM=real                 Specifies the amount of time fill      ASYNC 
                            (in milliseconds) required after       POLLVIP 
                            a backspace.  The default is 0.0. 
DVCFLW[CTRALG]={0|ENQ[ACK]|1|ETX[ACK]|2|DC1[DC3|3|D[C]]} 
                            Determines flow of data to a           ASYNC 
                            device with an internal output 
                            buffer.  The following values 
                            can be assigned: 
                            Value       Meaning 
                            {0|NONE}    Used as reset value. 
                            {1|ENQACK}  The computer sends ENQ; 
                                        the device responds 
                                        with an ACK. 
                            {2|ETXACK}  The computer sends 
                                        ETX; the device responds 
                                        with an ACK. 
                            {3|DC1DC3}  The device sends a DC1 
                                        to resume output and a 
                                        DC3 to halt output. 
DVCOTPB[FRSIZ]=value        Specifies the size (in bytes) of       ASYNC 
                            the output buffer internal to the      POLLVIP 
                            device.  The range is 0-4096.  The     3270 
                            default is 0. 
ERSTIM=real                 Specifies the amount of time fill      ASYNC 
                            (in milliseconds) after an ED0 or      POLLVIP 
                            ED2.  The default is 0.0. 
TIMAFTCT[RFNC]=real         Specifies the amount of time fill      ASYNC 
                            after a control function other         POLLVIP 
                            than ED0 or ED2.  The real value 
                            represents milliseconds, e.g., 1.5 
                            is one and one half milliseconds. 
                            The default is 0.0. 
TMNALG_AFTCR=value          Specifies a value (0-3) that           ASYNC 
                            identifies which of the following      POLLVIP 
                            timing algorithms to use 
                            following a carriage return: 
                            0  No timing fill requested.  This 
                               is the default. 
                            1  Used after horizontal movement 
                               on terminals with moving 
                               carriages and on CRT's at high 
                               speeds. 
                               TIME = (TMNALG_PRM1 X 
                               MOVEMENT-IN-COLUMNS) + 
                               TMNALG_PRM2 
                               If the time computed is less 
                               than the cross-over point 
                               (TMNALG_PRM3) then the time is 
                               re-computed with:  TIME = 
                               (TMNALG_PRM4 X SQUARE-ROOT 
                               (10 * MOVEMENT-IN-COLUMNS)) 
                               + TMNALG_PRM5 
                            2  Used after a line feed on 
                               terminals with moving 
                               carriages and on CRT's at 
                               high speeds. 
                               TIME = (TMNALG_PRM6 X 
                               MOVEMENT-IN-LINES) + 
                               TMNALG_PRM7 
                            3  Used before a line feed on 
                               belt and chain printers. 
                               TIME = TMNALG_PRM8 - 
                               (TIME SINCE LAST LINE FEED) 
                               If time is less than or equal 
                               to 0, then no fill is 
                               generated. 
                               If (TIME SINCE LAST LINE 
                               FEED) is 0, then no fill 
                               is generated. 
TMNALG_AFTCUP=value         Specifies a value (0-3) that           ASYNC 
                            identifies which timing algorithm      POLLVIP 
                            (see TMNALG_ATTCR) to use after 
                            a CUP.  The default is 0. 
TMNALG_AFTHPA=value         Specifies a value (0-3) that           ASYNC 
                            identifies which timing algorithm      POLLVIP 
                            (see TMNALG_AFTCR) to use after an 
                            HPA (see HPA_ALG). 
TMNALG_AFTHT=value          Specifies a value (0-3) that           ASYNC 
                            identifies which timing algorithm      POLLVIP 
                            (see TMNALG_AFTCR) to use after a 
                            tab.  The default is 0. 
TMNALG_AFTLF=value          Specifies a value (0-3) that           ASYNC 
                            identifies which timing algorithm      POLLVIP 
                            (see TMNALG_AFTCR) to use after a 
                            line feed.  The default is 0. 
TMNALG_BFRCR=value          Specifies a value (0-3) that           ASYNC 
                            identifies which timing algorithm      POLLVIP 
                            (see TMNALG_AFTCR) to use before a 
                            carriage return.  The default is 0. 
TMNALG_BFRLF=value          Specifies a value (0-3) that           ASYNC 
                            identifies which timing algorithm      POLLVIP 
                            (see TMNALG_AFTCR) to use before a 
                            line feed.  The default is 0. 
TMNALG_FILCHR=hex           Specifies a fill character to be       ASYNC 
                            used for terminals that are            POLLVIP 
                            sensitive to the DEL that is sent 
                            out.  The default is X'F'. 
TMNALG_PRM1=real            Specifies a value (0-3276.7) for       ASYNC 
                            the TMNALG_PRM1 timing algorithm       POLLVIP 
                            parameter in milliseconds.  The 
                            default is X'0.0'. 
TMNALG_PRM2=real            Specifies a value (0-3276.7) for       ASYNC 
                            the TMNALG_PRM2 timing algorithm       POLLVIP 
                            parameter in milliseconds.  The 
                            default is X'0.0'. 
TMNALG_PRM3=real            Specifies a value (0-3276.7) for       ASYNC 
                            the TMNALG_PRM3 timing algorithm       POLLVIP 
                            parameter in milliseconds.  The 
                            default is X'0.0'. 
TMNALG_PRM4=real            Specifies a value (0-3276.7) for       ASYNC 
                            the TMNALG_PRM4 timing algorithm       POLLVIP 
                            parameter in milliseconds.  The 
                            default is X'0.0'. 
TMNALG_PRM5=real            Specifies a value (0-3276.7) for       ASYNC 
                            the TMNALG_PRM5 timing algorithm       POLLVIP 
                            parameter in milliseconds.  The 
                            default is X'0.0'. 
TMNALG_PRM6=real            Specifies a value (0-3276.7) for       ASYNC 
                            the TMNALG_PRM6 timing algorithm       POLLVIP 
                            parameter in milliseconds.  The 
                            default is X'0.0'. 
TMNALG_PRM7=real            Specifies a value (0-3276.7) for       ASYNC 
                            the TMNALG_PRM7 timing algorithm       POLLVIP 
                            parameter in milliseconds.  The 
                            default is X'0.0'. 
TMNALG_PRM8=real            Specifies a value (0-3276.7) for       ASYNC 
                            the TMNALG_PRM8 timing algorithm       POLLVIP 
                            parameter in milliseconds.  The 
                            default is X'0.0'. 
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
TIMING_PROFILE_OPTIONS
DEVICE
TIE_PROJECT
Format: 
U[NTIE] [.]account, name [FA[CCOUNT][=facctlist] 
Parameters: 
account, name    identifies a user logon.  The account is limited to 8 
characters, the name to 12.  The valid character set consists of the 
alphanumeric characters plus the characters $ and :. 
facctlist    is a list of file management accounts, of the form 
[[DP]#psn.]acct, that are associated with the user and are to be removed from 
the project.  If FACCOUNT is specified but a list of accounts is not given, 
SUPER assumes the account is the specified account on the home packset. 
Description: 
This command removes a user logon and any specified file management accounts 
from a project, and makes the project a user administered by the system 
manager. 
00002
00001
Format: 
U[NTIE] PROJ[ECT] [.]account, name 
Parameters: 
account, name    identifies an existing project.  The account is limited to 8 
characters, the name to 12.  The valid character set consists of the 
alphanumeric characters plus the characters $ and :. 
Description: 
This command removes a sub-project from a project and makes the sub-project a 
project administered by the system manager. 
00002
00001
USER_COMMANDS
A list of user authorization commands and their definitions can be accessed by 
typing a ? or a ?? after this message.  To obtain definitions of individual 
user authorization commands, type 
HELP (SUPER) USER_CMDS command 
where command is any of the following: CREATE, CREATE_USERS, DELETE_USERS, 
DISPLAY, DISPLAY_USERS, LIST, LIST_USERS, MODIFY, MODIFY_USERS and REMOVE or 
REMOVE_USER. 
  Command    Description 
  CREATE 
             Invokes the user authorization mode of SUPER. 
  DELETE USERS 
             Deletes all and rebuilds default user definitions. 
  DISPLAY 
             Displays user authorization information. 
  LIST 
             Lists user logon ids. 
  MODIFY 
             Alters an existing authorization. 
  REMOVE 
             Removes an existing authorization. 
00001
00003
00002
00003
00004
00005
00006
A list of user authorization options can be accessed by typing a ? or a ?? 
after this message.  To obtain definitions of individual options, type 
HELP (SUPER) USER_OPTS option 
where  option is any of the following: 
ACCESS, ACCOUNT_OWNER, BANNERTEXT, BATNUM, BILLING, BUDGET, CPROC, EXPIRE, 
FACCOUNT, FEBILLING, FEDBACCN, FEMACCTMEM, FEMFPRG, FEMINTS, FEMMEMORY, 
FEMTIME, FEPPRIVILEGE, FEPRIVILEGE, FEPSEUDO, FERESOURCES, FESTEPACCNT, 
FORCE_SETUP, HSET, KEY, LAST_CPROC, LASTLOGON, MAXENQ, MEMORY, NATIVEL, 
OUTPUTPRIO, PASSWORD, PPRIVILEGE, PRIOB, PRIVILEGE, PROFILE, PSEUDO, QUAN, 
RESOURCES, S_ACCOUNTING, SERVICES, SETUP, STEPACCNT, TIME, WSN 
  Options    Description 
  AC[CESS] mode[={Y[ES]|N[O]}][,mode[={Y[ES]|N[O]}]] ... 
             Specifies the modes that may be used by this user. 
             mode is one of the following: 
             B    indicates batch access. 
             FE    indicates front end processing access. 
             G    indicates ghost access. 
             O    indicates on-line access. 
             T    indicates transaction processing access. 
             YES    indicates this mode of access is permitted. 
             NO    indicates access in this mode is to be denied.  If only 
             mode is specified, YES is assumed. 
  ACCOU[NT_OWNER] = string 
             Contains any text string useful to the administrator of the 
             account.  string is 0 to 80 ASCII characters.  If string is null, 
             the current contents of the text field will be deleted.  The 
             string, stored as BANNERTEXT 0, is neither used nor recognized 
             within the CP-6 system except as it may be useful to the 
             administrator of the account.  If the X account program GOAT is 
             used to display accounts, ACCOUNT_OWNER is displayed as the OWNER 
             BY: field. 
  BANNERTEXTn={'[string]'[,user_alterable]|user_alterable} 
             Specifies the text of a user banner field and/or the alterable 
             attribute of the text in the field, where: 
             n    is a numeric value, 1 through 9, that identifies the user 
             text field. 
             'string'    is 0 to 80 ASCII printable characters that are the 
             text for the field.  If string is null, the current contents of 
             the text field will be deleted. 
             user_alterable    is either: 
             A[LTERABLE]    specifies that the user can modify the contents of 
             the text field (via the IBEX command LET).  ALTERABLE is the 
             default. 
             U[NALTERABLE]    specifies that the user cannot modify the 
             contents of the text field. 
  BA[TNUM] = value 
             Specifies the maximum number of batch jobs the account can have 
             in the batch input queue at any one time.  If this option is not 
             specified, there is no maximum limit. 
             value defines the largest number of batch jobs this user may have 
             in the queue at any one time. 
             Note:  This capability is currently not available in the system. 
  BI[LLING] mode=schedule[, mode=schedule] ... 
             Specifies the rate schedule that is to be used to determine the 
             user's charges; the rate schedules are created by the RATES 
             processor described under HELP (RATES) TOPICS.  Note that the 
             rates schedule cannot be changed by the project administrator. 
             (The schedule can be changed only by the system manager.) 
             mode is one of the following: 
             B    indicates the batch rate schedule. 
             G    indicates the ghost rate schedule. 
             O    indicates the on-line rate schedule. 
             T    indicates the transaction processing rate schedule. 
             The schedule is the six-character name of the rate schedule built 
             by the RATES processor. 
  BU[DGET] 
             Indicates that the system manager wishes to enter the sub-option 
             mode to specify items related to this user's budget.  See HELP 
             (SUPER) BUDGET_SUBOPTS for a description of the BUDGET 
             suboptions. 
  CP[ROC] mode=cpname[, mode=cpname] ... 
             Identifies the command program the user is to be associated with 
             when he logs on. 
             mode is B (batch), G (ghost), O (on-line), or T (transaction 
             processing). 
             cpname is the name of the command program or NONE.  IBEX is the 
             default for all modes. 
             Note:  For users running TP as supplied by Bull, the default 
             should always be used. 
  EX[PIRE] {MAX|DEF} = {NEVER|days} 
             Specifies the period of time the user's files may be retained in 
             a non-expired state. 
             MAX defines the following parameter as the largest period of time 
             this user may specify. 
             DEF defines the following parameter as the default non-expiration 
             period for this user's files. 
             days specifies the expiration period.  The longest value 
             permitted is 10922 days. 
             NEVER indicates that files built by this user will never expire. 
  FA[CCOUNT] 
             Allows the creator of a logon account to create a matching file 
             management account without running PIG as a separate process. 
             Having entered the FACCOUNT sub-option mode, any of the attribute 
             options valid for the PIG CREATE or MODIFY commands (see HELP 
             (PIG) CREATE or HELP (PIG) MODIFY) may be entered separated by 
             commas.  A blank line ends the entry. 
  FEBI[LLING] femode=schedule[, femode=schedule] ... 
             Specifies the rate schedule that is to be used to determine the 
             FEP user's charges.  (The rate schedules are created by the RATES 
             processor.) 
             femode is one of the following:  C (the comgroup connected rate 
             schedule), G (the ghost rate schedule), H (the handler rate 
             schedule), or U  (the user connected rate schedule). 
             schedule is the six-character name of the rate schedule built by 
             the RATES processor. 
  FEDB[ACCN] = dbacct-name 
             Specifies the account which is to be granted debug access to 
             FPRGs running under this user's account.  FEDBACCN may be 
             wild-carded. 
             dbacct-name is a 8-character debug account name. 
  FEMA[CCTMEM] = num 
             Specifies the maximum amount of memory (in increments of FEP 
             pages) all users with this account may request from the system. 
             num is a maximum amount (0-9999) of account memory.  The default 
             is 9999. 
  FEMF[PRG] = num 
             Specifies the maximum number of user FPRG slots that may be used 
             by all users with this account at any one time. 
             num is the maximum number (0-99) of FPRGS.  The default is 0. 
  FEMI[NTS] femode=max-num[,femode=max-num] ... 
             Specifies the maximum number of FEP hardware interrupts available 
             to this user.  (Refer to the description of the M$INTCON monitor 
             service in the CP-6 FEP Monitor Services Reference Manual 
             (CE66).) 
             femode is one of the following:  C (comgroup connected), G 
             (ghost), H (handler), or U (user connected). 
             max-num is a maximum number (0-48) of interrupts allowed.  The 
             default is 0. 
  FEMME[MORY] femode=value[, femode=value] ... 
             Specifies the maximum amount of memory (in 256 word increments or 
             FEP pages) this user may request from the system.  If FEMMEMORY 
             is not specified, the default is 128 for each mode. 
             femode is one of the following: C (comgroup connected), G 
             (ghost), H (handler), or U (user connected). 
             value specifies the number of memory pages to be used as the 
             relevant limit. 
  FEMTI[ME] femode=value[, femode=value] ... 
             Specifies the maximum value for CPU-time that this FEP user may 
             have.  If FEMTIME is not specified, the default is 9999 for each 
             mode. 
             femode is one of the following: C (comgroup connected), G 
             (ghost), H (handler), or U (user connected). 
             value is the decimal number of minutes to be used as the limit. 
  FEPP[RIVILEGE] 
             Grants the FEP user the capability to use the system maintenance 
             and control processors. 
             Specifying FEPPRIVILEGE initiates the FEPPRIVILEGE sub-option 
             mode.  The format of all sub-options is of the form: 
             fepprivname femode [={Y[ES]}] [, femode [={Y[ES]}]] 
                                [ {N[O] }] [         [ {N[O] }]] ... 
             fepprivname is one of the processor authorizations described 
             under PPRIVILEGE. 
             femode is one of the following:  C (comgroup connected), G 
             (ghost), H (handler), or U (user connected).  Specifying the 
             femode only indicates a YES setting. 
             Note:  This capability is currently not available in the system. 
  FEPR[IVILEGE] 
             Permits specification of certain special privileges that grant 
             the FEP user capabilities not available to other FEP users. 
             Specifying FEPRIVILEGE initiates the FEPRIVILEGE suboption mode. 
             The format of all sub-options is of the form: 
             feprivname femode [={Y[ES}]  [, femode [={Y[ES]}]] 
                               [ {N[O]}]  [         [ {N[O] }]] ... 
             feprivname is one of the feprivileges described below. 
             femode is one of the following: C (comgroup connected), G 
             (ghost), H (handler), or U (user connected).  Specifying the 
             femode only indicates a YES setting. 
             The feprivileges that may be specified are: 
             CQ    allows the user to use the Circular Queue. 
             EXM[M]    allows the user to utilize a set of Extended 
             Memory Management services.  Management services, 
             M$CVM (read/write access), is the only one available to 
             date. 
             EXP[M]    allows the user to start and stop the monitor 
             performance monitor. 
             FMR[EAD]    allows the user to bypass all read only file 
             management security checks when using shared data 
             segments. 
             FMS[EC]    allows the user to bypass all of the file 
             management security checks when using shared data 
             segments. 
             GP[P]    allows the user to override the stealable page 
             limit and acquire physical memory pages. 
             IN[TCON]    allows the user to use the M$INTCON monitor 
             service. 
             MA[XM]    allows the user to allocate memory beyond his 
             authorized limit. 
             MS[YS]    allows the user to use the M$SYS monitor 
             service and to execute his interrupt processing routines 
             in Ring 1. 
             SCR[EECH]    allows the user to use M$SCREECH to dump 
             and reboot the front end. 
             SNAP    allows the user to use M$SCREECH to take a 
             snapshot dump. 
             SP[CLMM]    allows the user to utilize a set of SPeCiaL 
             Memory Management services.  M$CVM (read only access) is 
             the only one available to date. 
             SYSL[OG]    allows the user to use the M$WRSYSLOG monitor 
             service request. 
             TN[D]    allows the user to use the Test aNd Diagnostic 
             monitor service. 
  FEPS[EUDO] 
             Specifies the name and maximum number of FEP pseudo resources the 
             user may acquire.  The pseudo resources must be defined by the 
             NETCON processor.  (See HELP (NETCON) BOOT.) 
             Specifying FEPSEUDO will initiate a sub-option mode.  The format 
             of the sub-option is: 
             fepseudoname femode=value[, femode=value] ... 
             fepseudoname is the 1 to 8 character designation of the fepseudo 
             resource.  Up to 8 different fepseudo resources may be 
             authorized. 
             femode is one of the following: C (comgroup connected), G 
             (ghost), H (handler), or U (user connected). 
             value defines the largest number of this resource the user may 
             acquire. 
             Another form of the sub-option will delete the fepseudo 
             authorization from this user.  The format of the sub-option is: 
             fepseudoname R[EMOVE] 
  FERE[SOURCES] 
             Specifies the name and maximum number of the allocatable FEP 
             resources this user may acquire. 
             Specifying FERESOURCES will initiate sub-option mode.  Valid 
             sub-options are of the form: 
             feresname femode=value[, femode=value] ... 
             feresname is the 2-character designator of the FEP resource type. 
             These names represent the physical channels present on the FEP 
             and are defined via the CONFIG command of the NETCON processor 
             (see HELP topic CONFIG).  Up to 32 FERESOURCES may be authorized 
             per mode. 
             femode is one of the following: C (comgroup connected), G 
             (ghost), H (handler), or U (user connected). 
             value is the largest number of the specified resource this user 
             may acquire in the referenced mode. 
  FEST[EPACCNT] [={Y[ES]|N[O]}] 
             Indicates that an accounting record is to be written for this 
             user at the end of each FEP job step.  These records are in 
             addition to the accounting records generated at the end of every 
             FEP job.  YES means generate the FEP job step accounting records. 
             NO means do not generate these records.  The default is NO. 
  FORC[E_SETUP] mode={Y[ES]|N[O]}] 
             Specifies whether execution of a SETUP command is to be required 
             even if a user logs on specifying otherwise (via the NOSETUP (NS) 
             option). 
             mode is one of the following: 
             B    indicates batch execution of the SETUP command. 
             G    indicates ghost execution of the SETUP command. 
             O    indicates on-line execution of the SETUP command. 
             T    indicates transaction processing execution of the      SETUP 
             command. 
             YES    indicates execution of the SETUP command is forced.  If NS 
             is specified in the user logon string, it is ignored. 
             NO    indicates execution of the SETUP command is not forced.  If 
             NS is specified in the user logon string, it causes the SETUP 
             command to be bypassed. 
  HS[ET] = [DP#]setname 
             Specifies this logon ID's home packset.  The packset is defined 
             independently by the PIG processor.  Normally, the home packset 
             will contain this logon ID's file management account, also 
             specified by PIG and the FACCOUNT option. 
             The home packset is assumed as a resource for the user's batch 
             jobs.  The home packset is also assumed as the default packset 
             name for a file identifier, if the user attempts to access an 
             account that is not in the Master Account Directory. 
             setname is the 1-6 character packset identifier. 
  KEY = {ALL|NONE|keylist} 
             Establishes a set of keys that allow the user to access 
             restricted processors.  A restricted processor is a run unit that 
             is linked using the SLOCK or WLOCK option.  If the SLOCK option 
             was specified, the user can access the run unit only if he has a 
             key to match each of the locks specified for the run unit.  Note 
             that the project administrator cannot change the user keys. 
             (User keys can be changed only by the system administrator.)  If 
             the WLOCK option is specified, the user can access the run unit 
             if he has a key that matches any of the locks specified for the 
             run unit. 
             ALL specifies that all keys should be on. 
             NONE specifies that all keys should be off. 
             keylist is one or more of the following, separated by commas: 
             key [={YES|NO}] 
             where 
             key    is numbered between 1 and 72. 
  L[AST] CP[ROC] mode=cpname[, mode=cpname] 
             Identifies a command processor (installed by SPIDER) with which 
             the user is to be associated at log off time.  mode is B (batch), 
             G (ghost), O (on-line) or T (transaction processing).  cpname is 
             the name of the command processor or NONE.  NONE is the default 
             for all modes. 
  LASTLOG[ON] [TIME] = {date, time|time, date} 
             Specifies the last date and time the user logged on to the 
             system.  This value, updated and maintained by the system, can be 
             reset by the system manager. 
             date    is entered in the format mm/dd/yy. 
             time    is entered in the format hh:m[m:ss.tt]. 
  MA[XENQ] mode=n [,mode=n]... 
             Specifies by mode the maximum number of ENQ/DEQ requests to be 
             allowed for this user.  This value overrides the system default 
             (established by the CONTROL parameter MAXENQ).  The maximum 
             number is 2**18 -1.  The modes that can be specified are: 
                 B    indicates batch mode. 
                 G    indicates ghost mode. 
                 O    indicates on-line mode. 
                 T    indicates transaction processing mode. 
  ME[MORY] {M[AX]|D[EFAULT]} mode=value[, mode=value] ... 
             Specifies the maximum and default amounts of memory (in 1K-word 
             increments, that is, host pages) this user may request from the 
             system.  (The FPOOLS allocation obtained via the SUPER option 
             SERVICES is not constrained by this limit.) 
             mode is one of the following: B (batch), G (ghost), O (on-line) 
             or T (transaction processing). 
             MAX indicates the maximum values this user may request in each of 
             the specified modes. 
             DEFAULT indicates the following values are the defaults assumed 
             for the various modes if the user does not make an explicit 
             request. 
             value specifies the number of memory pages to be used as the 
             relevant limit. 
  NA[TIVEL] = {letter|NONE} 
             Permits the system manager to designate the language that will be 
             used for error messages while this user is logged on.  The 
             utility of this feature depends on the availability of an 
             appropriate foreign language error message file; the standard 
             CP-6 error message file is in English. 
             letter is the alphabetic-character used to identify the 
             foreign-language error message file.  Twenty-six different error 
             message file languages may be identified, but each user may have 
             only one. 
             NONE indicates that the standard CP-6 error message file is to be 
             used. 
  OU[TPUTPRIO] = value 
             Specifies the default priority for this user's output. 
             value is a decimal integer from 1 to 14 that represents the 
             default output queue priority for printing. 
  PA[SSWORD] = {password|NONE} 
             Specifies the password field of the logon ID.  User password 
             consists of 1 to 8 ASCII characters.  This option must appear 
             alone or as the last option when specifying multiple options. 
             NONE indicates that this logon ID does not include a password. 
  PP[RIVILEGE] 
             Grants the user the capability to use the system maintenance and 
             control processors.  These programs are described elsewhere in 
             this manual. 
             Specifying PPRIVILEGE will initiate the PPRIVILEGE sub-option 
             mode.  The format of all sub-options is of the form: 
             pprivname mode [={Y[ES]}] [, mode [={Y[ES]}]] 
                            [ {N[O] }] [       [ {N[O] }]] ... 
             where 
             pprivname is one of the processor authorizations described below. 
             mode is one of the following: B (batch), G (ghost), O (on-line) 
             or T (transaction processing).  Specifying the mode only 
             indicates a YES setting. 
             The processor authorizations that may be specified are: 
             CNTRLC    permits use of CONTROL to display and change system 
             control parameters. 
             CNTRLD    permits use of CONTROL to display (only) system control 
             parameters. 
             EF[T]    permits use of EFT for file maintenance activities. 
             EL    permits use of ELAN to examine the system's error log. 
             LA[BEL]    permits use of LABEL to initialize ANS tape volumes. 
             NETCON    permits use of NETCON to display an FEP (front-end 
             processor). 
             PADMIN    allows the use of the user and project authorization 
             function of SUPER.  The PADMIN PPRIVILEGE is given automatically 
             to project administrators by SUPER.  It cannot be given to a user 
             by a sub-option of the PPRIVILEGE option. 
             PIGC    permits use of PIG to create, modify, and display file 
             management packsets. 
             PIGD    permits use of PIG for display purposes only. 
             PIGETTE    permits use of the PIGETTE processor. 
             RATES    allows the use of RATES. 
             REPLAY    allows the user to run REPLAY. 
             SU[PER]    permits use of SUPER to create, modify, or display the 
             authorization information maintained by SUPER.  Specifying this 
             option is equivalent to specifying SUPERAUTH, SUPERFORM, and 
             SUPERWSN PPRIVILEGES. 
             SUPERA[UTH]    allows the use of the user and project 
             authorization functions of SUPER. 
             SUPERD    allows the use of SUPER LIST and DISPLAY commands. 
             SUPERF[ORM]    allows the use of the FORM definition function of 
             SUPER. 
             SUPERW[SN]    allows use of the CONSOLE, CONTROLLER, DEVICE, 
             LINE, LINK, PROFILE, STATION, TERMINAL, VIRTUAL CIRCUIT, and WSN 
             definition functions of SUPER. 
             SPIDERC    permits use of SPIDER to install, display, replace, or 
             remove shared processors. 
             SPIDERD    permits use of SPIDER for display purposes only. 
             SYSC[ON]    allows the user to run the SYSCON processor. 
             VOLINIT    allows the user to run VOLINIT. 
  PRIO[B] mode=value[, mode=value] ... 
             Specifies an execution priority relative to the default priority. 
             mode is one of the following: B (batch), G (ghost), O (on-line), 
             or T (transaction processing). 
             value ranges from -255 to +255 in units of priority units.  The 
             default is 0 to signify use of the default PRIOB value for the 
             given mode specified via CONTROL as PRIOB or PPRIO. 
  PRIV[ILEGE] 
             Permits specification of certain special privileges that grant 
             the user capabilities not available to other users.  Specifying 
             PRIVILEGE will initiate the PRIVILEGE sub-option mode.  The 
             format of all sub-options is of the form: 
             privname mode [={Y[ES]}] [, mode [={Y[ES]}]] 
                           [ {N[O] }] [       [ {N[O] }]] ... 
             where 
             privname is one of the privileges described below. 
             mode is one of the following: B (batch), G (ghost), O (on-line) 
             or T (transaction processing).  Specifying the mode only 
             indicates a YES setting. 
             The privileges that may be specified are: 
             AS[AVE]    permits the user's image to be saved automatically if 
             the terminal connection is lost.  Upon subsequent logon, the user 
             may reconnect to the saved image, picking up at the point of 
             disconnect. 
             CF[EP]    permits inspection of the contents of an FEP (front-end 
             processor). 
             DI[SPJOB]    permits user utilization of the M$JOBSTATS service 
             request to display other users jobs. 
             EXM[M]    permits user utilization of the M$CVM, M$SAD M$STLPP, 
             M$SMPRT, and M$SSC service requests to acquire read and write 
             access to any memory in the system. 
             EXP[M]    permits the user to start and stop the special 
             performance monitoring function. 
             FMD[IAG]    permits user access to packsets as unmanaged sets of 
             devices. 
             FMR[EAD]    permits user bypass of all the file management 
             security checks when reading only. 
             FMS[EC]    permits user bypass of all of the file management 
             security checks. 
             GP[P]    permits user override of the stealable-page limit and 
             acquire physical memory pages. 
             IOQ    permits use of the M$IOQ service request for reading only. 
             IOQW    permits the use of the M$IOQ service request for writing. 
             JI[T]    permits user modification of the JIT (Job Information 
             Table). 
             MA[XM]    permits user allocation of memory beyond the authorized 
             limit. 
             MF[EP]    permits user modification of the contents of an FEP 
             (front-end processor). 
             MS[YS]    permits the use of certain GOOSE features. 
             PM    permits the user to obtain performance monitor reports. 
             SP[CLMM]    permits the use of the M$CVM and M$SAD service 
             requests to acquire read access to any memory in the system. 
             SYSC[ON]    permits the use of the M$SYSCON service requests. 
             SYSL[OG]    permits the use of the M$WRSYSLOG service request. 
             TN[D]    permits the use of the test and diagnostic service 
             request. 
  PRO[FILE] = proname 
             Specifies the name of the terminal profile to be used when this 
             user logs on to a timesharing terminal. 
             proname is the 1 to 11 character name of a profile generated by 
             the CREATE PROFILE command.  The default is NONE.  (See HELP 
             (SUPER) PROFILE.) 
  PSEUDO 
             Specifies the name and maximum number of pseudo resources the 
             user may acquire.  The pseudo resources must be defined at boot 
             time with TIGR commands.  (See HELP (TIGR) MON.) 
             Specifying PSEUDO will initiate a sub-option mode.  The format of 
             the sub-option is: 
             pseudoname mode=value[, mode=value] 
             pseudoname is the 1 to 8 character designation of the pseudo 
             resource.  Up to 8 different pseudo resources may be authorized 
             per mode. 
             mode is one of the following: B (batch), O (on-line), G (ghost) 
             or T (transaction processing). 
             value defines the largest number of this resource the user may 
             acquire. 
             The following form of the sub-option will delete the pseudo 
             authorization from the user: 
             pseudoname R[EMOVE] 
  QU[AN] mode=value[, mode=value] ... 
             Specifies a change to the quantum of time to be assigned to an 
             execution period for this user's job for the specified mode. 
             mode is one of the following: B (batch), G (ghost), O (on-line), 
             or T (transaction processing). 
             value is either 0 or within the range -(20 to 2**35-1) to +(20 to 
             2**35-1) in units of milliseconds.  0 specifies use of the 
             default QUAN value for the given mode specified via CONTROL as 
             QUAN or PQUAN.  The default is 0. 
             If a positive or negative value is specified, the value will be 
             added to or subtracted from the CONTROL-set value resulting in a 
             larger or smaller QUANTUM for the user. 
  RE[SOURCES] 
             Specifies the name and maximum number of the allocatable system 
             resources this user may acquire. 
             Specifying RESOURCES will initiate a sub-option mode.  Valid 
             sub-options are of the form: 
             resname mode = value[, mode=value] ... 
             where 
             resname is the 2-character designation of the system resource 
             type.  These names represent the physical devices present on the 
             system and are defined at boot time with TIGR commands (see HELP 
             (TIGR) MON).  Standard resources include MT (tapes), DP (disk 
             packs), CP (card punch), and LP (line printer).  Up to 8 
             resources may be authorized per mode. 
             value is the largest number of the specified resource this user 
             may acquire in the referenced mode.  This value may not exceed 
             the project administrator's authorization. 
  *S_ACCOUNTING = {YES|NO} 
             Specifies whether or not :ACCTLG accounting records should be 
             written to the user's *S file.  YES specifies that accounting 
             records should be written into the *S file.  NO specifies that 
             accounting records should not be written into the *S file.  NO is 
             the default. 
  SER[VICES] 
             Specifies the maximum and default values of the service limits 
             this user may have. 
             Specifying SERVICES will initiate a sub-option mode.  The format 
             of the sub-option is: 
             {M[AX]|DEFAULT} servname mode=value[, mode=value] ... 
             MAX indicates that the following amounts are the maximums that 
             this user may have. 
             DEFAULT indicates that the following amounts are given to this 
             user by default. 
             servname can be any of the service limits described below. 
             mode is one of the following: B (batch), O (on-line), G (ghost) 
             or T (transaction processing). 
             value is the decimal number that is to be used on the appropriate 
             limit. 
             Note:  The MAX values should be established before the DEFAULT 
             values; if the specified DEFAULT is greater than the 
             corresponding MAX, the MAX value will be used for the DEFAULT. 
             The service limits (servname values) that may be specified are: 
             DO    designates the number of printed diagnostic output pages 
             generated by this user during a job or session.  If the value for 
             DO is 0, a diagnostic output symbiont file will not be generated. 
             FP[OOLS]    designates the number of file-management blocking 
             buffers this user may have during a job or session.  The maximum 
             is 31.  (FPOOLS allocation is not constrained by memory allocated 
             via the MEMORY option.) 
             LO    designates the number of printed output pages generated by 
             this user during a job or session.  If the value for LO is 0, a 
             printed output symbiont file will not be generated. 
             MA[XJOBPRIO]    designates the highest priority this user may 
             assign to a batch job.  The maximum is 15. 
             PD[IS]    designates the number of granules (1K words) of 
             permanent disk storage that may be generated by this user during 
             a job or session.  PDIS does not override the file-management 
             storage limits imposed by the PIG processor. 
             PO    designates the number of punched cards generated by this 
             user during a job or session.  If the value for PO is 0, a 
             punched card output symbiont file will not be generated. 
             TD[IS]    designates the number of granules (1K words) of 
             temporary disk storage that may be generated by this user during 
             a job or session.  TDIS does not override the file-management 
             storage limits imposed by the PIG processor. 
  SETUP mode={'[string]'[,user_alterable]|user_alterable} 
             Specifies a command processor command that is to be automatically 
             executed when the user logs on and/or the alternate attributes 
             for this mode where: 
             mode    is one of the following: B (batch), G (ghost), O 
             (on-line), or T (transaction processing). 
             'string'    is the text of the command.  The default is to use no 
             setup command.  A separate SETUP specification should be used for 
             each mode.  Note: For users running TP as supplied by Bull, the 
             default should always be used.  If string is null, the SETUP 
             command will be deleted.  When specifying a command for the 
             default CP-6 command processor (IBEX) the text must begin with an 
             exclamation point. 
             Example:  SETUP O = '!PRIV ALL' 
             user_alterable    is either: 
             A[LTERABLE]    specifies that the user can modify the SETUP 
             command (via the IBEX command SETUP for the default CP-6 command 
             processor).  ALTERABLE is the default. 
             U[NALTERABLE]    specifies that the user cannot modify the SETUP 
             command. 
  ST[EPACCNT] [={Y[ES]|N[O]}] 
             Indicates that an accounting record is to be written for this 
             user at the end of every job step.  These records are in addition 
             to the accounting record generated at the end of every job or 
             session.  YES means generate the step-accounting records.  The 
             default is YES.  NO means do not generate these records. 
  TI[ME] {M[AX]|D[EFAULT]} mode=value[ ,mode=value] ... 
             Specifies the maximum and default values for CPU-time that this 
             user may have. 
             MAX indicates the following values are the maximums this user may 
             have. 
             DEFAULT indicates the following values are defaults to be used in 
             the absence of a specific request by this user. 
             mode is one of the following: B (batch), O (on-line), G (ghost) 
             or T (transaction processing). 
             value is the decimal number of minutes to be used as the limit. 
  WS[N] = wname 
             Specifies the 1 to 8 character name of the workstation-of-origin 
             that this user should be associated with.  All printed output 
             will go to this destination unless specifically overridden by the 
             user.  wname is a designation defined by the CREATE WSN command, 
             described under HELP (SUPER) WSN. 
00039
00001
00002
00004
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
00026
00025
00025
00027
00028
00029
00030
00031
00032
00034
00033
00034
00035
00036
00037
00038
00040
00041
00042
00039
00043
00044
USER_OPTIONS
UNTIE_PROJECT
A list of virtual circuit profile options and their definitions can be 
accessed by typing a ? or ??.  To obtain individual options, type: 
HELP (SUPER) VIRCIR_PROFILE_OPTS options 
where option is any of the following: 
CALL_DELAYS, CALL_RETRIES, CALL_TIMEOUT, CHARGE_INFORMATION, CLEAR_RETRIES, 
CLEAR_TIMEOUT, DATA_TIMEOUT, EXTENDED_SEQUENCE, IDLE_TIMEOUT, 
INTERRUPT_TIMEOUT, MAXVIRCIR, MINVIRCIR, RECEIVE_SIZE, RECEIVE_THROUGHPUT, 
RECEIVE_WINDOW, RESET_RETRIES, RESET_TIMEOUT, RESPOND_TO_COMPLETE, 
RESPONSE_DELAY, RESPONSE_TIMER, REVERSE, SEND_SIZE, SEND_THROUGHPUT, 
SEND_WINDOW, TRANSIT_DELAY and TYPE. 
  Option                       Description                           Device 
CALL DEL[AYS]=value                                                VIRCIR 
                            Specifies the amount of time in 
                            seconds (0-255) before an attempt is 
                            made to reconnect a virtual circuit 
                            that has been cleared for reasons 
                            other than a higher level initiated 
                            clear.  A value of 0 indicates that 
                            no delay should be used.  The default 
                            is 60. 
CALL RETR[IES]=value                                               VIRCIR 
                            Specifies the number of consecu- 
                            tive unsuccessful call packets 
                            (0-10) that will be transmitted 
                            before the VC is declared lost.  A 
                            value of 0 indicates an infinite 
                            number of retries; this is true only 
                            for SUPER-defined circuits. 
                            The default is 10. 
CALL TIME[OUT]=value                                               VIRCIR 
                            The timeout value (0-255) used for 
                            timing out responses to call reset 
                            and clear packets.  The default 
                            is 200. 
CHA[RGE] INFO[RMATION][={Y[ES]|N[O]}                               VIRCIR 
                            Specifies whether or not charging 
                            information is to be requested for 
                            VCs that use this profile.  This 
                            option is meaningful only when con- 
                            nected to a public data network 
                            (PDN). 
CLEAR RETR[IES]=value                                              VIRCIR 
                            Specifies the number of times (0-99) 
                            to send a clear packet if a clear 
                            confirm was not received in the 
                            number of seconds specified in CLEAR 
                            TIMEOUT.  A restart procedure will be 
                            initiated if the CLEAR RETRIES value 
                            is exceeded.  A value of 0 means do 
                            not retry sending the clear packet. 
                            The default is 3. 
CLEAR TIME[OUT]=value                                              VIRCIR 
                            Specifies the number of seconds 
                            (0-999) that can elapse before a 
                            clear confirm must be received for 
                            each clear packet.  If this time 
                            expires for a clear packet, the 
                            timer is reset CLEAR RETRIES times. 
                            A value of 0 means there is no 
                            timeout value.  The default is 20. 
DATA TIME[OUT]=value                                               VIRCIR 
                            Specifies the number of seconds 
                            (0-999) that can elapse before a 
                            packet acknowledgement must be 
                            received for each data packet.  If 
                            this time expires for a data packet, 
                            the circuit is reset and all 
                            unacknowledged data packets will be 
                            retransmitted.  A value of 0 means 
                            there is no timeout value.  The 
                            default is 0. 
EXT[ENDED] SEQ[UENCE]={Y[ES]|N[O]}                                 VIRCIR 
                            If YES is specified, RECEIVE WINDOW, 
                            RESPONSE DELAY and SEND WINDOW sizes 
                            of up to 127, and SEND and RECEIVE 
                            packet SIZEs of 2048 and 4096 are 
                            legal.  If this option is set to NO, 
                            the maximum size for RECEIVE WINDOW, 
                            RESPONSE DELAY and SEND WINDOW is 7, 
                            and for packet SIZE is 1024.  The 
                            default is NO. 
IDL[E] TIME[OUT]=value                                             VIRCIR 
                            Specifies a number of seconds 
                            (0-255) to wait prior to clearing 
                            the virtual circuit if no activity 
                            has occurred on the virtual circuit. 
                            A value of 0, which is the default, 
                            means this timer is not used. 
INT[ERRUPT] TIME[OUT]                                              VIRCIR 
                            Specifies a number of seconds 
                            (0-999) to wait for an interrupt 
                            confirm after sending an interrupt 
                            packet before clearing the virtual 
                            circuit.  A value of 0 means this 
                            timer is not used.  The default 
                            is 20. 
MAXV[IRCIR]=value           Specifies the maximum number (0-255)   VIRCIR 
                            of virtual circuits to be used in a 
                            connection between a pair of nodes. 
                            The default for MAXVIRCIR is 1. 
                            If MAXVIRCIR is less than MINVIRCIR, 
                            MINVIRCIR is used.  The default is 
                            2.  If only one virtual circuit is 
                            to be defined, efficiency will be 
                            gained if MAXVIRCIR is set to 1. 
MINV[IRCIR]=value           Specifies the minimum number (0-255)   VIRCIR 
                            of virtual circuits to be used in a 
                            connection between two nodes.  The 
                            default for MINVIRCIR is 1. 
                            MINVIRCIR and MAXVIRCIR values are 
                            specified or defaulted for each 
                            virtual circuit between two nodes. 
                            If multiple virtual circuits are 
                            defined between a pair of nodes, the 
                            values for all MINVIRCIR/MAXVIRCIR 
                            for all the virtual circuits defined 
                            between the two nodes must be the 
                            same.  Otherwise, the MIN/MAX range 
                            selected will be somewhat unpredict- 
                            able. 
REC[EIVE] SIZ[E]={128|256|512|1024|2048|4096}                      VIRCIR 
                            Specifies the maximum size of data 
                            packets from the call recipient.  If 
                            this value is larger than the frame 
                            size of the LINK profile, the frame 
                            size value is used.  The default is 
                            1024.  2048 and 4096 are available 
                            only if EXT SEQ is set to YES. 
REC[EIVE] THR[OUGHPUT]={NONE|75|150|300|600|1200|2400| 
                        4800|9600|19200|48000} 
                            Specifies the throughput class         VIRCIR 
                            of the virtual circuit from the call 
                            recipient.  This option is meaningful 
                            only if the connection is made through 
                            a PDN.  The default is NONE. 
REC[EIVE] WIN[DOW]=value    Specifies the transmit window size     VIRCIR 
                            for the call recipient.  The 
                            default is 2. 
RESET RETR[IES]=value                                              VIRCIR 
                            Specifies the number of times (0-99) 
                            to send a reset packet if a reset 
                            confirm was not received in the 
                            number of seconds specified in RESET 
                            TIMEOUT.  A clear procedure will be 
                            initiated if the RESET RETRIES value 
                            is exceeded.  A value of 0 means do 
                            not retry sending the reset packet. 
                            The default is 1. 
RESET TIME[OUT]=value                                              VIRCIR 
                            Specifies the number of seconds 
                            (0-999) that can elapse before a 
                            reset confirm must be received for 
                            each reset packet.  If this time 
                            expires for a reset packet, the 
                            timer is reset RESET RETRIES times. 
                            A value of 0 means there is no 
                            timeout value.  The default is 0. 
RES[POND TO] COM[PLETE][={YES|NO}] 
                            Specifies whether (YES) or not (NO)    VIRCIR 
                            any complete data packet sequence 
                            should be acknowledged immediately, 
                            regardless of the response delay 
                            value.  The default is YES. 
RESP[ONSE] DEL[AY]=value    Specifies the number of unacknow-      VIRCIR 
                            legement packets that should be 
                            received before an explicit acknow- 
                            ledgement packet is generated.  The 
                            size that can be specified depends on 
                            whether or not the EXTENDED SEQUENCE 
                            option has been set.  If EXT SEQ=YES, 
                            this value can be in the range 1-127. 
                            If EXT SEQ=NO, the value is in the 
                            range 1-7.  If this value is larger 
                            than the receive window, the receive 
                            window value is used.  The default is 1. 
RES[PONSE] TI[MER]=value    The number of seconds (0-255) to       VIRCIR 
                            wait after deciding to send an 
                            explicit flow control message 
                            (based on response delay and 
                            response to complete).  If an 
                            implied flow control message is 
                            sent before the time expires, no 
                            flow control message needs to be 
                            sent.  The default is 1. 
RE[VERSE][={Y[ES]|N[O]}]    Specifies whether or not reverse       VIRCIR 
                            charging should be specified in the 
                            call packet.  The default is NO. 
SEN[D] SIZ[E]={128|256|512|1024|2048|4096} 
                            Specifies the maximum data size        VIRCIR 
                            of packets sent to the call 
                            recipient.  The default is 1024. 
                            2048 and 4096 can be specified only if 
                            the EXT SEQ option has been set to YES. 
SEN[D] THR[OUGHPUT]={NONE|75|150|300|600|1200|2400| 
                     4800|9600|19200|48000} 
                            Specifies the throughput class of      VIRCIR 
                            the VC to the call recipient.  This 
                            option is only meaningful if the 
                            connection is made through a PDN. 
                            The default is NONE. 
SEN[D] WIN[DOW]=value       Specifies the transmit window size     VIRCIR 
                            (2-7) to the call recipient.  The size 
                            that can be specified depends on 
                            whether or not the EXTENDED SEQUENCE 
                            option has been set.  If EXT SEQ=YES, 
                            the transmit window size range is 
                            2-127.  If EXT SEQ=NO, the transmit 
                            window size range is 2-7.  The default 
                            is 7. 
TRA[NSIT] DEL[AY]=value                                            VIRCIR 
                            Specifies a transit delay limit as 
                            the number of milliseconds (0-65535) 
                            tolerance for a packet to traverse 
                            the network to its destination, 
                            expressed as a 95% probability value 
                            (see the ISO publication, ISO 8208, 
                            Section 6.9).  This option is mean- 
                            ingful only if the link connects to 
                            a PDN that supports this capability. 
                            A value of 0, which is the default, 
                            means no transit delay limit is 
                            established. 
TY[PE]={P[RIMARY]|S[ECONDARY} 
                            Specifies usage type of the VC.        VIRCIR 
                            PRIMARY specifies that the VC 
                            should always be used.  SECONDARY 
                            is intended to meet peak loads. 
                            This option applies only to VCs 
                            associated with a multilink network 
                            connection.  The default is PRIMARY. 
00001
00002
00003
00001
00002
00003
00004
00004
00005
00006
00005
00006
00007
00007
00008
00008
00009
00009
00010
00010
00011
00012
00021
00013
00014
00015
00013
00014
00015
00018
00016
00017
00016
00017
00019
00018
00019
00020
00020
00021
00022
00023
00024
00022
00023
00024
00025
00025
00026
VIRCIR_PROFILE_OPTIONS
Format: 
{C[REATE]} 
{M[ODIFY]} VIR[TUAL] CIR[CUIT] vcnum FOR LINK link-name 
{R[EMOVE]} 
or 
D[ISPLAY] {[ALL] VIR[TUAL] CIR[CUITS] [FOR LINK link-name]} [(JCL)] 
          {VIR[TUAL] CIR[CUIT] vcnum [FOR LINK link-name] } 
or 
L[IST] {[ALL] VIR[TUAL] CIR[CUITS] [FOR LINK link-name]} 
       {VIR[TUAL] CIR[CUIT] vcnum [FOR LINK link-name] } 
Parameters: 
vcnum    specifies the virtual circuit number (0-4095) for the virtual circuit 
to be created, modified, removed, listed, or displayed.  Note that this number 
is a logical channel number (LCN) only when specifying a permanent vc.  The 
number simply identifies the virtual circuit to SUPER.  If MODIFY is specified 
and a virtual circuit does not exist, it is created.  If the LIST or DISPLAY 
form of the command is used, vcnum can be wildcarded. 
link-name    specifies the name of the link with which the virtual circuit 
will be associated (See the CREATE LINK command).  If the LIST or DISPLAY form 
of the command is used, link-name can be wildcarded. 
Description: 
The CREATE, MODIFY and REMOVE VIRTUAL CIRCUIT commands create, modify, and 
remove (one) virtual circuit definitions.  Virtual circuits are used by the 
CP-6 operating system to establish communications between nodes of a network. 
The LIST VIRTUAL CIRCUIT command lists the currently defined virtual circuits. 
The DISPLAY VIRTUAL CIRCUIT command shows virtual circuit definitions. 
SUPER prompts for options when it encounters a CREATE or MODIFY VIRTUAL 
CIRCUIT command.  The options are listed in HELP (SUPER) VIRTUAL_CIRCUIT_OPTS. 
00002
00001
A list of virtual circuit command options and their definitions can be 
accessed by typing a ? or ??.  To access individual options, type: 
HELP (SUPER) VIR_CIR_OPTS option 
where option is any of the following: 
ADDRESS, CUG, DESTINATION, PERMANENT, QOS, or PROFILE. 
  Option    Description 
  AD[DRESS] = n 
            Specifies the 1-14 decimal digit address of the link on the remote 
            node to which the circuit is directed.  This address is used as 
            the "called address" in call packets. 
  CU[G] = n 
            Specifies a closed user group.  n is a decimal digit of length 4 
            or less.  This option is meaningful only if the connection is made 
            through a PDN. 
  DES[TINATION] = nodename 
            Specifies the name of the node that will receive the call. 
            nodename is 1-8 characters.  If specified, the destination must be 
            a node defined in NETCON. 
  PERMANENT={Y[ES]|N[O]} 
            Specifies whether or not the virtual circuit is permanent.  Note 
            that if permanent and switched virtual circuits are to be created, 
            the permanent ones must be created first to ensure that they will 
            occupy the lowest LCNs. 
  QOS=n 
            Specifies the Quality of Service for the virtual circuit.  n is a 
            decimal integer between 2 and 255.  The default is 2. 
  PRO[FILE] = pname 
            where pname is a previously defined VIRTUAL CIRCUIT profile.  If 
            pname is specified, it must be defined, and defined as a virtual 
            circuit profile.  If no PROFILE is specified, the default profile 
            is $VIRCIR. 
The LIST VIRTUAL CIRCUIT command lists the name data for virtual circuits. 
Including vcnum in the LIST VIRTUAL CIRCUIT command is useful when wildcarding 
is used or to verify the existence of a virtual circuit definition. 
The DISPLAY VIRTUAL CIRCUIT command shows a columnized display of the options 
for selected virtual circuits (or all virtual circuits if the ALL option is 
specified), prefaced by a header consisting of the virtual circuit information 
as entered in a CREATE or MODIFY VIRTUAL CIRCUIT command.  The JCL option 
causes the command keyword CREATE to be written at the beginning of each 
virtual circuit definition and the END keyword is inserted where needed. 
00001
00002
00003
00004
00006
00005
VIRTUAL_CIRCUIT
VIRTUAL_CIRCUIT_OPTIONS
Format: 
{C[REATE]} WSN wname {[FOR STAT[ION] sname         ]} 
{M[ODIFY]}           {[FOR IND[IRECT] wname @ sname]} 
or 
R[EMOVE] WSN wname 
or 
D[ISPLAY] [ALL] WSN wname [FOR STAT[ION] sname] [(JCL)] 
or 
L[IST] [ALL] WSN wname [FOR STAT[ION] sname] [(JCL)] 
Parameters: 
wname    is the 1-8 character name of the workstation to be created, modified 
or removed.  If a MODIFY WSN command is specified, but the workstation does 
not exist, it is created.  If wname is not specified on the LIST WSN command, 
all workstations are listed.  If the LIST or DISPLAY form of the command is 
used, wname can be wildcarded. 
sname    is the name of a station.  The station must exist.  The workstation 
will include all devices on sname, and consoles associated with sname may 
control users associated with this workstation.  If the FOR clause is 
specified in the CREATE WSN command, and the specified station does not have a 
default workstation, wname will be its default workstation.  If the LIST or 
DISPLAY form of the command is used, sname can be wildcarded. 
Description: 
The CREATE, MODIFY and REMOVE WSN commands are used to create, modify and 
remove (one) workstation definitions.  The LIST WSN command lists currently 
defined workstations and the DISPLAY WSN command shows WSN definitions. 
Workstations are maintained by SUPER in the file :WSN.:SYS.  One workstation, 
LOCAL, is created when the file is created to describe the central site 
devices.  If the workstation option for TIGR (see Section 23) was used, other 
workstations are built to describe subsets of the central site devices as 
specified to TIGR. 
FOR INDIRECT wname @ sname establishes an equivalence between a (dummy) 
workstation on the local node and a workstation on another network node. 
The LIST WSN command lists the name data for selected workstations.  Including 
wname in the LIST WSN command is useful when wildcarding is used or to verify 
the existence of a WSN definition. 
The DISPLAY WSN command shows a columnized display of the options for selected 
workstations (or all workstations if the ALL option is specified), prefaced by 
a header consisting of the workstation information as entered in a CREATE or 
MODIFY WSN command.  The JCL option causes the command keyword CREATE to be 
written at the beginning of each workstation definition and the END keyword is 
inserted as needed. 
The RECONFIGURE STATION command is used to reconfigure IOM-devices for the 
identified workstation without having to reboot the system.  But, if this 
command is used, non-IOM devices associated with the workstation must be 
redefined.  (See the STATION commands.) 
After encountering a CREATE or MODIFY WSN command, SUPER prompts for options 
when it encounters a CREATE or MODIFY WSN command.  The options are listed in 
HELP (SUPER) WSN_OPTS. 
00002
00001
A list of WSN command options and their definitions can be accessed by typing 
a ? or ??.  To access individual options, type: 
HELP (SUPER) WSN_OPTS option 
where option is any of the following: 
ACCESS, DEVICE, or DFORM. 
  Option    Description 
  AC[CESS] [A[DD]|[R[EMOVE]] = list 
            Supplies (A) or deletes (R) the listed accounts (which may be 
            wildcarded) that may use the workstation.  If the ACC option is 
            not specified, any account may use the workstation.  If the A or R 
            option is not specified, the A is assumed.  For example, the 
            option specification: 
            ACC SAM,?HOST,FEP? 
            limits use of the workstation to account SAM, and any account 
            which ends in the characters HOST or begins with the characters 
            FEP. 
            This option is available for INDIRECT workstations. 
  DEV[ICE] = {ddnn@sname|dd@sname|@sname} 
            Makes devices from other stations available to users of this 
            workstation.  The user of this workstation can access devices that 
            are not present at this station or workstation. 
            dd is a device type (i.e., LP, CP, etc...). 
            nn is a device number. 
            sname is a 1-8 character station name. 
            ddnn@sname identifies a specific device at the specified station. 
            dd@sname identifies all devices of the specified type at the 
            specified station.  @sname specifies all devices at the specified 
            station. 
            This option is not available for INDIRECT workstations. 
  DF[ORM] type fname 
            Each workstation contains the default form (see HELP (SUPER) WSN) 
            supplied when a user of a workstation opens to a type of device. 
            Normally, this is the form mounted by default on this type of 
            device included in the workstation (see the DEVICE commands FORM 
            option).  The DFORM option can be used to change the default form 
            for a type of device.  The specified form must exist.  For 
            example, the option specification 
            DFORM LP 8BY11 
            causes the default form for printers under this workstation to be 
            8BY11. 
            This option is not available for INDIRECT workstations. 
00001
00002
00003
WSN_OPTIONS
