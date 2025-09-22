The SEND processor is invoked at the system control level (!) as follows: 
    SEND [fid] [(option[,option][...])] 
SEND responds by issuing one of its prompts, as described under SEND PROMPTS, 
if additional user input is needed.  Otherwise, it responds with a line 
telling the user that the message has been sent. 
Parameters: 
fid    specifies a file name.  The file which contains the message information 
may include information for the To, Subject, and Body fields.  Options must 
precede the body of the message.  If any of the required field information is 
missing, SEND prompts the user for the field information. 
The file which the user creates can contain any options or fields, with the 
following exceptions: 
    CANCEL 
    DISPLAY 
    DO 
    EDIT 
    END 
    HELP 
    LINK 
    SEND 
The fields or options that are specified must include a colon, e.g., To:, in 
order to distinguish them from body information. 
option    specifies one or more of the following options: 
    MAIL=address    specifies information required for address resolution and 
    optional profile settings.  The syntax for address is: 
        [name][/folder][.account][@site] 
        name    specifies a user name. 
        folder    specifies the folder name. 
        account    specifies a user account. 
        site    specifies the user site name. 
    If the name option is not specified, the message recipient's default 
    central folder is used. 
    OPT[IONS]    specifies that the user be prompted with the Options:  prompt 
    even if the message is complete.  At this prompt, the user can enter SEND 
    options.  (See OPTIONS for a list of available options and fields.) 
    Entries which the user chooses override the current field entries for the 
    message. 
