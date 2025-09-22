The MAIL processor is invoked at the system control level (!): 
    MAIL [name][/folder][.account][(options)] 
MAIL responds by printing the following message: 
    Mail B04 Here 
    LIST NEW 
    > 
The greater-than sign (>) is the prompt indicating that MAIL is prepared to 
receive commands.  The "LIST NEW" command is displayed the first time a user 
accesses the electronic MAIL system.  This command causes all new messages to 
be listed.  The "LIST NEW" command is the default Setup command when the user 
initially invokes MAIL and can be changed by the user (see the SETUP option of 
the PROFILE command). 
Parameters: 
name    specifies the user name.  MAIL searches the appropriate address lists 
to find the default folder for "name".  If name is specified, account must be 
excluded. 
folder    specifies the folder name where messages are stored.  If a folder is 
not specified, the Central folder is assumed. 
account    specifies the name of the account where the folder is stored.  If 
account is specified, name must be excluded. 
options    specifies one of the following options: 
    B[YPASS]    specifies that the SETUP option of the PROFILE command not be 
    executed. 
    E[ND]    specifies that the SETUP option of the PROFILE command be 
    executed.  If messages are processed, MAIL prompts for a command; 
    otherwise, MAIL is exited and control is returned to the system control 
    level. 
    E[ND] N[OUPDATE]    specifies that the SETUP option be executed, that no 
    message status flags be updated, and that MAIL be exited. 
