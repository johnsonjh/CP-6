The LABEL processor is used to initialize magnetic tapes for use as ANS 
volumes by writing standard labels on them. 
To obtain more information, type: 
HELP (LABEL) COMMANDS      For a brief description of the commands. 
HELP (LABEL) TOPICS        For a list of LABEL HELP topics. 
HELP (LABEL) command       For the format of a specific command. 
                           Then type ? or ?? for more. 
HELP (LABEL) command PARAM For the parameters for a specific 
                           command. 
HELP (LABEL) command DESC  For the description of a specific 
                           command. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
DO
A list of LABEL commands and their definitions can be accessed by typing a ? 
or a ??.  To obtain definitions of individual parameters, type 
HELP (LABEL) COMMANDS command 
where command is any of the following: 
DATE, DIRECTORY, DO, END, ENTER, ERASE, 
HELP, LABEL, OUTPUT, PRINT, QUIT, REMOVE, SCRATCH, SEQUENTIAL, TIME. 
  Command     Function 
  {DATE|TIME} 
              Displays the current time and date. 
  {DIRECTORY|DIR} 
              Changes the default account and packset. 
  {DO|!} 
              Enable IBEX command execution. 
  {END|EXIT|QUIT} 
              Terminates execution of the LABEL processor. 
  ENTER 
              Invokes a CP-6 ADAPT dialog from within this processor. 
  ERASE 
              Deletes accumulated output for logical devices. 
  HELP 
              Displays information on LABEL and other processors. 
  LABEL 
              Labels a single tape or optical disk cartridge volume. 
  OUTPUT 
              Sends subsequent output to the specified file. 
  PRINT 
              Directs that output accumulated for logical devices be sent to 
              destinations immediately. 
  REMOVE 
              Dismounts a specified tape volume. 
  SCRATCH 
              Writes a double tape file mark at the beginning of a tape. 
  SEQUENTIAL 
              Labels multiple tapes or optical disk cartridges in a sequential 
              order. 
Enter: HELP (LABEL) command for information on a specific command. 
00003
00001
00002
00003
00004
00005
00006
00004
00007
00008
00009
00010
00004
00011
00012
00013
00001
COMMANDS
Format: 
{DATE|TIME} 
Description: 
DATE (and its synonym TIME) displays the current date and time.  The format of 
the display is: 
mmm dd 'yy hh:mm    (month)(day)(year)(hours)(minutes) 
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
*DO DI 
means display the current system status 
*!LDEV LP09 TITLE='report title',PAGE=100,COPIES=3 
means set up a title and page number for a report destination 
00002
00003
00001
Format: 
{E[ND]|[E]X[IT]|Q[UIT]} 
Description: 
The END command (and is synonyms EXIT and QUIT) terminates execution of the 
LABEL processor. 
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
*ERASE ALL 
deletes all output accumulated for all logical devices defined for the session 
or job. 
00002
00003
00001
LABEL uses standard system reading and error reporting services to report 
syntax and monitor errors.  The following messages are the LABEL-specific 
error messages. 
*** A serial number cannot begin with blanks 
                    Although serial numbers may have trailing blanks (i.e., be 
                    shorter than 6 characters), they must begin with a 
                    non-blank character. 
*** A serial number cannot contain blanks 
                    Serial numbers must be composed of non-blank characters. 
*** An ACCOUNT must be specified if ACCESS is specified 
                    The ACCESS option implies that certain accounts are to 
                    have that access.  Therefore, specifying ACCESS without 
                    ACCOUNT is meaningless. 
*** At least 1 tape must be specified 
                    A labeling command must indicate at least one tape to be 
                    labeled. 
*** End of PLACE range must be at least as large as start 
                    In the PLACE option n2 is less than n1, thus specifying a 
                    non-existent field for serial number sequencing. 
*** Invalid platter side (must be A or B) 
                    A platter number must have an A or B as the last 
                    character.  The A or B specifies the side of the platter 
                    to be labeled. 
*** No more than 1 tape can be specified 
                    An attempt was made to label more than one tape with a 
                    LABEL command. 
*** PLACE must identify character position within serial number 
                    An attempt was made to sequence in a position in the 
                    serial number that cannot exist.  Both n1 and n2 must be 
                    integers between 1 and 6 inclusive. 