To obtain more HELP information if you are in the 
SEND processor, enter: 
HELP TOPICS                 for a list of SEND topics. 
HELP PROMPTS                for a list of SEND prompts. 
HELP OPTIONS                for a list of SEND options. 
HELP (MAIL) TOPICS          for a list of MAIL topics. 
HELP (MAIL)                 for invoking the MAIL processor. 
HELP (MAIL) COMMANDS        for a list of MAIL command groups. 
HELP (MAIL) command         for a specific MAIL command. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
DO_OPTION
Syntax: 
AP[PEND] [fid] 
Description: 
If fid is not indicated, APPEND specifies that additional lines be appended to 
the message body.  The user is prompted for more body lines in the same manner 
as for the Body: prompt, i.e., with Body: if there are currently no body 
lines, or with five leading blanks, if there are body lines. 
If fid is indicated, APPEND will append the lines from that file to the 
message body. 
00001
Syntax: 
ATT[ACH] fid [TI[TLE] 'title_string'] 
DESCRIPTION: 
Specifies a file to be attached as an additional enclosure to the current 
message.  The optional title may be up to 256 characters.  The first 80 
characters will be displayed when the message is displayed.  Additional files 
and titles may be specified in a list delimited by commas.  Any file may be 
attached to a message; however, when the enclosure is DETACHed by the receiver 
the file created will be ORG=CONSEC. 
00001
Syntax: 
B[LIND] C[OPY][:] [address] 
Description: 
Specifies the addresses (users) that are to receive blind copies of a message. 
One or more addresses can be entered separated by commas.  The Blind Copy 
field is invisible to message recipients listed in the To: and Copy: fields. 
If the BLIND COPY option is specified with no address list, the current Blind 
Copy list (if any) is displayed and the user is allowed to change or delete 
it. 
00001
Syntax: 
Body: text 
Description: 
A multi-line text field that contains the message information.  Lines of MAIL 
messages can contain up to 300 characters.  If a file is sent that has lines 
longer than 300 characters, they are truncated. 
00001
Syntax: 
BR[OADCAST][:] [Y[ES]|N[O]] 
Description: 
Specifies that undeliverable copies of the message are to be discarded; no 
error message is to be returned.  Generally, used to send copies of a message 
to multiple receivers.  This option minimizes space used in the recipient(s) 
mailbox because it does not include a formatted list of recipients. 
00001
Syntax: 
CA[NCEL] 
Description: 
Cancels sending of the message and exits SEND. 
00001
Syntax: 
C[OPY][:] [address] 
Description: 
Specifies the addresses (users) that are to receive copies of a message.  One 
or more addresses can be entered, separated by commas.  If the COPY option is 
specified with no address list, the current Copy list (if any) is displayed 
and the user is allowed to change or delete it. 
00001
Syntax: 
CRPT: value 
Description: 
Specifies the octal value to be used for encryption of a message.  Legal 
values aare:  a decimal number between one and 68719476735; an octal number 
preceded by a period (.), with a value between between .0 and .777777777777; 
or a string of 1 to 4 characters enclosed in single quotes (').  Only the 
message body is encrypted.  The default is no encryption (CRPT=0). 
00001
TIME
Syntax: 
DE[FER][:] [hh:mm[,mm/dd/yy]] 
Description: 
Specifies the date and time when a message is to be delivered.  The default is 
that the message be delivered immediately.  Time is specified using a 24 hour 
clock (e.g., 14:00 is 2 p.m.).  Date or time can appear in either order, 
either can be omitted, and yy defaults to the current year.  If the DEFER 
option is specified with no date or time, the current deferral timestamp (if 
any) is displayed and the user is allowed to change or delete it. 
00001
Syntax: 
D[ELIVERY] R[ECEIPT][:] [Y[ES]|N[O]] 
Description: 
Specifies that the message sender is to receive a system-generated message 
indicating when the message recipient(s) received the message (not when it is 
read).  Only one message is generated (per system) and the message is 
generated when the last recipient receives the message.  If combined with the 
BROADCAST option, any error messages are included in the delivery receipt 
message and are not sent as individual error messages.  The YES|NO options 
overrides the DELIVERY RECEIPT option in the folder's profile setting. 
00001
Syntax: 
DI[SPLAY] [field] 
Description: 
Displays the specified field's content for the message which is to be 
delivered.  If a field is not specified, the entire message is displayed.  The 
following fields can be displayed: 
B[LIND] C[OPY]        displays Blind Copy field. 
C[OPY]                displays Copy field. 
D[EFER]               displays the defer date and time. 
F[ILE] C[OPY]         displays whether a file copy is 
                      specified. 
[MESSAGE]             displays the entire message. 
RE[FERENCE]           displays Reference field. 
REP[LY] T[O]          displays Reply To field. 
R[ETURN] R[ECEIPT]    displays whether return receipt 
                      is specified. 
SI[GNED]              displays Signed field. 
SU[BJECT]             displays Subject field. 
T[O]                  displays To field. 
00001
Syntax: 
{DO|!} command 
Description: 
Suspends execution of SEND to request that another command be invoked.  When 
the DO option is entered at the Options: prompt, the message body is written 
to the file *BODY so that it is available for use by the invoked command. 
00001
Syntax: 
ED[IT] [W[ITH] fid] 
Description: 
Invokes an editor so that the user can modify the contents of the current 
message.  The optional fid parameter specifies the name of the editor to use. 
It no fid is specified, either the editor specified in the MAIL profile or the 
EDIT processor (the default) is used. 
The message header fields and the message body are written to the *BODY file 
for editing purposes.  The user is returned to the Options: prompt after 
exiting the editor. 
00001
Syntax: 
E[ND]|E[X][IT]|Q[UIT] 
Description: 
Exits SEND mode, delivers the created message, and returns the user to the 
MAIL prompt >.  If SEND is invoked at the system control level (!), the user 
is returned to the (!) when END is entered. 
00001
END_OPTION
Syntax: 
F[ILE] C[OPY][:] [Y[ES]|N[O]|[/folder][.account]] 
Description: 
Specifies that a copy of the delivered message be made and filed in the user's 
folder.  The YES|NO options can be used to override the FILE COPY option in 
the folder's profile setting.  If a file copy is specified without the YES|NO 
options, a file copy is made.  /folder.account specifies the folder to contain 
the copy of the message.  Specifying a folder implies YES.  If no folder is 
specified, the copy is put in the folder specified by the FILE FOLDER profile 
option, not in the current folder. 
00001
A 
  APPEND Option - 
      HELP APPEND_OPTION 
  ATTACH Option - 
      HELP ATTACH_OPTION 
B 
  BLIND COPY Option - 
      HELP BLIND_COPY_OPTION 
  *BODY file - 
      HELP DO_OPTION DESCRIPTION: 
      HELP EDIT_OPTION DESCRIPTION: 
  BODY Prompt - 
      HELP BODY_PROMPT 
  BODY: Prompt - 
      HELP BODY_PROMPT DESCRIPTION: 
  BROADCAST Option - 
      HELP BROADCAST_OPTION 
C 
  CANCEL Option - 
      HELP CANCEL_OPTION 
  COPY Option - 
      HELP COPY_OPTION 
  CRPT Option - 
      HELP CRPT_OPTION 
D 
  DEFER Option - 
      HELP DEFER_OPTION 
  DELIVERY RECEIPT Option - 
      HELP DELIVERY_RECEIPT_OPTION 
  DISPLAY Option - 
      HELP DISPLAY_OPTION 
  DO Option - 
      HELP DO_OPTION 
E 
  EDIT Option - 
      HELP EDIT_OPTION 
  END Option - 
      HELP END_OPTION 
F 
  FILE COPY Option - 
      HELP FILE_COPY_OPTION 
H 
  HELP Option - 
      HELP HELP_OPTION 
L 
  LINK Option - 
      HELP LINK_OPTION 
O 
  OPTIONS Prompt - 
      HELP OPTIONS_PROMPT 
  OPTIONS: Prompt - 
      HELP OPTIONS_PROMPT DESCRIPTION: 
  OUTPUT Option - 
      HELP OUTPUT_OPTION 
P 
  PREPROCESS Option - 
      HELP PREPROCESS_OPTION 
  PRINT Option - 
      HELP PRINT 
  Processor -   
    SEND - 
      HELP PROCESSOR 
  Prompts - 
      HELP SEND_PROMPTS 
R 
  Receipt (DELIVERY RECEIPT Option) - 
      HELP OPTIONS_PROMPT DESCRIPTION: 
  Receipt (RETURN RECEIPT) - 
      HELP RETURN_RECEIPT_OPTION DESCRIPTION: 
  REFERENCE Option - 
      HELP REFERENCE_OPTION 
  REPLY TO Option - 
      HELP REPLY_TO_OPTION 
  RETURN RECEIPT Option - 
      HELP RETURN_RECEIPT_OPTION 
S 
  SEND Option - 
      HELP SEND_OPTION 
  SEND Options -   
    BLIND COPY - 
      HELP BLIND_COPY_OPTION DESCRIPTION: 
    BROADCAST - 
      HELP BROADCAST_OPTION DESCRIPTION: 
    CANCEL - 
      HELP CANCEL_OPTION DESCRIPTION: 
    COPY - 
      HELP COPY_OPTION DESCRIPTION: 
    CRPT - 
      HELP CRPT_OPTION DESCRIPTION: 
    DEFER - 
      HELP DEFER_OPTION DESCRIPTION: 
    DELIVERY RECEIPT - 
      HELP DISPLAY_OPTION DESCRIPTION: 
    DISPLAY - 
      HELP DISPLAY_OPTION DESCRIPTION: 
    DO - 
      HELP DO_OPTION DESCRIPTION: 
    EDIT - 
      HELP EDIT_OPTION DESCRIPTION: 
    END - 
      HELP END_OPTION DESCRIPTION: 
    FILE COPY - 
      HELP FILE_COPY_OPTION DESCRIPTION: 
    HELP - 
      HELP HELP_OPTION EXAMPLES: 
    LINK - 
      HELP LINK_OPTION SEE_ALSO: 
    PREPROCESS - 
      HELP PREPROCESS_OPTION DESCRIPTION: 
    REFERENCE - 
      HELP REFERENCE_OPTION DESCRIPTION: 
    REPLY TO - 
      HELP REPLY_TO_OPTION DESCRIPTION: 
    RETURN RECEIPT - 
      HELP RETURN_RECEIPT_OPTION DESCRIPTION: 
    SEND - 
      HELP SEND_OPTION DESCRIPTION: 
    SIGNED - 
      HELP SIGNED_OPTION DESCRIPTION: 
    SUBJECT - 
      HELP SUBJECT_OPTION DESCRIPTION: 
    TO - 
      HELP TO_OPTION DESCRIPTION: 
  SEND Processor - 
      HELP PROCESSOR 
  SEND Prompts -   
    Body: - 
      HELP BODY_PROMPT DESCRIPTION: 
    Options: - 
      HELP OPTIONS_PROMPT DESCRIPTION: 
    Subject: - 
      HELP SUBJECT_PROMPT DESCRIPTION: 
    To: - 
      HELP TO_PROMPT DESCRIPTION: 
  SEND Prompts - 
      HELP SEND_PROMPTS 
  SIGNED Option - 
      HELP SIGNED_OPTION 
  SUBJECT Option - 
      HELP SUBJECT_OPTION 
  SUBJECT Prompt - 
      HELP SUBJECT_PROMPT 
  SUBJECT: Prompt - 
      HELP SUBJECT_PROMPT DESCRIPTION: 
  Syntax Notation Conventions - 
      HELP NOTATION_CONVENTIONS 
T 
  TIME Option - 
      HELP TIME 
  TO Option - 
      HELP TO_OPTION 
  TO Prompt - 
      HELP TO_PROMPT 
  To: Prompt - 
      HELP TO_PROMPT DESCRIPTION: 
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
Syntax: 
HELP [(fid)] [TOPICS] [keyword1 [-] [keyword2] 
Note:  The following elements can be specified in any order: 
         (fid) 
         TOPICS 
         [keyword1] [-] [keyword2] 
For example, HELP (fid) keyword1  - keyword2 TOPICS is acceptable. 
Parameters: 
(fid)    specifies the processor name (for example, SEND).  If (fid) is 
omitted, the current processor is assumed. 
TOPICS    requests a list of topic or subtopic names, rather than an 
information message. 
Form                                       Result 
-------------------------                  ------------------------- 
HELP (fid) TOPICS                          Lists all topics 
HELP (fid) TOPICS keyword1 - keyword2      Lists all topics in the range 
                                           specified by keyword1 - keyword 2 
HELP (fid) TOPICS keyword1?                Lists all topics beginning with 
                                           the prefix specified by keyword1 
HELP (fid) TOPICS keyword1                 Lists all subtopics for the 
                                           topic specified by keyword1 
keyword1 [- [keyword2]]    specifies a topic, a range of topics, or a topic 
and subtopic to identify what HELP information is requested. 
Form                                       Result 
-------------------------                  ------------------------- 
HELP (fid) keyword1                        Displays the first level 
                                           information message for 
                                           the topic keyword1 
HELP (fid) keyword1 keyword2               Displays the information 
                                           message for keyword1, but only 
                                           the level identified by the 
                                           subtopic keyword2 
HELP (fid) TOPICS keyword1 [-] [keyword2]  Lists topic or subtopic 
                                           names.  See TOPICS parameter. 
NOTE:  keyword1 may include the wildcard (?) character as the rightmost 
character, if TOPICS is specified. 
Description: 
HELP displays information.  The HELP command can be used either within a 
processor or in IBEX.  The standard HELP command is provided by both 
processors described in this manual.  The HELP facility for processors is 
available only to users with sufficient privilege to use the processor itself. 
HELP messages have levels.  Once the initial level has been displayed, 
entering a question mark displays the next level, usually containing greater 
detail.  Entering two question marks, displays the entire message. 
Examples: 
>HELP APPEND_OPTION 
means list the syntax of the APPEND option, enter ? or ?? for more 
information. 
>HELP APPEND_OPTION SYNTAX 
means the same as the above example. 
>HELP COPY_MESSAGE EXAMP 
means list example(s) of the COPY_MESSAGE command. 
>HELP TOPICS 
means list all topic names in the HELP file (depending on which processor the 
user is currently in). 
>HELP TOPICS C - D 
means list all concept topic names between C and D in the HELP file. 
>HELP TOPICS C - Z 
means list all command topic names from C to Z in the HELP file. 
>HELP LA - LIST 
means list the entire messages for the commands between LA and LIST, 
alphabetically. 
>HELP RENUMBER - RENUMBER 
means list all the information about the RENUMBER command. 
00002
00003
00001
HELP_INDEX
Syntax: 
LINK command 
Parameters: 
command    specifies the command to be invoked. 
Description: 
The LINK option causes SEND to suspend its own execution and another program 
or command be executed.  The other program can make use of the full set of 
CP-6 command line conventions (such as DCB assignment, options processing, and 
standard invocation checking.  When that program exits, control is returned to 
SEND.  When the LINK option is entered at the Options: prompt, the message 
body is written to the file *BODY so that it is available for use by the 
invoked command. 
Examples: 
To pass control to the CALENDAR processor, the user enters: 
    >LINK CALENDAR.X 
See also: 
DO DO_OPTION 
00002
00003
00001
NOTATION_CONVENTIONS
The following table shows the notation conventions used in commands, options 
and examples. 
  Notation       Description 
  Brackets 
                 Brackets are used to enclose an optional element.  If more 
                 than one element is enclosed in brackets, the notation 
                 indicates an optional choice, multiple elements in brackets 
                 can be separated with the OR bar.  For example: 
                 [list-name]    indicates that a value for list-name may 
                                be entered. 
                 When enclosing keywords, brackets signify that all or part of 
                 the bracketed portion may be entered.  For example: 
                 SE[LECT] [MESSAGE]    indicates that the command SELECT 
                                       MESSAGE can be entered as SELECT 
                                       MESSAGE, SELECT, SELEC, SELE, 
                                       SEL or SE. 
  OR Bar 
                 The OR bar separates elements enclosed in braces or brackets 
                 from which one must or may be chosen.  For example: 
                 [WHEN|WHERE]               indicates that either WHEN 
                                            or WHERE may be entered. 
  Braces 
                 Braces around words separated by | (OR bars) indicate a 
                 required choice.  For example: 
                 {E[ND]|Q[UIT]|E[XIT]|X}    means either END, QUIT, EXIT, 
                                            or X must be selected. 
  Lowercase 
                 Lowercase letters identify an element that must be replaced 
                 by a user-selected value.  For example: 
                 DEL[ETE] FO[LDER] folder-name    indicates the user 
                                                  supplies a value for 
                                                  folder-name. 
  Carated Letters 
                 Letters inside carats (<>) identify physical keys on the 
                 terminal.  Carats are not typed.  The indicated keys are 
                 pressed.  For example: 
                 <LF>    indicates touch the Linefeed key. 
  Horizontal Ellipsis 
                 Horizontal ellipsis indicates that a previous bracketed 
                 element may be repeated or that elements have been omitted. 
                 For example: 
                 [m1[-m2][,m3[-m4]]]...    indicates that one or more 
                                           message numbers or number 
                                           ranges may be entered with a 
                                           comma or dash inserted between 
                                           each number or number range. 
  Semicolon 
                 The semicolon is a continuation character for multiple line 
                 commands and for multiple commands on a single line.  For 
                 example: 
                 AN[SWER] [MESSAGE] [m1[-m2][,m3[-m4]]]... [WHEN|WHERE]; 
                 [criteria] R[ECEIVERS] 
  Vertical Ellipsis 
                 Vertical ellipsis indicates that something has been omitted 
                 purposely.  For example: 
                 >SELECT MESSAGE 2-5           Indicates that lines 
                 >DISPLAY MESSAGE 3            have been omitted. 
                        . 
                        . 
                        . 
                 >LIST MESSAGE 5 
OPTIONS_PROMPT
Syntax: 
Options: option 
Description: 
A SEND option or message field that the user can optionally specify when a 
message is send.  The options and message fields that can be entered or 
modified at the Options: prompt are: 
AP[PEND] [fid] 
ATT[ACH] fid [TI[TLE] 'title_string'] 
B[LIND] C[OPY][:] [address] 
BR[OADCAST][:] [Y[ES]|N[O]] 
CA[NCEL] 
C[OPY][:] [address] 
CRPT: value 
DE[FER][:] [hh:mm[,mm/dd/yy]] 
D[ELIVERY] R[ECEIPT][:] [Y[ES]|N[O]] 
DI[SPLAY] [field] 
{DO|!} command 
ED[IT] [W[ITH] fid] 
E[ND]|[E]X[IT]|Q[UIT] 
F[ILE] C[OPY][:] [Y[ES]|NO]|[/folder][.account]] 
HELP 
L[INK] command 
REF[ERENCE][:] [text] 
REP[LY] T[O][:] [address] 
R[ETURN] R[ECEIPT][:] [Y[ES]|N[O]] 
S[END] 
SI[GNED][:] [signature] 
SU[BJECT][:] [text] 
T[O][:] [address] 
For more information about a specific option, enter: 
HELP option 
00001
OPTIONS_PROMPT
Syntax: 
OUT[PUT] [{ON|TO|INTO|OVER} fid] [(option-list)] 
Parameters: 
ON|TO    specifies file creation.  If the file already exists, output attempts 
result in an error condition and the output operation will not be performed 
(the default). 
INTO    specifies file extension.  If a file does not exist, a file is 
created.  If a file does exist, the output is appended to it. 
OVER    specifies file replacement.  If a file does not already exist, a file 
is created. 
fid    specifies the file or destination for output.  option-list    is a list 
of one or more options from the list below, separated by commas.  The meaning 
of these options is the same as the corresponding PCL output options.  See 
'!HELP (PCL) OUT_OPS option' for more information. 
    O[RGANIZATION]={C[ONSECUTIVE]|U[NIT]R[ECORD]} 
    F[ORM]={formname|'formname'} 
    I[XTNSIZE]=number 
    X[TNSIZE]=number 
Description: 
Causes any output from subsequent DISPLAY options to be directed to the 
specified file. 
00002
00001
Syntax: 
PRE[PROCESS] [:] [Y[ES]|N[O]] 
Description: 
Specifies whether or not command and message lines should be preprocessed to 
do IBEX command variable substitutions.  If preprocessing is requested, a (%) 
percent sign followed by the name of a currently defined IBEX command variable 
are replaced with the value of that variable.  Also, a (%%) double percent 
sign before a string that could be a command variable name is replaced by a 
single percent sign, and the following string is not checked for command 
variable substitution.  The default is determined by the PREPROCESS option in 
the mail folder's profile.  When used to override the profile option, i.e., 
specified at the Options:  prompt without a value, the default is YES. 
00001
Syntax: 
PRI[NT] 
Description: 
Causes any open symbiont output streams to be closed and their contents queued 
for printing. 
00001
PRINT

SEND_PROMPTS
END_OPTION
Syntax: 
REF[ERENCE][:] [text] 
Description: 
Specifies relevant text information to be included with a message delivery. 
The Reference field can contain up to 255 characters.  If the REFERENCE option 
is specified with no text, the contents of the current Reference field (if 
any) is displayed and the user is allowed to change or delete it. 
00001
Syntax: 
REP[LY] T[O][:] [address] 
Description: 
Specifies the addresses (users) that are to receive replies to a message. 
This field works in cooperation with the RR SEND option, and the ACKNOWLEDGE, 
and ANSWER commands.  If a reply address is not specified, by default, a 
message is returned to the sender.  One or more addresses can be entered, 
separated by commas.  If the REPLY TO option is specified with no addresses, 
the contents of the current Reply To (if any) is displayed and the user is 
allowed to change or delete it. 
00001
Syntax: 
R[ETURN] R[ECEIPT][:] [Y[ES]|N[O]] 
Description: 
Specifies that the message sender or designated recipient receive an automatic 
acknowledgment when the delivered message has been read.  The YES|NO options 
can be used to override the RETURN RECEIPT option in the folder's profile 
setting.  If RETURN RECEIPT is specified without the YES|NO option, a receipt 
is requested. 
00001
Syntax: 
S[END] 
Description: 
Specifies that the created message be sent.  MAIL then prompts the user with 
Options: to request any other desired operations. 
00001
When SEND is invoked, the user is prompted for the message recipient(s), the 
subject, and body of the message (unless specified in the file being sent). 
SEND also allows the user to specify optional information (see OPTIONS) 
displayed when sending a message. 
After responding to all of the SEND prompts, the user must enter the END or 
CANCEL command to return to the system control level (!). 
A list of SEND prompts and their descriptions can be accessed 
by typing a ? or ??.  To obtain descriptions of individual 
SEND prompts, type: 
HELP (SEND) prompt 
where prompt may be any of the following: 
TO_PROMPT 
SUBJECT_PROMPT 
BODY_PROMPT 
OPTIONS_PROMPT 
Syntax: 
SI[GNED][:] [signature] 
Description: 
Specifies a name (signature) of the message sender to appear on the delivered 
message.  The Signed field can contain up to 200 characters.  If the SIGNED 
option is specified with no text, the contents of the current Signed field (if 
any) is displayed and the user is allowed to change or delete it. 
00001
Syntax: 
SU[BJECT][:] [text] 
Description: 
Specifies the topic of discussion of a message.  The Subject field can contain 
up to 256 characters.  The Subject option can be used to replace or delete the 
original text in the Subject field of the message.  If the SUBJECT option is 
specified with no text, the contents of the current Subject field (if any) is 
displayed and the user is allowed to change or delete it. 
00001
Syntax: 
Subject: text 
Description: 
A one-line description of the message which can contain up to 256 characters. 
The first 36 characters appear as the subject text in a LIST MESSAGE display. 
00001
Syntax: 
{T[IME]|DA[TE]} 
Description: 
The TIME command prints the current date and time. 
00001
TIME
Syntax: 
T[O][:] [address] 
Description: 
Specifies the addresses that are to receive a message.  One or more addresses 
can be specified, separated by commas.  The TO option can be used to modify 
the To list originally specified for the message.  If the TO option is 
specified with no address list, the contents of the current To field is 
displayed and the user is allowed to change or delete it. 
00001
Syntax: 
To: address 
Description: 
A 1-200 alphabetic character value that identifies the recipient(s) of a 
message.  The address can include one or more addresses or mailing lists 
separated by commas. 
00001
END_OPTION