To obtain more HELP information if you are in the 
MAIL processor, enter: 
HELP TOPICS               for a list of MAIL topics. 
HELP COMMANDS             for a list of MAIL command groups. 
HELP command              for a specific MAIL command. 
HELP (SEND)               for invoking the SEND processor. 
HELP (SEND) TOPICS        for a list of SEND topics. 
HELP (SEND) PROMPTS       for a list of SEND prompts. 
HELP (SEND) OPTIONS       for a list of SEND options. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
THIS
Syntax: 
AC[KNOWLEDGE] [MESSAGE] [selection_criteria] 
Parameters: 
selection_criteria    composed of message numbers, status flags, field names 
and logical or relational operators that specify the messages that are to be 
selected. 
SEE_ALSO: 
SELECTION_CRITERIA, RELATIVE_CRITERIA, EXPLICIT CRITERIA 
RANGE_SELECTION, CONTENT_SELECTION, STRING_SELECTION, DATE_SELECTION 
Description: 
The ACKNOWLEDGE_MESSAGE command returns a brief acknowledgment to the 
originator or to the designated recipient, that the delivered message has been 
received and read.  The Subject field of the returned message is the same as 
the original.  The message display heading identifies the message being 
acknowledged by message number.  The message body of the returned message will 
read:  "Message acknowledged".  In a LIST display, messages created by an ACK 
command have a description field of "ack". 
Examples: 
To acknowledge a received message, the MAIL user enters: 
    >ACKNOWLEDGE MESSAGE 199 
    msg#    when sent      recs          (from) subject 
     199   07/23 11:30       9 (Esther William> Swimming lessons 
      Message sent. 
    > 
Message number 199 is listed with a message indicating that an acknowledgment 
has been sent. 
Already selected messages can be acknowledged with a parameterless 
ACKNOWLEDGE_MESSAGE command as follows: 
    >DISPLAY MESSAGE 23 
           . 
           .    The requested message is listed. 
           . 
    >ACKNOWLEDGE MESSAGE 
Message number 23 is first displayed and then acknowledged. 
See also: 
ANSWER_MESSAGE, SELECTION_COMMANDS, SYSTEM_GENERATED_MESSAGES ACK_MESSAGE 
00002
00003
00001
Syntax: 
[name][/folder[.account]][@site] 
Parameters: 
name    is a string of 1 to 200 characters defined by the CREATE USER command 
(registered name) or the CREATE LIST command (local, personal names).  The 
valid character set for a name includes the uppercase and lowercase alphabet, 
the digits 0 through 9, and the following characters: 
    ^   (blank) 
    $   (dollar sign) 
    _   (underscore) 
    -   (hyphen) 
    #   (pound sign) 
    %   (percent sign) 
    .   (period) 
The maximum length of the name depends on the length of other parameters used; 
the 200 character limit applies to the whole address, of which name is only 
one part. 
folder    is a character string of 1 to 25 characters specifying the name of 
the folder.  The valid character set for a folder includes the uppercase and 
lowercase alphabet, the digits 0 through 9, and the following characters: 
    $    (dollar sign) 
    -    (hyphen) 
    _    (underscore) 
    :    (colon) 
account    is a string of 1 to 8 characters that identifies a file directory. 
The valid characters for the account parameter are the same as those for the 
folder parameter.  Accounts are created by the system manager. 
site    is a string of 1 to 8 characters specifying the destination system 
that contains the recipient's folder or the network name of a mail gateway. 
Workstations are defined by the system manager; sending messages between CP-6 
systems requires the active cooperation of all system managers wishing to 
exchange messages using MAIL. 
Description: 
The term "address" is used in the remainder of this manual to denote the 
generic destination of a message.  An address is a name, a folder, or a 
combination of the two. 
At least one of the parameters (name, folder or account) must be specified to 
form a valid address.  If name is specified, account cannot be, and vice 
versa.  When name is used in conjunction with folder, the account implied is 
that identified in the system registry for that name. 
If a folder name is not specified, the relevant central folder is assumed.  If 
the name parameter is specified, and it identifies a registered name, the 
central folder identified in the registry is used.  If the name is local or 
personal, the folder implied in the name definition is used.  If only the 
account is specified, the /CENTRAL folder in the named account is assumed. 
00002
00001
ADDRESSES
    Administration commands are: 
        CREATE_USER 
        DELETE_USER 
        DISPLAY_USER_ADMIN 
        MODIFY_USER 
    For more information enter: 
        HELP command 
CREATE_USER
DELETE_USER
MODIFY_USER
Syntax: 
AN[SWER] [MESSAGE] [selection_criteria] [S[ENDER]|R[ECEIVERS]] 
Parameters: 
selection_criteria    composed of message numbers, status flags, field names 
and logical or relational operators that specify the messages that are to be 
selected. 
SEE_ALSO: 
SELECTION_CRITERIA, RELATIVE_CRITERIA, EXPLICIT CRITERIA 
RANGE_SELECTION, CONTENT_SELECTION, STRING_SELECTION, DATE_SELECTION 
[S[ENDER]|R[ECEIVERS]]    specifies whether ANSWER commands are to send 
messages only to the originator or to the originator plus all recipients by 
default.  SENDER specifies that answers are to be sent only to the originator 
or the designated recipient for replies.  RECEIVERS specifies that copies of 
the answer are also to be sent to all recipients.  The default is the setting 
of the ANSWER profile option in the current folder. 
Description: 
The ANSWER_MESSAGE command sends a reply message to the originator or 
designated recipient in response to a received message.  The header of the 
original message is displayed to ensure that the response is made to the 
correct message.  The answer message includes a Reference field that 
identifies the sending user's message number and includes the Subject field of 
the original message.  If a new Subject field is specified, it is copied into 
the Subject field of the answered message. 
Examples: 
To respond to received message number 199, the MAIL user enters: 
    >ANSWER MESSAGE 199 
    msg#    when sent      recs          (from) subject 
     199   07/23 11:30       9 (Esther William> Swimming lessons 
    SUBJECT:See you at the pool 
    BODY:I shall be there 
         <CR> 
    OPTIONS:END 
      Message sent. 
Message number 199 is listed.  The user is placed in SEND mode and prompted 
for new message information.  The response to message number 199 is sent. 
See also: 
ACKNOWLEDGE_MESSAGE, PROFILE, SELECTION_COMMANDS 
00002
00003
00001
ANSWER_MESSAGE
Following is a summary of changes from past behavior that were made necessary 
by new features in the B04 release. 
1.  MAIL now allows data to be included with messages as enclosures. 
    Enclosures are attached to a mailgram by the sender, made known to the 
    receiver via the updated message and list displays, and removed by the 
    receiver to a file. 
    Enclosures are designed and intended as a method for enabling users to 
    include PC-specific files with electronic mail.  As such, any type of file 
    containing any type of data can be attached to a message.  There are no 
    limitations imposed by MAIL for the number or size of records, format, 
    etc.  Up to 99 enclosures can be attached to a mailgram. 
2.  MAIL opens enclosure source files when attaching, and destination files 
    when detaching, with ORG=CONSECUTIVE.  This implies that while any file 
    may be attached to a message, keyed or indexed files will not retain the 
    keys and/or indices. 
    Since there are no size limits on enclosures, the use of disk space can 
    easily become a factor where it may not have been in the past.  The DELETE 
    ON DETACH profile option, described below, is provided to help avoid this 
    problem. 
Enhancements in B04 
    This section describes new features that were added in the B04 release. 
    Each enhancement is described below separately; they appear in no 
    particular order. 
New SEND Option 
    ATT[ACH] fid [TI[TLE] 'title_string'] 
    Specifies a file to be attached as an additional enclosure to the current 
    message.  The optional title may be up to 256 characters, but only the 
    first 80 characters will be displayed.  Additional files and titles may be 
    specified in a list delimited by commas. 
New MAIL Command 
    DET[ACH] encl_num [(DEL[ETE])] output_clause [(option)] 
    The DETACH command is used to separate an enclosure from a message.  Any 
    enclosures contained in a message are displayed with the message header. 
    It is required when DETACHing an enclosure that one, and only one, message 
    be in the current selection context.  That is, enclosures can't be 
    DETACHed from more that one message at a time. 
New MAIL PROFILE Options 
    DEL[ETE] [ON] DET[ACH]={Y[ES]|N[O]} 
    YES specifies that when an enclosure is DETACHed, it will be deleted 
    whether or not the DELETE option is used.  NO indicates that an enclosure 
    will not be deleted unless DELETE is used explicitly in the DETACH 
    command.  The default is NO. 
    EXT[TENDED] ADDR[ESS] DISP[LAY]={Y[ES]|N[O]} 
    YES specifies that all address information is displayed from the address 
    records in the message.  NO displays the text strings from the address 
    fields in the message header.  The default is NO. 
STAR Fixes 
    A number of bug fixes and minor enhancements have also been made in this 
    release.  For a list of Stars fixed in this release (excluding those 
    enhancements that were described above) refer to the MAIL Software Release 
    Bulletin (SRB) or to STARLOG for MAIL Stars with a status of CLPEND. 
The CP-6 electronic MAIL commands can be separated into the following usage 
groups: 
MESSAGE_COMMANDS 
FOLDER_COMMANDS 
MAILING_LIST_COMMANDS 
MISCELLANEOUS_COMMANDS 
SELECTION_COMMANDS 
DELETE_COMMANDS 
DISPLAY_COMMANDS 
REGISTRATION_COMMANDS 
For more information about a specific command group, enter 
HELP command_group 
COMMANDS
Syntax: 
      {flag-selection     } 
[NOT] {string-selection   } [{AND|OR} content-selection] 
      {date-selection     } 
      {(content-selection)} 
Parameters: 
flag-selection    specifies that messages with a given status flag are to be 
selected.  Status flags, and their spellings in context selection, are: 
    AC[KNOWLEDGMENT] 
    AN[SWER] 
    {BRO[ADCAST] | B[RD]} 
    {DELI[VERY] | DLV} 
    D[ELETED] 
    ER[ROR] 
    EX[AMINED] 
    FC[OPY] 
    FW[D] 
    M[ARKED] 
    N[EW] 
    OL[D] 
    RR 
    UNE[XAMINED] 
string-selection    specifies that messages whose header field contents match 
or do not match a given value are to be selected, as described under 
STRING_SELECTION. 
date-selection    specifies that messages whose dates have the proper relation 
to a given value are to be selected, as described under DATE_SELECTION. 
content-selection    specifies that selection be made on multiple content 
selections, which can be combined by make a complex logical expression using 
the AND, OR and NOT operators, with parenthesis to indicate nesting.  In the 
absence of nesting, NOT refers to the criterion that immediately follows it, 
and AND and OR have equal precedence. 
Description: 
The content selection component of explicit selection criteria restricts a 
message command to only those messages whose header fields or status flags 
match the specified criteria.  Content selection criteria can combine tests 
against multiple header fields and flags to form logical expressions or 
arbitrary complexity.  The keywords NOT, AND and OR can be replaced with the 
symbols ~, &, and |, respectively. 
If the selection criteria of a command includes range-selection with no 
content-selection, all messages in the specified range are selected. 
Examples: 
    >LIST MESSAGE WHEN MARK AND SUBJECT ~= ACTION 
lists all messages whose Subject does not contain ACTION and whose status is 
marked.  Field comparisons are not case sensitive, so messages with a subject 
containing "action" or "Action" are also listed. 
    >DISPLAY MESSAGE WHEN SUBJECT 'SALARIED EMPLOYEES' AND (UNEX OR MARK) 
displays all messages in the current folder whose subject contains "SALARIED 
EMPLOYEES" and whose status is either unexamined or marked.  Parenthesis are 
used around an expression to indicate nesting.  Nesting influences how an 
expression is evaluated. 
See also: 
STRING_SELECTION, DATE_SELECTION, RANGE_SELECTION 
00002
00003
00001
Syntax: 
C[OPY] [MESSAGE] [selection_criteria] {IN[TO]|TO} [name][/folder][.account] 
Parameters: 
selection_criteria    composed of message numbers, status flags, field names 
and logical or relational operators that specify the messages that are to be 
selected. 
SEE_ALSO: 
SELECTION_CRITERIA, RELATIVE_CRITERIA, EXPLICIT CRITERIA 
RANGE_SELECTION, CONTENT_SELECTION, STRING_SELECTION, DATE_SELECTION 
INTO|TO    specifies folder extension. 
name    specifies a user name. 
folder    specifies the name of the folder where messages will be stored.  If 
a folder is not specified, the central folder is assumed. 
account    specifies the name of the user account. 
Description: 
The COPY_MESSAGE command makes a copy of selected messages and places them in 
the specified folder.  The original messages are retained in the current 
folder. 
Examples: 
To make copies of one or more messages and place them in a folder, the MAIL 
user enters: 
    >COPY MESSAGE 1-2 INTO /MEMOS 
    msg#    when sent      recs          (from) subject 
       1   08/29 12:35       5    (James Kelly) Vacation Plans 
       2   09/08 15:10       1    (William Woo) Review Meeting 
    2 messages copied 
Messages 1 and 2 are copied into the /MEMOS folder. 
See also: 
MOVE_MESSAGE, SELECTION_COMMANDS, USE 
00002
00003
00001
COPY_MESSAGE
Syntax: 
COU[NT] [MESSAGE] [selection_criteria] 
Parameters: 
selection_criteria    composed of message numbers, status flags, field names 
and logical or relational operators that specify the messages that are to be 
selected. 
SEE_ALSO: 
SELECTION_CRITERIA, RELATIVE_CRITERIA, EXPLICIT CRITERIA 
RANGE_SELECTION, CONTENT_SELECTION, STRING_SELECTION, DATE_SELECTION 
Description: 
The COUNT_MESSAGE command counts the number of messages that fit the current 
selection criteria. 
Examples: 
To count the number of messages in a folder which have been examined, the MAIL 
user enters: 
    >COUNT MESSAGE 1-12 WHEN FWD 
    5 messages found 
Of the 12 messages which were selected, 5 are found which have been forwarded. 
See also: 
SELECTION_COMMANDS, RENUMBER 
00002
00003
00001
COUNT_MESSAGE
Syntax: 
CR[EATE] FO[LDER] [/folder][.account] 
Parameters: 
folder    specifies the name of the folder where messages will be stored.  If 
a folder is not specified, the central folder is assumed.  Note that the slash 
(/) is a prefix used when specifying a folder name. 
account    specifies the name of the user account.  Note that a period must 
precede the account name. 
Description: 
The CREATE_FOLDER command creates folders.  If a folder name is not specified, 
a central folder is created.  To access a newly created folder other than the 
central folder, the USE command must be specified.  To place a message in a 
newly created folder however, the user does not need to use the folder (see 
the MOVE_MESSAGE or COPY_MESSAGE commands). 
When a folder is initially created, the contents may not be read or modified 
by anyone other than the creator.  This access assignment appears as 
ALL<A>=NOLIST when the user lists the folder attributes (using the PCL command 
LIST).  If other users need to modify the folder, they must be given 
permission to write into the folder contents (write access).  In order to 
reference a folder in a SRCH list, the referencing user must have PCL read 
access to the folder. 
Examples: 
To create a new folder named PERSONNEL in the current account, the MAIL user 
enters: 
    >CREATE FOLDER /PERSONNEL 
The folder name is entered, preceded by a slash.  To access the newly created 
folder, enter: 
    USE /PERSONNEL 
See also: 
USE, DELETE_FOLDER, DISPLAY_FOLDER, COPY_MESSAGE, MOVE_MESSAGE 
00002
00003
00001
CREATE_FOLDER
Syntax: 
CR[EATE] L[IST] list_name=address[,address]... 
Parameters: 
list_name    specifies the name of a mailing list. 
address    specifies the location of users to be included in a mailing list. 
The syntax is: 
    [name][/folder][.account][@site] 
name    specifies a user name of 1-200 characters.  The name is enclosed in 
single quotes if it contains characters that are not alphanumeric and are not 
one of the following: 
    $, -, _, #, or a blank space 
folder    specifies the name of the folder where messages will be stored.  If 
a folder is not specified, the central folder is assumed. 
account    specifies the name of the user account.  The account name must be 
preceded by a period. 
site    specifies the site name. 
Description: 
The CREATE_LIST command defines a mailing list consisting of one or more 
users.  The mailing list can reference other lists.  Mailing list names can be 
used wherever an address parameter is requested. 
Examples: 
To build a mailing list named MANAGERS, the MAIL user enters: 
    >CREATE LIST MANAGERS=JOHN DOE, JANE SMITH,/MEMO.AAATEST 
The mailing list named MANAGERS includes John Doe, Jane Smith, and a user 
known only by account and folder name.  Whenever the mailing list MANAGERS is 
specified as an address, each of the users in the mailing list receives the 
message. 
See also: 
DELETE_LIST, DISPLAY_LIST, MODIFY_LIST 
00002
00003
00001
CREATE_LIST
Syntax: 
CR[EATE] U[SER] registered_name=([.account],[uname],[address]) [,(...)] 
Parameters: 
registered_name    specifies the name that appears in the From field of 
messages sent by the user.  The registered name must be enclosed in single 
quotes if non-standard characters are used. 
account    specifies the user's logon account. 
uname    specifies the user's logon name.  The uname must be specified when 
multiple users are included in one account. 
address    specifies the location and name of the user's central folder in the 
format: 
    [name][/folder][.account][@site] 
    name    specifies a user name. 
    folder    specifies the name of the folder.  The default is the central 
        folder. 
    account    specifies the account which contains the user's central folder 
        (the default is account). 
    site    specifies the user's site name. 
Description: 
The CREATE_USER command allows the MAIL administrator to register new users, 
therefore establishing the user on the CP-6 MAIL system. 
The logon information is substituted with the registered name so that the From 
field of a message can be filled in. 
At least one of the above parameters must be specified.  Multiple logons and 
folders can be specified.  One user can have multiple logons and receive all 
messages in one central folder, or receive messages in multiple central 
folders. 
When multiple logon/folder specifications are defined for one registered name 
and the USE command is invoked, the following rules apply: 
o   If any address specifies a site name, the folder at the local site is 
    chosen (if a folder exists). 
o   If multiple addresses exist at one site, and the current directory account 
    contains one of the folders, then it will be used.  Otherwise, the first 
    address definition will be used. 
Examples: 
To register a new user, the MAIL administrator enters: 
    >CREATE USER BURT HAMILTON=(.ACCOUNT1, UNAME1,.ACCOUNT2) 
The registered name is entered followed by the logon (.ACCOUNT1,UNAME1) and 
the account in which the central folder is located (.ACCOUNT2). 
To register a user who has multiple logons and wants to receive all messages 
in one central folder, enter: 
    >CREATE USER GEORGE SMITH=(.ACCOUNT1,,.ACCOUNT1),(.ACCOUNT2,,.ACCOUNT1) 
Two different logons are specified, but the location of the central folder is 
the same for both logons. 
To direct the user's mail to multiple folders at different sites, enter: 
    >CREATE USER HENRY JAMES=(.ACCOUNT3,,.ACCOUNT3@SITE1), 
    (.ACCOUNT4,,.ACCOUNT4@SITE2) 
Two sets of logons and accounts are entered, one for each site. 
See also: 
DELETE_USER, DISPLAY_USER_ADMIN, MODIFY_USER 
00002
00003
00001
SELECTION_CRITERIA
CREATE_USER
TIME
Syntax: 
                               { <  } 
                               { <= } 
{ DA[TE] {R[CVD]|R[ECEIVED]} } { =  } { mm/dd[yy] [[,] hh:mm] } 
{ DA[TE] [S[ENT]]            } { ~= } { hh:mm [[,] mm/dd[/yy] } 
                               { >  } 
                               { >= } 
Parameters: 
mm/dd/yy, hh:mm    specifies an optional date and/or time on which to base 
message selection. 
Description: 
Date field values can specify both the date (mm/dd[/yy]) and time (hh:mm), or 
either date or time alone.  Date alone implies the entire day; time alone 
implies the current day.  If both date and time are specified, they can appear 
in either order, and can be separated by a comma or blanks. 
Example: 
    >LIST MESSAGE WHEN DATE RECEIVED > 06/11/90,7:00 
lists all messages received after the date specified. 
See also: 
STRING_SELECTION, CONTENT_SELECTION, RANGE_SELECTION 
00002
00003
00001
The following commands are used to delete information: 
DELETE_FOLDER    Deletes the specified folder. 
DELETE_LIST      Deletes a mailing list. 
DELETE_MESSAGE   Marks a message for deletion. 
DELETE_USER      Deletes a user from the global registry. 
Complete descriptions and syntax of the above commands can be displayed by 
entering: 
HELP command 
Syntax: 
DEL[ETE] FO[LDER] [/folder][.account] 
Parameters: 
folder    specifies the name of the folder to be deleted.  If a folder is not 
specified, the central folder is assumed.  Wildcarding can be specified. 
account    specifies the name of the user account.  Note that a period must 
precede the account name. 
Description: 
The DELETE_FOLDER command deletes the specified folder.  The folder can only 
be deleted by its owner.  Folder names can be wildcarded. 
Examples: 
To delete a folder, the MAIL user enters: 
    >DELETE FOLDER /CLASS_NOTES 
    1 folders deleted 
The folder named /CLASS_NOTES is deleted from the user's account. 
See also: 
CREATE_FOLDER, DISPLAY_FOLDER, USE 
00002
00003
00001
DELETE_FOLDER
Syntax: 
DEL[ETE] L[IST] list_name 
Parameters: 
list_name    specifies the mailing list name or names to be deleted. 
Wildcarding can be used to delete several mailing lists at one time. 
Description: 
The DELETE_LIST command deletes the specified mailing list.  Mailing list 
names can be wildcarded. 
Examples: 
To delete a mailing list named TELLERS, the MAIL user enters: 
    >DELETE LIST TELLERS 
    1 list definitions deleted 
MAIL responds with the message that one mailing list has been deleted. 
See also: 
CREATE_LIST, DISPLAY_LIST, MODIFY_LIST 
00002
00003
00001
DELETE_LIST
Syntax: 
DEL[ETE] [MESSAGE] [selection_criteria] 
Parameters: 
selection_criteria    composed of message numbers, status flags, field names 
and logical or relational operators that specify the messages that are to be 
selected. 
SEE_ALSO: 
SELECTION_CRITERIA, RELATIVE_CRITERIA, EXPLICIT CRITERIA 
RANGE_SELECTION, CONTENT_SELECTION, STRING_SELECTION, DATE_SELECTION 
Description: 
The DELETE_MESSAGE command marks each specified message for deletion. 
Messages are physically deleted when MAIL is exited (using the END command or 
equivalent) or the RENUMBER command is invoked.  Messages flagged for deletion 
can be unmarked by executing the UNDELETE_MESSAGE command. 
Examples: 
To delete a message, the MAIL user enters: 
    >DELETE MESSAGE 3-4 
    msg#    when sent      recs          (from) subject 
       3   07/11 12:35       2    (Jerry Smith) Vacation Schedule 
       4   08/13 10:55       9   (John Jackson) New Equipment 
    2 messages flagged for deletion 
Messages 3-4 have been flagged for deletion.  They are not physically deleted 
until the user exits MAIL or issues the RENUMBER command.  The deletion 
request can be reversed by specifying the UNDELETE_MESSAGE command before the 
user exits MAIL. 
See also: 
UNDELETE_MESSAGE, RENUMBER, SELECTION_COMMANDS 
00002
00003
00001
DELETE_MESSAGE
Syntax: 
DEL[ETE] U[SER] registered_name 
Parameters: 
registered_name    specifies the name of a user to be deleted from the global 
registry.  The registered name must be enclosed in single quotes if 
non-standard characters are used. 
Description: 
The DELETE_USER command deletes the specified registered name from the global 
registry.  Wildcarding of registered names is allowed. 
Examples: 
To remove a user from the global registry, the MAIL administrator enters: 
    >DELETE USER MIKE JONES 
The registered name MIKE JONES is deleted from the global registry. 
See also: 
CREATE_USER, DISPLAY_USER_ADMIN, MODIFY_USER 
00002
00003
00001
DELETE_USER
Syntax: 
DET[ACH] encl_num [(DEL[ETE])] output_clause [(option)] 
Parameters: 
 encl_num    specifies the enclosure number. 
DELETE    specifies that the enclosure is to be deleted after it is 
successfully detached.  The enclosure may also be deleted if the profile 
option DELETE ON DETACH = YES when this option is not specified. 
output_clause    specifies that the enclosure is to be written to a file.  The 
syntax is: 
    {ON|TO|INTO|OVER} fid 
where the meaning of all elements is as described in OUTPUT_COMMAND. 
option    refers to one of the options below.  The meaning of these options is 
the same as the corresponding PCL commands.  See 'HELP (PCL) OUT_OPS option' 
for more information. 
    I[XTNSIZE]=number 
    X[TNSIZE]=number 
Description: 
The DETACH command is used to separate an enclosure from a message.  Any 
enclosures contained in a messsage are displayed prior to the message body. 
The enclosure number, the number of records, and an optional title provided by 
the sender are shown.  Flags indicating if the enclosure is deleted or 
forwarded are displayed as required.  An enclosure may not be detached if it 
has already been deleted.  Note: it is required that one and only one message 
be currently selected or DETACH will not function.  It is also important to 
note that files created by DETACH will be ORG=CONSEC.  This implies that if 
keyed or indexed files are ATTACHed by the sender, the keys or indexes will 
not be created when the enclosure is DETACHed. 
Examples: 
To receive a formatted display of a message, the MAIL user enters: 
    >DISPLAY MESSAGE 23 
       Send: 11/04/85 16:33  Rcvd: 11/04/85 16:35  Number: 23 
         To: Harry Sandlewood                        From: Lisa Henry 
    Subject: Weekly Meeting 
       Encl: num   recs   Title 
              1     35    Performance stats (.wks) 
    Please review the stats(1-2-3 file) prior to the meeting 
    on Wednesday. 
    Lisa 
Message number 23 is displayed in formatted form.  To DETACH the 
enclosure from the message the MAIL user enters: 
    >DETACH 1 (DEL) OVER STATS_FILE 
    Enclosure 1 detached and deleted 
When the message is now DISPLAYed the enclosure is marked as deleted: 
    Encl: num   recs   Title 
           1  d  35    Performance stats (.wks) 
00002
00003
00001
The following commands are used to display information: 
DISPLAY_LIST      Displays users included in a mailing list. 
DISPLAY_MESSAGE   Generates formatted display of a message. 
DISPLAY_PROFILE   Displays the user profile settings. 
DISPLAY_STATUS    Displays information about the current folder. 
DISPLAY_USER      Displays users registered in the global registry. 
LIST_FOLDER       Lists summary information about all folders 
                  in the user's account. 
Complete descriptions and syntax of the above commands can be displayed by 
entering: 
HELP command 
Syntax: 
DI[SPLAY] L[IST] [list_name][, output-clause] 
Parameters: 
list_name    specifies the mailing list to be displayed.  If list_name is not 
specified, all mailing lists in the current folder are displayed.  Wildcarding 
must be used to display lists in the SRCH or GLOBAL folders. 
output-clause    specifies that the display (or list) is to be written to a 
file or a device, such as a printer, instead of to the user's terminal.  The 
syntax is: 
    {ON|TO|INTO|OVER} fid [(option-list)] 
where the meaning of all elements is as described under OUTPUT_COMMAND 
Note:  The comma (,) is required when using the output clause with the DISPLAY 
       LIST command.  Otherwise, MAIL will treat the clause as part of the 
       registered list to display, e.g.: 
           DISPLAY LIST MANAGERS, ON file 
             or 
           DISPLAY LIST MANAGERS, TO file 
Description: 
The DISPLAY_LIST command displays the specified mailing list and includes all 
user names contained in the list.  If no mailing list is specified, all 
mailing lists in the current folder are displayed.  Mailing list names can be 
wildcarded. 
Examples: 
To display a mailing list, the MAIL user enters: 
    >DISPLAY LIST SECRETARIES 
    Definition for: SECRETARIES 
         Jane Smith 
         John Doe 
The mailing list named SECRETARIES is displayed showing the individual names 
contained in the list.  To list all the mailing lists in the user's account, 
the following is entered: 
    >DISPLAY LIST 
    Definition for: Managers 
        Stan Jones 
        Ellen Smith 
    Definition for: Field Engineering 
        Alan Mason 
        Jerry Berger 
To display the entire global mailing list, enter: 
    >DISPLAY LIST ? 
    Definition for:  ADMINISTRATION  (**GLOBAL**) 
        Helen Klein 
        Linda Socol 
    Definition for:  CAROL SMITH     (**GLOBAL**) 
        CAROL SMITH 
    Definition for:  FIELD ENGINEERS (**GLOBAL**) 
         Joe Smith 
         Alex Jones 
              . 
              . 
              . 
The entire global mailing list is displayed in alphabetical order.  To find a 
particular list where only a part of the name is known, the user enters: 
    >DISPLAY LIST ?LIST 
    Definition for:  DISTRIBUTIONLIST  (**GLOBAL**) 
           Secretaries 
           Programmers 
    Definition for:  REGISTRATIONLIST  (**GLOBAL**) 
           Administration 
           Exempt Employees 
    2 list definitions displayed 
All lists with the suffix LIST are searched and displayed (including the 
global mailing list tagged with **GLOBAL**).  MAIL searches for lists in the 
following sequence: 
1.  Searches in the user's folder. 
2.  Searches folders specified by the SRCH option, if any. 
3.  Searches global mailing list, if present. 
Lists are always searched in this order when the DISPLAY_LIST command is used 
with the wildcard character. 
See also: 
CREATE_LIST, DELETE_LIST, MODIFY_LIST 
00002
00003
00001
DISPLAY_LIST
Syntax: 
DI[SPLAY] [MESSAGE] [selection_criteria] [CRPT=value][[,] output-clause] 
Parameters: 
selection_criteria    composed of message numbers, status flags, field names 
and logical or relational operators that specify the messages that are to be 
selected. 
SEE_ALSO: 
SELECTION_CRITERIA, RELATIVE_CRITERIA, EXPLICIT CRITERIA 
RANGE_SELECTION, CONTENT_SELECTION, STRING_SELECTION, DATE_SELECTION 
CRPT=value    specifies that an encrypted message be displayed.  Legal values 
are:  a decimal number between one and 68719476735; an octal number preceded 
by a period (.), with a value between .0 and .777777777777; or a string of 1 
to 4 characters enclosed in single quotes (').  Only the message body is 
encrypted.  The default is no encryption (CRPT=0). 
output-clause    specifies that the display (or list) is to be written to a 
file or a device, such as a printer, instead of to the user's terminal.  The 
syntax is: 
    {ON|TO|INTO|OVER} fid [(option-list)] 
where the meaning of all elements is as described under OUTPUT_COMMAND 
Note:  The ON keyword is recommended with the DISPLAY MESSAGE command in 
       circumstances where the TO keyword might be interpreted as the TO: 
       field, or use the optional comma (,).  For best results use either of 
       the following: 
           DISPLAY MESSAGE 1-5 ON file 
             or 
           DISPLAY MESSAGE 1-5, TO file 
Description: 
The DISPLAY_MESSAGE command gives a formatted display of all messages 
specified in the selection criteria.  Once messages have been displayed by the 
user, the status flag n (for new) is removed (see SUMMARIZED STATUS_FLAGS). 
"RETURN RECEIPT" messages are acknowledged after messages are displayed by the 
message recipient.  A delivery receipt message is created after delivery of 
the message to all recipients. 
Examples: 
To receive a formatted display of a message, the MAIL user enters: 
    >DISPLAY MESSAGE 23 
       Sent: 11/04/85 16:33  Rcvd: 11/04/85 16:35  Number: 23 
         To: Harry Sandlewood                        From: Lisa Henry 
    Subject: Weekly Meeting 
    The meeting for Wednesday has been cancelled. 
    No new date has been set. 
    Lisa 
Message number 23 is displayed in formatted form. 
To display all messages marked ans, enter: 
    >DISPLAY MESSAGE ANS 
Similarly, the following DISPLAY commands display messages with the specified 
message status descriptor: 
    >DISPLAY MESSAGE N      (new messages) 
    >DISPLAY MESSAGE U      (unexamined messages) 
See also: 
LIST_MESSAGE, SELECT_MESSAGE, SELECTION_COMMANDS, LIST_FOLDER, DISPLAY_LIST, 
DISPLAY_PROFILE, DISPLAY_STATUS, DISPLAY_USER 
00002
00003
00001
DISPLAY_MESSAGE
Syntax: 
DI[SPLAY] P[ROFILE][[,] output-clause] 
Parameters: 
output-clause    specifies that the display (or list) is to be written to a 
file or a device, such as a printer, instead of to the user's terminal.  The 
syntax is: 
    {ON|TO|INTO|OVER} fid [(option-list)] 
where the meaning of all elements is as described under OUTPUT_COMMAND 
Description: 
The DISPLAY_PROFILE command displays all profile settings set for the current 
MAIL session. 
Examples: 
To list profile settings of the current user, the MAIL user enters: 
    >DISPLAY PROFILE 
     Fcopy = N, Granules = 0, Headers = N, Autoedit = N 
     Page = N, Renumber = N, Return Receipt = N, Delivery Receipt = N 
     Displaytrace = Y, Combine = N, Answer = Sender, Preprocess = N 
     Setup='List New' 
     Signed='Signature' 
The above profile settings are the default values given if the user does not 
specify any (when the folder is first created).  The user can alter any of the 
profile settings using options available under the PROFILE command.  Note that 
SIGNED is displayed only if a value has been assigned using the SIGNED profile 
option, there is no default value. 
See also: 
PROFILE 
00002
00003
00001
DISPLAY_PROFILE
Syntax: 
DI[SPLAY] ST[ATUS][[,] output-clause] 
Parameters: 
output-clause    specifies that the display (or list) is to be written to a 
file or a device, such as a printer, instead of to the user's terminal.  The 
syntax is: 
    {ON|TO|INTO|OVER} fid [(option-list)] 
where the meaning of all elements is as described under OUTPUT_COMMAND 
Description: 
The DISPLAY_STATUS command displays information about the current folder. 
Examples: 
To list status information about the current folder, the MAIL user enters: 
    >DISPLAY STATUS 
        Current folder is .HDKACCT@SITE 
        CURRENT CONTEXT is: 1-15 WHEN NEW 
        SELECTED CONTEXT is: 1-15 
        Message position within SELECTED CONTEXT is: OUTSIDE SELECTED RANGE 
        Number of messages marked for deletion is 0 
        Number of new messages is 0 
        Total number of messages is 15 
        Highest message number is 15 
The information displayed includes: 
o   The location of the current folder. 
o   Definition of the current context. 
o   Definition of the selected context. 
o   Message position within the selected context. 
o   Number of messages marked for deletion. 
o   Number of new messages in the current folder. 
o   Total number of messages in the current folder. 
o   The highest message number in the current folder. 
See also: 
SELECT_MESSAGE 
00002
00003
00001
DISPLAY_STATUS
Syntax: 
DI[SPLAY] U[SER] [registered_name][, output-clause] 
Parameters: 
registered_name    specifies the recorded user name to be displayed.  If the 
registered name is not specified, all registered names in the global registry 
are displayed.  Registered Names may also be wildcarded. 
output-clause    specifies that the display (or list) is to be written to a 
file or a device, such as a printer, instead of to the user's terminal.  The 
syntax is: 
    {ON|TO|INTO|OVER} fid [(option-list)] 
where the meaning of all elements is as described under OUTPUT_COMMAND 
Note:  The comma (,) is required when using the output clause with the DISPLAY 
       USER command.  Otherwise, MAIL will treat the clause as part of the 
       registered name to display, e.g.: 
           DISPLAY USER JOHN, OVER file 
Description: 
The DISPLAY_USER command displays the specified registered name.  Wildcarding 
of registered names is allowed. 
Examples: 
To list information which defines a user in the global registry, the user 
enters: 
    >DISPLAY USER LISA HENRY 
    Definition for: LISA HENRY 
The registered name LISA HENRY is displayed.  To find the correct spelling of 
a registered name, the user enters: 
    >DISPLAY USER KATHY? 
    Definition for: KATHY SMITH 
    Definition for: KATHY NEILSEN 
All registered names beginning with KATHY are displayed. 
00002
00003
00001
Syntax: 
DI[SPLAY] U[SER] [registered_name][, output-clause] 
Parameters: 
registered_name    specifies the recorded user name to be displayed.  If the 
registered name is not specified, all registered names in the global registry 
are displayed.  The registered name must be enclosed in single quotes if 
non-standard characters are used. 
output-clause    specifies that the display (or list) is to be written to a 
file or a device, such as a printer, instead of to the user's terminal.  The 
syntax is: 
    {ON|TO|INTO|OVER} fid [(option-list)] 
where the meaning of all elements is as described under OUTPUT_COMMAND 
Note:  The comma (,) is required when using the output clause with the DISPLAY 
       LIST command.  Otherwise, MAIL will treat the clause as part of the 
       registered list to display, e.g.: 
           DISPLAY USER MANAGERS, ON file 
             or 
           DISPLAY USER MANAGERS, TO file 
Description: 
The DISPLAY_USER command displays the specified registered name and how it is 
defined in the global registry.  Wildcarding of registered names is allowed. 
Examples: 
To list information that defines a user in the global registry, the MAIL 
administrator enters: 
    >DISPLAY USER LISA HENRY 
    Definition for: LISA HENRY 
         (.ACCOUNT1,,.ACCOUNT1@SITE1) 
The registered name LISA HENRY is displayed with the accompanying definition. 
The logon information and account where the central folder is located are 
listed. 
See also: 
CREATE_USER, DELETE_USER, MODIFY_USER 
00002
00003
00001
DISPLAY_USER
DISPLAY_USER_ADMIN
Syntax: 
{DO|!} command 
Parameters: 
command    specifies the command to be invoked. 
Description: 
Using the DO command causes MAIL to suspend its own execution and to request 
that another program be executed.  The "linked-to" program can make use of the 
full set of CP-6 command line conventions (such as DCB assignment, options 
processing, and standard invocation checking). 
Examples: 
To access the EDIT processor within MAIL, the user enters: 
!MAIL 
Mail B04 Here 
LIST NEW|MARK 
None found 
>DO EDIT 
EDIT E03 here 
* 
The user is temporarily placed in the EDIT processor.  This is 
indicated by the greeting "EDIT E03 here" and the asterisk prompt. 
If the DO command is invoked at the OPTIONS: prompt while sending 
a message, the body of the message is written to the file *BODY 
to be used by the called command. 
See also: 
LINK Command 
00002
00003
00001
DO
Syntax: 
{E[ND]|[E]X[IT]|Q[UIT]} [N[OUPDATE]] 
Parameters: 
NOUPDATE    specifies that all messages marked for deletion be ignored and 
therefore not be deleted. 
Description: 
The END command is used to exit MAIL and return the user to the system control 
level.  If the NOUPDATE parameter is not specified, MAIL deletes any messages 
marked for deletion. 
Examples: 
To exit MAIL, the user enters: 
    >END 
    ! 
The user is returned to the system control level. 
See also: 
DELETE_MESSAGE 
00002
00003
00001
END
CHANGES
END
Syntax: 
[range-selection] [[WHEN|W[HERE]] [content-selection]] 
Parameters: 
range-selection    is a range (or ranges) of message numbers, as described 
under RANGE_SELECTION. 
content-selection    is a specification of field contents and status flag 
settings, as described under CONTENT_SELECTION. 
Description: 
Explicit message selection criteria can be used in any MAIL message command to 
specify the messages on which the command is to operate.  Messages can be 
selected by number, the content of message header fields and status flags, or 
any combination of these.  If no criteria are specified, the default is the 
same set of messages processed by the last message command. 
Example: 
    >LIST MESSAGE 1-20 WHEN ACK 
lists all messages between numbers 1 and 20 that have been acknowledged. 
See also: 
RANGE_SELECTION, CONTENT_SELECTION, STRING_SELECTION, DATE_SELECTION, 
RELATIVE_CRITERIA 
00002
00003
00001
Syntax: 
FI[RST] 
Description: 
The FIRST command selects the first message that matches the selection 
criteria in the selected context.  If selection criteria are not specified, 
the first message in the current folder is selected. 
Examples: 
To display the first message in the selected context, the user enters: 
    >SELECT MESSAGE 5-10 
    >LIST MESSAGE FIRST 
    msg#    when sent      recs          (from) subject 
       5   07/28 16:23       3   (Louis Hirsch) Review Meeting 
The SELECT_MESSAGE command sets the selected context (messages 5 through 10). 
The FIRST command is entered with the LIST_MESSAGE command, so the first 
message within the selected range is listed in summarized form. 
See also: 
SELECT_MESSAGE, SELECTION_COMMANDS 
00001
00002
FIRST
FOLDER_COMMANDS
The following commands are used to access, create, delete, and list folders: 
CREATE_FOLDER    Creates a folder in the user's account. 
LIST_FOLDER      Lists summary information about all folders 
                 in the user's account. 
DELETE_FOLDER    Deletes folder(s) specified by the user. 
USE              Identifies the folder to be accessed. 
Complete descriptions and syntax of the above commands 
can be displayed by entering: 
HELP command 
Syntax: 
{FO[RWARD] [MESSAGE]|FWD} [selection_criteria] [CRPT=value] 
Parameters: 
selection_criteria    composed of message numbers, status flags, field names 
and logical or relational operators that specify the messages that are to be 
selected. 
SEE_ALSO: 
SELECTION_CRITERIA, RELATIVE_CRITERIA, EXPLICIT CRITERIA 
RANGE_SELECTION, CONTENT_SELECTION, STRING_SELECTION, DATE_SELECTION 
CRPT=value    specifies that an encrypted message be forwarded.  Legal values 
are:  a decimal number between one and 68719476735; an octal number preceded 
by a period (.), with a value between .0 and .777777777777; or a string of 1 
to 4 characters enclosed in single quotes (').  Only the message body is 
encrypted.  The default is no encryption (CRPT=0). 
Description: 
The FORWARD_MESSAGE command sends copies of messages the user has received to 
other users.  The header of the message selected is always displayed.  MAIL 
includes all original header fields as well as the original body which appears 
as the body of the forwarded message.  The user is then prompted for new 
header information (i.e., TO, SUBJECT, BODY, OPTIONS) for the forwarded 
message. 
Note:  The keyword FWD is a synonymn for the FORWARD MESSAGE command to match 
the abbreviation shown in the flag field of a message which has been 
forwarded. 
Examples: 
To forward a message to one or more addresses, the MAIL user enters: 
    >FORWARD MESSAGE 10 
    msg#    when sent      recs          (from) subject 
      10   07/30 09:44 ack   3       (Jim Carr) Product Update 
    TO:Marv Mossmond 
    SUBJECT:Product Update 
    BODY:I am forwarding this information to keep you abreast 
         of latest product decisions. 
         <CR> 
    OPTIONS:END 
      Message sent. 
    > 
Message number 10 is forwarded to another user.  MAIL displays the message in 
summarized format to the user.  The user is prompted with TO:, SUBJECT:, 
BODY:, and OPTIONS:.  The recipient of the forwarded message will receive both 
the forwarded message and the newly created message which introduces the 
forwarded message. 
See also: 
SEND, COPY_MESSAGE, SELECTION_COMMANDS 
00002
00003
00001
FORWARD_MESSAGE
Syntax: 
G[OTO] number 
Parameters: 
number    specifies a single message number. 
Description: 
The GOTO command positions the user to the specified message.  The specified 
message is then listed or displayed depending on the previous command 
selection (i.e., DISPLAY_MESSAGE or LIST_MESSAGE command).  The message number 
must be within the selected context.  The message number specified defines the 
current context. 
Examples: 
To position to message number 8 in the selected context, the user enters: 
    >GOTO 8 
       Sent: 11/17/85 13:32   Recd: 11/17/85 13:33  Number: 8 
         To: Steve James                              From: Janet Lane 
    Subject: Accounting Change 
    Please call me for information on the Jones account. 
    Janet 
Message number 8 is displayed.  In this example, the DISPLAY_MESSAGE command 
had been entered previously. 
See also: 
SELECTION_COMMANDS 
00002
00003
00001
GOTO
COMMANDS
Syntax: 
HELP [(fid)] [TOPICS] [keyword1 [-] [keyword2] 
Note:  The following elements can be specified in any order: 
         (fid) 
         TOPICS 
         [keyword1] [-] [keyword2] 
For example, HELP (fid) keyword1  - keyword2 TOPICS is acceptable. 
Parameters: 
(fid)    specifies the processor name (for example, MAIL).  If (fid) is 
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
>HELP ANSWER_MESSAGE 
means list the syntax of the ANSWER_MESSAGE command, prompt for more 
information. 
>HELP ANSWER_MESSAGE SYNTAX 
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
HELP
A 
  ACKNOWLEDGE MESSAGE Command - 
      HELP ACKNOWLEDGE_MESSAGE 
  ADD subcommand -   
    MODIFY LIST Command - 
      HELP MODIFY_LIST DESCRIPTION: 
    MODIFY USER Command - 
      HELP MODIFY_USER DESCRIPTION: 
  Administrator Commands -   
    CREATE USER - 
      HELP CREATE_USER SEE_ALSO: 
    DELETE USER - 
      HELP DELETE_USER SEE_ALSO: 
    DISPLAY USER - 
      HELP DISPLAY_USER_ADMIN SEE_ALSO: 
    MODIFY USER - 
      HELP MODIFY_USER DESCRIPTION: 
  ANSWER MESSAGE Command - 
      HELP ANSWER_MESSAGE 
  AUTOEDIT Option - 
      HELP PROFILE AUTOEDIT 
B 
  Blind Copy Field - 
      HELP FORMATTED_MESSAGE_DISPLAYS 
  Body Field - 
      HELP FORMATTED_MESSAGE_DISPLAYS 
      HELP DO SEE_ALSO: 
  *BODY file - 
      HELP DO SEE_ALSO: 
      HELP PROFILE AUTOEDIT 
      HELP PROFILE EDITOR 
C 
  COMBINE Option - 
      HELP PROFILE COMBINE 
  Command Groups - 
      HELP COMMANDS 
  Content Selection - 
      HELP CONTENT_SELECTION 
  Copy Field - 
      HELP FORMATTED_MESSAGE_DISPLAYS 
  COPY MESSAGE Command - 
      HELP COPY_MESSAGE 
  COUNT MESSAGE Command - 
      HELP COUNT_MESSAGE 
  CREATE FOLDER Command - 
      HELP CREATE_FOLDER 
  CREATE LIST Command - 
      HELP CREATE_LIST 
  CREATE USER Command - 
      HELP CREATE_USER 
  Criteria - 
      HELP SELECTION_CRITERIA 
  Current Context - 
      HELP DISPLAY_STATUS EXAMPLES: 
D 
  Date and Time Field - 
      HELP SUMMARIZED_MESSAGE_DISPLAYS 
  Date Field - 
      HELP FORMATTED_MESSAGE_DISPLAYS 
  Date Selection - 
      HELP DATE_SELECTION 
  DELETE FOLDER Command - 
      HELP DELETE_FOLDER 
  DELETE LIST Command - 
      HELP DELETE_LIST 
  DELETE MESSAGE Command - 
      HELP DELETE_MESSAGE 
  DELETE ON DETACH Option - 
      HELP PROFILE DEL_DET 
  DELETE subcommand -   
    MODIFY LIST Command - 
      HELP MODIFY_LIST DESCRIPTION: 
    MODIFY USER Command - 
      HELP MODIFY_USER DESCRIPTION: 
  DELETE USER Command - 
      HELP DELETE_USER 
  DELIVERY RECEIPT Option - 
      HELP PROFILE DELIVERY_RECEIPT 
  descriptor, message - 
      HELP SUMMARIZED_MESSAGE_DISPLAYS 
  DETACH Command - 
      HELP DETACH_COMMAND 
  DISPLAY LIST Command - 
      HELP DISPLAY_LIST 
  DISPLAY MESSAGE Command - 
      HELP DISPLAY_MESSAGE 
  DISPLAY PROFILE Command - 
      HELP DISPLAY_PROFILE 
  DISPLAY STATUS Command - 
      HELP DISPLAY_STATUS 
  DISPLAY subcommand -   
    MODIFY LIST Command - 
      HELP MODIFY_LIST DESCRIPTION: 
    MODIFY USER Command - 
      HELP MODIFY_USER DESCRIPTION: 
  DISPLAY USER Command - 
      HELP DISPLAY_USER 
      HELP DISPLAY_USER_ADMIN 
  DISPLAYTRACE Option - 
      HELP PROFILE DISPLAYTRACE 
  DO Command - 
      HELP DO 
E 
  EDITOR Option - 
      HELP PROFILE EDITOR 
  END Command - 
      HELP END 
  END subcommand -   
    MODIFY LIST Command - 
      HELP MODIFY_LIST DESCRIPTION: 
    MODIFY USER Command - 
      HELP MODIFY_USER DESCRIPTION: 
  Enhancements in B04 - 
      HELP ENHANCEMENTS_IN_B04 
  equal to (=) - 
      HELP STRING_SELECTION PARAMETERS: 
  Explicit Criteria - 
      HELP EXPLICIT_CRITERIA 
  EXTENDED ADDRESS DISPLAY Option - 
      HELP PROFILE EXT_ADDR_DISP 
F 
  FILE COPY Option - 
      HELP PROFILE FILE_COPY 
  FILE FOLDER Option - 
      HELP PROFILE FILE_FOLDER 
  FIRST Command - 
      HELP FIRST 
  Folder Commands -   
    CREATE FOLDER - 
      HELP FOLDER_COMMANDS 
    DELETE FOLDER - 
      HELP FOLDER_COMMANDS 
    LIST FOLDER - 
      HELP FOLDER_COMMANDS 
    USE - 
      HELP FOLDER_COMMANDS 
  Folder Commands - 
      HELP FOLDER_COMMANDS 
  Formatted Message Fields -   
    Blind Copy Field - 
      HELP FORMATTED_MESSAGE_DISPLAYS 
    Body Field - 
      HELP FORMATTED_MESSAGE_DISPLAYS 
    Copy Field - 
      HELP FORMATTED_MESSAGE_DISPLAYS 
    Date Field - 
      HELP FORMATTED_MESSAGE_DISPLAYS 
    From Field - 
      HELP FORMATTED_MESSAGE_DISPLAYS 
    Number Field - 
      HELP FORMATTED_MESSAGE_DISPLAYS 
    Reference Field - 
      HELP FORMATTED_MESSAGE_DISPLAYS 
    Reply To Field - 
      HELP FORMATTED_MESSAGE_DISPLAYS 
    Signed Field - 
      HELP FORMATTED_MESSAGE_DISPLAYS 
    Subject Field - 
      HELP FORMATTED_MESSAGE_DISPLAYS 
    To Field - 
      HELP FORMATTED_MESSAGE_DISPLAYS 
  Formatted Message Fields - 
      HELP FORMATTED_MESSAGE_DISPLAYS 
  FORWARD MESSAGE Command - 
      HELP FORWARD_MESSAGE 
  From Field - 
      HELP FORMATTED_MESSAGE_DISPLAYS 
  From Field (from) - 
      HELP SUMMARIZED_MESSAGE_DISPLAYS 
G 
  gateway, mail - 
      HELP ADDRESSES PARAMETERS: 
  General Form of an Address - 
      HELP ADDRESSES 
  Global Registry - 
      HELP WAIT EXAMPLES: 
  GOTO Command - 
      HELP GOTO 
  GRANULE Option - 
      HELP PROFILE GRANULES 
H 
  HEADER Option - 
      HELP PROFILE HEADERS 
  HELP Command - 
      HELP HELP 
L 
  LAST Command - 
      HELP LAST 
  LINK Command - 
      HELP LINK 
  LIST FOLDER Command - 
      HELP LIST_FOLDER 
  LIST MESSAGE Command - 
      HELP LIST_MESSAGE 
M 
  MAIL administrator - 
      HELP WAIT EXAMPLES: 
  MAIL Command Groups - 
      HELP COMMANDS 
  mail gateway - 
      HELP ADDRESSES PARAMETERS: 
  MAIL Processor - 
      HELP PROCESSOR 
  Mailing List Commands -   
    CREATE LIST - 
      HELP MAILING_LIST_COMMANDS 
    DELETE LIST - 
      HELP MAILING_LIST_COMMANDS 
    DISPLAY LIST - 
      HELP MAILING_LIST_COMMANDS 
    DISPLAY USER - 
      HELP MAILING_LIST_COMMANDS 
    MODIFY LIST - 
      HELP MAILING_LIST_COMMANDS 
  Mailing List Commands - 
      HELP MAILING_LIST_COMMANDS 
  MARK MESSAGE Command - 
      HELP MARK_MESSAGE 
  Message Commands -   
    ACKNOWLEDGE MESSAGE - 
      HELP MESSAGE_COMMANDS 
    ANSWER MESSAGE - 
      HELP MESSAGE_COMMANDS 
    COPY MESSAGE - 
      HELP MESSAGE_COMMANDS 
    COUNT MESSAGE - 
      HELP MESSAGE_COMMANDS 
    DELETE MESSAGE - 
      HELP MESSAGE_COMMANDS 
    DISPLAY MESSAGE - 
      HELP MESSAGE_COMMANDS 
    FORWARD MESSAGE - 
      HELP MESSAGE_COMMANDS 
    LIST MESSAGE - 
      HELP MESSAGE_COMMANDS 
    MARK MESSAGE - 
      HELP MESSAGE_COMMANDS 
    MOVE MESSAGE - 
      HELP MESSAGE_COMMANDS 
    SELECT MESSAGE - 
      HELP MESSAGE_COMMANDS 
    UNDELETE MESSAGE - 
      HELP UNDELETE_MESSAGE SYNTAX: 
    UNMARK MESSAGE - 
      HELP UNMARK_MESSAGE SYNTAX: 
  Message commands - 
      HELP SELECTION_CRITERIA 
      HELP MESSAGE_COMMANDS 
  message descriptor - 
      HELP SUMMARIZED_MESSAGE_DISPLAYS 
  message status flag - 
      HELP CONTENT_SELECTION PARAMETERS: 
  Miscellaneous Commands -   
    DISPLAY PROFILE - 
      HELP MISCELLANEOUS_COMMANDS 
    DISPLAY STATUS - 
      HELP MISCELLANEOUS_COMMANDS 
    DO - 
      HELP MISCELLANEOUS_COMMANDS 
    END - 
      HELP MISCELLANEOUS_COMMANDS 
    HELP - 
      HELP MISCELLANEOUS_COMMANDS 
    LINK - 
      HELP MISCELLANEOUS_COMMANDS 
    OUTPUT - 
      HELP MISCELLANEOUS_COMMANDS 
    PAGE - 
      HELP MISCELLANEOUS_COMMANDS 
    PRINT - 
      HELP MISCELLANEOUS_COMMANDS 
    PROFILE - 
      HELP MISCELLANEOUS_COMMANDS 
    READ - 
      HELP MISCELLANEOUS_COMMANDS 
    RENUMBER - 
      HELP MISCELLANEOUS_COMMANDS 
    SEND - 
      HELP MISCELLANEOUS_COMMANDS 
    TIME - 
      HELP MISCELLANEOUS_COMMANDS 
    WAIT - 
      HELP MISCELLANEOUS_COMMANDS 
  Miscellaneous Commands - 
      HELP MISCELLANEOUS_COMMANDS 
  MODIFY LIST Command - 
      HELP MODIFY_LIST 
  MODIFY LIST Subcommands -   
    ADD - 
      HELP MODIFY_LIST DESCRIPTION: 
    DELETE - 
      HELP MODIFY_LIST DESCRIPTION: 
    DISPLAY - 
      HELP MODIFY_LIST DESCRIPTION: 
    END - 
      HELP MODIFY_LIST DESCRIPTION: 
  MODIFY USER Command - 
      HELP MODIFY_USER 
  MODIFY USER Subcommands -   
    ADD - 
      HELP MODIFY_USER DESCRIPTION: 
    DELETE - 
      HELP MODIFY_USER DESCRIPTION: 
    DISPLAY - 
      HELP MODIFY_USER DESCRIPTION: 
    END - 
      HELP MODIFY_USER DESCRIPTION: 
  MOVE MESSAGE Command - 
      HELP MOVE_MESSAGE 
N 
  New MAIL Command - 
      HELP NEW_MAIL_COMMAND 
  New MAIL PROFILE Options - 
      HELP NEW_MAIL_PROFILE_OPTIONS 
  New SEND Option - 
      HELP NEW_SEND_OPTION 
  NEXT Command - 
      HELP NEXT 
  not equal to (~=) - 
      HELP STRING_SELECTION PARAMETERS: 
  Number Field - 
      HELP FORMATTED_MESSAGE_DISPLAYS 
  Number Field (msg#) - 
      HELP SUMMARIZED_MESSAGE_DISPLAYS 
O 
  OUTPUT Command - 
      HELP OUTPUT 
  Overview -   
    MAIL - 
      HELP WILDCARDING 
P 
  PAGE Command - 
      HELP PAGE 
  PAGE Option - 
      HELP PROFILE PAGE 
  PREPROCESS Option - 
      HELP PROFILE PREPROCESS 
  PREVIOUS Command - 
      HELP PREVIOUS 
  PRINT Command - 
      HELP PRINT 
  PROFILE Command - 
      HELP PROFILE 
  PROFILE Options -   
    AUTOEDIT Option - 
      HELP PROFILE AUTOEDIT 
    COMBINE Option - 
      HELP PROFILE COMBINE 
    DELETE ON DETACH Option - 
      HELP PROFILE DEL_DET 
    DELIVERY RECEIPT Option - 
      HELP PROFILE DELIVERY_RECEIPT 
    DISPLAYTRACE Option - 
      HELP PROFILE DISPLAYTRACE 
    EDITOR Option - 
      HELP PROFILE EDITOR 
    EXTENDED ADDRESS DISPLAY Option - 
      HELP PROFILE EXT_ADDR_DISP 
    FILE COPY Option - 
      HELP PROFILE FILE_COPY 
    FILE FOLDER Option - 
      HELP PROFILE FILE_FOLDER 
    GRANULE Option - 
      HELP PROFILE GRANULES 
    HEADER Option - 
      HELP PROFILE HEADERS 
    PAGE Option - 
      HELP PROFILE PAGE 
    PREPROCESS - 
      HELP PROFILE PREPROCESS 
    RENUMBER Option - 
      HELP PROFILE RENUMBER 
    REPLY TO Option - 
      HELP PROFILE REPLY_TO 
    RETURN RECEIPT Option - 
      HELP PROFILE RETURN_RECEIPT 
    SETUP Option - 
      HELP PROFILE SETUP 
    SIGNED Option - 
      HELP PROFILE SIGNED 
    SRCH Option - 
      HELP PROFILE SRCH 
  PROFILE Options - 
      HELP PROFILE FILE_COPY 
R 
  Range Selection - 
      HELP RANGE_SELECTION 
  READ Command - 
      HELP READ 
  Receipt (RETURN RECEIPT Option) - 
      HELP PROFILE RETURN_RECEIPT 
  Record Field (recs) - 
      HELP SUMMARIZED_MESSAGE_DISPLAYS 
  Reference Field - 
      HELP FORMATTED_MESSAGE_DISPLAYS 
  Registration Commands -   
    CREATE USER - 
      HELP REGISTRATION_COMMANDS 
    DELETE USER - 
      HELP REGISTRATION_COMMANDS 
    DISPLAY USER - 
      HELP REGISTRATION_COMMANDS 
    MODIFY USER - 
      HELP REGISTRATION_COMMANDS 
  Registration Commands - 
      HELP REGISTRATION_COMMANDS 
  Relative Criteria - 
      HELP RELATIVE_CRITERIA 
  RENUMBER Command - 
      HELP RENUMBER 
  RENUMBER Option - 
      HELP PROFILE RENUMBER 
  Reply To Field - 
      HELP FORMATTED_MESSAGE_DISPLAYS 
  REPLY TO Option - 
      HELP PROFILE REPLY_TO 
  RESEND MESSAGE Command - 
      HELP RESEND_MESSAGE 
  REST Command - 
      HELP REST 
  RETURN RECEIPT Option - 
      HELP PROFILE RETURN_RECEIPT 
S 
  SELECT MESSAGE Command - 
      HELP SELECT_MESSAGE 
  SELECTED Command - 
      HELP SELECTED 
  Selected Context - 
      HELP DISPLAY_STATUS EXAMPLES: 
  Selection Commands -   
    FIRST - 
      HELP SELECTION_COMMANDS FIRST 
    LAST - 
      HELP SELECTION_COMMANDS LAST 
    NEXT - 
      HELP SELECTION_COMMANDS NEXT 
    PREVIOUS - 
      HELP SELECTION_COMMANDS PREVIOUS 
    REST - 
      HELP SELECTION_COMMANDS REST 
    SELECTED - 
      HELP SELECTION_COMMANDS SELECTED 
    THIS - 
      HELP SELECTION_COMMANDS THIS 
  Selection Commands - 
      HELP SELECTION_COMMANDS FIRST 
  Selection Criteria -   
    Content Selection - 
      HELP EXPLICIT_CRITERIA PARAMETERS: 
    Date Selection - 
      HELP RELATIVE_CRITERIA 
    Explicit Criteria - 
      HELP EXPLICIT_CRITERIA 
    Range Selection - 
      HELP RANGE_SELECTION 
    Relative Criteria - 
      HELP RELATIVE_CRITERIA 
    String Selection - 
      HELP EXPLICIT_CRITERIA DESCRIPTION: 
  Selection Criteria - 
      HELP SELECTION_CRITERIA 
  SEND Command - 
      HELP SEND 
  SEND Processor - 
      HELP SEND DESCRIPTION: 
  SETUP Option - 
      HELP PROFILE SETUP 
  Signed Field - 
      HELP FORMATTED_MESSAGE_DISPLAYS 
  SIGNED Option - 
      HELP PROFILE SIGNED 
  SRCH Option - 
      HELP PROFILE SRCH 
  STAR Fixes - 
      HELP STAR_FIXES 
  Status Field - 
      HELP SUMMARIZED_MESSAGE_DISPLAYS 
  Status Flag Field - 
      HELP SUMMARIZED_MESSAGE_DISPLAYS 
  status flag, message - 
      HELP CONTENT_SELECTION PARAMETERS: 
  Status Flags - 
      HELP SELECTION_CRITERIA 
  String Selection - 
      HELP STRING_SELECTION 
  Subject Field - 
      HELP FORMATTED_MESSAGE_DISPLAYS 
  Subject Field (subject) - 
      HELP SUMMARIZED_MESSAGE_DISPLAYS 
  Summarized Message Fields -   
    Date and Time Field (when sent) - 
      HELP SUMMARIZED_MESSAGE_DISPLAYS 
    From Field (from) - 
      HELP SUMMARIZED_MESSAGE_DISPLAYS 
    Number Field (msg#) - 
      HELP SUMMARIZED_MESSAGE_DISPLAYS 
    Record Field - 
      HELP SUMMARIZED_MESSAGE_DISPLAYS 
    Status Field - 
      HELP SUMMARIZED_MESSAGE_DISPLAYS 
    Status Flag Field - 
      HELP SUMMARIZED_MESSAGE_DISPLAYS 
    Subject Field (subject) - 
      HELP SUMMARIZED_MESSAGE_DISPLAYS 
  Summarized Message Fields - 
      HELP SUMMARIZED_MESSAGE_DISPLAYS 
  Syntax Notation Conventions - 
      HELP NOTATION_CONVENTIONS 
T 
  THIS Command - 
      HELP THIS 
  TIME Command - 
      HELP TIME 
  To Field - 
      HELP FORMATTED_MESSAGE_DISPLAYS 
U 
  UNDELETE MESSAGE Command - 
      HELP UNDELETE_MESSAGE 
  UNMARK MESSAGE Command - 
      HELP UNMARK_MESSAGE 
  USE Command - 
      HELP USE 
W 
  WAIT Command - 
      HELP WAIT 
  Wildcard Character - 
      HELP WILDCARDING 
  Wildcarding - 
      HELP WILDCARDING 
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
HELP_INDEX
Syntax: 
LA[ST] 
Description: 
The LAST command selects the last message which matches the selection criteria 
in the selected context.  If selection criteria is not specified, the last 
message in the current folder is selected. 
Examples: 
To list the last message in the selected context, the MAIL user enters: 
    >SELECT MESSAGE 2-8 
    >LAST 
    msg#    when sent      recs          (from) subject 
       8   07/31 13:33 ack   3     (Teresa Wai) Luncheon 
Message number 8 is listed.  The message is either displayed or listed in 
summarized form depending on whether the DISPLAY_MESSAGE or LIST_MESSAGE 
command was entered prior to the Selection command. 
See also: 
SELECTION_COMMANDS 
00001
00002
LAST
NEXT
Syntax: 
LINK command 
Parameters: 
command    specifies the command to be invoked. 
Description: 
The LINK command causes MAIL to suspend its own execution and another program 
or command be executed.  The LINK and DO commands are synonymous.  When that 
program exits, control is returned to MAIL. 
Examples: 
To pass control to the CALENDAR processor, the user enters: 
    >LINK CALENDAR.X 
See also: 
DO DO_COMMAND 
00002
00003
00001
LINK
MAILING_LIST_COMMANDS
Syntax: 
L[IST] FO[LDER] [/folder][.account][[,] output-clause] 
Parameters: 
folder    specifies the name of the folder.  If a folder is not specified, the 
central folder is assumed.  Wildcarding can be specified. 
account    specifies the name of the user account.  Note that the period must 
precede the account name. 
output-clause    specifies that the display (or list) is to be written to a 
file or a device, such as a printer, instead of to the user's terminal.  The 
syntax is: 
    {ON|TO|INTO|OVER} fid [(option-list)] 
where the meaning of all elements is as described under OUTPUT_COMMAND 
Description: 
The LIST_FOLDER command prints summary information about the named folder.  If 
a folder name is not specified, all folders owned by the user are displayed. 
Folder names can be wildcarded. 
Examples: 
To list all folders in the user's account, the following is entered: 
    >LIST FOLDER 
     07/17/86 15:00 .JDLSECR 
    OWNER  #MSGS #NEW USED GRAN  NAME 
      Y       10    2   70    -  /CENTRAL 
      Y        6    0    3 FULL  /ACCTS 
      Y        1    0    2   10  /MEMO 
    3 folders displayed 
The LIST_FOLDER command is entered alone, so all folders in the user's account 
are displayed.  The following information about each folder is listed: 
o   OWNER           Owner of the folder.  The "Y" means YES. 
o   #MSGS           Number of messages in the folder. 
o   #NEW            Number of new messages in the folder. 
o   USED            Number of granules used in the folder. 
o   GRAN            Maximum number of granules that can be used 
                    for this folder.  A dash (-) in this column 
                    indicates that an unlimited amount of granules 
                    have been allocated for this folder.  If "FULL" 
                    appears in this column, the folder is full. 
o   NAME            Name of the folder. 
See also: 
CREATE_FOLDER, DELETE_FOLDER, USE 
00002
00003
00001
LIST_FOLDER
Syntax: 
L[IST] [MESSAGE] [selection_criteria][[,] output-clause] 
Parameters: 
selection_criteria    composed of message numbers, status flags, field names 
and logical or relational operators that specify the messages that are to be 
selected. 
SEE_ALSO: 
SELECTION_CRITERIA, RELATIVE_CRITERIA, EXPLICIT CRITERIA 
RANGE_SELECTION, CONTENT_SELECTION, STRING_SELECTION, DATE_SELECTION 
output-clause    specifies that the display (or list) is to be written to a 
file or a device, such as a printer, instead of to the user's terminal.  The 
syntax is: 
    {ON|TO|INTO|OVER} fid [(option-list)] 
where the meaning of all elements is as described under OUTPUT_COMMAND 
Note:  The ON keyword is recommended with the LIST MESSAGE command in 
       circumstances where the TO keyword might be interpreted as the TO: 
       field, or use the optional comma (,).  For best results use either of 
       the following: 
           LIST MESSAGE 1-5 ON file 
             or 
           LIST MESSAGE 1-5, TO FILE 
Description: 
The LIST_MESSAGE command prints a summarized display of each message 
specified.  If no criteria are specified, all current messages are listed. 
Examples: 
To receive a summary display of a message, the MAIL user enters: 
    >LIST MESSAGE 14 
    msg#    when sent      recs          (from) subject 
      14   07/31 08:55       3   (Louis Hirsch) Status Report 
To receive a summary display of all messages in the current folder, the MAIL 
user enters: 
    >LIST MESSAGE ALL 
To list all messages sent from users with the character string Klein in their 
names and a status flag of u, enter: 
    >LIST MESSAGE FROM Klein & UNEXAM 
See also: 
DISPLAY_MESSAGE, SELECT_MESSAGE, SELECTION_COMMANDS 
00002
00003
00001
LIST_MESSAGE
MAILING_LIST_COMMANDS
The following commands allow the user and MAIL administrator to create and 
maintain personal or registered mailing lists: 
CREATE_LIST    Creates a mailing list. 
DELETE_LIST    Deletes a mailing list. 
DISPLAY_LIST   Displays users included in a mailing list. 
DISPLAY_USER   Displays users registered 
               in the global registry. 
MODIFY_LIST    Modifies a mailing list. 
Complete descriptions and syntax of the above commands 
can be displayed by entering: 
HELP command 
Syntax: 
MA[RK] [MESSAGE] [selection_criteria] 
Parameters: 
selection_criteria    composed of message numbers, status flags, field names 
and logical or relational operators that specify the messages that are to be 
selected. 
SEE_ALSO: 
SELECTION_CRITERIA, RELATIVE_CRITERIA, EXPLICIT CRITERIA 
RANGE_SELECTION, CONTENT_SELECTION, STRING_SELECTION, DATE_SELECTION 
Description: 
The MARK_MESSAGE command places a tag on specified messages.  The tag can be 
used at a later time to manupulate the message in some manner.  For instance, 
a user may need to follow up with some action based on the contents of a 
message.  If this cannot be done immediately, the user can mark the message as 
a cue for later action.  If the SETUP parameter in the user's profile is set 
to 'LIST NEW OR MARK', the tagged message would be listed every time MAIL is 
entered.  The mark can be removed by invoking the UNMARK_MESSAGE command. 
Examples: 
To tag a message, the MAIL user enters: 
    >MARK MESSAGE 33 
    msg#    when sent      recs          (from) subject 
      33   07/28 10:25       3     (Mary Quick) Vacation Plans 
    1 messages marked 
Message number 33 is now marked as shown: 
    >LIST MESSAGE 33 
    msg#    when sent      recs          (from) subject 
      33 m 07/28 10:25       3     (Mary Quick) Vacation Plans 
See also: 
UNMARK_MESSAGE, SELECTION_COMMANDS 
00002
00003
00001
MARK_MESSAGE
The following commands are used to process messages received by the user: 
ACKNOWLEDGE_MESSAGE    Acknowledges a received message. 
ANSWER_MESSAGE         Responds to a received message. 
COPY_MESSAGE           Makes a copy of a message. 
COUNT_MESSAGE          Counts messages which match the current 
                       selection criteria. 
DELETE_MESSAGE         Marks a message for deletion. 
DISPLAY_MESSAGE        Generates formatted display of a message. 
FORWARD_MESSAGE        Delivers received messages to a specified address. 
LIST_MESSAGE           Lists summary information of a message. 
MARK_MESSAGE           Tags/marks a message. 
MOVE_MESSAGE           Moves a message into another folder. 
SELECT_MESSAGE         Sets the selected context according to the 
                       messages which are selected. 
UNDELETE_MESSAGE       Reverses the DELETE MESSAGE command. 
UNMARK_MESSAGE         Reverses the MARK MESSAGE command. 
All message commands list two syntax formats. 
The first syntax uses standard selection criteria. 
The second syntax format uses selection commands 
which require an understanding of current and selected 
context. 
Complete descriptions and syntax of the above commands 
can be displayed by entering: 
HELP command 
These commands, which fall under the command group "Message commands", use 
standard selection criteria as discussed under SELECTION_CRITERIA When 
selection criteria or message numbers are not specified with a message 
command, the command is invoked on the previously selected message(s). 
The following commands provide information, allow the user to manipulate 
folder profiles, create hard copies of messages, and permit interaction with 
other CP-6 files and processors: 
DISPLAY_PROFILE    Displays the user profile settings. 
DISPLAY_STATUS     Displays information about the current folder. 
DO                 Invokes a command at the IBEX control level. 
END                Exits MAIL and returns user to the 
                   system control level. 
HELP               Supplies on-line HELP information. 
LINK               Causes control to be temporarily transferred to 
                   a named program. 
OUTPUT             Directs output to a specified destination. 
PAGE               Causes a page eject. 
PRINT              Initiates printing of messages at the line printer. 
PROFILE            Sets the MAIL profile for the current folder. 
READ               Reads commands from a file. 
RENUMBER           Renumbers all messages in a folder beginning 
                   with number one. 
SEND               Initializes the sending of a new MAIL message. 
TIME               Displays the current date and time. 
WAIT               Causes a pause in MAIL until a new message 
                   is received. 
Complete descriptions and syntax of the above commands 
can be displayed by entering: 
HELP command 
Syntax: 
MOD[IFY] L[IST] list_name 
Parameters: 
list_name    specifies the mailing list to be altered. 
Description: 
The MODIFY_LIST command is used to modify an already defined mailing list. 
The prompt LIST> is issued when the MODIFY_LIST command is entered.  The 
following subcommands are entered at the LIST> prompt to alter the mailing 
list: 
    A[DD] address              adds the specified address to the mailing 
                               list. 
    DEL[ETE] address           deletes the specified address from the 
                               mailing list. 
    DI[SPLAY]                  displays the entire mailing list. 
    {E[ND]|Q[UIT]|E[XIT]|X}    exits MODIFY_LIST command mode and 
                               returns the user to the MAIL prompt. 
address    specifies the location of users to be included in a mailing list. 
The syntax is: 
    [name][/folder][.account][@site] 
where 
name    specifies a user name of 1-200 characters.  The name must be enclosed 
in single quotes if it contains characters that are not alphanumeric and not 
one of the following: 
    $, -, _, #, or a blank space 
folder    specifies the name of the folder where messages will be stored.  If 
a folder is not specified, the central folder is assumed. 
account    specifies the name of the user account.  Note that a period must 
precede the account name. 
site    specifies the site name. 
Examples: 
To modify the mailing list DEVELOPMENT GROUP, the MAIL user enters: 
    >MODIFY LIST DEVELOPMENT GROUP 
    LIST>DISPLAY 
    Definition for:  DEVELOPMENT GROUP 
        CONSULTANT 
        DESIGNER 
        MANAGER 
    LIST>ADD PROGRAMMERS 
    LIST>DISPLAY 
    Definition for:  DEVELOPMENT GROUP 
        CONSULTANT 
        DESIGNER 
        MANAGER 
        PROGRAMMERS 
    LIST>DELETE MANAGER 
    LIST>DISPLAY 
    Definition for:  DEVELOPMENT GROUP 
        CONSULTANT 
        DESIGNER 
        PROGRAMMER 
    LIST>END 
    > 
The user enters MODIFY_LIST subcommands at the LIST> prompt to display, 
delete, and add to a mailing list.  The MODIFY_LIST command mode is exited by 
entering the END subcommand at the LIST> prompt. 
See also: 
CREATE_LIST, DELETE_LIST, DISPLAY_LIST 
00002
00003
00001
MODIFY_LIST
Syntax: 
MOD[IFY] U[SER] registered_name 
Parameters: 
registered_name    specifies the user definition to be altered. 
Description: 
The MODIFY USER command is used to modify an already defined user definition. 
The prompt USER> is issued when the MODIFY USER command is entered.  The 
following subcommands are entered at the USER> prompt to alter the used 
definition: 
A[DD] definition    adds the specified definition to the user's registration. 
DEL[ETE] definition    deletes the specified definition from the user 
    registration. 
DI[SPLAY]    displays the current user definition. 
{E[ND]|Q[UIT]|E[XIT]|X}    exits MODIFY USER command mode and returns the user 
    to the MAIL prompt. 
    definition    specifies the location of a mailbox to be included in the 
        user's registration.  The syntax is: 
            ([.account],[uname],[address]) 
        account    specifies the user's logon account. 
        uname    specifies the user's logon name.  The uname must be specified 
            when multiple users are included in one account. 
    address    specifies the location and name of the user's central folder in 
        the format: 
            [name][/folder][.account][@site] 
        name    specifies a user name. 
        folder    specifies the name of the folder.  The default is the 
            central folder. 
        account    specifies the account which contains the user's central 
            folder (the default is account). 
        site    specifies the user's site name. 
See also: 
CREATE_USER, DELETE_USER, DISPLAY_USER 
00002
00001
MODIFY_USER
Syntax: 
MOV[E] [MESSAGE] [selection_criteria] {IN[TO]|TO} [name][/folder][.account] 
Parameters: 
selection_criteria    composed of message numbers, status flags, field names 
and logical or relational operators that specify the messages that are to be 
selected. 
SEE_ALSO: 
SELECTION_CRITERIA, RELATIVE_CRITERIA, EXPLICIT CRITERIA 
RANGE_SELECTION, CONTENT_SELECTION, STRING_SELECTION, DATE_SELECTION 
criteria    is a logical expression composed of message status flags, message 
descriptors, field names and values (From, Reference, Reply To, Subject, and 
To fields only) and logical operators (&,~,|,~=,=) that specify the messages 
that are to be moved. 
INTO|TO    specifies folder extension. 
name    specifies a user name. 
folder    specifies the name of the folder where messages will be stored.  If 
a folder is not specified, the central folder is assumed. 
account    specifies the name of the user account. 
selection_criteria    composed of message numbers, status flags, field names 
and logical or relational operators that specify the messages that are to be 
selected. 
SEE_ALSO: 
SELECTION_CRITERIA, RELATIVE_CRITERIA, EXPLICIT CRITERIA 
RANGE_SELECTION, CONTENT_SELECTION, STRING_SELECTION, DATE_SELECTION 
Description: 
The MOVE_MESSAGE command moves messages into a specified folder.  At the same 
time, the selected messages in the current folder are marked for deletion. 
Examples: 
To place a message into another folder, the MAIL user enters: 
    >MOVE MESSAGE 20 INTO /MEMOS 
    msg#    when sent      recs          (from) subject 
      20   09/03 11:04       4  (David Jackson) Business Trip 
    1 messages copied 
    1 messages flagged for deletion 
Message number 20 is moved into the folder named /MEMOS and is marked for 
deletion in the current folder.  The message is physically deleted when MAIL 
is exited (using the END command or its equivalent), when the RENUMBER command 
is issued, or when another folder is used (with the USE command). 
See also: 
COPY_MESSAGE, USE, SELECTION_COMMANDS 
00002
00003
00001
MOVE_MESSAGE
CHANGES
Syntax: 
{NEX[T]|<LF>} 
Description: 
The NEXT command selects the next message after the current one which matches 
the selection criteria in the selected context.  If no message was selected 
previous to this message, the first message which matches the selection 
criteria in the selected context is used.  When selection criteria are not 
specified, the next message after the current one in the folder is selected. 
The Linefeed key can be used in place of the NEXT command. 
Examples: 
To answer the next message following the current one in the selected context, 
the MAIL user enters: 
    >SELECT MESSAGE 4-6 
    >DISPLAY MESSAGE FIRST 
       Sent: 07/07/86 11:20  Rcvd: 07/07/86 11:30  Number: 4 
         To: HELEN KLEIN                             From: LINDA SOCOL 
    Subject: Review of Documents 
    Please let me know status of review. 
    >ANSWER MESSAGE NEXT 
    msg#    when sent      recs          (from) subject 
       5   07/10 15:23       7   (Tom Fosnight) Minutes 
    SUBJECT:Meeting 
    BODY:The minutes for Tuesday's meeting have been mailed out. 
         <CR> 
    OPTIONS:END 
      Message sent. 
    > 
Message number 5 is answered.  The user is placed in SEND mode and is prompted 
for message fields to be included in the response. 
See also: 
SELECTION_COMMANDS, SELECT_MESSAGE 
00001
00002
NEXT
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
The OUTPUT command directs output from MAIL to a file or a device, such as a 
lineprinter.  When written to a file, the output is written as a unit record 
file unless the ORGANIZATION option specifies otherwise. 
Examples: 
To output messages to the line printer, the MAIL user enters: 
    >OUTPUT ON LP 
    >DISPLAY MESSAGE 1-3 
    3 messages displayed 
    >PRINT 
Messages 1-3 are printed at the line printer. 
See also: 
PAGE, PRINT 
00002
00003
00001
OUTPUT
Syntax: 
PA[GE] 
Description: 
The PAGE command forces an eject to the top of the page before the next 
DISPLAY_MESSAGE or LIST_MESSAGE command is executed.  The PAGE option of the 
PROFILE can be specified in the user's profile setting to always force an 
eject to the top of the page before the execution of either of these commands. 
Examples: 
To force a page eject if the PAGE option has not been specified in the user's 
profile setting, the user enters: 
    >PAGE 
    >DISPLAY MESSAGE 5 
    >PAGE 
    >DISPLAY MESSAGE 10 
Separate PAGE commands must be entered between each DISPLAY_MESSAGE 
or LIST_MESSAGE command for placement of each message on a separate 
page. 
See also: 
DISPLAY_MESSAGE, LIST_MESSAGE, OUTPUT, PRINT 
00001
00002
PAGE
Syntax: 
{PRE[VIOUS]|^} 
Description: 
The PREVIOUS command selects the message before the current one that matches 
all criteria in the selected context.  If no message has previously been 
selected, the last one in the context is used.  When selection criteria is not 
specified, the message before the current one in the folder is selected.  The 
uparrow can be entered in place of the PREVIOUS command. 
Examples: 
To acknowledge the message previous to the current one in the selected 
context, the user enters: 
    >SELECT MESSAGE 22-30 
    >DISPLAY MESSAGE FIRST 
        . 
        . 
        . 
    >LIST MESSAGE REST 
        . 
        . 
        . 
    >ACKNOWLEDGE MESSAGE PREVIOUS 
Message number 22 is displayed and messages 23-30 are listed.  Message number 
29 is acknowledged since the current message was number 30. 
See also: 
SELECTION_COMMANDS 
00001
00002
PREVIOUS
Syntax: 
PRI[NT] 
Description: 
The PRINT command directs MAIL to close all output streams.  This command can 
be used after an OUTPUT command and subsequent DISPLAY_MESSAGE and 
LIST_MESSAGE commands. 
Examples: 
To initiate printing of messages, the user enters: 
    >OUTPUT TO LP 
    >DISPLAY MESSAGE 25-30 
    6 messages displayed 
    >PRINT 
Message numbers 25-30 are printed at the specified line printer. 
See also: 
OUTPUT, PAGE 
00001
00002
PRINT

Syntax: 
PR[OFILE] optionlist 
Parameters: 
optionlist    is one or more of the options listed in PROFILE_OPTIONS. 
Options are specified in the format: 
    option [,option[,option]...] 
The following options can be specified using the PROFILE_COMMAND: 
    ANSWER 
    AUTOEDIT 
    COMBINE 
DELETE ON DETACH 
    DELIVERY_RECEIPT 
    DISPLAYTRACE 
    EDITOR 
EXTENDED ADDRESS DISPLAY 
    FILE_COPY 
    FILE_FOLDER 
    GRANULES 
    HEADERS 
    PAGE 
    PREPROCESS 
    RENUMBER 
    RETURN_RECEIPT 
    REPLY_TO 
    SETUP 
    SIGNED 
    SRCH 
For more information on a specific option, enter: 
    HELP (MAIL) PROFILE option 
For help on all options, enter ?? 
  Option     Description 
  AN[SWER]={S[ENDER]|R[ECEIVERS]} 
             Specifies whether ANSWER commands are to send messages only to 
             the originator or to the originator plus all recipients by 
             default.  SENDER specifies that answers are to be sent only to 
             the originator or the designated recipient for replies. 
             RECEIVERS specifies that copies of the answer are also to be sent 
             to all recipients.  The default is SENDER.  This option can be 
             overridden by specifying SENDER or RECEIVERS on the ANSWER 
             command. 
  A[UTOEDIT]={Y[ES]|N[O]} 
             Specifies whether an editor should be automatically called to 
             create the message body when sending a message.  If AUTOEDIT is 
             set, the user will not be prompted with BODY: to create the body 
             of a message.  Instead, the user is placed in the specified 
             editor.  Before editing the file, the user should examine the 
             contents.  Any fields such as TO or SUBJECT which were already 
             supplied, are inserted at the beginning of the *BODY file.  The 
             message body must be appended at the end of this information. 
  C[OMBINE]={Y[ES]|N[O]} 
             YES causes MAIL to discard ACKNOWLEDGMENT (ack) and DELIVERY 
             RECEIPT (dlv) messages, if a copy of the original message is 
             found in a folder.  Instead, a trace record (see the PROFILE 
             option DISPLAYTRACE) is added to the file copy of the message. 
             If a file copy resides in more than one folder, trace records are 
             added to both folders.  NO does not add trace records and does 
             not suppress creation of separate ack and dlv messages.  The 
             default is NO.  COMBINE processing also occurs when the MOVE or 
             COPY commands are being used to move/copy messages between 
             folders.  However, in this case, COMBINE processing occurs only 
             in the identified folder. 
  DEL[ETE] [ON] DET[ACH]={Y[ES]|N[O]} 
             YES specifies that when an enclosure is DETACHed, it will be 
             deleted whether or not the DELETE option is used.  NO indicates 
             that an enclosure will not be deleted unless DELETE is used 
             explicitly in the DETACH command.  The default is NO. 
  D[ELIVERY ]R[ECEIPT]={Y[ES]|N[O]} 
             YES specifies that a delivery receipt message (see 
             SYSTEM_GENERATED_MESSAGES DLV for more information) is 
             automatically generated for all mail sent.  A single delivery 
             receipt message is created only after all copies of a message 
             have been delivered (not read).  Creation of the delivery receipt 
             message cannot be subverted by a message recipient.  NO specifies 
             not to automatically generate a delivery receipt, and is the 
             default. 
  D[ISPLAY]T[RACE]={Y[ES]|N[O]} 
             YES specifies that trace records are to be added to the file 
             copies of mail messages to summarize acknowledgment, delivery, 
             and error conditions.  If there is an interface with a non-CP-6 
             mail system, header information records are also included where 
             appropriate. 
             NO specifies that trace records are not to be added in these 
             cases.  The default is YES.  The format of an ans trace record 
             is: 
                 Answered <date time> by <user> (see #<no>) 
             This record is automatically placed in the file copy of an 
             original message when an answer is received irrespective of use 
             of the DISPLAYTRACE option. 
             The format of a trace acknowledgment record is: 
                 Acknowledged <date time> by <user> 
             The format of a trace delivery record is: 
                 Delivered <date time> to <user> 
             The format of a trace return receipt record is: 
                 Return receipt <date time> from <user> 
             An example of a trace error record is: 
                 No mail folder has been created for <user> 
  E[DITOR]={'text string'|NONE} 
             Defines the editor to be used for editing the body of a message 
             which is being sent.  When the EDIT option is specified at the 
             OPTIONS:  prompt, either the editor specified in the profile or 
             EDIT (the default) is invoked.  The command passed to the editor 
             is the editor name appended with *BODY (e.g., EDIT *BODY). 
             NONE    resets the editor name in the user's profile. 
  EXT[TENDED] ADDR[ESS] DISP[LAY]={Y[ES]|N[O]} 
             YES specifies that all address information is displayed from the 
             address records in the message.  NO displays the text strings 
             from the address fields in the message header. 
  F[ILE ]C[OPY]={Y[ES]|N[O]} 
             Specifies whether to file a copy of all messages sent by the 
             user. 
             YES    specifies that all messages sent by the user be filed. 
             NO    specifies that messages sent by the user not be filed (the 
             default). 
  F[ILE ]F[OLDER]={[[/folder][.account]]|NONE} 
             Defines the folder to be used for filing copies of messages.  The 
             default is the central folder. 
             folder    specifies the name of the folder where messages will be 
             stored.  If a folder is not specified, the central folder is 
             assumed. 
             account    specifies the name of the user account.  Note that the 
             period must precede the account name. 
             NONE    specifies that no file folder is desired. 
  G[RANULES]=value 
             Specifies the maximum size of a folder.  If the value is 
             exceeded, only the headers of the messages are delivered and an 
             error message is returned to the sender.  The user is warned when 
             the folder has reached the limit.  A value of zero specifies an 
             infinite folder size is desired.  The default is zero (set to 
             zero when folder is created). 
             value    is a decimal number from 0 to 2**35-1. 
  H[EADERS]={Y[ES]|N[O]} 
             Determines if headers of messages are listed for verification 
             when operated on by certain message commands.  The message 
             commands which produce headers are: 
                 COPY_MESSAGE 
                 DELETE_MESSAGE 
                 MARK_MESSAGE 
                 MOVE_MESSAGE 
                 UNDELETE_MESSAGE 
                 UNMARK_MESSAGE 
             YES    specifies that headers be listed. 
             NO    specifies that headers not be listed (the default). 
  P[AGE]={Y[ES]|N[O]} 
             Causes a page to be ejected before each new message is displayed. 
             YES    specifies page ejection. 
             NO    specifies no page ejection (the default). 
  PRE[PROCESS] [:] [Y[ES]|N[O]] 
             Specifies whether or not command and message lines should be 
             preprocessed to do IBEX command variable substitutions.  If 
             preprocessing is requested, a (%) percent sign followed by the 
             name of a currently defined IBEX command variable are replaced 
             with the value of that variable.  Also, a (%%) double percent 
             sign before a string that could be a command variable name is 
             replaced by a single percent sign, and the following string is 
             not checked for command variable substitution.  The default is 
             NO. 
  REN[UMBER]={Y[ES]|N[O]} 
             Specifies whether all messages be renumbered at exit time. 
             Messages are renumbered starting with number one and incremented 
             by one.  Renumbering occurs only if the NOUPDATE parameter of the 
             END command is not specified. 
             YES    specifies that all messages in the folder be renumbered. 
             NO    specifies that no messages be renumbered (the default). 
  R[ETURN ]R[ECEIPT]={Y[ES]|N[O]} 
             Specifies whether an acknowledgment message stating "Return 
             Receipt for your message" be sent to the message sender the first 
             time that that message is displayed by the message recipient. 
             YES    specifies that the return receipt message be sent. 
             NO    specifies that the return receipt message not be sent. 
  REP[LY ]T[O]={[address[,address,...]]|NONE} 
             Specifies which addresses (users) are to receive replies to a 
             message.  This option works in cooperation with the SEND option 
             Return Receipt, and the ACKNOWLEDGE and ANSWER commands.  If a 
             reply to address is not specified, by default, a message is 
             returned to the sender. 
             NONE    resets the reply to addresses in the user's profile, and 
             does not send a reply. 
  SE[TUP]={'text string'|NONE} 
             Defines the first command to be executed when MAIL or a folder 
             within MAIL is accessed.  The default is 'LIST NEW' which lists' 
             summary information of all newly received messages. 
             text string    is a command string from 1-255 characters entered 
             within single quotes.  If a null string is specified, the current 
             string is deleted. 
             NONE    resets the SETUP command in the user's profile, and does 
             not invoke commands in the Setup file. 
  SI[GNED]={'text string'|NONE} 
             Specifies the name of the message sender to be included in the 
             Signed field of a message.  The Signed field appears below the 
             message body of a displayed message.  The primary function of 
             this option is to identify the message of a sender who is not 
             registered in the global registry. 
             text-string    is a text string of up to 200 characters entered 
             within single quotes.  If a null string is specified, the current 
             string is deleted. 
             NONE    resets the signature in the user's profile, and does not 
             add a signature in the Signed field. 
  SR[CH]={([name][/folder][.account][,.....])|NONE} 
             Specifies a list of folders to be searched in order to resolve 
             address information.  The list is limited to four entries.  This 
             allows the user to search folders other than the central folder 
             and the global mailing list.  The user must have the file 
             management READ access on any file named in the SRCH list. 
             name    specifies a user name. 
             folder    specifies a folder name.  If a folder is not specified, 
             the central folder is assumed. 
             account    specifies the name of the user account.  Note that a 
             period must precede the account name. 
             NONE    resets the folder names in the user's profile, and does 
             not search the list of folders listed in the Srch field. 
Description: 
The PROFILE command allows the user to customize the MAIL interface and set a 
profile which is different from the default profile set by MAIL. 
Examples: 
To change profile settings in the central folder, the MAIL user enters: 
    >PROFILE HEADERS=YES 
The user requests that headers appear on each message.  To change the profile 
settings of another folder, the folder must first be accessed with the USE 
command. 
See also: 
DISPLAY_PROFILE 
00001
00002
00003
00005
00005
00004
00021
00006
00005
00006
00007
00022
00008
00009
00010
00009
00010
00009
00010
00011
00012
00013
00014
00015
00017
00017
00017
00016
00016
00016
00018
00019
00020
PROFILE
PROFILE
END
Syntax: 
{ALL|m1 [- m2][,...]} 
Parameters: 
ALL    specified all messages. 
m1    specifies a single message number or, if m2 is present, the of a range 
of message numbers. 
m2    specifies the end for a range of message numbers. 
Description: 
The range selection component of explicit selection criteria restricts a 
message command to only those messages with numbers in the selected range. 
Multiple message numbers or ranges can be specified by separating each number 
of range the list with a comma.  A dash must separate the starting and ending 
number of each range.  The starting number for any range must not exceed its 
ending number.  Numbers and ranges in a list need not be in ascending 
numerical order. 
If the selection criteria for a command includes context selection with no 
range selection, ALL is implied. 
Example: 
    >DELETE 1-10,12,20-23 
deletes messages numbered between 1 and 10, message number 12, 
and messages numbered 20 through 23. 
See also: 
STRING_SELECTION, DATE_SELECTION, CONTENT_SELECTION 
00002
00003
00001
Syntax: 
READ fid 
Parameters: 
fid    is a disk file containing one MAIL command input line per record.  This 
file can be created with the EDIT processor. 
Description: 
The READ command reads and executes a file of MAIL commands.  Note that READ 
does not necessarily open or close files.  The READ command can be included in 
the SETUP option of the PROFILE command. 
Examples: 
To read commands from a file to be executed when logging on, the user enters: 
    >PROFILE SETUP='READ NEW_MESSAGES' 
The user created a file named NEW_MESSAGES which contains commands to be 
executed.  The READ command is specified in the SETUP option so that each time 
the user logs on, the NEW_MESSAGES file is read and executed. 
00002
00003
00001
READ
REGISTRATION_COMMANDS
The following commands are used by the MAIL administrator to maintain a global 
registry: 
CREATE_USER          Adds a new user to the global registry. 
DELETE_USER          Deletes a user from the global registry. 
DISPLAY_USER_ADMIN   Displays users registered on the electronic MAIL 
                     system. 
MODIFY_USER          Modifies an existing user in the global registry. 
Complete descriptions and syntax of the above commands 
can be displayed by entering: 
HELP command 
SELECTION_COMMANDS
Messages can be selected by their relative position:  first, last, next, 
previous, and so on.  the possible relative selections that can be made. 
Since these are the more common kinds of message selections, they can be made 
by simply entering the keyword for the selection as a separate command.  This 
will either display or list the selected message or messages, depending on 
which of these message operations was done most recently. 
Relative selections can also be specified as the selection criteria for any 
message processing command, but they cannot be combined with each other or any 
explicit selection criteria. 
The range of messages that can be operated on by relative selections is 
normally the entire current folder.  However, the SELECT MESSAGE command can 
be used to restrict relative selections to some subset of the messages in the 
folder.  When a SELECT MESSAGE command is in effect, relative selections will 
only select messages that meet the selected criteria, but explicit selection 
criteria can still be used to access any message in the folder. 
For additional information see: 
SELECTION_COMMANDS 
Syntax: 
           [    { DA[TE]      } ] 
           [    { FR[OM]      } ] 
REN[UMBER] [ BY { RE[FERENCE] } ] 
           [    { SU[BJECT]   } ] 
           [    { TO          } ] 
Description: 
The RENUMBER command causes all messages marked for deletion to be deleted, 
and all remaining messages to be renumbered.  Messages are renumbered 
sequentially, starting with one and incremented by one for each succeeding 
message.  If a field name is specified, messages are sorted in ascending order 
by that field.  Otherwise, the order of messages is not changed.  To renumber 
messages at exit time, the RENUMBER option of the PROFILE command can be 
specified.  These options do not affect the operation of the RENUMBER option 
of the PROFILE command. 
Examples: 
To renumber all messages in a folder, the user enters: 
    >RENUMBER 
See also: 
PROFILE, UNDELETE_MESSAGE 
00001
00002
RENUMBER
Syntax: 
RESE[ND] [MESSAGE] [selection_criteria] [CRPT=value] 
Parameters: 
selection_criteria    composed of message numbers, status flags, field names 
and logical or relational operators that specify the messages that are to be 
selected. 
SEE_ALSO: 
SELECTION_CRITERIA, RELATIVE_CRITERIA, EXPLICIT CRITERIA 
RANGE_SELECTION, CONTENT_SELECTION, STRING_SELECTION, DATE_SELECTION 
CRPT=value    specifies that an encrypted message be displayed.  Legal values 
are:  a decimal number between one and 68719476735; an octal number preceded 
by a period (.), with a value between .0 and .777777777777; or a string of 1 
to 4 characters enclosed in single quotes (').  Only the message body is 
encrypted.  The default is no encryption (CRPT=0). 
Description: 
The RESEND MESSAGE command sends copies of messages the user has received to 
other users.  The header of each message selected is printed, and the user is 
prompted for new header information (i.e., TO, SUBJECT, OPTIONS) for the 
resent message.  The body of the original message is retained in the resent 
message, but the user may alter it with of the EDIT option. 
Examples: 
To resend a message to one or more addresses, the MAIL user enters: 
    >RESEND MESSAGE 10 
    msg#    when sent      recs          (from) subject 
      10   07/30 09:44 ack   3       (Jim Carr) Product Update 
    TO:Marv Mossmond 
    SUBJECT:Product Update 
    OPTIONS:END 
      Message sent. 
    > 
Message number 10 is resent to another user.  MAIL displays the message in 
summarized format to the user.  The user is prompted with TO:, SUBJECT:, and 
OPTIONS:.  The recipient of the resent message receives the body of the 
original message. 
See also: 
SEND, COPY MESSAGE, FORWARD MESSAGE, Selection Commands 
00002
00003
00001
RESEND_MESSAGE
Syntax: 
RES[T] 
Description: 
The REST command selects all messages after the current one that matches all 
criteria in the selected context.  If no message has been previously selected, 
all messages in the context are used.  When selection criteria are not 
specified, all messages after the current one in the folder are selected. 
Examples: 
To mark all messages in the selected context following the current message, 
the user enters: 
    >SELECT MESSAGE 20-50 
    >LIST MESSAGE 25-37 
         . 
         . 
         . 
    >MARK MESSAGE REST 
Messages 38 through 50 are marked. 
See also: 
SELECTION_COMMANDS 
00001
00002
REST
Syntax: 
SEL[ECTED] 
Description: 
The SELECTED command selects all messages in the selected context. 
Examples: 
To display all messages in the selected context, the user enters: 
    >SELECT MESSAGE 10-20 
    >DISPLAY MESSAGE 30 
    >DISPLAY MESSAGE SELECTED 
Messages 10 through 20 are selected.  Message 30 is displayed.  Then, messages 
10 through 20 are displayed since they are all in the selected context. 
See also: 
SELECTION_COMMANDS 
00001
00002
SELECTED
  Command        Description 
  FI[RST] 
                 Specifies that the first message in the folder or in the 
                 SELECTed context be processed. 
  LA[ST] 
                 Specifies that the last message that matches the selection 
                 criteria in the selected context be processed. 
  NEX[T] (or linefeed) 
                 Specifies that the next message following the current message 
                 that matches the selection criteria in the selected context 
                 be processed.  If no message has been selected previously, 
                 the first message in the selected context matching the 
                 criteria is processed. 
  PREV[IOUS] (or ^) 
                 Specifies that the message before the current message that 
                 matches the selection criteria in the selected context be 
                 processed.  If no previous message was selected, the last 
                 message is processed. 
  RES[T] 
                 Specifies that all messages after the current message that 
                 match the selection criteria in the selected context be 
                 processed.  If no message was selected previously, all 
                 messages in the selected context are processed. 
  SEL[ECTED] 
                 Specifies that all messages that match the selection criteria 
                 be processed. 
  TH[IS] (or .) 
                 Specifies that the current message in the selected context be 
                 reprocessed.  The message need not be contained in the 
                 current context. 
For complete descriptions of these commands, enter: 
HELP command 
Selection criteria specify the messages to which a MAIL command applies.  A 
variety of different criteria can be used to select messages, individually or 
in groups.  Selection criteria can be broadly classed in two types: 
Relative criteria:  Selects messages by their position in the folder or 
    relative to the last message processed. 
Explicit criteria:  Selects messages explicitly by their number, field 
    contents, status flag setting, or any combination of these. 
If no selection criteria is specified for a message processing command, the 
default is the same set of messages processed by the last command that did 
specify criteria. 
The most commonly used selections are simple to specify, but the criteria can 
also contain complex expressions to select very specific groups of messages. 
See also: 
RELATIVE_CRITERIA, EXPLICIT_CRITERIA 
Syntax: 
SE[LECT] [MESSAGE] [selection_criteria] 
Parameters: 
selection_criteria    composed of message numbers, status flags, field names 
and logical or relational operators that specify the messages that are to be 
selected. 
SEE_ALSO: 
SELECTION_CRITERIA, RELATIVE_CRITERIA, EXPLICIT CRITERIA 
RANGE_SELECTION, CONTENT_SELECTION, STRING_SELECTION, DATE_SELECTION 
Description: 
The SELECT_MESSAGE command sets the criteria for selecting messages in the 
selected context. 
Examples: 
To select one or more tagged messages in a folder, the user enters: 
    >SELECT MESSAGE 11-20 WHEN MARK 
All messages between 11-20 which have been marked, are selected. 
See also: 
LIST_MESSAGE, DISPLAY_MESSAGE, SELECTION_COMMANDS 
00002
00003
00001
SELECT_MESSAGE
Syntax: 
SEN[D] [fid] 
Parameters: 
fid    specifies the file which contains the message.  If any required field 
information is missing, SEND prompts the user with SEND prompts.  This file 
can be created by any editor. 
Description: 
The SEND command is used to create and transmit a message to another user. 
SEND can be invoked at the MAIL prompt (>) or at the system control level (!). 
The user is first prompted for any required fields not presupplied in the 
message fid, then the Options: prompt is issued to allow the user to supply 
additional message fields or change other options.  The END or CANCEL option 
returns the user to MAIL. 
Examples: 
To send a message while in a MAIL session, the user enters: 
    >SEND 
    TO:Joe Smith 
    SUBJECT:Holidays 
    BODY:This is to remind everyone that the following Monday 
         is a legal holiday. 
         <CR> 
    OPTIONS:END 
      Message sent. 
    > 
The user responds to the TO: and SUBJECT: prompts by entering the required 
information and entering <CR>.  After all the necessary text is entered at the 
BODY: prompt, <CR> is entered on the next blank line.  Since no optional SEND 
fields or commands are desired, the END command is entered at the OPTIONS: 
prompt.  The user exits SEND mode and is returned to the > prompt.  If SEND is 
invoked at the system control level (!), the user is returned to the (!) when 
the SEND mode is exited. 
See also: 
HELP (SEND) TOPICS          for a list of SEND topics. 
HELP (SEND)                 for invoking the SEND processor. 
HELP (SEND) PROMPTS         for a list of SEND prompts. 
HELP (SEND) OPTIONS         for a list of SEND options. 
00002
00003
00001
SEND
Syntax: 
field [operator] value 
Parameters: 
field    specifies the message header field to be tested.  This must be one of 
the following: 
    F[ROM] 
    RE[FERENCE] 
    REP[LY] [TO] 
    S[UBJECT] 
    TO 
operator    specifies whether fields whose value does or does not match the 
one given are to be selected: 
    =     equal to values that match are selected. 
    ~=    not equal values are selected. 
If no operator is specified, = (equal) is implied. 
value    specifies the value of fields to be included (if the equal operator 
(=) is omitted), or omitted (if the operator is not equal (~=) is included, 
from the messages selected. 
Description: 
String selections can be used within explicit selection criteria to select 
messages whose header field values either match or do not a specified string. 
Comparisons are made, insensitive to case, and a match is found if the value 
is found anywhere within the specified field.  In other words, a leading and 
trailing wildcard is implied; an embedded wildcard can also be specified. 
Example: 
    >DISPLAY MESSAGE SUBJECT SALARIED 
If field values contain blanks, the alphanumeric string must be enclosed in 
single quotes, e.g.: 
    >DISPLAY MESSAGE SUBJECT 'SALARIED EMPLOYEES' 
See also: 
CONTENT_SELECTION, DATE_SELECTION, RANGE_SELECTION 
00002
00003
00001
Syntax: 
{TH[IS]|.} 
Description: 
The THIS command selects the current message in the selected context.  This is 
not necessarily the message contained in the current context.  If selection 
criteria is not specified, the message the user has just listed or displayed 
is selected.  A period can be entered in place of the THIS command. 
Examples: 
To display the current message in the selected context again, the user enters: 
    >SELECT MESSAGE 8-14 
    >DISPLAY MESSAGE FIRST 
         . 
         . 
         . 
    >DISPLAY MESSAGE THIS 
Message number 8 is displayed, as it is the first message of the selected 
context.  It is displayed again, since it is also the message at which the 
user is currently positioned. 
See also: 
SELECTION_COMMANDS 
00001
00002
THIS
Syntax: 
{T[IME]|DA[TE]} 
Description: 
The TIME command prints the current date and time. 
Examples: 
To display the current date and time, the MAIL user enters: 
    >TIME 
     11/23/85 15:21 
The current date and time (military time) are displayed. 
00001
00002
TIME
Syntax: 
UND[ELETE] [MESSAGE] [selection_criteria] 
Parameters: 
selection_criteria    composed of message numbers, status flags, field names 
and logical or relational operators that specify the messages that are to be 
selected. 
SEE_ALSO: 
SELECTION_CRITERIA, RELATIVE_CRITERIA, EXPLICIT CRITERIA 
RANGE_SELECTION, CONTENT_SELECTION, STRING_SELECTION, DATE_SELECTION 
Description: 
The UNDELETE_MESSAGE command removes the delete flag from the selected 
messages. 
Examples: 
To remove a deletion flag from a message, the MAIL user enters: 
    >UNDELETE MESSAGE 25 
Message number 25 has its deletion flag (d) removed. 
See also: 
DELETE_MESSAGE, MARK_MESSAGE, UNMARK_MESSAGE, SELECTION_COMMANDS 
00002
00003
00001
UNDELETE_MESSAGE
Syntax: 
UNM[ARK] [MESSAGE] [selection_criteria] 
Parameters: 
selection_criteria    composed of message numbers, status flags, field names 
and logical or relational operators that specify the messages that are to be 
selected. 
SEE_ALSO: 
SELECTION_CRITERIA, RELATIVE_CRITERIA, EXPLICIT CRITERIA 
RANGE_SELECTION, CONTENT_SELECTION, STRING_SELECTION, DATE_SELECTION 
Description: 
The UNMARK_MESSAGE command removes the mark flag (m) from the specified 
messages that had been marked by the MARK_MESSAGE command. 
Examples: 
To remove a tag from a message, the MAIL user enters: 
    >UNMARK MESSAGE 22-23 
Messages 22 and 23 are unmarked. 
See also: 
DELETE_MESSAGE, MARK_MESSAGE, SELECTION_COMMANDS, UNDELETE_MESSAGE 
00002
00003
00001
UNMARK_MESSAGE
Syntax: 
{US[E]|MAIL} [name][/folder][.account][(options)] 
Parameters: 
name    specifies a user name. 
folder    specifies the name of the folder where messages will be stored.  If 
a folder is not specified, the central folder is assumed. 
account    specifies the name of the user account.  Note that a period must 
precede the account name. 
options    specifies one of the following options: 
    B[YPASS]    specifies that the SETUP option of the PROFILE command not be 
    executed. 
    N[OUPDATE]    specifies that the SETUP option be executed, that no message 
    status flags be updated, and that MAIL be exited. 
Description: 
The USE command allows the user to specify the folder to be accessed.  If no 
folder is specified, the central folder is assumed.  If the END command is 
entered, any updating such as message deletion is performed on the current 
folder. 
Note:  The keyword MAIL is a synonymn for USE to permit the use of ESC-D to 
recall a MAIL invocation or fix a misspelled folder name. 
Examples: 
To specify which folder be accessed, the MAIL user enters: 
    >USE /MEMOS 
    LIST NEW 
The command LIST NEW is displayed when the /MEMOS folder is accessed and any 
new messages are listed (this is the default SETUP option for the /MEMOS 
folder).  The user is now in the /MEMO folder (the current folder). 
See also: 
CREATE_FOLDER, DELETE_FOLDER, DISPLAY_FOLDER 
00002
00003
00001
USE
Syntax: 
W[AIT] 
Description: 
The WAIT command specifies that MAIL pause until a new message is received. 
MAIL checks every 30 seconds to see whether any new messages have been 
received.  MAIL returns the user to the > prompt when new messages are 
received or the BREAK key is hit. 
Examples: 
To specify that MAIL wait until a new message is received, the MAIL user 
enters: 
    >WAIT 
00001
00002
WAIT
Wildcarding means that one or more folders, lists, or registered names can be 
selected and processed at the same time, on the basis of matching strings to a 
template folder name, list name or registered name.  The question mark is 
called a wildcard character.  The wildcard character is used to specify which 
portion of a folder name or list name is variable for selection and matching. 
For example: 
    >DELETE FOLDER /?_MEMOS 
The DELETE FOLDER command is entered followed by the folder or folders to be 
deleted.  The question mark implies that any folder name found in the user's 
account which has the suffix "_MEMOS" be deleted.  If the account contained 
the following folders: 
    /VACATION_MEMOS      /MY_MEMOS 
both folders would be deleted. 
The wildcard character can be used to imply any segment of a folder name, 
mailing list, or registered name.  The following commands permit wildcarding: 
    DELETE FOLDER 
    DELETE LIST 
    DISPLAY LIST 
    DISPLAY MESSAGE 
    DISPLAY USER 
    LIST FOLDER 
Wildcarding can be used to find the correct spelling of a user's last name in 
the global registry.  For example: 
    >DISPLAY USER TOM? 
All user names in the global registry beginning with TOM are listed. 
The wildcarding option is mentioned in the description of the MAIL commands 
which allow its use. 
END