*** The serial sequence number cannot be placed in the SN 
                    The next serial number in a sequence of tapes cannot be 
                    labeled, as the PLACE option specified a field that was 
                    too small for the incremented portion of the serial number 
                    to contain.  For example, if PLACE=6, only 10 tapes can be 
                    initialized (counting the first tape whose serial number 
                    ends in zero). 
*** You are not allowed to run LABEL 
                    You do not have the LABEL processor privilege or the FMS 
                    privilege. 
*** You must specify an input platter number 
                    A platter number was not specified on a LABEL or 
                    SEQUENTIAL optical disk command. 
END
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
  DO Command - 
      HELP DO 
E 
  END Command - 
      HELP END 
  END Command (LABEL) - 
      HELP END FORMAT: 
  ENTER Command - 
      HELP ENTER 
  ERASE Command - 
      HELP ERASE 
H 
  HELP Command - 
      HELP HELP 
I 
  Invoking LABEL - 
      HELP INVOKING_LABEL 
L 
  LABEL -   
    END Command - 
      HELP END FORMAT: 
    LABEL Command - 
      HELP LABEL FORMAT_1: 
    REMOVE Command - 
      HELP REMOVE FORMAT: 
    SCRATCH Command - 
      HELP SCRATCH FORMAT: 
    SEQUENTIAL Command - 
      HELP SEQUENTIAL FORMAT_1: 
  LABEL Command - 
      HELP LABEL 
  LABEL Confirmation Messages - 
      HELP LABEL_MESSAGES 
  LABEL Error Messages - 
      HELP ERROR_MESSAGES 
O 
  OUTPUT Command - 
      HELP OUTPUT 
P 
  PRINT Command - 
      HELP PRINT 
  Privileges Required for LABEL - 
      HELP PRIVILEGES 
R 
  REMOVE Command -   
    LABEL - 
      HELP REMOVE FORMAT: 
  REMOVE Command - 
      HELP REMOVE 
S 
  SCRATCH Command -   
    LABEL - 
      HELP SCRATCH FORMAT: 
  SCRATCH Command - 
      HELP SCRATCH 
  SEQUENTIAL Command - 
      HELP SEQUENTIAL 
T 
  tapes -   
    named - 
      HELP SEQUENTIAL PARAMETERS: 
    relabeled - 
      HELP PRIVILEGES 
      HELP LABEL PARAMETERS: 
    scratch - 
      HELP SCRATCH DESCRIPTION: 
      HELP LABEL_MESSAGES EXAMPLES: 
    unnamed - 
      HELP SEQUENTIAL PARAMETERS: 
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
!LABEL invokes the LABEL processor, which responds with the date and time, and 
an asterisk prompt.  The user then specifies the LABEL task by using the 
appropriate LABEL commands.  The LABEL processor is exited by entering END. 
LABEL can be run in a time-sharing or batch environment, or as a console 
ghost. 
Format 1: 
LAB[EL] TO LT#serial[, option] ... 
Format 2: 
LAB[EL] TO OD#serial,#volume [,option] 
Parameters: 
LT    specifies Labeled Tape. 
OD    specifies Optical Disk cartridge. 
serial    specifies the serial number to be assigned to the tape or optical 
disk cartridge.  This can be from 1 to 6 characters. 
volume    is a 2 to 6 alphanumeric character optical disk cartridge volume 
identification.  The last character identifies the cartridge platter side and 
must be either "A" or "B". 
option    specifies one or more of the following options, separated by commas: 
    Tape and Optical Disk Cartridge Options: 
    ACC[OUNT]=account    specifies the volume owner's account.  The default is 
    no owning account. 
    ACCESS={IN|ALL|NONE}    specifies that 
        IN - any user can input the volume; only the owner can write to the 
        volume. 
        NONE - only the owner can read from or write to the volume. 
        ALL - any account can read from or write to this volume. 
    The default is ALL.  ACCESS cannot be specified without an ACCOUNT option. 
    Tape (Only) Options: 
    [{LT|MT|FT}] #serial    specifies the serial number of the tape to be 
    relabeled.  If unspecified, a new scratch tape is assumed. 
    DEN[SITY]={800|1600|6250}    specifies the allowable tape densities. 
    B[YPASS] C[ONTENT] C[HECK]    specifies that the original label on the 
    tape is not to be read to determine its actual serial number.  This is 
    necessary when reading the tape results in I/O errors. 
Description: 
The LABEL command is used to label tapes and optical disk cartridges. 
For tapes, the LABEL command labels or relabels a single volume, optionally 
assigning an owning account and an account access control.  Density can be 
specified and the processor can be directed to bypass an original label. 
00003
00001
00002
LABEL confirms the successful labeling or scratching of volume by printing a 
message or messages which contain: 
1.  The new serial number. 
2.  The serial number by which the reel was requested. 
3.  The actual old serial number. 
Confirmation messages have the following form: 
xxxxxx < yyyyyy (zzzzzz) 
where 
xxxxxx    is the new serial number.  This field is always present unless the 
operation is a SCRATCH, in which case it is printed as blanks. 
yyyyyy    is the serial number by which the reel was requested; if not 
present, no tape was named. 
zzzzzz    is the actual old serial number; if not present, the tape did not 
have a label. 
Examples: 
SN010A < A      (A     ) 
This message means that a volume requested as serial number A, did exist with 
the serial number A, and was successfully relabeled as serial number SN010A. 
SN020A <        (B     ) 
This message means that an unnamed volume was requested, and a tape 
(presumably no longer necessary) that was labeled B was mounted and relabeled 
to serial number SN020A. 
SN030A < C 
This message means that the volume C was requested and an unlabeled tape was 
mounted and labeled to serial number SN030A. 
SN040A 
This message means that an unlabeled tape was requested, mounted, and 
relabeled to SN040A. 
< A      (B     ) 
This message means that a scratch request for labeled tape A actually caused 
volume B to be scratched. 
< A 
This message confirms the successful scratching of labeled tape A. 
When a series of unlabeled tapes are labeled via the SEQUENTIAL command, a 
variation of the confirmation message will be printed in the form: 
nnnnnn - mmmmmm 
where 
nnnnnn    specifies the new serial number of the first volume in the sequence 
of tapes. 
mmmmmm    specifies the new serial number of the last volume in the sequence 
of tapes. 
TAPE01 - TAPE08 
This message indicates that a sequence of volumes, each previously unlabeled, 
was successfully labeled.  The actual number of tapes depends upon the 
INCREMENT option in the SEQUENTIAL command. 
00001
LABEL_MESSAGES
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
LP    directs output to the default line printer; @location specifies a 
particular workstation. 
fid    identifies the file to receive the output.  Output can be directed to 
any valid fid. 
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
This command sends subsequent output to a destination.  OUTPUT with no options 
redirects output to the original output destination. 
Examples: 
*OUTPUT ON OUTPUTFILE 
*OUTPUT ON ME 
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
*PRINT LP01,LP02 
The above example causes the accumulated output associated with logical 
devices LP01 and LP02 to be sent immediately to the associated destinations. 
For optical disk cartridges, the LABEL command is used to label an unlabeled 
volume, optionally assigning an owning account and an account access control. 
If the cartridge already has a label, an error message is displayed. 
Example: 
LABEL TO LT#NEWVOL,FT#OLDVAL,ACC=:SYS,ACCESS=NONE 
This command writes a label on free tape #OLDVAL, which then becomes labeled 
tape #NEWVOL, belonging to the :SYS account.  Only the :SYS account is 
permitted to access the tape. 
LABEL TO OD#CART2,#VOL1A,ACC=:OPACCT 
This command writes the label CART2 on side A of optical disk cartridge VOL1 
belonging to the :OPACCT account. 
00002
00004
00003
00001
The FMSEC privilege or LABEL processor privilege (PPR_LABEL) is required for 
the use of LABEL.  In either a semi-protected or fully-protected system, any 
type of tape can be relabeled by a user possessing these privileges. 
END
Format: 
REM[OVE] [{LT|MT|FT}]#serial 
Parameters: 
serial    specifies the serial number of the tape to be dismounted. 
Description: 
The REMOVE command causes the specific volume to be dismounted.  Note that the 
tape type (LT, MT, FT) need not be specified. 
Example: 
REM #GORBLE 
means remove tape #GORBLE. 
00002
00003
00001
Format: 
SCRATCH [{LT|MT|FT}] #serial[#serial] ... 
Parameters: 
serial    specifies a volume to be scratched. 
Description: 
The SCRATCH command writes a double tape file mark at the beginning of the 
tape. 
Note:  This command destroys data only on the first portion of tape.  Tapes 
that contain sensitive information should be degaussed (demagnetized) for 
additional security. 
Example: 
SCRATCH LT#A#B#C 
This command requests that labeled tapes #A, #B, and #C be mounted and 
scratched. 
00002
00003
00001
Format 1: 
SEQ[UENTIAL] [NUM[BER]] TO LT#serial[, option] ... 
Format 2: 
SEQ[UENTIAL] [NUM[BER]] TO OD#serial,#volume[,#volume]... [,option] 
Parameters: 
NUMBER    is documentary in purpose. 
LT    specifies Labeled Tape. 
OD    specifies Optical Disk cartridge. 
serial    specifies a serial number image that is used as a basis (template) 
for composing a list of sequential serial numbers. 
volume    is one or more 2 to 6 alphanumeric character optical disk cartridge 
volume identifications.  The last character identifies the cartridge platter 
side and must be either "A" or "B". 
option    specifies one or more of the following options separated by commas. 
    Labeled Tape and Optical Disk Cartridge Options: 
    START=n    specifies the initial sequence number value.  This value is 
    placed in the serial number image to determine the first serial number. 
    INC[REMENT]=n    specifies the value by which to increment each successive 
    sequence number, based upon the initial serial number given in the "TO 
    LT#" or "TO OD#" portion of the command.  This default is 1. 
    PLACE=n1[-n2] 
    where 
        n1    specifies the character position in the template serial number 
        that will be altered as successive volumes are initialized.  The 
        default is the sixth character of the serial number; if the serial 
        number is less than six characters in length, the sequence number will 
        be padded to the left with zeroes. 
        n1-n2    specifies starting and ending character positions that define 
        a field within SN to be altered as successive volumes are initialized. 
    ACC[OUNT]=account    specifies the volume owner's account. 
    ACCESS={IN|ALL|NONE}    specifies that 
        IN - any user can input these volumes; only the owner can write to 
        these volumes. 
        NONE - only the owner can read from or write to these volumes 
        ALL - any account can read from or write to these volumes. 
    The default is ALL.  ACCESS cannot be specified unless ACCOUNT is also 
    specified. 
    Labeled Tape Only Options: 
    n [TAPE[S]]    specifies a number (n) of unnamed tapes to be initialized. 
    [{LT|MT|FT}] #sn1[#sn2] ...    specifies the serial numbers of named tapes 
    to be relabeled. 
    Note:  The sequence of the options n [TAPE[S]] and [{LT|MT|FT}] #sn1[#sn2] 
    ... determines the order in which tapes are requested. 
    DEN[SITY]={800|1600|6250}    specifies the allowable tape densities. 
    B[YPASS] C[ONTENT] C[HECK]    specifies that the original label on the 
    tape is not to be read to determine its actual serial number.  This is 
    necessary when reading the tape results in I/O errors. 
Description: 
The SEQUENTIAL command labels a number of tapes or optical disk cartridges in 
a sequential order, optionally assigning an owning account and an account 
access control. 
Example: 
SEQ TO LT#XXX,3 TAPES,LT#A,START=3,INC=2 
This command involves four tapes:  three that are nameless (new or scratch) 
and one that is presently named #A.  When the command has successfully been 
completed, the four tapes will be numbered XXX003, XXX005, XXX007, and XXX009 
(which was tape LT#A). 
SEQ TO LT#SNXXXA,1,LT#A,2,LT#B#C,START=10,PLACE=3-5 
This command involves six tapes.  The first is nameless (specified as 1 in the 
command).  The second is labeled #A.  The third and fourth are nameless 
(specified by 2 in the command), and the fifth and sixth are labeled #B and 
#C.  After successful completion of the command, the six tapes will be 
numbered SN010A, SN011A, SN012A, SN013A, SN014A, and SN015A.  Note that the 
PLACE option determines the area in which the sequencing took place. 
Named and nameless volumes can be freely intermixed to create volume sets from 
various kinds of tapes.  Nameless volumes should be mounted for labeling at 
the operator's discretion from the new and old tapes available. 
SEQ TO OD#VOLXXX,#VOL1A,#VOL1B,#VOL2A,#VOL2B,START=1,PLACE=4-6 
This command labels successive sides of VOL1 and VOL2 as OD#VOL001, OD#VOL002, 
OD#VOL003, and OD#VOL004, respectively. 
00002
00003
00001
DATE
