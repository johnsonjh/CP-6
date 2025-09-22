Welcome to CP-6 HELP! 
The HELP command prints information about CP-6 and its processors 
(system programs). 
The message you are reading tells how to use the HELP command, 
and a little about how the HELP information is structured. 
We suggest that you read this entire message before actually 
issuing HELP commands. 
Now type a question mark "?" followed by a carriage return. 
to get the next part of this message. 
Type     <?><CR> 
You have now learned an important lesson about HELP.  Typing a 
question mark displays the next part of the message. 
Just for your information, typing a double question mark (??) will 
print all the parts of the message. 
For example, if you typed     ??<CR>  at the next "!" prompt, 
the entire remaining description of HELP will be printed. 
But don't type a double question mark yet.  Just enter a single 
question mark for more information about HELP. 
Type     <?><CR> 
Let's look at the general rules about HELP.  You can almost always 
find out how to call a processor by entering: 
   HELP (processor) 
For example: 
   HELP (BASIC) 
prints the syntax of the call to BASIC.  In some processors, a 
description of the processor is printed instead. 
To find out what processors have HELP information, enter: 
   HELP (?) 
A list of processor names will be printed at your terminal. 
Any one of these can be inserted into the parentheses to query 
the HELP file for that processor. 
Type     <?><CR> 
HELP files typically have individual messages that can be printed. 
To obtain a list of message names (or topics), type TOPICS after 
the processor name, like so: 
    HELP (EDIT) TOPICS 
Any item in the resulting list can be substituted for the word 
TOPICS to print information about that item.  For example: 
    HELP (EDIT) MERGE 
prints information about the EDIT command MERGE. 
All interactive processors on CP-6 (except for APL and RPG) have 
their own HELP commands.  If you are currently in the processor, 
you do not need to include its name.  For example, since you are 
currently in IBEX (with the "!" prompt) you do not need to put 
"(IBEX)" in your help command to ask about IBEX commands. 
Similarly, if in EDIT, you need only enter: 
     HELP MERGE 
to print information about the EDIT command MERGE. 
Type     <?><CR> 
Many processors (typically compilers) are not truly interactive. 
To ask for information about these processors, you will always 
have to include the processor name.  For example, if you are in 
EDIT and wish to know about the FORTRAN statement GO TO, you 
can enter: 
     HELP (FORTRAN) GO_TO 
Or to obtain a list of FORTRAN topics: 
     HELP (FORTRAN) TOPICS 
Type     <?><CR> 
Many HELP files have a special message that gives you another way 
of finding out "what is in" that HELP file.  This special message 
is called HELP_INDEX, and works much like the index of a book, 
except that, instead of page numbers, the actual HELP command 
is given. 
For example: 
     HELP (PCL) HELP_INDEX C 
prints a list of subjects beginning with the letter "C", 
along with what HELP commands to issue to find out about those 
subjects. 
Type     <?><CR> 
Just as most HELP files have many messages, many messages have 
"submessages" or "message chunks".  You have been paging through 
message chunks as you read this by entering question marks. 
Individual message chunks can be printed in many cases without 
using the question mark "step-through".  For example: 
      HELP (PCL) COPY EXAMPLE 
prints example of the COPY command.  Another example: 
      HELP (EDIT) BUILD DESCRIPTION 
prints the description of the BUILD command. 
Sometimes large lists will be entered with callable submessages. 
For example: 
      HELP ESCAPE A 
prints a description of what typing <ESC><A> will do.  Usually these 
large lists have a default message that is printed if you don't 
add an additional item.  This default message usually tells you what 
callable message chunks are in the message. 
Type     <?><CR> 
For command descriptions, a standard set of submessage names are 
used, although this varies slightly from processor to processor. 
But in general: 
    HELP command SYNTAX          prints the syntax. 
    HELP command DESCRIPTION     prints the command description. 
    HELP command PARAMETERS      prints the command options. 
    HELP command EXAMPLES        prints one or more examples. 
    HELP command USAGE           prints usage notes. 
    HELP command RELATED         prints a list of related commands. 
Any of these can be abbreviated to one letter (S for SYNTAX or D for 
DESCRIPTION) 
Of course, within any one help file these message chunk names may 
or may not be used.  Also note that some processors have statements 
or directives rather than commands. 
Type     <?><CR> 
Enough theory.  Why not try some HELP calls?  If you need some 
ideas, try issuing: 
    HELP HELP EXAMPLES 
which prints a list of (you guessed it) examples of the HELP 
command. 
Incidentally, if you are new to the CP-6 system or to computers in 
general, you may be interested in "The CP-6 Introduction to 
Programming" (publication 
number CE45), which describes, in a tutorial fashion, the 
essential operation, (such as logging on, setting your terminal 
profile, etc) that every CP-6 user needs to know. 
If you already have some programming experience, you may be 
interested in "The CP-6 Application Programmer Handbook" 
(publication number CE55), which describes various capabilities 
of CP-6 from a task-oriented viewpoint. 
Of course, there are many CP-6 manuals describing different parts 
of the CP-6 system.  Enter HELP MANUALS for a list of manuals. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
Syntax: 
ACCEPT optionlist 
Parameters: 
optionlist   -   specifies one or more of the following options in the format 
option [,option]... 
AL[L]   -   accept all operator messages (including those specified under 
SEND, BROADCAST, and ANNOUNCE). 
S[END]   -   accept operator messages sent via the SEND keyin. 
B[ROADCAST]   -   accept operator messages sent via the BROADCAST and SENDALL 
keyins. 
AN[NOUNCE]   -   accept tape and disk mount announcements. 
Description: 
ACCEPT allows operator-originated messages or tape mount messages to be 
printed on the user's terminal. 
Examples: 
!ACCEPT ALL 
means allow all operator-originated and tape mount messages. 
!ACCEPT SEND 
means allow all operator SEND keyins. 
Related Commands: 
DONT, MESSAGE 
00002
00003
00001
00004
Syntax: 
{ACQ|ACQUIRE} resourcelist 
Parameters: 
resourcelist   -   specifies a list of resources, separated by commas.  Valid 
resources are: 
MEM[ORY]=VALUE 
TI[ME]={hh:mm:ss|mm:ss|mm|:ss} 
{MT|LT|FT}[dd][({6250|1600|800}[BPI])][=n] 
DP[dd][({200|500|600|1000}[MEG])][=n] 
DP#name[({E[XCLUSIVE]|S[HARED]})] 
ACC[OUNT]=({a[,a]...|NO}) 
LP[dd][({APL|OVERPRINT|LC})][=n] 
CP[dd][({BIN|LC})][=n] 
Pseudo-resources can also be specified.  See RESOURCELIST for a complete 
description. 
Description: 
ACQUIRE requests additional resources for the online and ghost user, resources 
in addition to those presently allocated for his use.  ACQUIRE cannot be used 
in batch processing. 
Examples: 
!ACQUIRE MT=2 
Indicates that two additional tape drives are to be allocated for this 
session. 
Related Commands: 
RESOURCE, ORESOURCE, LIMIT 
00002
00003
00001
00004
Syntax: 
ADJUST dcb  [fid][,optionlist] 
Parameters: 
dcb   -   identifies by dcb name or unit number the DCB whose assignments are 
to be adjusted. 
fid   -   specifies the file identification assignment of the DCB. 
optionlist   -   specifies file and/or device attributes. 
ACC[ESS]=({ALL|account|(accountlist)}[,controllist]) 
ACS={J[RNL]|D[IRECT]|S[EQUEN]} 
ACSV[EH]=((processorlist)[,controllist]) 
ALLD[CBS]{[=YES]|=NO} 
ALLT[RMS]{[=YES]|=NO} 
ALT[KEYS]=((altkey_spec) [,(altkey_spec)...]) 
AN[YDCB]{[=YES]|=NO} 
AU{[=YES]|=NO} 
BLK[L]=value 
BLO[CKED]{[=YES]|=NO} 
BT[MBRDR]{[=YES]|=NO} 
BU[PM]{[=YES]|=NO} 
COM[P]{[=YES]|=NO} 
COP[IES]=value 
CT[G]{[=YES]|=NO} 
CV[OL]{[=YES]|=NO} 
DC[BCONLGL]{[=YES]|=NO} 
DEB[UG]{[=YES]|=NO} 
DE[NSITY]={800|1600|6250}[BPI] 
DIR[ONLY]{[=YES]|=NO} 
DIS[P]={NA[MED]|SC[RATCH]} 
DV[FC]={'value'|O'value'} 
EB[CDIC]{[=YES]|=NO}[(CN[VRT]{[=YES]|=NO})] 
EOFN[ONE]{[=YES]|=NO} 
EOFO[NE]{[=YES]|=NO} 
EOFT[IME]=value 
EV[ENT]=value 
EXI[ST]={E[RROR]|N[EWFILE]|O[LDFILE]} 
EXP[IRE]={value|N[EVER]} 
FO[RM]='formname' 
FP[RG_FID]=fid 
FS[N]=value 
FU[N]={C[REATE]|I[N]|U[PDATE]} 
FW[INDOW]=name 
GH[STACS]={value|NONE} 
HBRDRC[HR]=c 
HBRDRS[IZ]=value 
HD[RHEIGHT]=value 
IG[NOREFSN]{[=YES]|=NO} 
ILA[TCH]{[=YES]|=NO} 
ILO[CK]{[=YES]|=NO} 
IM[SGTYP]=text 
IN[DENT]=value 
INITI[ALIZE]{[=YES]|=NO} 
INITV[ALUE]=value 
IO[ERROK]{[=YES]|=NO} 
INSTATTR={attr_opt|(attr_opt [,attr_opt...])} 
INSTATTRS[IZE]=value 
IS[TATION]=station 
IX[TNSIZE]=value 
JRNLB[YPASS]{[=YES]|=NO} 
KEYL=value 
KEYX=value 
LD[BYPRO]=value 
LFT[BRDR]{[=YES]|=NO} 
LI[NES]=value 
LO[AD]{[=YES]|=NO} 
LR[DLO]=value 
LS[LIDE]=value 
LST[AOR]{[=YES]|=NO} 
MAR[GIN]=value 
MAX[VOL]=value 
MINL[ENGTH]=value 
MI[NPHYS]=value 
MINW[IDTH]=value 
MY[STATION]=station 
NO[FILE]{[=YES]|=NO} 
N[RECS]=value 
OLA[TCH]{[=YES]|=NO} 
OLO[CK]{[=YES]|=NO} 
OM[SGTYP]=text 
OPT[IONAL]{[=YES]|=NO} 
OR[G]=organization 
OS[TATION]=station 
P[AGECOLUMN]=value 
PH[YSICAL]=value 
PO[SITION]= option 
PROCATTR={attr_opt|(attr_opt[,attr_opt...)] 
PROCATTRS[IZE]=value 
PROF[ILE]=name 
Q[ISS]{[=YES]|=NO} 
{RD|RE[AD]}={ALL|account|(accountlist)} 
REC[L]=value 
RES[ETPAGE]=YES 
RH[TBRDR]{[=YES]|=NO} 
SC[RUB]{[=YES]|=NO} 
SEE[D]=(octstr|"charstr"|NONE) 
SEGN[UM]={VS1|VS2|VS3} 
SEGS[IZE]=value 
SEQ{[=YES]|=NO} 
SEQC[OL]=value 
SEQI[D]='string' 
SN={packsetname|(seriallist)} 
SH[ARE]={A[LL]|I[N]|N[ONE]} 
SPAN[NED]{[=YES]|=NO} 
SPAR[E]=value 
TA[B]=(tablist) 
TE[RMCONLGL]{[=YES]|=NO} 
TI[TLE]='string' 
TO[PBRDR]{[=YES]|=NO} 
TY[PE]=value 
UATTR={attr_opt|(attr_opt[,attr_opt...])} 
UATTRS[IZE]=value 
UOPTn{[=YES]|=NO} 
VBRDRC[HR]=c 
VBRDRS[IZ]= value 
V[OL]=value 
VOLA[CCESS]={A[LL]|I[N]|N[ONE]} 
WR[ITE]={ALL|account|(accountlist)} 
W[AS]{[=YES]|=NO} 
WL[ENGTH]=value 
WW[IDTH]=value 
XTE[ND]{[=YES]|=NO} 
XTN[SIZE]=value 
Enter HELP SET_OPS for complete descriptions. 
Description: 
ADJUST modifies DCB assignments to disk, tape, unit record files, exclusive 
devices and comgroups during a job step.  ADJUST requests that an immediate 
fix be made at other than job step time.  If the specified DCB is open, it is 
closed with DISP=SAVE so that the modifications can be made. 
The ADJUST command is valid only when not at a job step. 
The effects of an ADJUST command are valid only for the duration of the job 
step; they are not remembered as are attributes specified through options on 
the SET and RESET commands. 
Examples: 
!SET M$INPUT INDAT 
!U 
!MYPROG. 
>GO 
*** FILE INDAT DOES NOT EXIST 
<CNTL-Y> 
!!ADJUST M$INPUT INDATA 
!!GO 
>GO 
This example illustrates the principal use of ADJUST:  to provide a patch 
capability during execution.  In the example, the user issues a SET command in 
which he mistypes the name of the file he wishes to assign to DCB M$INPUT.  He 
invokes program execution under DELTA; the user is informed that the file 
cannot be located.  Assume that the user program has been executing for quite 
some time before the error condition is discovered.  Reinitializing would be 
expensive and time-consuming.  ADJUST provides a better solution.  The user 
interrupts program execution and assigns INDATA to the DCB.  The user directs 
that execution be resumed and that the input file be read and the program 
resumes execution at the point of interrupt reading the correct file. 
Related Commands: 
SET, RESET 
00002
00003
00001
00004
Syntax: 
!ALTKEY fid 
Parameters: 
fid   -   identifies a file with alternate indexes. 
Description: 
ALTKEY invokes the ALTKEY processor to rebuild the alternate indexes of 
indexed files.  The alternate indexes can be left incomplete by a user 
explicitly requesting that the alternate indexes not be updated on the open 
and close of the file, or a recovery that interrupts the rebuild. 
Examples: 
!ALTKEY WORKPLAN_FILE 
00002
00003
00001
ASC_CARD
To obtain information about the ASCII character set, enter: 
!HELP (IBEX) ASCII character 
where character is: 
    A character or mnemonic (for unprintables) 
    An octal value in the form          O'ooo' 
    A decimal value in the form         D'ddd' 
    An hexadecimal value in the form    X'xx' 
NOTE:  The following must be enclosed in single quotes:  dash ('-'), double 
quote ("), greater than ('>').  To list the entire ASCII character set, type 
??<CR> at the next prompt. 
The table has the following format: 
  CHAR     OCTAL     DECIMAL   HEX         MEANING 
  NUL      O'000'    D'000'    X'00'       NULL of time fill character 
  SOH      O'001'    D'001'    X'01'       Start Of Heading 
  STX      O'002'    D'002'    X'02'       Start Of Text 
  ETX      O'003'    D'003'    X'03'       End Of Text 
  EOT      O'004'    D'004'    X'04'       End Of Transmission 
  ENQ      O'005'    D'005'    X'05'       ENQuiry 
  ACK      O'006'    D'006'    X'06'       ACKnowledge 
  BEL      O'007'    D'007'    X'07'       BELl 
  BS       O'010'    D'008'    X'08'       BackSpace 
  HT       O'011'    D'009'    X'09'       Horizontal Tabulation 
  LF       O'012'    D'010'    X'0A'       Line Feed 
  VT       O'013'    D'011'    X'0B'       Vertical Tabulation 
  FF       O'014'    D'012'    X'0C'       Form Feed 
  CR       O'015'    D'013'    X'0D'       Carriage Return 
  SO       O'016'    D'014'    X'0E'       Shift Out 
  SI       O'017'    D'015'    X'0F'       Shift In 
  DLE      O'020'    D'016'    X'10'       Data Link Escape 
  DC1      O'021'    D'017'    X'11'       Device Control 1 
  DC2      O'022'    D'018'    X'12'       Device Control 2 
  DC3      O'023'    D'019'    X'13'       Device Control 3 
  DC4      O'024'    D'020'    X'14'       Device Control 4 
  NAK      O'025'    D'021'    X'15'       Negative AcKnowledge 
  SYN      O'026'    D'022'    X'16'       SYNchronous Idle 
  ETB      O'027'    D'023'    X'17'       End of Transmission Blocks 
  CAN      O'030'    D'024'    X'18'       CANcel 
  EM       O'031'    D'025'    X'19'       End of Medium 
  SUB      O'032'    D'026'    X'1A'       Special Sequence 
  ESC      O'033'    D'027'    X'1B'       ESCape 
  FS       O'034'    D'028'    X'1C'       File Separator 
  GS       O'035'    D'029'    X'1D'       Group Separator 
  RS       O'036'    D'030'    X'1E'       Record Separator 
  US       O'037'    D'031'    X'1F'       Unit Separator 
  SP       O'040'    D'032'    X'20'       SPace 
  !        O'041'    D'033'    X'21'       Exclamation Point 
  "        O'042'    D'034'    X'22'       Quotation Mark 
  #        O'043'    D'035'    X'23'       Number Sign 
  $        O'044'    D'036'    X'24'       Currency Symbol 
  %        O'045'    D'037'    X'25'       Percent 
  &        O'046'    D'038'    X'26'       Ampersand 
  '        O'047'    D'039'    X'27'       Apostrophe 
  (        O'050'    D'040'    X'28'       Opening Parenthesis 
  )        O'051'    D'041'    X'29'       Closing Parenthesis 
  *        O'052'    D'042'    X'2A'       Asterisk 
  +        O'053'    D'043'    X'2B'       Plus 
  ,        O'054'    D'044'    X'2C'       Comma 
  -        O'055'    D'045'    X'2D'       Hyphen or Minus 
  .        O'056'    D'046'    X'2E'       Period 
  /        O'057'    D'047'    X'2F'       Virgule 
  0        O'060'    D'048'    X'30'       Zero 
  1        O'061'    D'049'    X'31'       One 
  2        O'062'    D'050'    X'32'       Two 
  3        O'063'    D'051'    X'33'       Three 
  4        O'064'    D'052'    X'34'       Four 
  5        O'065'    D'053'    X'35'       Five 
  6        O'066'    D'054'    X'36'       Six 
  7        O'067'    D'055'    X'37'       Seven 
  8        O'070'    D'056'    X'38'       Eight 
  9        O'071'    D'057'    X'39'       Nine 
  :        O'072'    D'058'    X'3A'       Colon 
  ;        O'073'    D'059'    X'3B'       Semicolon 
  <        O'074'    D'060'    X'3C'       Less Than 
  =        O'075'    D'061'    X'3D'       Equal 
  >        O'076'    D'062'    X'3E'       Greater Than 
  ?        O'077'    D'063'    X'3F'       Question Mark 
  @        O'100'    D'064'    X'40'       Commercial At 
  A        O'101'    D'065'    X'41'       Uppercase Letter 
  B        O'102'    D'066'    X'42'       Uppercase Letter 
  C        O'103'    D'067'    X'43'       Uppercase Letter 
  D        O'104'    D'068'    X'44'       Uppercase Letter 
  E        O'105'    D'069'    X'45'       Uppercase Letter 
  F        O'106'    D'070'    X'46'       Uppercase Letter 
  G        O'107'    D'071'    X'47'       Uppercase Letter 
  H        O'110'    D'072'    X'48'       Uppercase Letter 
  I        O'111'    D'073'    X'49'       Uppercase Letter 
  J        O'112'    D'074'    X'4A'       Uppercase Letter 
  K        O'113'    D'075'    X'4B'       Uppercase Letter 
  L        O'114'    D'076'    X'4C'       Uppercase Letter 
  M        O'115'    D'077'    X'4D'       Uppercase Letter 
  N        O'116'    D'078'    X'4E'       Uppercase Letter 
  O        O'117'    D'079'    X'4F'       Uppercase Letter 
  P        O'120'    D'080'    X'50'       Uppercase Letter 
  Q        O'121'    D'081'    X'51'       Uppercase Letter 
  R        O'122'    D'082'    X'52'       Uppercase Letter 
  S        O'123'    D'083'    X'53'       Uppercase Letter 
  T        O'124'    D'084'    X'54'       Uppercase Letter 
  U        O'125'    D'085'    X'55'       Uppercase Letter 
  V        O'126'    D'086'    X'56'       Uppercase Letter 
  W        O'127'    D'087'    X'57'       Uppercase Letter 
  X        O'130'    D'088'    X'58'       Uppercase Letter 
  Y        O'131'    D'089'    X'59'       Uppercase Letter 
  Z        O'132'    D'090'    X'5A'       Uppercase Letter 
  [        O'133'    D'091'    X'5B'       Opening Bracket 
  \        O'134'    D'092'    X'5C'       Reverse Virgule 
  ]        O'135'    D'093'    X'5D'       Closing Bracket 
  ^        O'136'    D'094'    X'5E'       Circumflex 
  _        O'137'    D'095'    X'5F'       Underscore 
  `        O'140'    D'096'    X'60'       Grave Accent 
  a        O'141'    D'097'    X'61'       Lowercase Letter 
  b        O'142'    D'098'    X'62'       Lowercase Letter 
  c        O'143'    D'099'    X'63'       Lowercase Letter 
  d        O'144'    D'100'    X'64'       Lowercase Letter 
  e        O'145'    D'101'    X'65'       Lowercase Letter 
  f        O'146'    D'102'    X'66'       Lowercase Letter 
  g        O'147'    D'103'    X'67'       Lowercase Letter 
  h        O'150'    D'104'    X'68'       Lowercase Letter 
  i        O'151'    D'105'    X'69'       Lowercase Letter 
  j        O'152'    D'106'    X'6A'       Lowercase Letter 
  k        O'153'    D'107'    X'6B'       Lowercase Letter 
  l        O'154'    D'108'    X'6C'       Lowercase Letter 
  m        O'155'    D'109'    X'6D'       Lowercase Letter 
  n        O'156'    D'110'    X'6E'       Lowercase Letter 
  o        O'157'    D'111'    X'6F'       Lowercase Letter 
  p        O'160'    D'112'    X'70'       Lowercase Letter 
  q        O'161'    D'113'    X'71'       Lowercase Letter 
  r        O'162'    D'114'    X'72'       Lowercase Letter 
  s        O'163'    D'115'    X'73'       Lowercase Letter 
  t        O'164'    D'116'    X'74'       Lowercase Letter 
  u        O'165'    D'117'    X'75'       Lowercase Letter 
  v        O'166'    D'118'    X'76'       Lowercase Letter 
  w        O'167'    D'119'    X'77'       Lowercase Letter 
  x        O'170'    D'120'    X'78'       Lowercase Letter 
  y        O'171'    D'121'    X'79'       Lowercase Letter 
  z        O'172'    D'122'    X'7A'       Lowercase Letter 
  {        O'173'    D'123'    X'7B'       Opening Brace 
  |        O'174'    D'124'    X'7C'       Vertical Bar 
  }        O'175'    D'125'    X'7D'       Closing Brace 
  ~        O'176'    D'126'    X'7E'       Tilde 
  DEL      O'177'    D'127'    X'7F'       DELete 
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
00059
00060
00061
00062
00063
00064
00065
00066
00007
00067
00008
00009
00068
00025
00014
00069
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
00059
00060
00061
00062
00063
00064
00065
00066
00067
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
00018
00019
00020
00021
00128
00017
00070
00026
00006
00005
00028
00024
00004
00071
00013
00029
00072
00030
00073
00010
00074
00075
00076
00077
00011
00078
00079
00022
00001
00080
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
00059
00060
00061
00062
00063
00064
00065
00066
00067
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
00081
00082
00083
00031
00084
00016
00015
00002
00033
00003
00027
00023
00085
00086
00032
00087
00012
00088
00089
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
00059
00060
00061
00062
00063
00064
00065
00066
00067
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
Syntax: 
!ASC 
Parameters: 
None 
Description: 
The ASC control card terminates binary input mode. 
The ASC control card is used as a terminator for binary input.  The control 
card causes subsequent data to be interpreted as ASCII input, that is, as 80 
9-bit characters per card. 
Examples: 
!ASC 
means terminate binary input and interpret subsequent data as ASCII input. 
Related Commands: 
BIN, EOD 
00002
00003
00001
00004
Syntax: 
ATITLE [textstring] 
Parameters: 
textstring   -   is an alphanumeric character string from 1 to 32 characters 
long. 
Description: 
ATITLE allows the user to insert a title consisting of up to 32 alphanumeric 
characters into the accounting records(s) generated for a job, or to delete a 
previously assigned title.  This title may be used at some later time to 
identify and retrieve the job's accounting information.  ATITLE with no title 
string specified deletes the previously generated accounting record title. 
Examples: 
!ATITLE NEW TITLE 
places the string NEW TITLE into the accounting records generated for this 
job. 
!ATITLE 
deletes the previously generated ATITLE title string for this job. 
Related Commands: 
NONE 
00002
00003
00001
00004
The CP-6 front-end processor can handle the following line speeds: 
  110    Baud 
  150    Baud 
  200    Baud 
  300    Baud 
  600    Baud 
 1200    Baud 
 1800    Baud 
 2400    Baud 
 4800    Baud 
 9600    Baud 
19200    Baud 
The front-end processor automatically adapts for the correct terminal baud 
value.  To obtain a log-on salutation, the user slowly types the character 8 
until a message is printed requesting that a left parenthesis be typed. 
Typing a left parenthesis completes the autobaud sequence, and a log-on 
salutation is printed.  It is possible for an installation to define terminal 
lines such that autobauding is not required.  In this case, the logon 
salutation is immediately presented without entering 8's, or is presented 
after entry of a break signal. 
BUILD
Syntax: 
BACKUP fid 
Parameters: 
fid   -   identifies a file to be saved on the standard system backup tape. 
The file continues to be available to users.  No file attributes (including 
access and modification dates) are changed. 
Description: 
BACKUP qualifies a file to be saved on a one-time basis on backup tape during 
the next EFT backup operation. 
Examples: 
!BACKUP COSMIC_FILE 
means qualify file COSMIC_FILE to be saved. 
Related Commands: 
NONE 
00002
00003
00001
00004
Syntax: 
BATCH  fid [(optionlist)][,fid[(optionlist)]]... 
Parameters: 
fid   -   identifies a job file generally created through EDIT or PCL. 
optionlist   -   any of the following keywords and values can be specified in 
the option list.  If only one fid is specified, the parentheses around option 
are optional, but the option must be separated from the fid by a blank space. 
    CRPT=(octstr|"charstr")   -   specifies a SEED to be applied to the XEQ 
    file if it is encrypted. 
        octstr   -  specifies an octal string from 0 to 777777777777. 
        charstr  -  specifies from 1 to 4 characters. 
    P[RINT]   -   directs that while the file is being submitted for 
    execution, every record is printed (echoed) on the output destination. 
    S[CAN]   -   checks the contents of the command file for syntax errors. 
    If an error is found, appropriate diagnostics are written to the user's 
    console, and the BATCH aborted. 
    T[EST]   -   directs IBEX to inhibit submitting the job for execution and 
    instead to print each record as it is altered through the string 
    substitution specifications contained in the command.  This test mode 
    allows the user to examine the effects of data replacement requests before 
    submitting the job for execution.  Only altered records are displayed. 
    NG[SUBS]   -   specifies that GLOBAL data replacements are not to be used 
    in processing this file. 
    START=record specifier   -   identifies the record at which command 
    execution is to start.  If the START option is not selected command 
    execution begins with the first record in the file.  Record specifier may 
    be a record number, a record EDIT key, or a label.  A record EDIT key is 
    distinguished from a record number by the inclusion of a period. 
    END=record specifier   -   identifies the record at which command 
    execution is to end.  If not specified, command execution ends with the 
    last record.  Record specifier is defined as for START=record specifier. 
    NS[TATUS]   -   specifies that BATCH is not to return the status of the 
    submitted job.  This job will be put into the user's NOTIFY/CHECK list. 
    rep   -   specifies a replacement specification in the format: 
        {field1|'string1'}={field2|'string2'} 
    See REPLACEMENT for a complete description. 
Description: 
BATCH specifies one or more files to be submitted for batch job execution and 
can include data replacement specifications. 
Any number of replacement equations can be included in the BATCH command. 
Each equation supplies a substitution value as described under Command Files. 
The source identified by fid must be a disk file. 
Examples: 
!BATCH RUNEXAMPLE(P),COBOLCOMP('YOURACCT'=MYACCT) 
Places the jobs RUNEXAMPLE and COBOLCOMP into the batch queue.  The job 
RUNEXAMPLE will have all records of its command stream displayed as they are 
submitted for execution, and when the job COBOLCOMP is submitted for execution 
all occurrences of the string YOURACCT will be replaced by the field MYACCT. 
!BATCH NEWJOB 
Places the file NEWJOB into the batch queue for execution. 
The system responds to this command by assigning each batch job a unique 
system identification (sysid) and informing the user of the status of the job. 
Related Commands: 
XEQ, JOB, CHECK, CANCEL, XMIT, INCLUDE 
00002
00003
00001
00004
Syntax: 
!BIN 
Parameters: 
NONE 
Description: 
The BIN control card specifies that subsequent punched cards are to be 
interpreted as binary input. 
The BIN control card specifies that subsequent input will be in binary (where, 
each card is interpreted as 960 bits (80 columns x 12 bits)) instead of ASCII 
(80 9-bit characters).  The ASC or EOD control card terminates binary input 
mode. 
Examples: 
None 
Related Commands: 
ASC, EOD 
00002
00003
00001
00004
Syntax: 
{B|BUILD} fid[,[n][,i][,tc]] 
Parameters: 
fid   -   is the identifier of the file to be created. 
n   -   is the key at which the new file is to start.  The default is 1. 
i   -   is the increment for the keys of the new file.  The default 
is 1 or the last-issued increment in a previous command. 
tc   -   specifies a two character file type code for the file.  The 
default is SE (Source Edit).  File types are defined by processors at 
file creation.  Users can define their own file types to aid in 
associating groups of selected files. 
Description: 
BUILD creates a newly-named keyed disk file and causes EDIT to print 
keys as prompts for the assignment of records.  A null line 
(an unaccompanied carriage return or line feed) terminates the 
the operation.  When issued from EDIT, the null line returns control 
to EDIT, and the newly-created file remains open for editing.  When 
issued from IBEX, the null line returns control to IBEX, and the file 
is closed.  An error message is printed if an attempt is made to 
create a file that already exists.  BUILD is always a file command. 
Examples: 
!BUILD LEMEGETON 
means create a new file called LEMEGETON, prompt with key 1.000, 
and continue adding to the file (next record 2.000, next 3.000, etc.) 
until a null line is entered. 
!BUILD CONSCIOUSNESS..COSMIC,100,.001 
means create new file CONSCIOUSNESS with password COSMIC, prompt 
with key 100.000, and continue adding to the file (next key 100.001, 
next 100.002, etc.). 
!BUILD :DATA,,MD 
means create new file :DATA, and give it user-defined file code MD. 
Related Commands: 
See the EDIT Help Facility. 
00002
00003
00001
00004
Syntax: 
BYE [{F[ULL]|S[UMMARY]|N[ONE]}] 
Parameters: 
FULL   -   specifies full accounting information. 
SUMMARY   -   specifies a summary of the accounting information.  This is the 
default. 
NONE   -   specifies no accounting information. 
Description: 
BYE (a synonym for the OFF command) ends a terminal session. 
Examples: 
!BYE FULL 
means terminate the terminal session, print detailed accounting information. 
Related Commands: 
OFF 
00002
00003
00001
00004
COPY
COPYALL
Syntax: 
CANCEL [jobidlist[output-file-spec] {(O[UTPUT][=YES|=NO]) 
    |(number,number...)}] [[,](OPTIONLIST)] 
Parameters: 
jobidlist   -   specifies one or more of the following three options in the 
format option[,option]... 
    sysid   -   is the job sysid assigned by the system and displayed in a 
    message sent to the user when the BATCH command that submitted the job was 
    processed. 
    jobname[.account]   -   is the alphanumeric job name which was defined 
    with the NAME option on the JOB command for the job to be aborted.  The 
    named job must have been submitted under the running account.  Account 
    specifies the account in which the named job is to be found. 
     .account   -   is any job that was submitted under the given account. 
    output-file-spec   -   takes one of the following forms: 
    -1 or (1)   -   allows the specification of one subfile. 
    (1[2,...])   -   allows the specification of a list of subfiles. 
Note: Since CANCEL allows a jobname of just digits, whenever a sysid or a 
jobname is allowed, if IBEX encounters a 6 or less digits number, it treats 
this as a sysid.  Anything of greater length is treated as a jobname.  If a 
jobname exists that can be treated as a sysid, the user must put the jobname 
inside single quotes to indicate to IBEX that this is a jobname.  Some 
examples are CANCEL 'jobname'-1, CANCEL '1234'-1, CANCEL '1234'(1), CANCEL 
'jobname'(1). 
O[UTPUT]   -   specifies whether or not a job's output is to remain in the 
output queue.  When NO, there is no output (i.e., the output is deleted). 
When YES, the output remains.  The default is NO. 
number   -   specifies a symbiont output file number. 
optionlist   -   specifies one or more of the following options in the format 
option[,option]...[,option]: 
    INPUT [suboption]   -   searches only the Input queue with the following 
    suboptions: 
        ALL   -   cancels all the input jobs. 
        HELD   -   cancels only those jobs held in the queue. 
        READY   -   cancels only those jobs ready to run. 
        The default suboption is READY. 
    JOB   -   searches only the Running queue. 
    ME   -   searches the queue(s) for only job(s) under the user's account 
    name. 
    OUTPUT   -   searches only the Output queue. 
    RUNNING   -   searches only the Running queue. 
    SYSTEM   -   searches the queue(s) for job(s) for any/everyone. 
    TERMINAL   -   searches the queue(s) for job(s) using the user's current 
    sysid. 
    USE   -   allows the user to specify a fid which contains sysids that are 
    to be deleted. This file may have been generated by the USE option of the 
    CHECK command.  If a file is named but no account is specified, a default 
    account (or default account or packset) will be used as described in the 
    CHECK/NOTIFY Options table. 
    See CHECK_OPTIONS or NOTIFY_OPTIONS for complete descriptions and syntax. 
Description: 
CANCEL deletes a job from the batch job queue, aborts processing of an 
executing job, or deletes a job's output from the output queue. 
Note that the results of a CANCEL action can differ depending on the time at 
which the CANCEL is requested as follows: 
Job status                     Result 
----------                     ------ 
Currently                      Job is aborted.  The job's output is 
running                        deleted (not printed) if OUTPUT=NO; 
                               otherwise, it is printed. 
Printing                       Remaining output is deleted if 
                               OUTPUT=NO. 
Waiting to                     Job is deleted before execution. 
be run 
Completed                      Message 'JOB xxx HAS ALREADY COMPLETED' 
                               is output. 
Does not                       Message 'JOB xxx DOES NOT EXIST' is 
exist                          output. 
Examples: 
!CANCEL EXAMPLE 
Deletes the job named EXAMPLE from the batch queue. 
!CANCEL 389 
Deletes the job with the sysid of 389. 
!CANCEL 390 (OUTPUT=NO) 
Deletes the job with the sysid of 390 and deletes its output. 
!CANCEL 400(1,2) 
Deletes the symbiont output files with sysids of 400-1 and 400-2. 
!CANCEL EXAMPLE (1,2) 
Deletes the symbiont output files with jobname of EXAMPLE-1 and EXAMPLE-2. 
!CANCEL (OUTPUT) 
Deletes all symbiont output files that belong to the user. 
Related Commands: 
PRINT, ERASE, CHECK, NOTIFY 
00002
00003
00001
00004
FID_CG
Changes have been made to the following processors:  IBEX, EDIT, PLOVER and 
LEMUR.  No changes have been made to PCL, IMP AND LINK. 
For information on changes to a specific processor, type: 
HELP (processor) CHANGES processor 
For IBEX HELP changes, see also HELP CHANGES TERMINAL and HELP CHANGES VFC. 
  Processor    Changes 
  Section 1 - Manual Overview. 
               No changes. 
  Section 2 - File and I/O management concepts. 
  Section 3 - IBEX command language. 
               o  New options have been added to the $INPUT builtin 
                  function: 
                        REPLY_EXPRESSION - sets up a default reply. 
                        REREAD_POSITION - sets up the cursor within 
                                          the REPLY_EXPRESSION. 
               o  A new builtin function $CMDVAR_EXISTS (cmdvarname) 
                  returns 1 if specified command variable exists, else 
                  returns 0. 
               o  New TERMINAL suboptions have been added to the 
                  CHARSETNAME option: 
                        ASC8 - has slightly different functionality. 
                        ASC8I - has been added as a new type. 
               o  A new option has been added to SET/ADJUST/RESET: 
                        The COPIES option has been added for 
                        UR files and devices. 
               o  The SET option TYPE now allows a quote string. 
               o  DI BUDGET now displays more information. 
               o  CANCEL now has the same output as CHECK. 
               o  The CHECK command now accepts ~JOBID to allow deletion 
                  from the USE file. 
               o  DI PROFILES and VARS accept wildcards against which to 
                  match the output list. 
               o  The SET command now displays SET information if no SET 
                  options are specified. 
               o  XEQ/BATCH/XMIT now accept encrypted files via the CRPT 
                  option. 
               o  LET BANNERTEXTn now accepts IBEX expressions. 
               o  CHECK now allows accounts to be checked. 
               o  CANCEL now accepts most of the options of CHECK. 
               o  The option ORG=X364 has been added to the SET command. 
               o  The JOBNAME parameter (for JOB, FOLLOW, CHECK, CANCEL 
                  and UNHOLD) now accepts digits. 
               o  The IBEX CHECK command now allows a user to specify an 
                  output file. 
               o  The documentation has been corrected for the TERMINAL 
                  option HALFDUXPAPERTAPE. 
               o  The option ONESPACEEDIT has been added to the 6EDIT 
                  FORMAT command Esc-1-LF. 
  Section 4 - EDIT Processor. 
               o  A new topic EQUAL (or =) has been added to EDIT. 
                  The equal sign can now be used as a way of specifying 
                  the current file you are editing (in place of the 
                  filename). 
               o  A new topic XUG_SERVICES (or XUG) has been added to EDIT. 
                  XUG services allow you to use a DO (!) command at the * 
                  prompt. 
               o  The RF/MK/MD commands have been improved with minor bug 
                  fixes. 
               o  The MERGE command now allows 'ON'|'TO' and 'OVER'. 
               o  '==' is now allowed on the MERGE command as the second 
                  fid. 
               o  A new topic ROUNDING (or RO) has been added to EDIT. 
                  AP and IN will now round the next line number inserted 
                  to a multiple of INCR. 
               o  The IN command has been updated to act like AP if the 
                  whole file is selected. It has also been updated to 
                  work for consecutive files. 
               o  The IS command has been updated to work for consecutive 
                  files. 
               o  The RR command can now specify column positioning. 
               o  The STATUS command will now display MODE. The STATUS 
                  display has been rearranged by level of importance. 
                  STATUS now also allows options and has had the new 
                  synonym SHOW added to it. 
               o  The TP command now uses the last TY/TS/TC format when 
                  displaying the selected lines. 
  Section 5 - PCL processor. 
               No changes. 
  Section 6 - Terminal Editing Features. 
               o  The option ONESPACEEDIT has been added to the 6EDIT 
                  FORMAT command Esc-1-LF. 
  Section 7 - IMP processor. 
               No changes. 
  Section 8 - LINK processor. 
               No changes. 
  Section 9 - LEMUR processor. 
               o  Upon exit, LEMUR now sets the STEPCC to indicate 
                  whether any errors were found. 
  Section 10 - PLOVER processor. 
               o  The documentation for the EXTERNAL command has been 
                  clarified. 
  Appendix A - DELTA directives. 
               No Changes. 
  Appendix B - ASCII Character set. 
               No changes. 
  Appendix C - Device Format Control Characters. 
               No changes. 
  Appendix D - Monitor Error Messages. 
               No changes. 
  Appendix E - Making ANS and IBM-compatible Tapes. 
               No changes. 
  Appendix F - X3.64 Functions. 
               No changes. 
00012
00011
00004
00002
00016
00003
00007
00009
00008
00014
00001
00005
00010
00015
00006
00013
Syntax: 
CHECK [jobidlist[output-file-spec]] [[,](optionlist)] 
Parameters: 
jobidlist   -   specifies one or more jobids in the format 
jobid[,jobid]...[,jobid], where jobid is one of the following, possibly 
preceded by "NOT" or "~": 
    sysid   -   is the job sysid assigned by the system and displayed in a 
    message sent to the user when the BATCH command that submitted the job was 
    processed. 
    jobname[.account]   -   is the alphanumeric job name which was defined 
    with the NAME option on the JOB command for the job to be checked.  If the 
    user does not have DISPJOB privilege, the named job must have been 
    submitted under the running account.  If account is not specified, the 
    current user's account name is the default. 
     .account   -   is any job that was submitted under the given account. 
    {NOT|~}   -   specifies that the jobid is to be removed from the USE file. 
    The jobid will still be CHECKed. 
output-file-spec   -   takes one of the following forms: 
    -1 or (1)   -   allows the specification of one subfile. 
    (1[2,...])   -   allows the specification of a list of subfiles. 
Note: Since CHECK allows a jobname of just digits, whenever a sysid or a 
jobname is allowed, if IBEX encounters a 6 or less digits number, it treats 
this as a sysid.  Anything of greater length is treated as a jobname.  If a 
jobname exists that can be treated as a sysid, the user must put the jobname 
inside single quotes to indicate to IBEX that this is a jobname.  Some 
examples are CHECK 'jobname'-1, CHECK '1234'-1, CHECK '1234'(1), CHECK 
'jobname'(1). 
optionlist   -   specifies one or more of the following options in the format 
option[,option]...[,option]: 
    INPUT [suboption]   -   searches only the Input queue with the following 
    suboptions: 
        ALL   -   displays all the input jobs. 
        HELD   -   displays only those jobs held in the queue. 
        READY   -   displays only those jobs ready to run. 
        The default suboption is READY. 
    JOB   -   searches only the Running queue. 
    ME   -   searches the queue(s) for only job(s) under the user's account 
    name. 
    OUTPUT   -   searches only the Output queue. 
    RUNNING   -   searches only the Running queue. 
    SYSTEM   -   searches the queue(s) for job(s) for any/everyone. 
    TERMINAL   -   searches the queue(s) for job(s) using the user's current 
    sysid. 
    USE   -   allows the user to specify a fid in which CHECK will store 
    sysids to be checked on later by the user.  If a file is named but no 
    account is specified, a default account (or default account and packset) 
    will be used as described in the CHECK/NOTIFY Options table. 
    WAIT [suboption]   -   directs the system to wait a specified interval, 
    then report on BATCH jobs that have changed status since last checked. 
    <BREAK> displays the status of all jobs being checked.  <CNTL-Y> or 
    <ESC><ESC> will abort the CHECK command.  Suboptions are as follows: 
        PRINT   -   wait until all jobs being checked are printing. 
        DONE   -   wait until all jobs being checked are done. 
        nnn   -   interval, in seconds, that CHECK is to sleep between 
        checking status of the jobs.  Default is 15 seconds. 
        The default is DONE. 
If neither jobid or optionlist is specified, all jobs with the current user's 
name and account which were BATCHed and not yet reported completed will be 
displayed.  Upon being reported completed, the record(s) corresponding to the 
job sysid will be deleted from the USE file. 
NOTE:  if both ME and SYSTEM are used in a single CHECK command, each applies 
only to the options following it.  Options without a preceeding ME or SYSTEM 
assume ME. 
See CHECK_OPTIONS or NOTIFY_OPTIONS for complete descriptions and syntax. 
Description: 
CHECK determines the status of batch jobs that have been submitted for 
execution. 
Sysids of jobs batched during the current session, plus sysids CHECKed by the 
user will be stored in the star file *$$JOB, which is created by CHECK.  If 
the user wants to store this information in a permanent file, the USE option 
allows him to specify any file.  When the sysid job has completed, the 
corresponding record will be deleted from the USE file.  When all records have 
been deleted, the file will be deleted. 
If the user wishes to see all the system input, output, and/or running job 
queues, he must be authorized for DISPJOB privilege. 
All options specified by CHECK are treated as one-time, no-remember commands. 
If options are specified with NOTIFY, they will be remembered and used as 
defaults for future CHECKs and NOTIFYs (at job steps). 
Examples: 
    !CHECK MYJOB 
displays the status of the job named MYJOB. 
    !CHECK 54 
displays the status of the job with the sysid 54. 
    !CHECK .:SYS 
displays the status of any job submitted under .:SYS. 
    !CHECK (INPUT,SYSTEM,OUTPUT,ME,RUNNING) 
displays all user's input, all output, and all user's running jobs. 
    !CHECK (WAIT DONE 15) 
CHECK goes to sleep for 15 seconds then awakens to report any BATCH jobs 
which have changed status since last checked.  When all jobs to be checked 
are done the WAIT command will terminate. 
    !CHECK (WAIT) 
Same as above using defaults. 
Related Commands: 
NOTIFY 
00002
00003
00001
00004
The options for the CHECK and NOTIFY commands are: 
INPUT, JOB, ME, OUTPUT, RUNNING, SYSTEM, TERMINAL, USE, and WAIT. 
Type HELP (IBEX) CHECK_OPS option. 
  Opt        Meaning 
  I[NPUT] [option] [[(~|NOT)] .[account]] [[(~|NOT)] @[wsn]] 
        Only the input queue is searched.  The INPUT option causes subsequent 
        queue inquiries to access the Input queue. 
        Valid options are: 
        A[LL]   -   report all the input jobs. 
        H[ELD]   -   report only those jobs held up in the queue for some 
        reason, such as FOLLOW condition. 
        R[EADY]   -   report all jobs that are ready to run. 
  J[OB] [[(~|NOT)] .[account]] [[(~|NOT)] @[wsn]] 
        Only the Running queue is searched.  Causes only running jobs to be 
        displayed. 
  M[E] 
        Searches the queue(s) for jobs under the user's account name.  The ME 
        option restricts subsequent queue inquiries to only access the user's 
        jobs and/or output.  (The alternative option is SYSTEM.) 
  O[UTPUT] [[(~|NOT)] .[account]) [[(~|NOT)] @[wsn]] 
        Searches only the output queue.  The OUTPUT option causes subsequent 
        queue inquiries to access the Output queue. 
  R[UNNING] [[(~|NOT)] .[account]] [[(~|NOT)] @[wsn]] 
        Searches only the Running queue.  Displays running jobs. 
  S[YSTEM] 
        Will search for any jobs or output in the queue only if the user is 
        authorized the DISPJOB privilege; searches the queues for jobs for 
        any/everyone. 
  T[ERMINAL] 
        Searches the queue(s) for job(s) using the user's current sysid, and 
        reports on all output status for that sysid. 
  U[SE] [=] [fid] 
        Allows the user to specify a fid in which sysids will be stored (to be 
        checked on later by the user).  This option sets up the file to be 
        used to store sysids from CHECKs.  If no fid is specified, then *$$JOB 
        is used.  If a file is named but no account is specified, the user's 
        default file management account (FMA) and default file management 
        packset are assumed. 
        The default FMA is the logon account unless the DIRECTORY command has 
        specified a new default account and optional packset.  When the USE 
        option is used with NOTIFY, the file name, account name, and optional 
        packset name will be remembered for future use. 
  W[AIT] [D[ONE]|P[RINT]] [n] 
        WAIT will sleep n seconds, if specified, then report those sysids that 
        have changed status, and then go back to "sleep" to repeat the cycle. 
        The default for n is 15 seconds.  DONE specifies that waiting will 
        terminate when all sysids have completed, and is the default.  PRINT 
        specifies that waiting will terminate when all sysids have completed 
        running, and are just printing, waiting to print, or have been 
        spooled.  NOTE:  CHECK does not wait for deferred jobs.  If the user 
        presses the BREAK key, CHECK will force a report on all jobs being 
        remembered in the USE file.  If the user presses <CNTL-Y>, CHECK(WAIT) 
        will be terminated. 
00001
00002
00003
00004
00005
00006
00007
00008
00009
CHECK_OPS
SPECIAL_KEYS
COPY
COPYALL
FID_CG
IBEX commands can be grouped into the following categories: 
Compilation and Execution    compiler, rununit, RUN, START 
Debugging                    DELTA, PMD, RUM, START, UNDER 
Command File                 BATCH, CANCEL, CHECK, ECHO, INCLUDE, 
                             JOB, PRIORITY, XEQ, XMIT 
Data Replacement             DEFAULT, GLOBAL 
Command Logic                END, GOTO, IF, LET, OUTPUT, QUIT, STOP, 
                             WHEN 
Interrupt Processing         CONTINUE, END, GET, GO, PROCEED, PROTECT, 
                             QUIT, RESTORE, SAVE, STOP 
Resource Control             ACQUIRE, LIMIT, ORESOURCE, PRIV, RELEASE, 
                             RESOURCE 
File and Device Control      ADJUST, DIRECTORY, LDEV, RESET, SET 
Output Control               COMMENT, ERASE, HOLD, LIST, PRINT, TITLE, 
                             UNHOLD 
Terminal Manipulation        EXPOUND, DRIBBLE, PLATEN, POINT, POSITION, 
                             PROFILE, TABS, TERMINAL 
Informational                CHECK, DATE, DISPLAY, HELP, REPORT, STATUS, 
                             TIME 
Miscellaneous                ACCEPT, ATITLE, BACKUP, BYE, DONT, ENTER, 
                             MESSAGE, NOTIFY, OFF, PASSWORD, SETUP, SWITCH 
Punched Deck                 ASC, BIN, EOD, FIN, NCTL 
HELP messages for each command can be obtained by typing: 
HELP (IBEX) command 
    To obtain summary information about IBEX command groups, enter: 
    o   Compilation and Execution 
     - !HELP GROUPS COMP 
    o   Debugging 
     - !HELP GROUPS DEBUG 
    o   Command Files 
     - !HELP GROUPS COMFILE 
    o   Data Replacement 
     - !HELP GROUPS DATA 
    o   Command Logic 
     - !HELP GROUPS LOGIC 
    o   Interrupt Processing 
     - !HELP GROUPS INTERRUPT 
    o   Resource Control 
     - !HELP GROUPS RESOURCE 
    o   File and Device Control 
     - !HELP GROUPS FILCON 
    o   Output Control 
     - !HELP GROUPS OUTPUT 
    o   Terminal Manipulation 
     - !HELP GROUPS TERMINAL 
    o   Informational Commands 
     - !HELP GROUPS INFO 
    o   Miscellaneous Commands 
     - !HELP GROUPS MISC 
    o   Punched Decks 
     - !HELP GROUPS CARDS 
    o   Other Processor Commands 
     - !HELP GROUPS OTHER 
    The following commands compile and execute programs: 
    "compiler"  -  Invoke a language processor (compiler). 
    "rununit"   -  Fetch and initiate execution of a rununit. 
    RUN         -  Link an object file (or files) and initiate 
                   execution of the resulting rununit. 
    START       -  Fetch and initiate execution of a rununit. 
    On the CP-6 system, language processors are system run-units.  Language 
    processor invoking commands have a common syntax, as represented by the 
    "compiler" command. 
    User created rununits are invoked by the "rununit" or the START command. 
    The RUN command performs a linking operation (see the LINK processor) and 
    then puts the resulting rununit into execution. 
    Debug processors are invoked through the following IBEX commands: 
    DELTA  -  Invokes DELTA following an execution interrupt. 
    PMD    -  Invokes DELTA to perform PMD (post-mortem dump) functions. 
    RUM    -  Invokes DELTA to perform patching operations. 
    START  -  Specifies a run unit and the controlling debug processor in 
              a single command.  Invokes the debug processor prior to 
              program execution. 
    UNDER  -  Specifies a controlling debug processor in a separate 
              command that is issued prior to specifying a run unit. 
    Debug activities are initiated by starting the execution of a run unit 
    under control of a debug processor.  The debug processor may be the CP-6 
    debug processor (DELTA), or a user written debug processor.  The debug 
    processor can be invoked before or after program execution is initiated. 
    DELTA is invoked after execution of a run unit has been initiated through 
    the DELTA command.  This command allows the interactive user to invoke 
    DELTA after execution is interrupted, either via a <CNTL-Y> interactive 
    interrupt or a program abort, or DELTA may be invoked as a stand alone 
    desk calculator (i.e., performs various arithmetic and numeric conversion 
    functions). 
    The following commands submit command files for execution and aid in the 
    monitoring and control of such files: 
    BATCH         -  Submit a command file to the batch queue for 
                     execution. 
    CANCEL        -  Delete a batch job or output from a batch job. 
    CHECK         -  Determine status of a batch job. 
    ECHO          -  Control the printing of an XEQ file. 
    INCLUDE       -  Merges the disk fid specified into the command stream 
                     without any data replacements being applied. 
    JOB, PRIORITY -  Define default batch job priority level. 
    XEQ           -  Submit a command file for immediate execution. 
    XMIT          -  Submit a file of some other system connected as a 
                     HASP workstation. 
    Command files, in most cases, can be executed in batch or online mode. 
    An execute (XEQ) file contains IBEX commands, run unit calls, and data. 
    It provides a convenient method of executing a frequently used sequence of 
    commands. 
    An XEQ file can contain any number of XEQ commands, giving the user the 
    capability to nest XEQ files.  When execution of a nested file is 
    completed, execution continues at the line in the calling XEQ file that 
    follows the line containing the XEQ. 
    The size limit for XEQ files is 2**27-1 records.  Batch files are used to 
    submit jobs to the system batch queue for execution.  Once in the batch 
    queue, the job is scheduled and executed by the system without any further 
    interaction with the user. 
    The user can submit a batch job from the card reader, interactive 
    terminal, or a running batch job.  If the job is submitted from a card 
    reader, the command stream can be contained in the card deck, which is 
    converted into a job file, or the command stream can be read from a 
    pre-stored job file.  If the job is submitted from an interactive session, 
    the command stream is contained in a pre-stored job file; the stream may 
    also be created directly from input typed at the terminal.  A pre-stored 
    job file is built normally through EDIT or PCL (though one can also be 
    built through a user program) and must reside on disk.  A record in a job 
    file may not exceed 256 characters. 
    When a job file is submitted for batch processing, it is queued, 
    scheduled, and executed.  A feature of batch processing is that the system 
    schedules jobs for execution based on priority and resource requirements. 
    The user can, within limits established for the installation, influence 
    scheduling of a job by assigning a batch job a higher or lower priority 
    than the default established for the installation. 
    The user defines a batch job and its priority through the JOB command, and 
    submits a batch job with the BATCH command.  Once a batch job is 
    submitted, the status of the job can be determined through the CHECK 
    command, and the job can be cancelled through the CANCEL command. 
    The size limit for BATCH files is 2**27-1 records. 
    The following two commands control the replacement of data, sometimes 
    called string substitution, within command files: 
    DEFAULT  -  Establish default replacement values. 
    GLOBAL   -  Establish global replacement values. 
    Prior to submitting a command file for execution, the user can replace 
    existing values with new ones.  He or she can: 
o   Define and modify data replacement parameters for a single BATCH or XEQ 
    file (through the DEFAULT command). 
o   Define and modify data replacement parameters for all BATCH, XMIT, and XEQ 
    files in the session (through the GLOBAL command). 
o   Override DEFAULT and GLOBAL data replacements for a file by specifying 
    data replacement parameters as part of the BATCH or XEQ command that 
    submits the file. 
Through string substitution parameters, the user specifies which string or 
field is to be changed, and what the new value is to be.  Every occurrence in 
the file of the specified field or string will be changed. 
If a string or field is identified for replacement more than once, (i.e., the 
field or string specified on the left-hand side of the replacement expression 
is specified in more than one command) it will be modified only once in 
accordance with the following three rules of precedence: 
1.  Within a job command stream, XEQ and BATCH command data replacement 
    specifications have precedence over DEFAULT data replacement 
    specifications and GLOBAL replacements (i.e., they are always honored). 
2.  Within a session, GLOBAL data replacement specifications have precedence 
    over DEFAULT replacement specifications.  A later GLOBAL specification 
    redefines an earlier one. 
3.  Within a file, a later DEFAULT replacement specification redefines an 
    earlier one. 
    The following commands provide logic and control within the structure of a 
    command file, or within the structure of an on-line session: 
    END     -  Terminate command file execution. 
    GOTO    -  Branch to a labeled command in a command file. 
    IF      -  Execute a command if a condition proves true. 
    LET     -  Define the value of a variable 
    OUTPUT  -  Print an expression through M$LL. 
    QUIT    -  Terminate command file execution. 
    STOP    -  Terminate command file execution. 
    WHEN    -  Execute a command if a condition proves true at JOBSTEP. 
    The flow of control from one job step to the next may be affected by the 
    IF, WHEN, LET and GOTO commands.  These commands operate on command 
    variables and command labels, giving the user the ability to conditionally 
    modify command stream flow. 
    The IF command allows the user to specify the conditions for affecting a 
    change in the command stream flow (the IF clause) and to redirect the flow 
    (the object clause).  The IF clause establishes a relational test which, 
    if true, causes the object clause that follows it to be executed.  The 
    object clause may consist of any IBEX command. 
    The WHEN command does the same thing as the IF command but it is executed 
    at each JOBSTEP while it is in effect. 
    The LET command establishes values, the GOTO command branches within the 
    command stream, and the QUIT, END and STOP commands terminate processing 
    of the command stream.  The OUTPUT command aids in the interaction of a 
    command file with the user. 
    IF, WHEN, LET, and OUTPUT utilize a powerful component called an 
    "expression".  An expression consists of variables, strings, functions, 
    operators, and other expressions, and is resolved (according to set of 
    definite rules) into a single numeric or string value. 
Command File Processing 
The following steps illustrates how IBEX XEQs (or BATCHes, or XMITs) a file: 
1.  The IBEX command file is opened. 
2.  Any GLOBAL substitution definitions are picked up. 
3.  A record is read. 
4.  IBEX asks, is this a !DEFAULT?  If yes, insert definition into tables; go 
    to step 3. 
5.  Is this an !INCLUDE?  If yes, perform substitutions on this command, then 
    parse.  Then copy the specified file to the destination. 
    Do not look for !DEFAULT or !INCLUDE in this included file.  Go to step 3. 
6.  Do string substitution on the record: 
    a.  Do command line substitutions (i.e. XEQ A B=XXX,Z=YYY). 
    b.  Do GLOBAL substitutions (i.e. !GLOBAL A=XXX). 
    c.  Do DEFAULT substitutions (i.e. !DEFAULT A=YYY). 
7.  Write the result to the destination. 
8.  Go to step 3.  Repeat until end of file. 
See PREPROCESSING for a detailed discussion of the differences between online 
substitutions and substitutions performed when a command file is XEQed, 
BATCHed, or XMITed. 
An activity can be interrupted by the system or by the user.  The user 
interrupts processing of an activity by entering a <CNTL-Y>.  The following 
commands handle processing of interrupted processes: 
CONTINUE  -  Resume interrupted activity. 
END       -  Cancel interrupted activity. 
GET       -  Retrieve suspended image. 
GO        -  Resume interrupted activity. 
PROCEED   -  Resume interrupted activity. 
PROTECT   -  Issue warning before discarding interrupted 
             activity. 
QUIT      -  Cancel interrupted activity. 
RESTORE   -  Retrieve suspended image. 
SAVE      -  Preserve suspended activity as an image. 
STOP      -  Cancel interrupted activity. 
IBEX controls processing until it invokes an activity (a user program or a 
processor (such as EDIT, LINK, PCL, or a compiler)) at which time it transfers 
control to the activity.  The activity controls processing until it completes 
or is interrupted.  In either case, control is returned to IBEX. 
When an activity completes normally and control is transferred to IBEX, the 
user is at a job step. 
The <CNTL-Y> interrupt suspends the current process, and IBEX initiates 
interrupt mode, in which the user is prompted with a double bang (!!) to enter 
a command.  The user responds by entering an IBEX command which is processed 
unless processing will result in making the interrupted activity unresumable 
and the PROTECT command has been issued earlier in the job stream.  This 
procedure continues until interrupt mode is terminated by GO or QUIT. 
If any of the following commands are issued, an interrupted activity cannot be 
resumed if the command is processed: 
BUILD              GOTO               MODIFY            Rununit 
Compiler           IF                 MOUNT             START 
COPY               L                  REMOVE            UNDER 
DELETE             LINK               RESTORE           WHEN 
EDIT               LOAD               REWIND 
EXAMINE            LYNX               RUM 
GET                MAP                RUN 
The processing path caused by any of these commands depends on whether a 
PROTECT command has been previously issued; if not, the interrupted process is 
automatically terminated and the command performed. 
If the PROTECT is in force, the user is asked if he wishes to quit with the 
message QUIT?  and then he is prompted again with the system prompt.  At this 
point, the user may: 
1.  Press carriage return, causing the interrupted process to be terminated; 
    the command causing the QUIT? query is then executed. 
2.  Enter another command; the command causing the QUIT? query is discarded in 
    favor of the most recent command.  If this command is any one of the 
    above, the whole process is repeated, starting with the QUIT? query. 
    The following commands handle the allocation of resources. 
    ACQUIRE    -  Requests and allocates (if available) additional resources 
                  for the user. 
    LIMIT      -  Sets maximum values for various system services required 
                  by a job. 
    ORESOURCE  -  Establishes resources and global limits required to run 
                  an online job.  (Ignored in batch jobs.) 
    PRIV       -  Alter user privileges. 
    RELEASE    -  Releases or deallocates previously allocated resources 
                  assigned to a job. 
    RESOURCE   -  Establishes resources and global limits required to run a 
                  batch job.  (Ignored in online jobs). 
    Allocatable resources are those resources (namely, tape, packsets and 
    devices, pseudo resources, TIME, and MEMORY) that may be reserved for a 
    user.  The RESOURCE command reserves these resources for batch processing; 
    it is used to communicate the user's allocation requirements to the system 
    before batch processing begins.  Similarly, the ORESOURCE command 
    communicates allocation requirements to the system for online job 
    processing.  The ACQUIRE command requests resources for allocation to his 
    use in addition to those he is currently allocated. The ACQUIRE command is 
    valid for online processing only. 
    After the ACQUIRE command has been processed, IBEX informs the user of any 
    acquired resources and any that were not available. 
    Service resources refer to those job execution resources for which the 
    user can establish limits (for example, job execution time, the number of 
    output pages, etc.)  The LIMIT command gives the user the ability to 
    specify limits on the use of these resources which, if reached, cause the 
    job to be aborted.  The user is given an option that allows him to 
    accumulate usage over job steps or to establish limits for a single job 
    step. 
    Once a resource has been allocated by a job, it remains allocated to that 
    job either until the job is terminated, or the resource is released via 
    the RELEASE command. 
    The PRIV command does not deal directly with allocatable resources, but 
    instead alters the way that the system perceives the user.  PRIV changes 
    the user privileges from their defaults, provided that the user has been 
    allocated the potential to obtain such privileges. 
    The following commands designate and define files and devices: 
    ADJUST     -  Modifies DCB assignments during a job step. 
    DIRECTORY  -  Defines default account assignments. 
    LDEV       -  Defines attributes for a logical device 
    RESET      -  Modifies DCB assignments between job steps. 
    SET        -  Assigns DCBs to files, devices, and comgroups. 
    The SET command makes DCB and attribute assignments to disk, tape and unit 
    record files, exclusive devices and comgroups.  Attribute values are 
    assigned initially either in the processor (user program or system 
    processor) or by the LINK Processor.  The SET command options are used to 
    re-assign those initial values at job steps.  The DCB assignments and 
    option values assigned by the SET command remain effective throughout the 
    job or session unless modified: 
o   At a subsequent job step by another SET command. 
o   At a subsequent job step by a RESET command which resets some or all DCB 
    parameter values to the default assignments by deleting the existing 
    assignments. 
o   During the job step by the ADJUST command.  ADJUST assigns the specified 
    option values to the specified DCB; but, the assignment does not survive 
    the job step. 
The LDEV command defines logical devices and defines and modifies logical 
device attributes.  The LDEV command is used when the Logical Device Special 
Names and/or their default attributes cannot be used. 
The following commands control the output of a job or terminal session: 
COMMENT  -  Defines a file for diagnostic output. 
ERASE    -  Delete accumulated output. 
HOLD     -  Holds symbiont output for later delivery. 
LIST     -  Define a file for listing output. 
PRINT    -  Direct accumulated output to destination. 
TITLE    -  Print title on each page at LP01. 
UNHOLD   -  Removes a job's symbiont output from HOLD status. 
These output control commands affect output assigned to a logical device 
(including line printers and card punches).  Normally, output from 
compilations, assemblies, PCL operations, DELTA dumps, and the like, destined 
for logical devices is accumulated until the interactive user logs off or 
until batch job processing is completed.  At that time, the accumulated output 
is sent to its destination on a first-in-the-queue first-out (spooled) basis. 
The three output control commands allow the user to: 
o   Interrupt the accumulation process (PRINT command) 
o   Drop accumulated output (ERASE command) 
o   Specify title text for the headers of pages of listing output (TITLE 
    command) 
The COMMENT or LIST commands: 
o   Define the destination of the output listing.  Output parameters set up in 
    this way are valid across job steps from the time given until the session 
    is terminated or until reset. 
o   Suppress the output listing.  Output parameters set up in this way are 
    valid only during a job step and only if the processor that creates the 
    output listing respects this convention.  Within a job step, they can be 
    reset. 
The DONT command can be used to suppress listings.  The effect of DONT is 
rescinded by the subsequent appearance in the command stream of a COMMENT or 
LIST command.  The command verb is used alone to rescind listing suppression 
and re-establish the most immediately previous output parameters. 
The timing of the rescind action depends on whether or not the command is 
issued between job steps. 
The following commands are oriented to terminal usage: 
DRIBBLE   -  Keep record of terminal session. 
EXPOUND   -  Reactivates '?' feature of CP-6 error message. 
PLATEN    -  Define page size. 
POINT     -  Provides a caret (^) as part of the syntax error message. 
POSITION  -  Reactivates automatic positioning of cursor in error message. 
PROFILE   -  Establish terminal profile. 
TABS      -  Define tab positions. 
TERMINAL  -  Modify terminal attributes. 
The PROFILE and TERMINAL commands define the characteristics of a terminal. 
The TERMINAL command also displays the current state of these characteristics. 
The PLATEN command defines the page size for terminal input and output.  The 
TABS command sets system-recognized tab stops. 
The DRIBBLE command provides a record of what took place during a user 
session.  This capability improves the usefulness of CRT devices, because 
errors and events can be examined after they have scrolled off the screen. 
The following commands print information: 
CHECK    -  Determine the status of a batch job. 
DATE     -  Print current date and time. 
DISPLAY  -  Print session attribute information. 
HELP     -  Provide user information. 
REPORT   -  Establish level of job statistics displayed. 
STATUS   -  Print accounting information. 
TIME     -  Print current date and time. 
It is part of the CP-6 philosophy to keep users as informed as possible.  To 
accomplish this, a family of information-oriented commands are included in 
IBEX. 
The following commands provide miscellaneous functions: 
ACCEPT    -  Accept various types of operator and system messages. 
ATITLE    -  Write a title into the accounting record. 
BACKUP    -  Identify file for back-up. 
BYE       -  Terminate session. 
DONT      -  Cancel effect of other commands. 
ENTER     -  Starts execution of an ADAPT dialog. 
MESSAGE   -  Send a message to the operator. 
NOTIFY    -  Sends list of all jobs run to completion to user after 
             each job step. 
OFF       -  Terminate session. 
PASSWORD  -  Set logon password. 
SETUP     -  Execute command at logon. 
SWITCH    -  Set and reset sense switches. 
The following cards are used primarily in punched card decks: 
!ASC   -  Terminate binary input and interpret subsequent data as 
          ASCII. 
!BIN   -  Interpret cards as binary input. 
!EOD   -  Define data blocks within a deck. 
!FIN   -  Specifies end of card deck.  (!JOB also terminates 
          the preceding job in the card deck.) 
!NCTL  -  Interpret non-control input at control device. 
The control cards are included in card decks to communicate information about 
the deck primarily to the card reader rather than to IBEX.  They are included 
here for completeness. 
The following other processor commands can be issued directly from IBEX. 
EDIT 
The following EDIT commands can be issued directly from IBEX: 
{EDIT|E}      -  invokes EDIT to modify an existing file. 
{BUILD|B}     -  invokes EDIT to build a new file. 
{EXAMINE|EX}  -  invokes EDIT to examine (but not modify) an existing file. 
When BUILD is issued from IBEX, control returns to IBEX at the completion of 
the BUILD operation. 
PCL 
The following PCL commands can be issued directly from IBEX: 
{COPY|C}         -  Transfers data between storage media. 
C[OPY]A[LL]      -  Copies a group of source files to a group of 
                    destination files. 
{DELETE|DEL}     -  Deletes files. 
{MODIFY|RENAME}  -  Modifies disk file name and attributes. 
MOUNT            -  Mounts a tape. 
{REMOVE|REM}     -  Removes a tape. 
{REWIND|REW}     -  Rewinds a tape. 
L                -  Lists a summary of disk and labeled tape storage. 
LINK 
The following LINK commands can be issued directly from IBEX: 
LINK             -  Creates an executable program. 
MAP              -  Produces a map of an existing run unit. 
RUN              -  Creates an executable program (run unit) and 
                    submits the run unit for immediate execution. 
EFT 
The following EFT commands can be issued directly from IBEX: 
FETCH     -  Requests return of specified file(s) to disk 
             from the archive tapeset. 
UNFETCH   -  Rescinds previous FETCH request for specified 
             files. 
STOW      -  Requests to enter files into the archive system. 
UNSTOW    -  Rescinds a previous STOW request for specified 
             files. 
UNARCHIVE -  Removes specified files from archive records; once 
             this is done, no record of the archive copy exists. 
ALTKEY 
The ALTKEY command invokes the ALTKEY processor to rebuild the alternate 
indexes of indexed files. 
00020
00014
00003
00003
00006
00001
00004
00002
00016
00019
00009
00012
00007
00018
00005
00013
00015
00010
00017
00008
00004
00011
Syntax: 
COMMENT [{ON|INTO|OVER} fid] 
Parameters: 
fid   -   identifies a disk file, a line printer or other symbiont device, the 
on-line terminal or a logical device. 
Description: 
COMMENT specifies the destination of diagnostic output produced by a 
processor. 
Examples: 
!COMMENT INTO LP 
directs diagnostic output to the line printer for the next job step. 
!COMMENT 
rescinds any DONT COMMENT command and re-establishes the previously 
established output destination for this job step. 
Related Commands: 
DONT 
00002
00003
00001
00004
Syntax: 
compiler [fid1][,fid2][{ON|OVER|INTO} [fid3][,fid4]][(optionlist)] 
Parameters: 
compiler   -   specifies one of the CP-6 compilers or other language 
processors.  For example: 
    PL6   COBOL   FORTRAN 
fid1   -   specifies the fid that contains source code.  The default DCB 
association is M$SI.  Implicitly sets the SI compiler option. 
fid2   -   specifies the fid that contains source code updates.  The default 
DCB association is M$UI.  Implicitly sets the UI compiler option. 
ON   -   specifies that if an object or listout file already exists, the 
existing file is not to be overwritten and the command is to be aborted. 
OVER   -   specifies that if an object or listout file already exists, the 
existing file is to be overwritten and the command is to be processed. 
INTO   -   specifies that if an object or listout file already exists, new 
output is to be added to the existing file.  If either of these files does not 
exist, it is created. 
fid3   -   specifies the fid to contain object units.  The default DCB 
association is M$OU.  Implicitly sets the OU compiler option. 
fid4   -   specifies the fid of the listing output destination.  The default 
DCB association is MSLO.  Implicitly sets the LS compiler option. 
optionlist   -   specifies one or more of the compiler options in the format 
(option[,option]...). 
Standard options are: 
    BC({ALL|number[,number]...}) 
    [{N|M}]DM[AP][(option[,option]...)] 
    [N]LO 
    [N]LS 
    [N]OU 
    [{M|N}]PM[AP] 
    [{M|N}]SC[HEMA] 
    [N]SO 
    SR[CH](fid[,fid]...) 
    [N]UI 
    [N]UR[EF] 
    [N]WA[RN] 
    [{M|N}]XR[EF] 
See COMPILER_OPS for complete descriptions. 
Individual language processors may accept numerous other options. 
Description: 
In CP-6, language processors are system run units.  The commands used to 
invoke language processors are rununit commands.  This subsection describes 
the standard aspects of language-processor invoking commands:  the common 
syntax they share, keywords that can be included in the option list of any of 
these commands, and the default DCB assignment all language processors make. 
Note that BASIC and APL do not follow these conventions. 
The specification of an update fid, object fid, and/or listout fid on the 
invocation line causes the UI, OU, and/or LS option to be implicitly set.  If 
these options are not desired, they must be explicitly reset using the NUI, 
NOU, and/or NLS options. 
In the absence of contrary specified options in the calling sequence for a 
compiler, the compiler also assumes the following: 
    LS, OU, BC(ALL), MSCHEMA, and WARN or NWARN 
Note: the setting of WARN or NWARN is compiler-dependent.  For example, the 
Fortran compiler sets WARN, while the COBOL compliler sets NWARN, unless 
specified otherwise. 
Examples: 
!PL6 
sets the option LS, OU, BC(ALL), MSCHEMA, and NWARN (the defaults assumed by 
the compiler). 
!PL6 A,B ON C,D 
sets the options UI, OU, LS, BC(ALL), MSCHEMA and NWARN.  Note that OU always 
implies MSCHEMA unless the user specifies otherwise.  Also note that UI is 
enabled because an update file is referenced within the compiler call. 
!PL6 A,B ON ,D (NSCHEMA, NUI) 
sets the options OU, LS, BC(ALL), NSCHEMA, and NWARN. 
!PL6 A,B 
sets the options OU, LS, MSCHEMA, UI, BC(ALL) and NWARN. 
!PL6 A,B (LS) 
sets the options UI, OU, MSCHEMA, LS, BC(ALL) and NWARN. 
Related Commands: 
See RUNUNIT 
00002
00003
00001
00004
COMPILER
The following options are standard to CP-6 language processor compilers: 
BC, DMAP, LO, LS, OU, PMAP, SCHEMA, SO, SRCH, UI, UREF, WARN, and XREF. 
See the COMPILER command for the default settings of LS, OU, BC(ALL), MSCHEMA, 
and WARN or NWARN. 
Type HELP (IBEX) COMPILER_OPS option 
  Option 
  BC({ALL|number[,number]...}) 
  Specifies the sequential number of each procedure in the source file to be 
  included as a compile unit.  ALL requests that ALL procedures be included. 
  {DM[AP]|NDM[AP]|MDM[AP]}[(option[,option]...)] 
  Requests a data map listing of the compilation object unit be written 
  through the M$LO DCB.  Option may consist of the following data types: 
  AU[TO], BA[SED], ST[ATIC], SY[MREF].  The prefix M requests a mini-map that 
  consists of the first level of a structure only.  The prefix N disables the 
  option. 
  {LO|NLO} 
  Specifies that the symbolic object listing is to be written through the M$LO 
  DCB.  The prefix N disables the option. 
  {LS|NLS} 
  Specifies that all source lines are to be listed through the M$LO DCB.  If 
  LS is not specified, only source lines with errors are listed.  The prefix N 
  disables the option. 
  {OU|NOU} 
  Specifies that the object unit is to be generated through the M$OU DCB.  The 
  prefix N disables the option. 
  {PM[AP]|NPM[AP]|MPM[AP]} 
  Requests a procedure map indicating the relative location of external entry 
  points, local subroutines, and labels be written through the M$LO DCB.  The 
  prefix M requests that the statement locations be omitted from the map.  The 
  prefix N disables the option. 
  {SC[HEMA]|NSC[HEMA]|MSC[HEMA]} 
  Specifies that debugging schema records are to be written through the M$OU 
  DCB.  The prefix M causes schema records to be written only for referenced 
  external or SYMDEFed items.  The prefix N disables the option. 
  {SO|NSO} 
  Requests that a new source file with updates merged is to be written through 
  the M$LO DCB.  The prefix N disables the option.  For information on update 
  files, insert HELP (HOSTLIB) UPDATE and HELP (HOSTLIB) XUU UPDATE 
  SR[CH](fid[,fid]...) 
  This option augments the specification of the accounts and packsets to be 
  searched if the language processor encounters an INCLUDE statement or 
  directive which specifies a file by file name only.  The list is a list of 
  accounts and/or packsets, separated by commas.  Each account designation 
  must have a leading period.  The packsets and accounts are searched in the 
  order specified in the list. 
  {UI|NUI} 
  Specifies that update source code is to be read from the M$UI DCB.  The 
  prefix N disables the option.  For information on update files, insert HELP 
  (HOSTLIB) UPDATE and HELP (HOSTLIB) XUU UPDATE 
  {UR[EF]|NUR[EF]} 
  Requests that a list of unreferenced data be written through the M$LO DCB. 
  The prefix N disables the option. 
  {WA[RN]|NWA[RN]} 
  Requests that all warning messages generated by the compiler be written 
  through the M$DO DCB.  The prefix N disables the option. 
  {XR[EF]|NXR[EF]|MXR[EF]} 
  Requests a cross reference listing of the compiled object units to be 
  written through M$LO DCB.  This listing contains a dictionary of symbol 
  definitions including all occurrences of all references to the definition. 
  The prefix M generates a cross-reference for used references only. 
00001
00002
00003
00004
00002
00006
00007
00013
00002
00003
00004
00005
00006
00007
00008
00010
00011
00012
00013
00005
00006
00007
00008
00009
00010
00011
00012
00013
COMPILER_OPS
The following syntactical constructs are shared among several IBEX commands: 
EXPRESSION  -  Numeric or string representation. 
REPLACEMENT  -  Alteration of fields and strings. 
RESOURCELIST  -  Allocatable system resources. 
HELP messages for these components can be obtained by typing:  HELP (IBEX) 
component 
COMPILER_OPS
Syntax: 
CONTINUE 
Parameters: 
NONE 
Description: 
CONTINUE (a synonym for the GO command) resumes an interrupted activity. 
CONTINUE is only meaningful at the double-bang (!!)  prompt. 
Examples: 
!!CONTINUE 
means resume the interrupted activity. 
Related Commands: 
GO, PROCEED 
00002
00003
00001
00004
SPECIAL_KEYS
The following conventions apply to a series of IBEX commands: 
o   Only one IBEX command may be used per line.  If the command and its 
    options extends over multiple lines, a semicolon must be used at the end 
    of each line except the last. 
o   Labels may not be used with the following commands: 
        !JOB 
        !RESOURCE 
        !INCLUDE 
        !DEFAULT 
    Labels may be used with all other IBEX commands.  A label may be 1-31 
    characters in length, and must be followed, with no intervening blanks, by 
    a colon.  The following characters are allowed (at least one character 
    must be non-numeric): 
        A-Z 
        a-z 
        0-9 
        $_#@ 
o   Comments may be included as part of a series of IBEX commands and may 
    appear anywhere arbitrary blanks are allowed.  Comments must be enclosed 
    in double quotes ("), but the closing quote is not required at the end of 
    a line.  If a comment extends over multiple lines, each line is treated as 
    a separate comment. 
o   The following IBEX commands may not be indented (i.e., no blanks are 
    allowed after !) and must be in upper case: 
        !JOB 
        !FIN 
        !EOD 
        !ASC 
        !BIN 
        !NCTL 
    For all other IBEX commands, indentation is allowed; i.e., any number of 
    intervening blanks may appear between ! and the command, as long as the 
    command appears on a single line. 
o   IBEX commands can only be continued where a delimiter (such as a blank, 
    comma, or equal sign) is permitted.  A continuation is signified by a 
    semicolon (;) to the right of the command.  Comments may appear to the 
    right of the semicolon. 
o   In IBEX command files, commands may be preceded by multiple bangs (!) to 
    create nested command files, as shown in the following example: 
        !JOB 
        !RES MEM=216,TIME=3 
        !IF %$FID_EXIST(X) THEN GOTO COMP_X 
        !COMP_Y: 
        !BUILD * 
        !!JOB 
        !!RES MEM=216, TIME=3 
        !!FORTRAN Y OVER Y_OU, Y_LS 
        !!LINK Y_OU OVER Y_RU 
        !!Y_RU. 
        !GOTO THE_END 
        !COMP_X: 
        !BUILD * 
        !!JOB 
        !!RES MEM=216,TIME=3 
        !!FORTRAN X OVER X_OU, X_LS 
        !!LINK X_OU OVER X_RU 
        !!X_RU. 
        !THE_END: 
        !XMIT * TO JE 
    The purpose of the above command file is to have a job running which will 
    create and submit a job to do a FORTRAN compile and run. 
COPY
COPYALL
Syntax: 
C[OPY] sourcelist[ {TO|ON|OVER|INTO} destination][ FROM fid] 
Parameters: 
sourcelist   -   specifies a list of sources with input options. 
A maximum of ten input options is allowed.  See PCL INOPS. 
The basic format of the source parameter is: 
fid[(option[,option]..)] 
TO   -   specifies file creation. 
ON   -   specifies file creation. 
OVER   -   specifies file replacement. 
INTO   -   specifies file extension. 
destination   -   specifies a single destination fid with output 
options and attributes that may replace or add to the attributes of 
the source fid.  The COPY command issued from IBEX always defaults 
to LP in batch and to ME online.  The first time a COPY command is 
issued from PCL, the default is the same as it would be in IBEX. 
Subsequent COPY commands issued inside PCL default to the last COPY 
destination.  The COPY command defaults INTO fid.  If an error 
condition occurs, the default is reset back to the original 
default. 
The basic format of the destination parameter is: 
fid[(option[,option]...)] 
FROM fid   -   specifies default values for parts of a fid not specified in 
the source parameters.  See PCL SINGLE_SOURCE, DESTINATION, and FROM for more 
detailed syntactical information. 
Description: 
COPY copies a source or list of sources to a single specified 
destination.  When a copying operation begins, a message "..COPYing" 
is printed. 
Examples: 
<COPY LESLIE 
means copy the file LESLIE to the default destination (the terminal 
in on-line operations, the line printer in batch if no previous COPY 
has been done in this session). 
<COPY LESLIE,HELEN TO FILEA 
means copy files LESLIE and HELEN into a new file FILEA. 
<COPY ?A? (OR=CON) TO FILEB(RD=ALL) 
means copy all files that contain the character "A" in their file 
name, and that are of consecutive file organization, into a new file 
FILEB giving READ access to all accounts. 
<COPY A>C TO FILEC 
means copy all files between A and C (using file range selection) to 
a new file FILEC. 
Related Commands: 
See the PCL Help Facility. 
00002
00003
00001
00004
Syntax: 
C[OPY]A[LL] [sourcelist][ {TO|ON|OVER|INTO} destination][ FROM fid] 
Parameters: 
sourcelist   -   specifies a list of sources with input options.  If 
unspecified, all files in the user's account are assumed.  Input 
file selection is also dependent upon any input options included as 
part of a source parameter.  The basic format of the source 
parameter is: 
fid[(option[,option]...)] 
TO   -   specifies file creation. 
ON   -   specifies file creation. 
OVER   -   specifies file replacement. 
INTO   -   specifies file extension. 
destination   -   specifies a special fid with associated output 
options that define the characteristics of the output files.  This 
may be any valid fid, except that no file name can be included 
unless it is a wildcard file name.  The default, if not specified, 
is the user's account directory. 
FROM fid   -   specifies default values for parts of a fid not 
specified in the source parameters. 
See PCL SINGLE_SOURCE, RANGE_SOURCE, WILD_SOURCE, COMPLEX_SOURCE, 
DESTINATION, and FROM for detailed syntactical information. 
Description: 
COPYALL copies a source or group of sources to a group of 
destinations, generally preserving any associated file names, but 
allowing the modification of other fid elements. 
COPYALL is primarily for multiple file transfers.  Unless a 
wildcarded fid is included as part of the destination parameter, the 
names of the input files in the source parameters are preserved in 
the output files.  The other fid elements of the input files are not 
retained; the destination parameter defines device type, account, 
password, etc. of the output files. 
WILDCARD CONSIDERATIONS:  If wildcarding is used recursion may 
occur.  If the output file name places the output file in the input 
selection range, the operation may be repeated on the output file. 
To prevent recursion other input selection criteria may be added 
(such as DATEC < NOW). 
Examples: 
<COPYALL .MYACCOUNT 
DANIEL    HELEN     LESLIE    PAPPY 
     4 files,     32 granules copied 
< 
means copy all the files in the account .MYACCT into the user's account.  As 
each file is transferred, its file name is printed at the terminal. 
<COPYALL ?N? TO ?n? 
means copy all files that contain the character "N", creating new files that 
contain (in their file names) the character "n" in place of the character "N". 
As each file is copied, the source file name is printed with an "arrow" 
pointing to the new file. 
DANIEL -> DAnIEL    HELEN -> HELEn 
     2 files,     16 granules copied 
< 
<L  . 
DANIEL    DAnIEL    HELEN     HELEn     LESLIE    PAPPY 
     6 files listed 
< 
Note that only the first occurrence of the letter is changed. 
However, recursion may occur if output file falls within the 
selection range. 
<CA  ?P? TO ?H? 
PAPPY -> HAPPY 
      1 file,        8 granules copied 
<COPYALL ?E? TO ?e? 
DANIEL -> DANIeL    DAnIEL -> DAnIeL    HELEN -> HeLEN 
HELEn -> HeLEn      HeLEN -> HeLeN      HeLEn -> HeLen 
LESLIE -> LeSLIE    LeSLIE -> LeSLIe 
      8 files,      32 granules copied 
<L . 
DANIEL    DANIeL    DAnIEL    DAnIeL    HAPPY     HELEN 
HELEn     HeLEN     HeLEn     HeLeN     HeLen     LESLIE 
LeSLIE    LeSLIe   PAPPY 
      7 files listed 
< 
Related Commands: 
See PCL HELP facility. 
00002
00003
00001
00004
WINDOWS
SPECIAL_KEYS
Syntax: 
DATE 
Parameters: 
None 
Description: 
DATE (a synonym for the TIME command) prints the current date and time. 
Examples: 
!DATE 
requests a display of the current data and time.  A sample display is: 
MAR 02  '84  11:03 
Related Commands: 
TIME 
00002
00003
00001
00004
Any user-created DCB defaults to FUN=IN, with the special name ME. 
The following DCBs are predefined: 
  DCB          Function           Default Fid 
M$LO         CREATE             ME 
M$LL         CREATE             LO 
M$DO         CREATE             LO 
M$PO         CREATE             NO 
M$SI         IN                 CR 
M$SO         CREATE             NO 
M$UI         IN                 CR 
M$OU         CREATE             *G 
M$EI         IN                 CR 
M$EO         CREATE             NO 
M$ME         UPDATE             ME 
Command line DCBs for compilers have the following conventions: 
  DCB          Function           Default Fid 
#1           IN                 CR 
#2           IN                 CR 
#3           CREATE             *G 
#4           CREATE             LO 
The FORTRAN compiler assigns FORTRAN program DCBs F$ names.  Other processors 
or users may create F$ DCB names, also. 
  DCB          Function           Default Fid 
F$xxx        UPDATE             ME 
F$101        IN                 ME 
F$102        CREATE             ME 
F$103        IN                 NO 
F$104        CREATE             NO 
F$105        IN                 CR 
F$106        CREATE             CP 
F$107        UPDATE             ME 
F$108        CREATE             L0 
F$5          IN                 CR 
F$6          CREATE             LO 
F$7          CREATE             CP 
DCB_DEFAULTS
Syntax: 
DEFAULT [{rep[,rep]...|DELETE[{field1|'string1'}[{field2|'string2'}]...]}] 
Parameters: 
rep   -   specifies a replacement specification in the format: 
{field1|'string1'}={field2|'string2'} 
See the REPLACEMENT component for a complete description. 
DELETE   -   removes a previous default replacement equation.  If DELETE is 
not followed by one or more fields or strings, all of the previously specified 
default replacements are cancelled. 
field1|'string1'   -   specifies the current replacement specification that is 
to be deleted, e.g., if "A='OX'", then "DELETE A" kills the replacement. 
Description: 
DEFAULT specifies data replacement equations to be applied to subsequent 
records in a command file.  The DEFAULT command may appear any number of times 
and anywhere within the file, and it is effective only in the file in which it 
is contained.  Note that the strings within a DEFAULT command are not subject 
to string substitution.  Command variable expressions will not be evaluated at 
the time the DEFAULT command is processed. 
Type HELP GROUPS LOGIC for additional information. 
Examples: 
!DEFAULT abc=DEF 
All subsequent occurrences of the field abc are to be replaced by the field 
DEF. 
!DEFAULT 'NOT'=NON,EQUAL=GREATER,'o'=' ' 
All subsequent occurrences of the string NOT will be replaced by the field 
NON, the field EQUAL will be replaced by the field GREATER, and the string o 
will be replaced by a blank. 
!DEFAULT DELETE 
deletes all previous DEFAULT replacement specifications. 
Related Commands: 
GLOBAL 
00002
00003
00001
00004
Syntax: 
DEL[ETE] sourcelist[FROM fid] 
Parameters: 
sourcelist   -   specifies a list of disk filenames, ranges of disk files, or 
wildcard filenames, with only OR and TY input options permitted. 
FROM fid   -   specifies a default set of fid elements that are used when the 
source components are parsed. 
Description: 
DELETE deletes a file or range of files from disk storage. 
When a single file is deleted with DELETE, a message is printed that confirms 
the deletion and the number of granules that the file contained.  When 
multiple files are deleted with a DELETE command, a verification of the 
operation is requested.  The user must type YES$ in response to this 
verification, or the operation is aborted.  If the operation is not aborted, 
the name of each file is printed as it is deleted, and upon completion, a 
message is printed confirming the number of files deleted and the number of 
granules freed. 
When the DELETE command is used to delete multiple files in batch job 
execution or as part of an XEQ command file, verification is not requested. 
Examples: 
!DELETE FILEA,FILEB,FILEC 
means delete files FILEA, FILEB, and FILEC.  A message is printed that 
confirms the deletions. 
!DELETE ?Q.PIG FROM ..MAGIC 
means delete all files in account PIG where names end with a Q, that 
have a password MAGIC, or no password. 
Related Commands: 
See the PCL Help Facility 
00002
00003
00001
00004
INVOKING_DELTA
DISPLAY
Syntax: 
{DIR|DIRECTORY} [fid|R[ESET]] 
Parameters: 
fid   -   specifies the new default account fid, and may consist of an account 
or a packset name and an account. 
RESET   -   specifies that the default account is to be reset to the running 
account. 
Description: 
DIRECTORY changes the default account and packset.  The default account and 
set are the account and associated packset that are selected if an account is 
not supplied as part of a disk file fid specification.  Initially, the default 
account is the logon or running account and the packset name is nil.  When 
used without parameters, DIRECTORY displays the current directory pointer. 
Examples: 
!DIRECTORY .SYSLIB 
This command directs that subsequent fids that do not include an account are 
to default to the .SYSLIB account and the packset associated with that 
account. 
!DIRECTORY DP#UTIL.Y 
This command specifies that subsequent fids that do not include an account are 
to default to the Y account on the packset named UTIL. 
!DIRECTORY RESET 
This command re-establishes the running account and its associated packset as 
the default. 
Related Commands: 
NONE 
00002
00003
00001
00004
FID_DISK
Syntax: 
{DI|DISPLAY} [optionlist] 
Parameters: 
optionlist   -   specifies one or more of the following options in the format 
option[,option]... 
ALL   -   displays all of the individual displays that may be requested 
through the DISPLAY command. 
BA[NNERTEXT]{(PERM|SESSION)}   -   displays the user's banner text lines 1 
through 9; these may be inserted or modified by the LET command.  PERM 
displays the permanent banner text.  SESSION displays the session banner text, 
which is the default.  The DISPLAY ALL command includes both. 
BUDGET   -   displays the user's budget. 
DATE   -   displays the date and time. 
DCBS   -   displays all current user DCB assignments and attributes. 
DCB(dcb-list)   -   displays the list of dcb names and/or numbers separated by 
commas. 
dcb name   -   displays the current attributes of the named DCB. 
DCB number   -   displays the current attributes of the FORTRAN DCB specified 
by dcb number (the FORTRAN DCB name is of the form F$dcb number where dcb 
number is the number indicated for this option). 
{DIR|DIRECTORY}   -   displays the account's directory name. 
FLAGS   -   describes the SET or RESET status of the output control flags for 
the COMMENT, DRIBBLE, ECHO, EXPOUND, LIST, NOTIFY, POINT, POSITION, 
PROTECT,and WHEN commands and the ANNOUNCE, BROADCAST, and SEND options of the 
ACCEPT command. 
GLOBAL   -   displays the GLOBAL definitions for string substitutions. 
LDEV [item|(item list)]   -   displays settings of currently defined Logical 
Devices (LDEVs) where item is: 
        ALL   -   display all defined LDEVs. 
        dv   -   2 alpha characters which will display all LDEVs 
                 with that resource name. 
        dvnn   -   2 alpha characters followed by 2 digits which will 
                 display that specific LDEV (for example UC98). 
        The default is LP. 
LIMIT[S]   -   displays current LIMIT-defined limits. 
NOTIFY   -   displays the current USE command if one exists.  Also, displays 
the settings of the various NOTIFY flags. 
PLATEN [UCnn]   -   displays the current terminal platen settings. 
PPRIV[S]   -   displays what processor privileges this user is allowed. 
PRIO[RITY]   -   displays the default and maximum batching priority. 
PRIV[S]   -   displays the current processor privileges as defined by the 
system manager. 
PROFILE[S] [pattern]   -   displays the user profile.  If pattern is given, 
then available profiles matching that pattern are displayed; otherwise, all 
available profiles are displayed. 
REPORT   -   displays the level of accounting statistics to be displayed. 
REG[ISTEREDNAME]   -   displays the user's registered name, which is the mail 
alias when available or account/user's name (default). 
{RES|RESOURCES}   -   displays current batch and on-line resource usage. 
SETS   -   displays the current DCB assignments. 
SETUP   -   displays the current command defined through the SETUP command. 
STEPCC   -   displays the current value of the system variable STEPCC. 
SWITCH   -   displays the current sense switches which are set to ON. 
TABS   -   displays the current terminal tab settings. 
{TERM|TERMINAL}   -   displays the current terminal attributes for the 
terminal at which the user is logged on. 
TIME   -   displays the date and time. 
USER   -   displays the user logon id, the SYSID and the user number for the 
current session. 
{VARS|VARIABLES} [pattern]   -   displays command variables set by the LET 
command.  If pattern is given, only the variables matching the pattern are 
displayed. 
WHEN   -   displays the current WHEN command if one exists. 
WSN   -   displays the work station name of origin. 
Description: 
The DISPLAY command displays information regarding system operation and the 
currently logged on user. 
The DISPLAY command entered without options produces the following display: 
    USERS = xxxx 
    ETMF = xxxx 
    90% RESPONSE < xxxx MSECS 
    mmm dd 'yy hh:mm 
where 
USERS   -   is the total number of currently active batch, on-line, and ghost 
users. 
ETMF   -   is the execution multiplier currently relating program CPU time to 
job throughput time.  ETMF is calculated and updated each minute.  If ETMF=10, 
a user requiring 1 minute of CPU time could expect to get that amount in 10 
minutes of wall clock time. 
RESPONSE   -   gives the number of milliseconds that just exceeds the response 
time of 90 percent of the responses to terminal requests. 
Examples: 
!DI ALL 
displays all the individual displays produced by the DISPLAY command, 
including the users complete bannertext (registered name, permanent 
bannertext, and session bannertext). 
!DI DCBS 
displays the user's current DCB assignments and attributes. 
!DI SETUP,SWITCH,PRIV 
displays the user's current setup command, sense switch settings, and 
privileges. 
!DI VARS L? 
displays all command variables that start with "L". 
!DI BA 
displays the user's session banner text (the default): 
   SESSION BANNERTEXT: 
   1: 
   2: 
   3:               Horatio Albatross 
   4:               5250 West Century Blvd. 
   5:               Los Angeles Ca. 
   6:               90045 
   7: 
   8: 
   9: 
DI BA (PERM) 
displays the users permanent banner text: 
   PERMANENT BANNERTEXT: 
   1: 
   2: 
   3:               Harlow Enterprises 
   4:               6000 Sunset Blvd. 
   5:               Los Angeles Ca. 
   6:               90024 
   7: 
   8: 
   9: 
Related Commands: 
LET 
00002
00003
00001
00004
Syntax: 
DONT dontlist 
Parameters: 
dontlist   -   specifies one or more of the following options in the format 
option[,option]... 
    ACCEPT [suboption|(acceptlist)]   -   cancels the user's display of 
    specified messages. 
    where 
    suboption   -   may be any of the following: 
        ALL   -   inhibits all operator messages. 
        ANNOUNCE   -   inhibits tape and disk mount announcements. 
        BROADCAST   -   inhibits operator BROADCAST and SENDALL keyin 
        messages. 
        SEND   -   inhibits operator SEND keyin messages. 
    If none of the above suboptions is used, ALL is assumed. 
acceptlist   -   specifies one or more of the above suboptions in the format 
option[,option]... 
    COMMENT   -   cancels the COMMENT command. 
    DRIBBLE   -   terminates recording of interactive terminal transactions 
    (see DRIBBLE command). 
    ECHO   -   cancels the ECHO command. 
    EXPOUND   -   suppresses the "?" function of the syntax error message. 
    LIST   -   suspresses output by turning off the list flag in the JIT. 
    NOTIFY   -   cancels the NOTIFY command. 
    POINT   -   cancels the display of a caret as part of the syntax error 
    message. 
    POSITION   -   cancels the automatic respositioning of the cursor as part 
    of the syntax error message. 
    PROTECT   -   cancels the PROTECT command. 
    WHEN   -   cancels the WHEN command. 
See the command description for the LIST and COMMENT commands for limitations 
regarding their use. 
Description: 
DONT cancels a condition which has been set either by default or by the user 
explicitly issuing a command. 
Examples: 
!DONT ECHO 
cancels the previously issued ECHO command. 
!DONT LIST,PROTECT 
cancels the PROTECT commands previously issued by the user and turns off the 
list flag in the JIT.  (To cancel the LIST command, enter RESET #4). 
Related Commands: 
ACCEPT, COMMENT, DRIBBLE, ECHO, LIST, NOTIFY, PROTECT, WHEN 
00002
00003
00001
00004
Syntax: 
DRIBBLE [{ON|OVER|INTO} fid] 
Parameters: 
fid   -   designates the file, device, or magnetic tape on which the user's 
interactive terminal transactions are to be recorded. 
Description: 
DRIBBLE provides a means of recording interactive terminal transactions on a 
file, device or magnetic tape.  The command specifies that recording is to 
commence on a designated fid.  Once started, recording continues through 
successive job steps until the end of job or until the DONT DRIBBLE command is 
processed.  If an error occurs (such as, acct disk space exceeded) during the 
write to the dribble file, the dribble file is closed and the dribbling is 
stopped. 
Examples: 
!DRIBBLE OVER MY_DRIB_FILE 
means record interactive transactions on the file MY_DRIB_FILE. 
!DRIBBLE ON LT#MYTAPE/MYFILE 
means record interactive transactions on the file MYFILE on labeled tape 
MYTAPE. 
Related Commands: 
DONT 
00002
00003
00001
00004
EDIT
Syntax: 
ECHO 
Parameters: 
NONE 
Description: 
ECHO prints IBEX commands contained in an XEQ file as they are read from the 
command stream.  The default is ECHO; that is, if the ECHO command is not 
issued, the echoing of commands read from the XEQ file does occur.  The 
commands are echoed through the M$LL DCB.  The form DONT ECHO is included in 
an input stream to terminate echoing. 
IBEX continues to echo commands being executed from XEQ files until a DONT 
ECHO command is issued or the session terminates.  The leading character 
printed for echo commands is a $ (instead of a !). 
Examples: 
!ECHO 
means print commands from the command file as they are read from the command 
stream. 
Related Commands: 
DONT 
00002
00003
00001
00004
Syntax: 
{E|EDIT} fid 
Parameters: 
fid   -   is the disk file to be opened. 
Description: 
EDIT opens a previously-created disk file for editing.  The EDIT processor is 
designed to edit keyed disk files.  Any attempt to open any other file 
organization results in a message describing the restrictions applied to 
editing or examining that file.  An error message is printed if the file does 
not exist, or if the user is not permitted to access the file.  EDIT is always 
a file command. 
Examples: 
!EDIT LEMEGETON 
means open file LEMEGETON for editing. 
!EDIT RELFILE 
means open the file RELFILE for editing. 
Related Commands: 
See the EDIT Help Facility 
00002
00003
00001
00004
Syntax: 
EJECT [dev[nn]] 
Parameters: 
dev   -   is a two-character device name (e.g., LP or UC).  The default is the 
current destination of the M$LL DCB. 
nn   -   is a two-digit device number. 
Description: 
EJECT allows the user to do a page eject on the output listing.  For UC00 
through UC99, the EJECT command instead clears the window associated with the 
specified stream.  A true page-eject only happens for the user's terminal if a 
PLATEN command with length greater than 11 is in effect.  Otherwise, if the 
cursor is not already at the bottom line of the window, and the terminal or 
IBEX window is a scrolling one, the EJECT command causes the cursor to advance 
to the bottom line. 
Examples: 
!EJECT 
IBEX will eject to the top of the form for each EJECT command input. 
Related Commands: 
NONE 
00002
00003
00001
00004
Syntax: 
END 
Parameters: 
NONE 
Description: 
END (a synonym for the QUIT command) cancels an interrupted activity, or 
terminates all command files. 
Examples: 
!!END 
means do not resume the interrupted activity, return to IBEX prompt (!). 
Related Commands: 
QUIT, CONTINUE, GO 
00002
00003
00001
00004
Syntax: 
ENTER [ script-fid ] [ , frame-name ] [ initial-input ] 
Parameters: 
script-fid    is the file identifier for the script to execute. 
frame-name    is the first frame of the script to execute. 
initial-input    supplies responses to the initial prompts for the dialog. 
Description: 
The ENTER command starts execution of an ADAPT dialog at the IBEX level.  It 
can be used to run dialogs that only issue IBEX commands, or to start a dialog 
that invokes and runs under another program.  It can also be used to test 
dialogs to be started by another program. 
Rules: 
1.  The script-fid parameter specifies the file containing the compiled script 
    for the dialog to be executed.  The default is the current setting of the 
    ADAPT$SCRIPT DCB.  If the script-fid does not specify an account, the file 
    of the specified name in :SYS is used if it exists; otherwise, the current 
    directory account is the default.  To ensure that the file in the current 
    account is used, a period (.) must follow the file name. 
2.  The frame-name parameter specifies the first frame of the script-fid to be 
    executed.  The default is the MAIN frame for the script. 
3.  The initial-input parameter can be used to presupply responses to the 
    initial prompts for the dialog.  The text supplied is put into the dialog 
    input buffer before the first frame is started.  The default is no initial 
    input text, which means that the user is prompted for all dialog inputs. 
    Either the script-fid or frame-name must be specified if initial-input is 
    provided. 
4.  The dialog is put into execution at the IBEX level.  It can issue IBEX 
    commands and start programs by using the DO statement to pass command 
    lines to IBEX.  If the dialog executes any ISSUE statements to pass 
    commands to the running program, the commands are echoed through M$LO. 
5.  If any frame of the script, including the top frame, is defined to be run 
    under another program (via the DO clause on the frame definition 
    statement), that frame and all frames it enters run under the specified 
    program, not at the IBEX level.  Dialogs running under another program 
    function as described under HELP (ADAPT) ENTER_COMMAND. 
6.  Terminal input for a dialog running at the IBEX level is read through 
    M$SI.  Output to the interaction window is written through M$LO. 
00002
00001
00003
Syntax: 
!EOD 
Parameters: 
NONE 
Description: 
The EOD control card defines data blocks within a data deck. 
The End Of Data (EOD) control card follows the data block it defines.  Any 
number of EOD cards can be included in a card deck.  The EOD control card will 
terminate binary input mode. 
Examples: 
!EOD 
means the current data block has ended. 
Related Commands: 
BIN, ASC 
00002
00003
00001
00004
Syntax: 
ERASE [ALL|ldevlist] 
Parameters: 
ALL   -   specifies that the accumulated outputs for all logical devices are 
to be deleted.  This is the default. 
ldevlist   -   specifies that the accumulated outputs for the specified 
logical device or devices are to be deleted.  The list is entered in the 
format 
ldevname[,ldevname]... 
ldevname is a logical device name established through the LDEV command. 
Description: 
ERASE deletes the accumulated outputs for logical devices. 
Examples: 
!ERASE ALL 
deletes all output accumulated for all logical devices defined for the session 
or job. 
Related Commands: 
LDEV, PRINT, HOLD, UNHOLD 
00002
00003
00001
00004
This message shows the escape sequences which are standard on the CP-6 system. 
Certain escape sequences can include optional numeric characters.  For 
example, <ESC> n <I>, where n=23, positions to column 23 of the current 
record.  In cases when numeric characters are permitted within an escape 
sequence, the numeric values recognized can be from 1 to 9999.  A negative 
n-value is permitted in some cases and is designated with a trailing minus 
sign (e.g., <ESC> n [-] <I>). 
Note:  The n-value is limited in magnitude to 9999.  An attempt to enter a 
larger value is interpreted by zeroing the accumulated value before attempting 
to accumulate a digit that would otherwise cause overflow, e.g., 
<ESC> 10234 <S> is interpreted as <ESC> 4 <S>.  Using an n-value greater than 
9999 could be useful on terminals where function keys use <ESC> <digit> 
sequences.  For such terminals, it is possible to IMP a function key to 
T=ESC,/9999/ I R IN, and use it instead of <ESC> to introduce any numeric 
sequence, even one that would otherwise look like a function key.  This 
approach works at normal typing speed and in typeahead.  This characteristic 
is also useful if you forget which digits you have typed, or know that you 
have entered an error.  Just enter 9000 to cancel any current accumulation, 
e.g., if you enter 43 instead of 42, the sequence <ESC> 43 9000 42 <I> yields 
the intended <ESC> 42 <I>. 
If you IMP a function key introducer as a SPECIAL_CHAR and not as an 
introducer, the corresponding function keys will not work, but the 
SPECIAL_CHAR will. 
The following mode-toggling escape sequences trigger a terminal response to 
indicate whether the associated mode setting is on (+) or off (-):  <A>, <C>, 
<E>, <ESC>N<T>, <P>, <S>, <T>, <U>, <W>, <CNTL-T>, <CNTL-A>, and the 
mode-toggling numeric escape, <ESC> n <T>. 
For example, typing <ESC> <A> causes one of the following responses: 
    <A+>      indicates that PAGEHALT is now active 
    <A->      indicates that PAGEHALT is now inactive 
and typing <ESC> 13 <T> causes one of these responses: 
    <PK+>     indicates that PARKCURSOR is now active 
    <PK->     indicates that PARKCURSOR is now inactive 
To obtain information about ESCAPE sequences type: 
HELP ESC sequence, where 'sequence' may be: 
                              Example 
                              ------- 
  an alphabetic character     HELP ESC  B 
  n_ and an alpha character   HELP ESC  n_I 
  CNTL_letter                 HELP ESC CNTL_R 
  a special character         HELP ESC $  or  HELP ESC '$' 
  NOTE: the - and > characters 
  must be in single quotes    HELP ESC '>' 
To list all the Escape sequences, type ??<CR> at the next prompt.  See also 
HELP SPECIAL_KEYS. 
The information is ordered into two columns as shown below: 
  Sequence   Function 
  <ESC> <A> 
             Toggles (reverses the setting of) CRT pagination mode.  When on, 
             output will halt at the end of each screen full of output, 
             relative to the last input line (depends upon whether relative 
             pagination is on.) Pressing carriage return resumes output.  See 
             HELP TERMINAL_OPS PAGEHALT 
  <ESC><CNTL-A> 
             Toggles the WRAPPAGE pagination mode.  See HELP TERMINAL_OPS 
             WRAPPAGE 
  <ESC> <B> 
             Simulates <BREAK>.  This deletes any type-ahead and any partially 
             input record, and transfers the running program to its break 
             entry point.  Output is not deleted. 
  <ESC><CNTL-B> 
             Same as <ESC> <B> but does not delete any type-ahead. 
  <ESC> <C> 
             Toggles relative tabbing mode.  When on, tab positions are 
             relative to the position where the prompt ended, such as an EDIT 
             sequence number.  When off, tabs are computed relative to column 
             1 of the terminal.  See HELP TERMINAL_OPS TABRELATIVE 
  <ESC> [n[-]] <C> 
             Moves cursor right n characters.  If n is omitted, is zero, or is 
             negative (n-), the default is one character.  Same as <CNTL-R> 
             unless n is greater than one. 
  <ESC> <D> 
             Recalls the last saved input record as if the user had just 
             retyped it.  See HELP INPUT_EDITING RETRIEVING 
  <ESC> [n[-]] <D> 
             Moves cursor left n characters.  If n is omitted, is zero, or is 
             negative (n-), the default is one character.  Same as <BS> unless 
             n is greater than one. 
  <ESC><CNTL-D> 
             Recalls the last saved input record for this domain. 
  <ESC> <E> 
             Toggles echoplex mode.  When off, input characters are not echoed 
             back to the terminal.  See HELP TERMINAL_OPS DISPINPUT. 
  <ESC> <F> 
             Terminates the current terminal read request with an end-of-file 
             completion code. 
  <ESC> <G> 
             Displays the FEP number, port channel number, VDH context block 
             address, and session number (see <ESC> n <.>). 
  <ESC> <H> 
             Halts terminal output immediately.  Pressing carriage return 
             resumes output. 
  <ESC> n <H> 
             Sets HSSHIFT (the number of columns that an input image is to be 
             shifted) to the value n.  See TERMINAL_OPS HSSHIFT 
  <ESC> [n[-]] <I> 
             Simulates a horizontal tab.  Moves the cursor to the next input 
             tab stop if n is omitted or is zero; moves the cursor to the 
             column specified by n of the input record or of the window 
             (depending on the setting of TABRELATIVE) if n is a positive 
             number; moves the cursor to the previous tab stop if n is any 
             negative number (n-).  If the stop (or column) is outside of the 
             insertion window, the insertion window is reset. 
  <ESC> <J> 
             Toggles setting or activation of the insertion window.  Sets the 
             left and right limit of the insertion window.  Note:  <ESC> <J> 
             is equivalent to <ESC> <<> <ESC> <>> or <ESC> <R>, whichever 
             toggles the insertion window. 
  <ESC> <K> 
             Deletes from the current edit point to the right end of the 
             insertion window. 
  <ESC><CNTL-K> 
             Deletes to the left end of the insertion window. 
  <ESC> <L> 
             Ejects a page if a logical (form) page length has been set. 
  <ESC> <M> 
             Resets overstrike and insertion modes, disabling overstriking. 
             See <ESC> <O> and <ESC> <'>.  Also see HELP TERMINAL_OPS 
             SENDBKSPACE and HELP TERMINAL_OPS INSERT. 
  <ESC> n <M> 
             Sets HSMARGIN (the closest the cursor is to be allowed to 
             approach the end of an input area) to the value n.  See HELP 
             TERMINAL_OPS HSMARGIN. 
  <ESC> <N> 
             Positions to the right limit of the insertion window unless the 
             edit point is already there.  In this case, <ESC> <N> resets the 
             insertion window first. 
  <ESC> <O> 
             Sets overstrike (as opposed to replacement or insertion) mode for 
             input.  When on, typing on top of an existing character creates 
             an input record that contains both characters, separated by a 
             backspace character.  See <ESC> <'> and <ESC> <M>.  Also see HELP 
             TERMINAL_OPS SENDBKSPACE and HELP TERMINAL_OPS INSERT. 
  <ESC> <P> 
             Sets half-duplex paper tape mode.  In this mode, nothing is 
             output or echoed to the terminal.  This is exited upon receipt of 
             a <BREAK>, <CNTL-Y>, <ESC> <ESC>, or <ESC> <Y>.  Note the ASCII 
             character DC1 sets full duplex paper tape and DC3 disables full 
             duplex paper tape.  See HELP TERMINAL_OPS HALFDUXPAPERTAPE. 
  <ESC> <Q> 
             Status request:  The front-end immediately responds with !HI!. 
             The system responds with !state! where state is the user's 
             current scheduler state.  Type HELP SCHED_STATE for listing of 
             host scheduler states or HELP FEP_SCHED_STATE for listing of FEP 
             scheduler states. 
  <ESC> <R> 
             Retypes the current input record.  Resets both the left and right 
             limits of the insertion window to frame the entire record. 
  <ESC><CNTL-R> 
             Same as <ESC><R>, except no retype occurs. 
  <ESC> n <R> 
             Resets the terminal control parameter identified by n.  For a 
             list of the n-values and their meanings, type HELP ESC_TERMCTL. 
  <ESC> <S> 
             Toggles space insertion mode for tabs.  If on, an appropriate 
             number of spaces are generated in the input record when the <TAB> 
             key (or <CNTL-I>), or <ESC> <I> key is pressed.  See HELP 
             TERMINAL_OPS SPACEINSERT. 
  <ESC> n <S> 
             Sets the terminal control parameter identified by n.  For a list 
             of the n-values and their meanings, type HELP ESC_TERMCTL. 
  <ESC> <T> 
             Toggles tab simulation mode.  When on, tab characters in the data 
             streams are evaluated before being sent to the terminal; when 
             off, they are written as literal characters.  See HELP 
             TERMINAL_OPS TABSIM. 
  <ESC><CNTL-T> 
             Toggles the truncate mode.  See HELP TERMINAL_OPS TRUNCATE 
  <ESC> n <T> 
             Toggles the terminal control parameter identified by n.  For a 
             list of the n-values and their meanings, type HELP ESC_TERMCTL. 
  <ESC> <U> 
             Toggles uppercase restriction converting lowercase alphabetic 
             input to uppercase.  See HELP TERMINAL_OPS UPPERCASE. 
  <ESC> <V> 
             <ESC> <V> are the first two characters of a three character 
             sequence in which the third character is to act as a criterion 
             for a search of the input record within the insertion window.  If 
             the character is located in the window, the edit point is moved 
             to that column.  The direction of the search is set by the 
             last-received cursor-motion function (e.g., <ESC> <V>, <ESC> <I>, 
             <BS>, or <CNTL-R>, <TAB>, <CNTL-W>) or by parameter 5.  <ESC> <V> 
             sets the direction to the direction moved during the last 
             successful search. 
  <ESC> <W> 
             Stops printing of all pending output until another <ESC> <W> is 
             typed or a read is issued that is not satisfied by type-ahead. 
             See HELP TERMINAL_OPS OUTPUTDISCARD. 
  <ESC> <X> 
             Deletes the current input record. 
  <ESC> <Y> 
             Monitor attention:  deletes type-ahead and any partially input 
             record, and returns control to the command processor. 
  <ESC> <.> 
             (period) Switches the cursor between sessions.  See HELP LDEV_OPS 
             LOGON. 
  <ESC> n <.> 
             n (period) Permits switching directly to a particular session. 
             Each new session for a given user is allocated the lowest unused 
             non-zero number.  Once a session is created, its number does not 
             change.  The session number to be used for 'n' is displayed by 
             the <ESC> <G> sequence. 
  <ESC> <'> 
             (single quote) Sets insertion mode, resetting overstrike mode, if 
             active. 
  <ESC> <*> 
             Saves the characters in the insertion window for later recall via 
             <ESC> <:>. 
  <ESC> <:> 
             (colon) Recalls the characters last saved with <ESC> <*> for this 
             terminal. 
  <ESC> [n] <^> 
             (caret) Sets wordwrap column.  Sets wordwrap column to the 
             current cursor position if n is not specified; sets wordwrap 
             column to column n.  If n is omitted and the cursor is at the 
             beginning of the input record (up to column 12) or if n is less 
             than 12, disables wordwrap mode.  For more information, see HELP 
             TERMINAL_OPS WORDWRPCLM. 
  <ESC> <$> 
             Changes terminal font; users with APL terminals type <ESC> <$>, 
             where the specified $ key is the one in the font they want to be 
             in. 
  <ESC> <|> 
             <ESC> <|> changes the font to an APL one on a standard ASCII 
             terminal.  To return to the normal font, enter an <ESC> <$>, 
             using the key that is labeled <$> on the keyboard. 
  <ESC> <~> 
             <ESC> <~> changes the font to an APL one on a standard ASCII 
             terminal.  To return to the normal font, enter an <ESC> <$>, 
             using the key that is labeled <$> on the keyboard. 
  <ESC> <)> 
             Enters lowercase shift, converting uppercase alphabetic 
             characters to lower case.  The following conversions are also 
             made: 
             [  ->  { 
             \  ->  | 
             ]  ->  } 
             ^  ->  ~ 
  <ESC> <(> 
             <ESC> <(> exits lowercase shift mode. 
  <ESC> <-> 
             Indicates that a hardcopy terminal is positioned at the 
             perforation of the paper; used when a page length has been 
             previously established.  For a CRT, clears the screen and 
             repaints any borders, forms, or screen-editing windows, if any 
             exist. 
  <ESC> <<> 
             Sets (not toggles) the left limit of the insertion window. 
  <ESC> <>> 
             Sets (not toggles) the right limit of the insertion window. 
  <ESC> <CR> 
             Moves the edit point to the left limit of the insertion window, 
             unless the edit point is already there.  In this case, <ESC><CR> 
             resets the insertion window first. 
  <ESC> <DEL> 
             Delete the character to the left of the cursor.  If the cursor is 
             at the beginning of the insertion window, <ESC> <DEL> does 
             nothing. 
  <ESC> <ESC> 
             Same as <ESC> <Y>. 
  <ESC> <CNTL-W> 
             Deletes the word which is under and to the right of the cursor. 
             A 'word' in this sense is any sequence of non-blank characters 
             followed by any number of blanks; the word and the blanks 
             following it are deleted. 
  <ESC> [n] <CNTL-I> 
             Sets auto-tab column mode.  Sets auto-tab column to the current 
             cursor position if n is omitted; sets auto-tab column to column n 
             if n is specified.  If n=0 or 1 or if the cursor is at the 
             beginning of the record, disables auto-tab column mode.  Type 
             HELP TERMINAL_OPS AUTOTABCLM for more information. 
  <ESC> <LF> 
             Local LINE FEED.  The terminal is advanced one line, but no 
             changes are made to the current input record. 
00045
00041
00049
00048
00042
00050
00039
00043
00051
00052
00001
00003
00005
00002
00004
00009
00018
00027
00032
00056
00053
00007
00050
00054
00010
00055
00011
00012
00013
00015
00016
00017
00019
00058
00020
00022
00006
00057
00008
00014
00015
00021
00028
00030
00033
00006
00008
00014
00015
00021
00028
00030
00033
00023
00024
00025
00026
00053
00029
00031
00034
00035
00036
00037
00038
00044
00001
00003
00005
00007
00010
00011
00012
00013
00015
00016
00017
00019
00020
00022
00040
00006
00057
00008
00014
00015
00021
00028
00030
00033
00006
00008
00014
00015
00021
00028
00030
00033
00023
00024
00025
00026
00029
00031
00034
00035
00036
00037
00038
00046
00047
ESC
The following table lists the n values permitted in the <ESC> n <R>, 
<ESC> n <S>, and <ESC> n <T> sequences. 
The information is ordered in three columns:  the n-value, the acronym used in 
the response to <ESC> n <T>, and the terminal control parameter affected. 
    n       ACK       Meaning 
(any n<20 is available in CP5, CP5S1, CP5S2, SE1, and SE2, except 
9 and 10, which are available only in SE1 and SE2) 
    1       AT      Autotabclm - toggle is not able to set non-zero. 
    2       IN      Insert. 
    3       ML      Msglin. 
    4       WC      Wordwrapclm - toggle is unable to set. 
    5       ER      Edit-right.  Establishes the direction for word and 
                    character searches. 
    6       TC      Truncate. 
    7       AO      Actontrn. 
    8       WW      Wordwrap. 
    9       RW      Recordwrap.  (SE1 and SE2 only) 
   10       TE      Textedit.  (SE1 and SE2 only) 
   11       EA      Easyappend.  (SE1 and SE2 only) 
   12       CC      Changecase - makes forward cursor movement change 
                    the case of the characters under it. 
   13       PK      Parkcursor. 
   14       OS      Onespaceedit.  (SE1 and SE2 only) 
(any n>19 is available only in CP5 and CP5S1) 
   20       SB      Sendbackspace - also known as overstrike mode. 
   21       DI      Dispinput - also known as echoplex. 
   22       PC      Paritycheck. 
   23       OD      Outputdiscard. 
   24       UC      Uppercase. 
   25       AL      Apllcnrm. 
   26       RO      Retypovr. 
   27       EO      Editovr. 
   28       SC      (unused) 
   29       PA      Pagehalt. 
   30       PR      Printhalt. 
   31       RP      Relpage. 
   32       SP      Simperf. 
   33       NO      Nooptimiz. 
   34       WP      Wrappage. 
   35       LE      Localecho. 
   36       MH      Msghalt. 
   37       AC      Autocursor. 
   38       TO      Truovrprt. 
   39       CR      Cursorread. 
   40       KT      Keeptypahd. 
(any n>49 is available only in CP5) 
   50       TS      Tabsim. 
   51       TR      Tabrelative. 
   52       SI      Spaceinsert. 
   53       LC      Lowercase. 
   54       FP      Fullduxpapertape. 
   55       HP      Halfduxpapertape. 
Syntax: 
EX[AMINE] fid 
Parameters: 
fid   -   is the disk file to be opened for reading. 
Description: 
EXAMINE opens a disk file for reading; no updating is permitted. 
Examples: 
*EXAMINE CONCEPT 
means open the file CONCEPT for reading. 
Related Commands: 
See the EDIT Help Facility 
00002
00003
00001
00004
Syntax: 
EXIT 
Parameters: 
NONE 
Description: 
EXIT allows the user to exit out of an XEQ file without interrupting the 
complete command stream for nested XEQs.  If the user wants to interrupt the 
complete command stream the QUIT command should be used. 
Example: 
File A 
         !XEQ B 
         !OUTPUT "Hi Ma" 
         ... 
File B 
         !Blotto. 
         !If STEPCC > 7 then QUIT 
         !If STEPCC > 0 then EXIT 
         !LDEV LP99  LP@LOCAL 
         !COPY BLOTTO_OUT TO LP99 
         !PRINT 
         !END 
Execution of the preceding code works as follows: 
File B is executed from within file A.  If STEPCC is greater 
than 7, the execute mode is stopped and the  command stream 
is flushed.  If STEPCC is greater than 0 but 7 or less, then 
flow is returned to file A at the next command.  "Hi Ma" is 
output and the flow continues from there.  If STEPCC is 0, 
the remainder of file B is executed and the flow returns to 
file A at the next command.  "Hi Ma" is output and the flow 
continues. 
Related Commands: 
END, QUIT, STOP 
00002
00003
00001
00004
Syntax: 
EXPOUND 
Description: 
The EXPOUND command reactivates the "?" message feature of the CP-6 syntax 
error message after the !DONT EXPOUND command has been used.  This feature is 
active by default unless !DONT EXPOUND is used. 
Related Commands: 
DONT, POINT, POSITION 
00001
00002
Format: 
[unary]{variable|string|integer|function|system_variable}[operator expression] 
Parameters: 
unary   -   specifies a modifier for the field that follows it. 
Valid modifiers are: 
    +  or .PLUS.   specifies identity 
    -  or .MINUS.  specifies negation 
    ~  or .NOT.    specifies 'not', a truth value operation 
variable   -   specifies a 1 to 31 character variable that must begin with an 
alphabetic character.  The legal character set is: 
    A-Z a-z 0-9 $_#@ 
'string'   -   specifies a quoted string of any ASCII characters.  If the 
string has a numeric form, it will be treated as a numeric value when used 
with arithmetic operators.  All functions that manipulate strings use zero as 
the origin, that is, the first character is considered to be the zero 
character.  The length of a string is one greater than the last character 
position.  The length of a null string is zero. 
integer   -   specifies a decimal integer.  The maximum arithmetic size of an 
integer is 34359738367. 
    Examples of integers: 
    In the following example, overflow will occur: 
    LET A = 34359738367 
    LET A = A + 1 
    Following is an example of an invalid integer: 
    LET A = 34359738368 
    LET A = A + 1 
function   -   specifies one of the following system functions: 
    $ACCT 
    $ABS 
    $CMDVAR_EXISTS(variable-name) 
    $DATE [(TYPE=type)] 
    $DAY [(TY[PE)]=type)] 
    $DIR 
    $EOF 
    $FID_ASN  (expression) 
    $FID_EXIST(expression) 
    $FID_GRANS (expression) 
    $FID_NGAVAL (expression) 
    $FID_ORG (expression) 
    $FID_RECS(expression) 
    $FID_TYPE(expression) 
    $FID_UGRANS (expression) 
    $FLAG (FLAGS) 
    $HSET 
    $INDEX(expression1,expression2[,expression3[,expression4]]) 
    $INPUT(expression1[,expression2[,expression3]]) 
    $KEYIN(expression) 
    $LAST[BATCH] 
    $LEN[GTH](expression) 
    $LOC (expression) 
    $MAX (arg1,arg2...) 
    $MIN (arg1,arg2...) 
    $MOD (arg1,arg2) 
    $MODE 
    $NAME 
    $PRIV_ACTIVE (PRIV) 
    $PRIV_AUTH (PRIV) 
    $REM (arg1,arg2) 
    $RERUN 
    $SEARCH(expression1,expression2[,expression3[,expression4]]) 
    $SITE 
    $SUBSTR(expression1[,expression2[,expression3]]) 
    $SWITCH(expression) 
    $SYSID 
    $TERM_FEP 
    $TERM_LINE 
    $TERM_PROFILE 
    $TERM_SPEED 
    $TIME ([TYPE=type]) 
    $UPC (expression) 
    $VERIFY(expression1,expression2[,expression3[,expression4]]) 
    $VERSION 
    $WOO 
See FUNCTIONS for complete descriptions. 
system_variable   -   specifies one of the following standard variables, which 
reflect the status of the last executed job step: 
    STEPCC   -   yields 0 if processing terminated normally; 4 if it 
    terminated because of an error; 6 if the program aborted. 
    OK   -   yields 1 if processing terminated normally; 0 if not. 
    ERROR   -   yields 1 if processing errored; 0 if not. 
    ABORT   -   yields 1 if processing aborted; 0 if not. 
The user must access these system variables through IBEX.  Note that the 
STEPCC setting is a default and can be altered by user intervention (e.g., LET 
STEPCC=200).  The other system variables are non-alterable. 
operator   -   specifies an arithmetic, a relational, or a truth operator or 
the concatenation operator. 
Arithmetic Operators are: 
    +  or .PLUS.     plus 
    -  or .MINUS.    minus 
    *  or .TIMES.    multiply 
    /  or .DIVIDED.  divide 
Relational Operators are: 
    =   or  .EQ.          equals 
    ~=  or  .NE.          not equals 
    >   or  .GT.          greater than 
    >=  or  .GE.          greater than or equal to 
    <   or  .LT.          less than 
    <=  or  .LE.          less than or equal to 
    ?=  or  .IMB.         is matched by string on the right 
    =?  or  .MAT[CHES].   matches string on the left 
    ?>  or  .IN.          is contained in string on the right 
    <?  or  .CON[TAINS].  contains string on the left 
Note that comparisons for relational operators are numeric comparisons if the 
two operands are numeric and string comparisons otherwise. 
Two types of wildcard comparisons are possible:  exact match of a pattern or 
string, and containment of a pattern or string. 
Wildcarding Exact Match 
The following operators look for the exact match of a pattern.  According to 
the rules of wildcarding, the expression must exactly fit the wildcard pattern 
to return a 1.  Otherwise a 0 is returned. 
expression=?'pattern' - symbolic form, right-side pattern 
'pattern'?=expression - symbolic form, left-side pattern 
expression.MATCHES.'pattern' - mnemonic form, right-side pattern 
'pattern'.IMB.expression - mnemonic form, left-side pattern 
Wildcarding Contained Pattern 
The following operators look for a contained pattern.  If the expression 
contains a substring that matches the pattern according to the rules of 
wildcarding, a 1 is returned.  Otherwise a 0 is returned.  Note that the same 
behavior could be obtained by adding a wild token on each side of the pattern 
to be matched. 
'pattern'?>expression - symbolic form, left-side pattern 
expression<?'pattern' - symbolic form, right-side pattern 
'pattern'.IN.expression - mnemonic form, left-side pattern 
expression.CON[TAINS].'pattern' - mnemonic form, right-side pattern 
Truth Operators are: 
    &  or .AND.    and 
    |  or .OR.     or 
The Concatenation Operator is: 
    || or !! 
expression   -   specifies a valid expression, including a string or pattern 
for wildcarding.  Recursion is permitted. 
Expressions in IBEX are evaluated from left to right with operators of the 
higher precedence being performed first.  The precedence may be modified by 
the use of enclosing parentheses. 
    OPERATION                PRECEDENCE   OPERATOR 
    ---------                ----------   -------- 
    $functions                   9 
    UNARY PLUS                   8           + 
    UNARY MINUS                  8           -    
    MULTIPLY                     7           * 
    DIVIDE                       7           / 
    PLUS                         6           + 
    MINUS                        6           -    
    CONCATENATION                5       ||  or   !! 
    EQUAL                        4       =   or  .EQ. 
    NOT EQUAL                    4       ~=  or  .NE. 
    LESS THAN                    4       <   or  .LT. 
    LESS THAN EQUAL              4       <=  or  .LE. 
    GREATER THAN                 4       >   or  .GT. 
    GREATER THAN EQUAL           4       >=  or  .GE. 
    WILDCARD - IS MATCHED BY     4       ?=  or  .IMB. 
    WILDCARD - MATCHES           4       =?  or  .MAT[CHES]. 
    WILDCARD - IS CONTAINED IN   4       ?>  or  .IN. 
    WILDCARD - CONTAINS          4       <?  or  .CON[TAINS]. 
    UNARY NOT                    3       ~   or  .NOT. 
    LOGICAL AND                  2       &   or  .AND. 
    LOGICAL OR                   1       |   or  .OR. 
Description: 
An expression is a numeric or string representation that can consist of 
constants, variable references, or function calls, optionally combined with an 
operator and another expression.  The maximum length string is 511. 
When an expression is encountered in an IBEX command, all functions are 
resolved, then any unary plus or minus is applied, next all multiplication and 
division is resolved, followed by addition and subtraction.  All 
concatenations are then made, followed by all relations as defined by 
relational operators.  The unary ~ is then resolved, then .AND. and finally an 
.OR. 
This order may be altered through the use of parentheses.  The end result is, 
in the LET command, assigned to the specified variable, or in the IF or WHEN 
command, tested for "truthfulness" (the criteria being - if the resulting 
value is positive, the expression is true). 
Examples: 
(See the LET and IF command for expression examples.) 
Usage: 
Expressions are used in the IF, WHEN, LET, and OUTPUT commands. 
00002
00008
00009
00001
00003
00007
00006
00010
00005
00004
EXPRESSION
FEP_SCHED_STATES
To obtain information about the FEP user scheduler states, enter: 
!HELP (IBEX) FEP_SCHED_STATE state 
where state is the state designator.  For example, 
     HELP FEP_SCHED_STATE SCI 
provides information on user scheduler state SCI 
To list all the FEP user scheduler states, type ??<CR> 
at the next prompt. 
The table has the following format: 
  State               Meaning 
No Host       The FEP has detected a host outage. 
Connecting    The FEP has initiated a session creation for this device. 
Logging on    The FEP wants you to type a legal logon string. 
Profile       The FEP is waiting for profile information to be sent 
              from the host. 
SC1           FEP user in compute queue 1 (highest) 
SC2           FEP user in compute queue 2 
SC3           FEP user in compute queue 3 
SC4           FEP user in compute queue 4 
SC5           FEP user in compute queue 5 
SC6           FEP user in compute queue 6 
SC7           FEP user in compute queue 7 
SC8           FEP user in compute queue 8 
SC9           FEP user in compute queue 9 
SC10          FEP user in compute queue 10 
SC11          FEP user in compute queue 11 (lowest) 
SCU           FEP user in execution 
SIOW          FEP user waiting for I/O to complete 
SW            FEP user asleep 
SQFI          FEP user waiting for interrupt to fire 
SMEM          FEP user waiting for memory 
SMF           FEP user waiting for outstanding I/Os to fall below 
              control threshold 
SQA           FEP user queued for access 
SQFP          FEP user queued waiting for FPRG to load 
SCOB          FEP user in output blocked state (too much output) 
SCI           FEP user in communications input state (terminal input) 
SCW           FEP user in communications I/O wait state (host I/O) 
SNUL          FEP user slot empty (just run down or starting) 
00002
00002
00003
00003
00001
00001
00004
00004
00005
00014
00015
00006
00007
00008
00009
00010
00011
00012
00013
00025
00024
00016
00026
00017
00020
00021
00027
00022
00019
00023
00018
FEP_SCHED_STATES
Format: 
FET[CH] fid1[, fid2] ... 
Parameters: 
fid1, fid2    specify CP-6 file identifiers. 
Description: 
The FETCH command requests the return to disk of the file(s) in the archive 
system.  The most recent copy of the file from the archive tapeset is obtained 
by FETCH.  To prevent update activity, the file is locked until it is returned 
from tape at the next RETRIEVE run, performed by the system manager. 
Usage Notes: 
1.  If an active file is fetched, the tape copy replaces the current 
    disk file, and the file remains stowed on tape. 
2.  A user may be able to FETCH an inactive file, but be unable to 
    access it if access controls for the file exclude the user. 
3.  This command may be used:  a) if the user is the creator of the file, b) 
    if the user has FMSEC active via !PRIV FMSEC or c) for stowed inactive 
    files, if the user is able to create files in the account. 
4.  While the file is queued for STOW or FETCH, it may not be 
    updated.  Following the successful FETCH of an archived file, 
    the file must be UNARCHIVEd before it can be updated. 
5.  If the file management account limit is exceeded, FETCH requests are 
    ignored by the RETRIEVE process unless, however, the FETCH request was 
    made with FMSEC active. 
!FETCH TESTFILE 
requests retrieval of the file TESTFILE; at the next RETRIEVE run, the most 
recently archived version of the file is returned to disk (over the current 
copy of the file). 
00002
00004
00001
00003
The basic formats are: 
DISK FID: 
[DP[nn][#setname]/]name[.[account][.password]] 
TAPE FID: 
{MT|LT|FT}[nn]#serial[#serial]...[/[name][.[account][.password]]] 
UNIT RECORD FID: 
Format 1: 
dv[@[wsn]] 
Format 2: 
dvnn[#] 
COMGROUP FID: 
CG[nn][#setname]/name[.[account][.password]] 
Note: 
Any part of a fid (i.e., nn, name, account, etc.) may be specified in any of 
three ways: 
1.  in clear text - AAA 
2.  in quotes - 'AAA' 
3.  in octal - O'101101101' 
For example, the legal fid 
    O'104120'#PSN/'NAME'.ACCT.O'101102103' 
is equivalent to: 
    DP#PSN/NAME.ACCT.ABC 
This is true for all fid formats (disk, tape, unit record, and comgroup). 
However, for simplicity each format is described below with entries specified 
in clear text. 
Quotes must be used, however, to enclose ASCII non-printing or control 
characters that are part of a password. 
Type:       HELP FID_DISK     for more information about disk fids 
            HELP FID_TAPE     for more information about tape fids 
            HELP FID_UR       for more information about unit record fids. 
            HELP FID_CG       for more information about the comgroup fid. 
00001
Format: 
CG[nn][#setname]/name[.[account][.password]] 
Parameters: 
nn   -   is a two digit field indicating which disk resource (if the user has 
reserved more than one) is to be accessed.  This number is user-defined and 
not related to the system configuration. 
setname   -   specifies a string of 1 to 6 characters that identifies the 
packset on which the comgroup is located.  Packset names are assigned by the 
system manager. 
name   -   is a string of 1 to 31 characters that assigns an identifying name 
to the comgroup.  The valid characters for this parameter are A through Z, a 
through z, the digits 0 through 9, and the $ _ : and - characters. 
account   -   is a string of 1 to 8 characters that identifies a file 
directory.  The valid characters for the account parameter are the same as 
those for the name parameter.  Accounts are created by the system manager.  If 
unspecified, the user's default file management account is assumed.  The 
default file management account is the log-on account unless the default is 
changed through the IBEX DIRECTORY command. 
password   -   is a string of 1 to 8 characters that provides a 
user-controlled security check for comgroup access.  The password parameter 
can consist of any ASCII characters (including non-printing characters and 
control sequences).  Quotes must be used to enclose a password that contains 
non-printing or control sequence characters.  The user must include the 
password if the comgroup is password protected. 
Examples: 
CG#WONG/MY_COMGROUP 
means comgroup MY_COMGROUP on packset WONG. 
CG#ZILCH/SWITCHER..PRIORITY 
means comgroup SWITCHER (with password PRIORITY) on packset ZILCH. 
00002
00001
Format: 
[DP[nn][#setname]/]name[.[account][.password]][@remote-node] 
Parameters: 
nn   -   is a two digit field indicating which disk resource (if the user has 
reserved more than one) is to be accessed.  This number is user-defined and 
not related to the system configuration. 
setname   -   specifies a string of 1 to 6 characters that identifies a 
packset.  Packset names are assigned by the system manager. 
name   -   is a string of 1 to 31 characters that assigns an identifying name 
to a file.  The valid characters for this parameter are A through Z, a through 
z, the digits 0 through 9, and the $ _ :  and - characters.  The * character 
is used as a first character to identify star files, which are temporary files 
that are deleted when the user leaves the system. 
account   -   is a string of 1 to 8 characters that identifies a file 
directory.  The valid characters for the account parameter are the same as 
those for the name parameter.  Accounts are created by the system manager.  If 
unspecified, the user's default file management account is assumed.  The 
default file management account is the log-on account unless the default is 
changed through the IBEX DIRECTORY command. 
password   -   is a string of 1 to 8 characters that provides a 
user-controlled security check for file access.  The password parameter can 
consist of any ASCII characters (including non-printing characters and control 
sequences).  Quotes must be used to enclose a password that contains 
non-printing or control sequence characters.  The user must include the 
password if the file is password protected. 
@remote-node   -   is an ISO FTAM reference to data at some other network 
node. 
Examples: 
LOIS 
means disk file LOIS, in the current directory account. 
LOIS.TOME 
means disk file LOIS, in the account TOME. 
LOIS.TOME.HERMETIC 
means disk file LOIS, sealed with password HERMETIC in the account TOME. 
DP#RICK/LOIS.TOME.HERMETIC 
means disk file LOIS, sealed with password HERMETIC, in account TOME, on disk 
pack RICK. 
00002
00001
Format: 
{MT|LT|FT}[nn]#serial[#serial]...[/[name][.[account][.password]]] 
Parameters: 
MT   -   specifies that magnetic tape (either labeled, managed, or free) is 
being identified.  If the tape is labeled, a slash character must follow the 
final serial number in the fid, whether or not a file name is specified as 
part of the fid.  If the tape is free, a slash character cannot follow the 
final serial number and no name can be specified as part of the fid. 
LT   -   specifies that labeled tape is being identified.  The slash character 
must be present only if a file name is included as part of the fid. 
FT   -   specifies that a managed or free tape is being identified.  This form 
of the fid terminates with the last serial number; a slash is not permitted. 
The minimum size record that may be written to a managed or free tape is 4 
bytes. 
nn   -   is a two digit field indicating which of the tape resources (if the 
user has reserved more than one) is to be accessed.  This numbering is 
user-defined and not related to the system configuration.  If nn is omitted, 
the system allocates a default-type drive. 
serial   -   specifies a string of 1 to 6 characters that identify the tape 
volume.  At least one serial number must be specified as part of a tape fid. 
If multiple serial numbers are specified, the additional tape volumes are 
mounted when the storage of the initial tape is exceeded.  Each serial number 
must be preceded by a # character.  For input, the serial numbers must be 
specified in the order that the volume set was created. 
name   -   is a string of 1 to 31 characters that assigns an identifying name 
to a file.  The valid characters for this parameter are A through Z, a through 
z, the digits 0 through 9, and the $ _ :  and - characters.  For ANSI format 
tape file names, lowercase alphabetic characters are not allowed and, to 
conform to ANSI standards, the following rule must be observed:  a name must 
be composed of at most 17 characters from the center four columns of the code 
table specified in ANSI X3.4-1968 (except for position 5/15 and those 
positions where there is a provision for alternate graphic representation). 
If a name includes unusual characters such as the period, the name must be 
enclosed in quotes. 
account   -   is a string of 1 to 8 characters that identifies a file 
directory.  The valid characters for the account parameter are the same as 
those for the name parameter.  Accounts are created by the system manager.  If 
unspecified, the user's default file management account is assumed.  The 
default file management account is the log-on account unless the default is 
changed through the IBEX DIRECTORY command. 
password   -   is a string of 1 to 8 characters that provides a 
user-controlled security check for file access.  The password parameter can 
consist of any ASCII characters (including non-printing characters and control 
sequences).  Quotes must be used to enclose a password that contains 
non-printing or control sequence characters.  The user must include the 
password if the file is password protected.  Passwords only apply to CP-6 
labeled tapes. 
Examples: 
LT#PO/TAI 
means file TAI on labeled tape PO. 
LT#PO/TAI.CHI 
means file TAI, belonging to account CHI, on labeled tape PO. 
LT#PO/TAI.CHI.CHUAN 
means file TAI, sealed with password CHUAN, belonging to account CHI, on 
labeled tape PO. 
FT#WUSHU#KUNGFU 
means a two volume free tape with serial numbers WUSHU and KUNGFU 
MT01 
means the managed tape reserved as 01 by the user. 
00002
00001
Format: 
The device fid identifies unit record devices whether acquired as a resource 
or used as a logical device.  To simplify the discussion the device fid is 
described here in terms of its usage and is therefore presented in two 
formats: 
Format 1: 
dv[@[wsn]]   -   Used to identify a logical device.  The most common use of 
this format is simply dv where dv is a special name. 
Format 2: 
dvnn[#]   -   Used to identify a unit record device.  The device is either a 
logical or resource device, depending on whether it was defined with an LDEV 
or RESOURCE command. 
Parameters: 
dv   -   is a two-character device mnemonic.  All special names are valid 
mnemonics; however, only CP and LP can be used with nn. 
nn   -   is a two digit field.  The parameter is required only when referring 
to resource (reserved) devices or user-defined logical devices.  For resource 
devices, the field indicates which of the requested devices is to be accessed. 
For logical devices, the nn field is an integral part of the device fid.  The 
logical device fids LP01 and CP01 are system defined and may be referred to as 
LP and CP, respectively. 
#   -   need only be specified if dv is not one of the special names. 
Otherwise, dvnn is interpreted as a file name. 
@   -   specifies that the device is located at a particular workstation and 
that output is to be directed to it in a disk spooled manner. 
wsn   -   specifies a 1 to 8 character string designating the workstation 
location of the specified device. 
Examples: 
LP 
means logical device LP01, which is predefined to mean any line printer at the 
user's workstation. 
PR02# 
means printer device (installation-defined) number 02. 
CP@BULLDOG 
means the card punch device at workstation BULLDOG. 
LP@ 
means any line printer at the user's workstation. 
00002
00001
The owner of a file can assign a password to a file or change it.  If a 
password is assigned to a file, permission to open the file is denied any user 
(including the creating user) who cannot supply the correct password.  To 
further enhance security, the password is encoded by a non-reversible 
algorithm, and only the encoded version is stored with the file. 
If a password has been assigned to a file, a copy of that file will also have 
the same password assigned unless the PCL NFA output option is used. 
The CP-6 file type is a two-character file designator.  File types are 
automatically assigned by each CP-6 processor.  See PCL Input Options table 
under Type for processor-assigned file types and legal entries.  The user may 
modify file type by using the !SET command TYPE option, the PCL input TYPE 
option, the PCL output TYPE option, or the EDIT TYPE command.  File type may 
be used as selection criteria (for example, in copying or listing files). 
Syntax: 
!FIN 
Parameters: 
NONE 
Description: 
The !FIN control card specifies the end of card deck input and causes 
processing of input from the card reader to be terminated. 
Examples: 
!FIN 
means the end of the card deck has been reached. 
Related Commands: 
NONE 
00002
00003
00001
00004
Valid IBEX functions can be grouped into the following categories: 
Job Status Functions:     $CMDVAR_EXISTS, $FLAG, $RERUN, $PRIV_ACTIVE, 
                          $PRIV_AUTH 
Numeric Functions:        $ABS, $MAX, $MIN, $MOD, $REM 
Terminal Information 
Functions:                $TERM_FEP, $TERM_LINE, $TERM_SPEED, $TERM_PROFILE 
String Functions:         $INDEX, $LEN, $LOC, $SEARCH, $SUBSTR, $UPC, $VERIFY 
File Management 
Functions:                $ACCT, $DIR, $EOF, $FID_EXIST, $FID_TYPE, $HSET, 
                          $INPUT, $KEYIN, $NAME, $WOO 
File Information 
Functions:                $FID_ASN, $FID_GRANS, $FID_NGAVAL, $FID_ORG, 
                          $FID_RECS, $FID_UGRANS 
General Information 
Functions:                $DATE, $DAY, $LASTBATCH, $MODE, $SITE, $SWITCH, 
                          $SYSID, $TIME, $VERSION 
Type ?? for a complete list of IBEX functions and their descriptions, or type 
HELP FUNCTIONS function for a specific function. 
  Function             Meaning 
  $ABS(expression) 
             Returns the absolute value of the argument. 
  $ACCT 
             Returns the account portion of the current logon. 
  $CMDVAR_EXISTS(variable-name) 
             Returns 1 if the specified command variable exists; otherwise, 
             returns 0. 
  $DATE [(TY[PE]=type)] 
             Returns the date in the form YYMMDD.  TYPE=type is an optional 
             parameter, where type may be 'EXT',' ANS', or 'LOCAL' (enclosed 
             in single quotes). 
  $DAY [(TY[PE]=type)] 
             Returns SUN, MON, TUE, WED, THU, FRI, or SAT.  TYPE=type is an 
             optional parameter, where type may be 'EXT', 'ANS', or 'LOCAL' 
             (enclosed in single quotes). 
  $DIR 
             Returns the current directory account. 
  $EOF 
             Returns 1 if an end-of-file has been encountered on M$UC. 
             Returns 0 otherwise. 
  $FID_ASN(fid_string_expression) 
             Performs a call to M$FID, but does not try to OPEN the fid.  If 
             the M$FID call was successful, the assignment type (ASN) is 
             returned.  Examples are FILE, DEVICE, and COMGROUP. 
  $FID_EXIST(expression) 
             Returns a 0 if an attempt by IBEX to open the file yields 'file 
             does not exist'.  Any result other than 'file does not exist' 
             returns a 1.  A '1' is no guarantee that the user may access the 
             file. 
  $FID_GRANS(fid_string_expression) 
             Returns the size of the file in total number of granules. 
  $FID_NGAVAL(fid_string_expression) 
             Returns the size of the file in number of unused granules. 
  $FID_ORG(fid_string_expression) 
             Returns the file organization, e.g., CONSEC, KEYED, RANDOM, 
             INDEXED, RELATIVE, IDS, etc. 
  $FID_RECS(fid_string_expression) 
             Returns the size of the file in number of records. 
  $FID_UGRANS(fid_string_expression) 
             Returns the size of file in number of granules used. 
  $FID_TYPE(expression) 
             Returns the two-character file type of any disk fid represented 
             by expression. 
  $FLAG(fname) 
             Returns YES if a particular IBEX flag is set.  The fname may be 
             any of the following: 
             PROTECT 
             LIST 
             COMMENT 
             DRIBBLE 
             ECHO 
             NOTIFY 
  $HSET 
             Returns the home packset name. 
  $INDEX(expression1,expression2[expression3[,expression4]]) 
             Returns the index into expression1 where expression2 was found. 
             If expression2 is not found, the length of expression1 is 
             returned.  Expression3 and expression4 refer to expression1, and 
             are integers that respectively delimit the beginning and ending 
             characters for the indexing search according to a positional 
             count. 
  $INPUT(prompt_expression[,reply_expression[,reread_position]]) 
             Prompts through M$UC with prompt_expression.  Returns a reply 
             from the user, stripped of leading and trailing blanks.  If the 
             reply expression is given, it is put on the prompt line as the 
             default reply.  The reread_position specifies the starting cursor 
             position within the reply_expression; the default position is at 
             the end of the reply_expression. 
  $KEYIN(expression) 
             Sends expression to the system consoles.  Execution is suspended 
             until a reply is received from the system console.  $KEYIN then 
             takes on the value of the reply.  If the user's reply includes 
             leading or trailing blanks, these are stripped from the input. 
             When the user desires the blanks not be stripped, the input 
             string must be enclosed in quotes (which will be stripped). 
             Doubled quotes within a quote string are translated to a single 
             quote in the resultant string. 
  $LAST[BATCH] 
             Returns the sysid of the last job issued via the BATCH command. 
             Works only for the current session. 
  $LEN(expression) 
             Returns the number of characters in expression.  The length of a 
             string expression is one greater than the character index of the 
             last character position in that expression. 
  $LOC(string_expression) 
             Returns the string expression converted to lower case. 
  $MAX(arg1,arg2...) 
             Returns the value of the largest argument. 
  $MIN(arg1,arg2...) 
             Returns the value of the smallest argument. 
  $MOD(arg1,arg2) 
             Returns the arithmetic modulus of A and B. 
  $MODE 
             Returns ONLINE, BATCH, GHOST, or TP, whichever mode the user is 
             operating under. 
  $PRIV_ACTIVE(pname) 
             Returns YES if a particular PRIV bit is turned on. 
             pname may be: 
             AS[AVE] 
             CF[EP] 
             DI[SPJOB] 
             EXM[M] 
             EXP[M] 
             FMD[IAG] 
             FMR[EAD] 
             FMS[EC] 
             GP[P] 
             IOQ 
             IOQW 
             JI[T] 
             MA[XMEM] 
             MF[EP] 
             P[M] 
             SP[CLMN] 
             SYSC[ON] 
             SYSL[OG] 
             TN[D] 
  $PRIV_AUTH(pname) 
             Returns YES if a particular PRIV bit is authorized.  See 
             $PRIV_ACTIVE for pnames. 
  $NAME 
             Returns the name portion of the logon. 
  $REM(arg1,arg2) 
             Returns the remainder of A/B.  B may not be zero. 
  $RERUN 
             Returns YES if the job is being rerun. 
  $SEARCH(expression1,expression2[,expression3[,expression4]]) 
             Each character in expression1 is checked for membership in 
             expression2.  The index of the first match is returned; if not 
             found the length of expression 1 is returned.  Expression3 and 4 
             refer to expression1 and are integers that delimit the beginning 
             and ending characters for the search according to a positional 
             count. 
  $SITE 
             Returns the textual site identification. 
  $SUBSTR(expression1[,expression2[,expression3]]) 
             A character string is extracted from expression1 beginning at the 
             nth character as specified by expression2 with a length specified 
             by expression3.  If expression2 is not specified then the first 
             or zeroth character is assumed.  If expression3 is not specified 
             then the length of expression1 minus expression2 is assumed. 
  $SWITCH(expression) 
             Returns the switch values as defined in the SWITCH command.  The 
             expression must evaluate to a numeric value between 0 and 35. 
  $SYSID 
             Returns the user's sysid. 
  $TERM_PROFILE 
             Returns the current terminal profile.  (This function will return 
             an error if mode is not ONLINE.) 
  $TERM_FEP 
             Returns node of the user's FEP.  (This function will return an 
             error if mode is not ONLINE.) 
  $TERM_LINE 
             Returns the channel to which the user is connected.  (This 
             function will return an error if mode is not ONLINE.) 
  $TERM_SPEED 
             Returns the user's line speed, in bps.  (This function will 
             return an error if mode is not ONLINE.) 
  $TIME [(TY[PE]=type)] 
             Returns the current time in the form HHMM.  TYPE=type is an 
             optional parameter, where type may be 'EXT','ANS', or 'LOCAL' 
             (enclosed in single quotes). 
  $UPC(string_expression) 
             Returns the string expression converted to upper case. 
  $VERIFY(expression1,expression2[,expression3[,expression4]]) 
             Each character of expression1 is checked for membership in 
             expression2.  The index of the first non-match is returned; if 
             not found, the length of expression1 is returned.  Expression3 
             and 4 refer to expression 1 and are integers that delimit the 
             beginning and ending characters for the search according to a 
             positional count. 
  $VERSION 
             Returns the current version of the CP-6 system. 
  $WOO 
             Returns the current workstation of origin. 
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
00015
00014
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
00030
00028
00029
00031
00032
00033
00034
00035
00036
00037
00039
00040
00038
00041
00042
00043
00044
00045
00046
GO
Syntax: 
{GET|RESTORE} fid 
Parameters: 
fid   -   specifies the name of the file to be restored.  This file must be in 
the user's logon account. 
Description: 
GET (a synonym for RESTORE) recalls an interrupted activity that has been 
saved in mid-execution via the SAVE command.  After execution of this command, 
IBEX enters the double-bang (!!) mode.  The original run-unit file must exist 
for a saved image to be restored.  Refer to the description of 'XCON: SAVE 
Files/GET Process' in the Monitor Services Reference Manual (CE74) for more 
detail. 
Examples: 
!GET OLDSAVEDPROG 
!!GO 
Fetches the interrupted activity SAVEd in the file OLDSAVDPROG.  The GO 
command resumes the interrupted activity. 
Related Commands: 
SAVE, GO 
00002
00003
00001
00004
Syntax: 
GLOBAL  [{rep[,rep]...|DELETE[{field|'string'}[,{field|'string'}...]}] 
Parameters: 
rep   -   specifies a replacement specification in the format: 
{field1|'string1'}={field2|'string2'} 
See the REPLACEMENT component for a complete description. 
DELETE   -   removes a previous default replacement equation.  If DELETE is 
not followed by one or more fields or strings, all of the previously specified 
global replacements are cancelled. 
field|'string'   -   specifies the current replacement specification that is 
to be deleted.  (e.g., if "A='OX'", then "DELETE A" kills the replacement.) 
Description: 
GLOBAL specifies data replacement equations to be applied to records in 
command files.  The GLOBAL command may appear any number of times and anywhere 
within a command file or at the IBEX command level.  Data replacement 
initiated by a GLOBAL command is not overridden by data replacement 
specifications contained in any DEFAULT command.  Data substitutions defined 
through a GLOBAL command can be changed through a subsequent GLOBAL, BATCH, or 
XEQ command.  The user removes a global replacement by adding the keyword 
DELETE to the GLOBAL command.  GLOBAL without options will produce a display 
of the current GLOBAL data replacement specifications. 
Examples: 
!GLOBAL AND=OR,DO=FOR 
Causes the field OR to replace the field AND, and the field FOR to replace the 
field DO. 
!GLOBAL DELETE DO 
Terminates substitution of the field FOR for the field DO. 
Related Commands: 
DEFAULT 
00002
00003
00001
00004
Syntax: 
{G[O]|PROCEED|CONTINUE} 
Parameters: 
NONE 
Description: 
GO resumes an interrupted activity and terminates interrupt mode.  GO is only 
meaningful at the double-bang (!!) prompt. 
Examples: 
!!GO 
means resume the interrupted activity. 
Related Commands: 
QUIT 
00002
00003
00001
00004
Syntax: 
GOTO label 
Parameters: 
label   -   specifies the label (a 1 to 31 character alphanumeric name) 
assigned to an IBEX command present in the command file. 
Description: 
GOTO directs branching within a command stream.  The user can precede an IBEX 
command with a label in the format: 
!label: command 
Enter HELP CONCEPTS CONVENTIONS for restrictions in use of labels.  The value 
for label is a 1 to 31 character alphanumeric name.  Note that a blank must 
separate the colon from the command. 
Examples: 
!GOTO JAIL 
means branch to the command labeled JAIL. 
Related Commands: 
IF 
00002
00003
00001
00004
COMMAND_GROUPS
Syntax: 
HELP [(fid)] [TOPICS] [keyword1] [-] [keyword2] 
Note:  The following elements can be specified in any order: 
         fid 
         TOPICS 
         [keyword1] [-] [keyword2] 
For example, HELP (fid) keyword1 - keyword2 TOPICS is acceptable. 
Parameters: 
fid    specifies the processor name (for example, PCL).  If fid is omitted, 
the current processor is assumed.  The processor name can be ? to request a 
listing of processors that have HELP facilities available. 
TOPICS    requests a list of topic or subtopic names, rather than an 
information message. 
Form                                       Result 
----                                       ------ 
HELP (fid) TOPICS                          Lists all topics. 
HELP (fid) TOPICS keyword1 - keyword2      Lists all topics in the range 
                                           specified by keyword1 - keyword 2. 
HELP (fid) TOPICS keyword1?                Lists all topics beginning with 
                                           the prefix specified by keyword1. 
HELP (fid) TOPICS keyword1                 Lists all subtopics for the 
                                           topic specified by keyword1. 
keyword1 [- [keyword2]]    specifies a topic, a range of topics, or a topic 
and subtopic to identify what HELP information is requested. 
Form                                       Result 
----                                       ------ 
HELP (fid) keyword1                        Displays the first level 
                                           information message for 
                                           the topic keyword1. 
HELP (fid) keyword1 keyword2               Displays the information 
                                           message for keyword1, but 
                                           only the level identified 
                                           by the subtopic keyword2. 
HELP (fid) TOPICS keyword1 [-] [keyword2]  Lists topic or subtopic 
                                           names.  See TOPICS parameter. 
keyword1 and keyword2 may be abbreviated (by truncation).  keyword1 may 
include the wildcard (?) character as the rightmost character, if TOPICS is 
specified. 
Description: 
HELP displays information. 
HELP messages have levels.  Once the initial level has been displayed, 
entering a question mark displays the next level, usually containing greater 
detail.  Entering two question marks displays all the remaining levels. 
Any processor with a standard HELP file can be read from IBEX, but is 
available only to users with sufficient privilege to use the processor itself. 
The HELP command can be used either within the processor or in IBEX. 
The HELP can be issued at the double-bang (!!) without losing the suspended 
activity.  Thus, one may exit a processor (such as FORTRAN) with a <CNTL-Y>, 
query for HELP information, and then issue GO to return to FORTRAN. 
Examples: 
!HELP (IBEX) TOPICS 
means print the names of all the messages available for the IBEX processor. 
!HELP TOPICS 
means the same as the previous command (because the current processor is 
IBEX). 
!HELP (FORTRAN) TOPICS A - C 
means print the names of messages between A and C in the FORTRAN HELP file 
(HELP:FORTRAN:.:SYS). 
!HELP (FORTRAN) A - C 
means print the entire messages between A and C in the FORTRAN HELP file. 
!HELP (PCL) COPY 
means print the syntax of the PCL COPY command.  Typing question marks obtains 
deeper levels of information. 
!HELP (?.X) 
means print the names of all the programs that have HELP files in account X. 
!HELP ACCEPT SYNTAX 
means print the syntax of the ACCEPT command. 
!HELP LDEV PARAMETERS 
means print the command parameters for the LDEV command. 
!HELP HELP DESCRIPTION 
means print a description of the HELP command. 
!HELP LET EXAMPLES 
means print examples of the LET command. 
!HELP LIMIT RELATED 
means print a list of commands that are related to the LIMIT command. 
!? 
means print the next deeper level of the current message. 
!?? 
means print all further levels of the current message. 
HELP HELP_INDEX A prints a lists of terms, beginning with A.  HELP (?) prints 
a list of processors with HELP files.  HELP (?.X) prints a list of programs in 
account x that have HELP files.  HELP (PL6) TOPICS prints a list of available 
PL6 messages.  HELP (BASIC) GOTO prints the syntax of the GOTO statement. 
HELP (COBOL) TOPICS D - E prints available COBOL messages from D to E.  HELP 
(EDIT) COMMANDS prints a list of EDIT commands.  HELP (PCL) COPY - DELETE 
prints the messages for COPY, COPYALL, COPYSTD, 
                  and DELETE. 
Related Commands: 
NONE 
00002
00003
00001
00004
A 
  ACCEPT Command - 
      HELP ACCEPT 
  access vehicles -   
    IBEX - 
      HELP SET_OPS ACSVEH 
  ACQUIRE Command - 
      HELP ACQUIRE 
  ADJUST Command - 
      HELP ADJUST 
  Allocating Resources - 
      HELP COMMAND_GROUPS INTERRUPT 
  ALTKEY Command - 
      HELP ALTKEY 
  APL character sets - 
      HELP PROFILE RESET_PROFILE_CHAR 
  archiving (EFT) - 
      HELP COMMAND_GROUPS EFT 
  ASC Card - 
      HELP ASC_CARD 
  ATITLE Command - 
      HELP ATITLE 
  Autobaud - 
      HELP AUTOBAUD 
B 
  BACKUP Command - 
      HELP BACKUP 
  BATCH Command - 
      HELP BATCH 
  BATCH, PUNCHED DECKS - 
      HELP COMMAND_GROUPS MISC 
  BIN Card - 
      HELP BIN_CARD 
  BREAK Key Function - 
      HELP SPECIAL_KEYS BREAK 
  BYE Command - 
      HELP BYE 
C 
  CANCEL Command - 
      HELP CANCEL 
  CHARSETNAME - 
      HELP PROFILE RESET_PROFILE_CHAR 
  CHECK Command - 
      HELP CHECK 
  CHECK/NOTIFY Options - 
      HELP CHECK_OPS 
  CNTL-Y - 
      HELP COMMAND_GROUPS INTERRUPT 
      HELP SPECIAL_KEYS CNTL_Y 
  Comgroup Fids - 
      HELP FID_CG 
  command file processing - 
      HELP COMMAND_GROUPS COMMAND_FILE_PROCESSING 
  command files (nested) - 
      HELP CONVENTIONS 
      HELP COMMAND_GROUPS COMFILE 
  command labels (IBEX) - 
      HELP CONVENTIONS 
  command variable (IBEX) - 
      HELP PREPROCESSING 
      HELP PREPROCESSING 
      HELP PREPROCESSING PREPROCESSOR_SUBSTITUTION 
  COMMENT Command - 
      HELP COMMENT 
  comments (IBEX) - 
      HELP CONVENTIONS 
  Compiler Command - 
      HELP COMPILER 
  Compiler Options - 
      HELP COMPILER_OPS 
  concurrent output mode - 
      HELP LDEV_OPS CONCURR 
  CONTINUE Command - 
      HELP CONTINUE 
  control-Y - 
      HELP COMMAND_GROUPS INTERRUPT 
      HELP SPECIAL_KEYS CNTL_Y 
  CP-6 LOGON profile option - 
      HELP PROFILE 
  CP-6 Windowing - 
      HELP WINDOWS 
D 
  Data Control Blocks (DCBs) -   
    SET Command - 
      HELP SET PARAMETERS: 
  Data Replacement - 
      HELP COMMAND_GROUPS DATA_REPLACE 
  DATE Command - 
      HELP DATE 
  DCB default assignment and attributes - 
      HELP DCB_DEFAULTS 
  DCB Defaults - 
      HELP DCB_DEFAULTS 
  DCB names - 
      HELP DCB_DEFAULTS 
  DEFAULT Command - 
      HELP DEFAULT 
  DEFER option (JOB command) - 
      HELP JOB OPTIONS 
  DELTA Command - 
      HELP INVOKING_DELTA 
  Device Control - 
      HELP COMMAND_GROUPS FILCON 
  DIRECTORY Command -   
    IBEX - 
      HELP DIRECTORY SYNTAX: 
  DIRECTORY Command - 
      HELP DIRECTORY 
  Disk Fids - 
      HELP FID_DISK 
      HELP FID_DISK PARAMETERS: 
  DISPLAY Command - 
      HELP DISPLAY 
  DONT Command - 
      HELP DONT 
  DRIBBLE Command - 
      HELP DRIBBLE 
E 
  ECHO Command - 
      HELP ECHO 
  EDIT point - 
      HELP INPUT_EDITING POSITIONING 
  Effect of CP-6 Windows on TERMINAL Control - 
      HELP WINDOW_CONTROL 
  EFT -   
    FETCH Command - 
      HELP COMMAND_GROUPS EFT 
    STOW Command - 
      HELP COMMAND_GROUPS EFT 
    UNARCHIVE Command - 
      HELP COMMAND_GROUPS EFT 
    UNFETCH Command - 
      HELP COMMAND_GROUPS EFT 
    UNSTOW Command - 
      HELP COMMAND_GROUPS EFT 
  EJECT Command -   
    IBEX - 
      HELP EJECT SYNTAX: 
  EJECT Command - 
      HELP EJECT 
  END Command -   
    IBEX - 
      HELP END SYNTAX: 
  END Command - 
      HELP END 
  ENTER Command - 
      HELP ENTER 
  EOD Card - 
      HELP EOD_CARD 
  ERASE Command -   
    IBEX - 
      HELP ERASE SYNTAX: 
  ERASE Command - 
      HELP ERASE 
  Escape or CNTL-Y - 
      HELP SPECIAL_KEYS CNTL_Y 
  Escape Sequences - 
      HELP ESC 
  Execution Control - 
      HELP COMMAND_GROUPS COMPILATION 
  EXIT Command -   
    IBEX - 
      HELP EXIT SYNTAX: 
  EXIT Command - 
      HELP EXIT 
  EXPOUND Command - 
      HELP EXPOUND 
  EXPRESSION Component - 
      HELP EXPRESSION 
F 
  FEP User's Current Scheduler State - 
      HELP FEP_SCHED_STATES 
  FETCH Command (EFT) - 
      HELP COMMAND_GROUPS EFT 
  fid password - 
      HELP FID 
  fid password, disk - 
      HELP FID_DISK PARAMETERS: 
  fid password, tape - 
      HELP FID_TAPE PARAMETERS: 
  FID, TAPE - 
      HELP FID 
  FID, UNIT RECORD - 
      HELP FID_UR FORMAT: 
  Fids - 
      HELP FID 
  FIDS, TAPE - 
      HELP FID_DISK EXAMPLES: 
  file function, DCB - 
      HELP DCB_DEFAULTS 
  File Passwords - 
      HELP FILE_PASSWORD 
  File Types - 
      HELP FILE_TYPES 
  FIN Card - 
      HELP FIN_CARD 
  FOLLOW option (JOB command) - 
      HELP JOB OPTIONS 
  FUN option - 
      HELP DCB_DEFAULTS 
G 
  GET Command - 
      HELP GET 
  GLOBAL Command - 
      HELP GLOBAL 
  GO Command - 
      HELP GO 
  GOTO Command - 
      HELP GOTO 
H 
  HELP Command - 
      HELP HELP 
  HOLD Command - 
      HELP HOLD 
  Host User's Current Scheduler State - 
      HELP SCHED_STATES 
I 
  IBEX -   
    command conventions - 
      HELP CONVENTIONS 
    comments - 
      HELP CONVENTIONS 
    continued commands - 
      HELP CONVENTIONS 
    indented commands - 
      HELP CONVENTIONS 
    labels - 
      HELP CONVENTIONS 
  IBEX Command Groups - 
      HELP COMMAND_GROUPS 
  IBEX Commands - 
      HELP COMMANDS 
  IBEX Common Components - 
      HELP COMPONENTS 
  IBEX Conventions - 
      HELP CONVENTIONS 
  IBEX Functions - 
      HELP FUNCTIONS 
  IF Command -   
    IBEX - 
      HELP IF SYNTAX: 
  IF Command - 
      HELP IF 
  IMP and TERMINAL control - 
      HELP WINDOW_CONTROL 
  INCLUDE Command - 
      HELP INCLUDE 
  Input Editing - 
      HELP INPUT_EDITING 
  Insertion Mode - 
      HELP TERMINAL_OPS INSERTMODE 
  Insertion Window - 
      HELP TERMINAL_OPS INSERTMODE 
  IXTNSIZE - SET option - 
      HELP SET_OPS IXTNSIZE 
J 
  JOB Command - 
      HELP JOB 
  jobname - 
      HELP JOB OPTIONS 
L 
  labels (IBEX) - 
      HELP CONVENTIONS 
  LDEV Command - 
      HELP LDEV 
  LDEV Options - 
      HELP LDEV_OPS 
  LET Command - 
      HELP LET 
  LIMIT Command - 
      HELP LIMIT 
  LIST Command -   
    IBEX - 
      HELP LIST SYNTAX: 
  LIST Command - 
      HELP LIST 
  LOGON profile option - 
      HELP PROFILE 
M 
  MESSAGE Command - 
      HELP MESSAGE 
N 
  NCTL Card - 
      HELP NCTL_CARD 
  nested command files (IBEX) - 
      HELP CONVENTIONS 
      HELP COMMAND_GROUPS COMFILE 
  NOTIFY Command - 
      HELP NOTIFY 
O 
  OFF Command - 
      HELP OFF 
  ORESOURCE Command - 
      HELP ORESOURCE 
  OUTPUT Command - 
      HELP OUTPUT 
  output mode, concurrent - 
      HELP LDEV_OPS CONCURR 
P 
  PASSWORD Command - 
      HELP PASSWORD 
  password, disk fids - 
      HELP FID_DISK PARAMETERS: 
  password, fid - 
      HELP FID 
  password, tape fid - 
      HELP FID_TAPE PARAMETERS: 
  PLATEN Command - 
      HELP PLATEN 
  PMD Command - 
      HELP PMD 
  POINT Command - 
      HELP POINT 
  POSITION Command - 
      HELP POSITION 
  Preallocating File Space - 
      HELP PREALLOCATING_FILE_SPACE 
  Preprocessing of Commands - 
      HELP PREPROCESSING 
  PRINT Command -   
    IBEX - 
      HELP PRINT SYNTAX: 
  PRINT Command - 
      HELP PRINT 
  PRIORITY Command - 
      HELP PRIORITY 
  PRIV Command - 
      HELP PRIV 
  PROCEED Command - 
      HELP PROCEED 
  PROFILE Command -   
    character sets - 
      HELP PROFILE RESET_PROFILE_CHAR 
  PROFILE Command - 
      HELP PROFILE 
  profile option (LOGON) - 
      HELP PROFILE 
  PROTECT Command - 
      HELP PROTECT 
Q 
  QUIT Command -   
    IBEX - 
      HELP QUIT SYNTAX: 
  QUIT Command - 
      HELP QUIT 
R 
  RELEASE Command -   
    IBEX - 
      HELP RELEASE SYNTAX: 
  RELEASE Command - 
      HELP RELEASE 
  remote-node, disk fids - 
      HELP FID_DISK PARAMETERS: 
  rep equation (IBEX) - 
      HELP REPLACEMENT PARAMETERS: 
  REPLACEMENT Component - 
      HELP REPLACEMENT 
  REPORT Command - 
      HELP REPORT 
  RESET Command - 
      HELP RESET 
  RESOURCE Command - 
      HELP RESOURCE 
  RESOURCELIST Component - 
      HELP RESOURCELIST 
  RESTORE Command - 
      HELP RESTORE 
  RUM Command - 
      HELP RUM 
  Rununit Command - 
      HELP RUNUNIT_COMMAND 
S 
  SAVE Command - 
      HELP SAVE 
  Session-specific Parameters - 
      HELP WINDOW_CONTROL SESSION_SPECIFIC_PARAMETERS 
  SET Command - 
      HELP SET 
  SET Options - 
      HELP SET_OPS 
  SETUP Command - 
      HELP SETUP 
  Special Keys - 
      HELP SPECIAL_KEYS 
  special names (unit record) - 
      HELP UR_SPECIAL_NAMES 
  START Command - 
      HELP START 
  STATUS Command -   
    IBEX - 
      HELP STATUS SYNTAX: 
  STATUS Command - 
      HELP STATUS 
  STEPCC - 
      HELP EXPRESSION PARAMETERS: 
      HELP STEPCC 
      HELP JOB OPTIONS 
  STOP Command - 
      HELP STOP 
  STOW Command (EFT) - 
      HELP COMMAND_GROUPS EFT 
  Stream-specific Parameters - 
      HELP WINDOW_CONTROL STREAM_SPECIFIC_PARAMETERS 
  SWITCH Command - 
      HELP SWITCH 
T 
  TABS Command - 
      HELP TABS 
  Tape Fids - 
      HELP FID_TAPE 
  TERMINAL Command - 
      HELP TERMINAL 
  TERMINAL control and IMP - 
      HELP WINDOW_CONTROL 
  TERMINAL Options - 
      HELP TERMINAL_OPS 
  Terminal profile (PROFILE command) - 
      HELP PROFILE 
  TIME Command - 
      HELP TIME 
  TITLE Command - 
      HELP TITLE 
U 
  UNARCHIVE Command (EFT) - 
      HELP COMMAND_GROUPS EFT 
  UNDER Command - 
      HELP UNDER 
  UNFETCH Command (EFT) - 
      HELP COMMAND_GROUPS EFT 
  UNHOLD Command - 
      HELP UNHOLD 
  Unit Record Fids - 
      HELP FID_UR 
  Unit Record Special Names - 
      HELP UR_SPECIAL_NAMES 
  UNSTOW Command (EFT) - 
      HELP COMMAND_GROUPS EFT 
  update files - 
      HELP COMPILER_OPS SO 
  update files and INCLUDE command - 
      HELP INCLUDE DESCRIPTION: 
  upper level index - 
      HELP M$OPEN_AND_SET_OPTIONS 
  Using CP-6 Windows - 
      HELP USING_WINDOWS 
V 
  Vehicle (Processor) Permission - 
      HELP SET_OPS ACSVEH 
W 
  WHEN Command -   
    IBEX - 
      HELP WHEN SYNTAX: 
  WHEN Command - 
      HELP WHEN 
  Window-specific Parameters - 
      HELP WINDOW_CONTROL WINDOW_SPECIFIC_PARAMETERS 
  windows - 
      HELP WINDOWS 
      HELP USING_WINDOWS 
X 
  XEQ Command - 
      HELP XEQ 
  XEQ files - 
      HELP COMMAND_GROUPS COMFILE 
  XMIT Command - 
      HELP XMIT 
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
HELP_INDEX
Syntax: 
HOLD [{ALL|ldevlist}] 
Parameters: 
ALL   -   specifies to HOLD the accumulated outputs for all logical devices. 
ldevlist - specifies to HOLD the accumulated outputs for the specified logical 
device or devices.  The list is entered in the format 
    ldevname[,ldevname]... 
    ldevname is a logical device name established through the LDEV command. 
The default is LP01. 
Description: 
The HOLD command specifies that output is not to be sent to the destination 
device, but is to be held for later delivery (see the UNHOLD command).  For a 
stream, the only way to turn off HOLD is by using the LDEV command (!LDEV 
lname HOLD = NO). 
Related Commands: 
LDEV, UNHOLD 
Examples: 
HOLD LP99 
HOLD ALL 
HOLD LP05,LP09 
00002
00004
00001
00003
IBEX (Interactive and Batch EXecutive) is the primary command and control 
processor for the CP-6 system.  In general, IBEX controls the conditions under 
which a terminal session or a batch job takes place.  Through IBEX commands, 
the user controls resources, files, devices, comgroups, and terminals.  Often, 
IBEX commands are gathered into command files, which may include data 
replacement specifications and logical branching within command files. 
Through IBEX, the user submits source files for compilation, linking, and 
execution.  IBEX also supplies miscellaneous user functions, such as the 
printing of helpful information. 
The prompt for IBEX is the exclamation point or bang (!), which is usually 
issued after the user logs on to the CP-6 system.  IBEX also has a special 
prompt, the double-bang (!!) that is issued when an activity is interrupted. 
IBEX commands in XEQ or batch files must be preceded by a ! in column 1. 
Syntax: 
IF expression THEN command 
Parameters: 
expression   -   is a valid IBEX expression; the format is: 
[unary]{variable|'string'|integer|function|system_variable} 
    [operator expression] 
See EXPRESSION for a complete description.\ 
command   -   is any valid IBEX command. 
Description: 
The IF command allows the user to establish the conditions for affecting a 
change in the command stream flow (the IF clause) and to redirect the flow 
(the object clause).  The IF clause establishes a relational test which, if 
true, cause the IBEX command that follows it to be executed. 
Examples: 
!IF ERROR THEN QUIT 
If the preceding program terminated with a M$ERR, abort the remainder of the 
job. 
!IF A=B THEN GOTO ENDLBL 
If command variable A is equal to command variable B, skip to the command 
labeled ENDLBL. 
!IF OK THEN GOTO SAVIT 
If the preceding program terminated with a M$EXIT, skip to the command labeled 
SAVIT. 
!IF STEPCC>VAR THEN LET STEPCC=0 
If the value of STEPCC is greater than the value of the command variable VAR, 
set STEPCC=0. 
!IF $DAY='TUE' THEN XEQ FID 
This example shows the use of the function $DAY.  If today is Tuesday, then 
the file FID will be XEQed.  This would be useful for running jobs that need 
only run on specific days or dates. 
NOTE:  To repeat an IF statement at each JOBSTEP use the WHEN command. 
Related Commands: 
WHEN, LET, GOTO 
00002
00003
00001
00004
Syntax: 
INCLUDE fid 
Parameters: 
fid   -   designates the fid to be merged. 
Description: 
INCLUDE is actually a directive for BATCH, XEQ, or XMIT processing.  It causes 
a specified file to be merged into the command stream.  No data replacements 
are applied to this file.  Command variable expressions will not be evaluated 
at the time the INCLUDE command is processed.  The file specified may be an 
update file.  For information on update files, insert HELP (HOSTLIB) UPDATE 
and HELP (HOSTLIB) XUU UPDATE 
Type HELP GROUPS LOGIC for additional information. 
Example: 
!INCLUDE GORP 
means include file GORP in the current command stream. 
Related Commands: 
BATCH, XEQ, XMIT 
00002
00003
00001
00004
To obtain information about input editing, type: 
HELP INPUT_EDITING DESCRIPTION      General Description 
HELP INPUT_EDITING RETRIEVING       Recalling last typed input 
HELP INPUT_EDITING POSITIONING      Positioning the cursor 
HELP INPUT_EDITING REPLACING        Replacing characters 
HELP INPUT_EDITING INSERTING        Inserting characters (<ESC><J> 
HELP INPUT_EDITING INSERTION_MODE   Inserting characters (<ESC><'> 
HELP INPUT_EDITING OVERSTRIKE_MODE  Overstriking characters (<ESC><O> 
HELP INPUT_EDITING DELETING         Deleting characters 
HELP INPUT_EDITING INSERT_WINDOW    The area used for insertion. 
An input record is data typed at the terminal.  Input records are not sent to 
the host until terminated by an activation character.  A number of different 
characters can be used as activation characters, but for the purpose of this 
discussion, the carriage return key or the line feed key "activates" the input 
line, sending the data from the terminal to the host computer. 
With input editing the user can add, delete, or replace characters in a record 
before it is sent from the terminal.  Previously submitted input records can 
be retrieved, modified, and resubmitted. 
In addition, a set of escape sequences and special keyins help promote a 
flexible time-sharing environment. 
The last-issued input record (excluding the activation character) can be 
retrieved by typing the escape key and then D.  This deletes the current input 
record (if any) and retypes the last-issued input record (without its 
activation character).  The retyped input record can be altered using terminal 
editing and then resubmitted. 
Input editing is performed on the input record at the "edit point", the place 
where the cursor (or carriage) is positioned.  Generally this edit point is at 
the end of the input line, for example: 
!ABCDEFG <DEL> 
The delete key deletes the character G. 
During normal operation, the cursor (or carriage) can be repositioned within 
the input record.  Typing the backspace key moves the edit point one column to 
the left (on terminals without a backspace key, holding down the control key 
and pressing H will cause a backspace).  Holding down the control key and 
pressing R causes the edit point to move one column to the right; if this is 
done at the end of the input record, a blank space is generated.  Striking the 
escape key and then the carriage return moves the edit point to the beginning 
of the insertion window.  The tab key moves the edit point to the next tab 
stop to the right.  These edit positioning sequences are summarized below: 
SEQUENCE                MEANING 
--------                ------- 
<BS> or <CNTL-H>        Move left one column. 
<CNTL-R>                Move right one column. (ASCII DC2) 
<ESC> <RET>             Move to beginning of the insertion window. 
<TAB>                   Move right one tab stop. 
<ESC> <N>               Move to end of the insertion window. 
If the edit point is moved to the left, and new characters are typed, the new 
characters replace the old characters in that column (unless overstrike mode 
is set via <ESC> <O> or insertion mode is set via <ESC> <'>).  In the 
following examples, the subscripted arrow (^) indicates the carriage or cursor 
position. 
The user presses     Printed at       Displayed on CRT       Record actually 
keys:                terminal:        terminal:              contains: 
----------------     ----------       ----------------       --------------- 
<A> <X> <Y>            AXY                 AXY                   AXY 
                          ^                   ^ 
<ESC> <RET>            AXY                 AXY                   AXY 
                       ^                   ^ 
<CNTL-R>               AXY                 AXY                   AXY 
                        ^                   ^ 
<B> <C> <D>            AXY                 ABCD                  ABCD 
                        BCD                    ^ 
                           ^ 
To replace an entire input record, type the escape key and then strike the X 
key.  For example: 
The user presses     Printed at       Displayed on CRT       Record actually 
keys:                terminal:        terminal:              contains: 
----------------     ----------       ----------------       --------------- 
<A> <B> <C> <D>       ABCD                ABCD                   ABCD 
                          ^                   ^ 
<ESC> <X>             ABCD<X>_                                   (none) 
                      ^                   ^ 
<W> <X> <Y> <Z>       ABCD<X>_            WXYZ                   WXYZ 
                      WXYZ                    ^ 
                          ^ 
Typing the escape key and striking J toggles (activates or inactivates) the 
CP-6 insertion window.  For an activated insertion window on a CRT terminal, 
characters typed by the user that are at the right edge of the insertion 
window are inserted one column to the left of the cursor position.  For 
non-CRT terminals, the inserted characters will appear preceded by a backward 
slash.  For example: 
The user presses     Printed at       Displayed on CRT       Record actually 
keys:                terminal:        terminal:              contains: 
----------------     ----------       ----------------       --------------- 
<A> <D> <BS>           AD                AD                      AD 
                        ^                 ^ 
<ESC> <J>              AD                AD                      AD 
                        \                 ^ 
                         ^ 
<B> <C>                AD                ABCD                    ABCD 
                        \BC                 ^ 
                           ^ 
<ESC> <R>             AD                 ABCD                    ABCD 
                       \BC<R>               ^ 
                      ABCD 
                          ^ 
Note that the <ESC> <J> sequence prints (on a hard-copy terminal) as a 
downward carriage movement and a backward slash (\). 
When the insertion window has been activated, all characters typed at the 
right edge are inserted until one of the following characters or sequences is 
issued: 
<RET>      <ESC> <B>     <ESC> <R>     <ESC> <D>     <ESC> <CNTL-R> 
<LF>       <ESC> <J>     <ESC> <X>     <ESC> <Y> 
<TAB>*     <ESC> <F>     <ESC> <ESC>   <ESC> <I>* 
<CNTL-R>*  <ESC> <N>*    BREAK         <BS>* 
* Only if the user attempts to move the edit point out of the insertion 
window. 
The general rule is that the insertion window stays active until another <ESC> 
<J> or an attempt to move the edit point out of the insertion window. 
NOTE:  Insertion only takes place when the edit point is at the right end of 
the insertion window.  Backspacing or holding the control key and pressing R 
resets the insertion window if the editing point is moved out of the insertion 
window. 
The delete key removes characters within the insertion window from the input 
line.  If the cursor is positioned at the right end of the insertion window, 
characters at the end of the window are deleted.  (Although not shown in this 
example, note that in deletions on non-teletype hard-copy terminals, the slash 
will overstrike the deleted characters.) For example: 
The user presses    Printed at TTY      Displayed on CRT     Record actually 
keys:               terminal:           terminal:            contains: 
-----------------   -----------------   -----------------    ----------------- 
<A> <X> <Y> <B>        AXYB                 AXYB                 AXYB 
                           ^                    ^ 
<DEL>                  AXYB\                AXY                  AXY 
                            ^                  ^ 
<DEL>                  AXYB\\               AX                   AX 
                             ^                ^ 
If the cursor is positioned inside the insertion window, the delete key 
removes the character at which the cursor is positioned.  For example: 
The user presses    Printed at TTY      Displayed on CRT     Record actually 
keys:               terminal:           terminal:            contains: 
-----------------   -----------------   -----------------    ----------------- 
<A> <B> <Y> <BS> <BS>      ABY                 ABY                  ABY 
                            ^                   ^ 
<DEL>                      AB\Y                AY                   AY 
                             ^                  ^ 
If the insertion window is active, only characters in the insertion window are 
deleted.  For example: 
The user presses    Printed at TTY      Displayed on CRT     Record actually 
keys:               terminal:           terminal:            contains: 
-----------------   -----------------   -----------------    ----------------- 
<A> <C> <BS>               AC                  AC                   AC 
                            ^                   ^ 
<ESC> <J>                  AC                  AC                   AC 
                            \                   ^ 
                             ^ 
<B> <T>                    AC                  ABTC                 ABTC 
                            \BT                   ^ 
                               ^ 
<DEL>                      AC                  ABC                  ABC 
                            \BT\                 ^ 
                                ^ 
The insertion window represents by its left and right limits that portion of 
the input record currently being edited.  The default of the insertion window 
is the entire record.  The left limit of the insertion window is set by <ESC> 
<<>.  The right limit is set by <ESC> <>>.  <ESC> <J> sets or resets both 
limits of the insertion window.  The insertion window is reset only by <ESC> 
<R>, <ESC> <J>, <ESC> <CNTL-R>, activation or by positioning out of it with 
<BS>, <CNTL-R>, <TAB> or <ESC> <I>.  If the editing point is at the edge of 
the insertion window, the window is reset with <ESC> <CR> or <ESC> <N>. 
Use of the insertion window is not the same as use of the insertion mode, 
which is described under INSERTION_MODE. 
Insertion mode allows the insertion of new characters into the input record at 
any time, without having to type <ESC> <J>.  Insertion mode is entered by 
typing <ESC> <'>, and is exited by typing <ESC> <M>.  Alternately, the IBEX 
TERMINAL command may be used to enter or exit insertion mode: 
    !TERMINAL INSERT=YES    Enters insertion mode 
    !TERMINAL INSERT=NO     Exits insertion mode 
Insertion mode is only available on CRT terminals. <ESC> <'> and !TERMINAL 
INSERT=YES are ignored for hardcopy terminals. 
When insertion mode has been entered, all characters typed are inserted into 
the input record.  To replace characters in the input record, they must first 
be deleted, then the new characters are inserted.  For example: 
The user presses    Displayed on CRT     Record actually 
keys:               terminal:            contains: 
-----------------   -----------------    ----------------- 
<A><C><BS>                 AC                   AC 
                            ^ 
<V>                        AVC                  AVC 
                             ^ 
<BS>                       AVC                  AVC 
                            ^ 
<DEL>                      AC                   AC 
                            ^ 
<B>                        ABC                  ABC 
                             ^ 
In insertion mode, the action of the <DEL> key is modified:  the <DEL> key 
always deletes the character under the cursor.  When the cursor is at the end 
of the input record, pressing the <DEL> key has no effect. 
Overstrike mode allows more than one character to be assigned to a column. 
Overstrike mode is entered by typing <ESC> <O>, and is exited by typing <ESC> 
<M>. 
For example (some CRT screens do not permit the display of more than one 
character per column): 
The user presses    Printed at        Displayed on CRT     Record actually 
keys:               terminal:         terminal:            contains: 
-----------------   ---------------   -----------------    ----------------- 
<A><B><Q><ESC><O>        ABQ                ABQ                ABQ 
                            ^                  ^ 
<ESC> <RET>              ABQ                ABQ                ABQ 
                         ^                  ^ 
<_> <_> <_>              ABQ                                   A<BS>_B<BS>_ 
                            ^                  ^               Q<BS>_ 
<DEL>                    ABQ\                                  A<BS>_B<BS>_ 
                             ^                ^ 
<C><D>                   ABQ\CD               CD              A<BS>_B<BS>_CD 
                               ^                ^ 
<BS><BS><_><_>           ABQ\CD                               A<BS>_B<BS>_ 
                               ^                ^             C<BS>_D<BS>_ 
Note that the delete key deletes the entire column rather than just a single 
character. 
00006
00001
00005
00008
00007
00007
00009
00003
00004
00002
Syntax: 
DELTA 
Parameters: 
NONE 
Description: 
DELTA is invoked after execution of a run unit has been initiated through the 
DELTA command.  This command allows the interactive user to invoke DELTA after 
execution is interrupted, either via a <CNTL-Y> interactive interrupt or a 
program abort, or DELTA may be invoked as a stand alone desk calculator (i.e., 
performs various arithmetic and numeric conversion functions). 
Examples: 
!DELTA 
means associate the DELTA debugger. 
Related Commands: 
RUN, UNDER 
00002
00003
00001
00004
RUNUNIT_COMMAND
Syntax: 
JOB [account,user[,password]] [optionlist] 
Parameters: 
account   -   is an authorized account.  The account name consists of from one 
to eight characters. 
user   -   is a user name.  The user name consists of from one to twelve 
alphanumeric ASCII characters. 
password   -   is a user password consisting of from one to eight ASCII 
characters. 
Note:  the requirements for account, user and password in the JOB command 
syntax differ depending upon the conditions shown below: 
Condition                 Requirement 
---------                 ----------- 
User is operating from    Account, user, and password are 
user's own account.       not required entries. 
User is not operating     Account and user are required 
from own account, or      entries; password is also 
job is batched from       required if a password is 
a card reader.            associated with the specified 
                          account. 
optionlist   -   specifies one or more of the following options in the format 
option[,option]... 
    A[CCOUNT]   -   prevents other jobs which specify this account from 
    running concurrently with this job. 
    D[EFER] (hh:mm[,mm/dd/yy])   -   delays scheduling of the job for 
    execution until after the specified time (and date).  The default is the 
    current date.  See the ORDER option for the interaction between DEFER and 
    ORDER. 
    O[RDER]   -   specifies whether this job is to wait until all ordered jobs 
    previously submitted from the same account have run.  ORDER checks all 
    queues, including DEFER queues.  ORDER checks only other jobs which have 
    had ORDER specified. 
    F[OLLOW]{(jobidlist)}   -   bases the execution of a job, or series of 
    jobs, upon the acceptable completion of a previously submitted job. 
    FOLLOW without jobidlist allows a job to run only after all jobs from the 
    same account with earlier submission times have run. 
    FOLLOW with jobidlist specifies that if the specified job terminates 
    within the limits established by the termination condition (described 
    below), the job following it will be eligible for execution.  If the 
    leading job does not complete within the termination condition, the job(s) 
    following it are deleted. 
    The format of jobidlist is: 
    {jobname|sysid}[output-file-spec][(termcondition)][,({jobname|sysid} 
        [output-file-spec][(termcondition)]... 
        jobname   -   is the name assigned to a previously submitted batch job 
        as specified on the NAME option of the JOB command. 
        sysid   -   is the job sysid assigned by the system. 
        output-file-spec   -   takes one of the following forms: 
            -1 or (1)   -   allows the specification of one subfile. 
            (1[2,...])   -   allows the specification of a list of subfiles. 
        Note: Since JOB allows a jobname of just digits, whenever a sysid or a 
        jobname is allowed, if IBEX encounters a 6 or less digits number it 
        treats this as a sysid.  Anything of greater length is treated as a 
        jobname.  If a jobname exists that can be treated as a sysid, the user 
        must put the jobname inside single quotes to indicate to IBEX that 
        this is a jobname.  Some examples are 'jobname'-1, '1234'-1, 
        '1234'(1), and 'jobname'(1). 
        termcondition is: 
        {STEPCC relation value}{ERROR|OK|ABORT} 
            STEPCC   -   is a system defined command variable.  STEPCC = 0 is 
            the default termination condition. 
            relation   -   specifies one of the following logical relations: 
                Logical 
                Relation                Meaning 
                --------                ------- 
                {=|.EQ.}                Equal to. 
                {>=|.GE.}               Greater than or equal to. 
                {<=|.LE.}               Less than or equal to. 
                {>|.GT.}                Greater than. 
                {<|.LT.}                Less than. 
                {~=|.NE.}               Not equal to. 
            value   -   specifies a numeric value from 0 through 511. 
            ERROR   -   means follow if the job(s) errored. 
            OK   -   means follow if the job(s) ran correctly. 
            ABORT   -   means follow if the job(s) aborted. 
            If no termcondition is specified, the termination conditions for 
            the leading job will be assumed to be STEPCC=0. 
    NA[ME]=jobname   -   specifies that this job is to have a symbolic name 
    specified by jobname.  Jobname may be from one to thirty-one characters 
    from the following set: 
        A-Z, a-z, 0-9 : $ _ 
    The jobname is used on the CHECK command to obtain job status information, 
    and on the CANCEL command for cancelling a job deleting output.  Jobname 
    is also used in the FOLLOW option. 
    {R[ERUN]|NR[ERUN]}   -   requests whether the job is to be reinitiated 
    automatically if the system should crash during its execution.  The 
    default is RERUN. 
    SCA[N]   -   checks the job command stream for IBEX command syntax errors 
    prior to queuing the job for scheduling.  If any errors are found, 
    appropriate diagnostics are written to the current output destination and 
    the job is not queued.  If no syntax errors are found, the job is 
    submitted to the batch queue. 
    PRIO=n   -   specifies the priority of a job as follows: 
        0       Hold in the job queue until the priority is changed by a 
        PRIORITY operator key-in. 
        1-15    Schedule at the specified priority:  1 is the lowest priority; 
        15 is the highest.  The default priority for a job, and the maximum 
        priority which may be specified, depend on intallation-defined values 
        for each user. 
    W[SN]=workstationname   -   specifies the output destination for a remote 
    batch job.  The default is the workstation of origin. 
Description: 
JOB defines the beginning of a batch job.  It must be the first command in 
each job command stream (with the exception of the DEFAULT or INCLUDE 
commands).  If in a card deck, JOB defines a new job and forces reading of 
subsequent commands in ASCII input mode.  The ACCOUNT, DEFER, ORDER, and 
FOLLOW options allow the user to set the priority for multiple jobs. 
The JOB command FOLLOW option provides two different ways of testing the 
termination status of a job:  1) by the STEPCC value at the end of the last 
job step (i.e., STEPCC=6), and 2) by the job's run status (OK|ERROR|ABORT). 
Note that these two tests are mutually exclusive, i.e., the user can specify 
STEPCC=6, or ABORT, but cannot specify STEPCC = ABORT. 
Examples: 
!JOB MYACCT,JOHN,PASSWORD ORDER,NRERUN 
Defines a batch job from account MYACCT, user-name JOHN and with password 
PASSWORD.  Also indicates that this job is to be scheduled in the order 
submitted among other jobs in this account, and that the job is not to be 
reinitiated automatically if the system should crash. 
!JOB MISACCT,GENERAL 
Defines a batch job from account MISCACCT with user name GENERAL. 
!JOB MASTACCT,WALTON PRIO=10,SCAN,FOLLOW(FIRSTJOB(STEPCC>0),SECONDJOB,123; 
(STEPCC=2)),NAME=SYSTOTS 
Defines a batch job from account MASTACCT with user-name WALTON.  The job will 
have a priority of 10, a name of SYSTOTS, and all commands in the command 
stream will be syntax checked before the job is submitted to the batch queue. 
Also, the job will be executed only if the jobs named FIRSTJOB,SECONDJOB, and 
sysid 123 complete as specified in the FOLLOW option. 
!JOB MYACCT,LOIS,PASSWORD DEFER (17:00) 
!JOB MYACCT,HELEN,PASSWORD FOLLOW 
The first command defines a batch job from account MYACCT, user-name LOIS with 
password PASSWORD to be deferred until 17:00.  The second command defines a 
batch job from account MYACCT, user-name HELEN, which will not run until all 
jobs from MYACCT, including the deferred job, have run. 
Related Commands: 
RESOURCE, LIMIT, ASC, NCTL 
00002
00003
00001
00004
JOB
Syntax: 
L [(listopt)][sourcelist{TO|ON|OVER|INTO}[destination] [FROM fid] 
Parameters: 
listopt   -   specifies either an A, C, CRIT, ORG, DATE, EA, FA, or TY 
listing format input option.  The default is A.  See HELP (PCL) INOPS. 
sourcelist   -   specifies a list of disk or labeled tape fid with options. 
The only valid options are A, EA, C, CRIT, DATE, FA, FSN, OR, PHYS, TY, and 
VOL.  If a source has an A, EA, C, or FA input option, the request overrides 
the default listing format.  If an account is specified, it should be one to 
which the user has authorized access.  If unspecified, the user's directory 
account is assumed as a default source.  The basic format of the source 
component is: 
fid[(option[,option]...)] 
TO   -   specifies file creation. 
ON   -   specifies file creation. 
OVER   -   specifies file replacement. 
INTO   -   specifies file extension. 
destination   -   specifies the output for the listing operation.  This may be 
either a file, or a device stream.  The default is ME, which indicates the 
user's terminal (on-line) or the line printer (batch).  The CR, FA, LC, NCR, 
NFA, O, TX, VC, VF, X, FV, NV, and X1 are invalid PCL output options for this 
command. 
FROM fid   -   specifies a default fid whose elements are used when PCL parses 
the source components. 
The default list option for single file specifications is A; for multiple 
specifications, the default is C=12. 
Description: 
LIST prints a summary of disk and labeled tape storage.  The A option 
causes files to be listed with file organization, the file type, the 
number of granules, the NGAV rating, the number of records, the date 
the file was last modified, and the file name.  The EA option adds 
additional file management information.  The FA option includes the EA 
and also provides key, KEYL, and alternate key information for 
indexed files. 
Examples: 
!L(A) 
means list the files in the account with attributes. 
!L AGRIPPA 
means list the file AGRIPPA, with attributes. 
!L ?FIG.MYACCT 
means list the filenames of all files ending with FIG in account MYACCT. 
Related Commands: 
See the PCL Help Facility 
00002
00003
00001
00004
Syntax: 
LDEV lname [fid][,optionlist] 
Parameters: 
lname   -   is a user-assigned logical device name, such as LP02 or CP01. 
Logical device names must be four characters long, with the last two 
characters digits.  Also accepted are LP, CP, UC, and ALL.  LP means LP01, CP 
means CP01, and UC means user console for online use only.  ALL means all 
defined logical devices. 
If lname is UC, only the following options may be used:  FORM, HDRHEIGHT, 
MARGIN, PAGECOLUMN, TAB, TITLE, REMOVE, or window options (BTMBRDR, FWINDOW, 
HBRDRCHR, HBRDRSIZ, LFTBRDR, LOGON, MINLENGTH, MINWIDTH, OPTIONAL, POSITION, 
RHTBRDR, TOPBRDR, VBRDRCHR, VBRDRSIZ, WLENGTH, and WWIDTH). 
fid   -   specifies a device fid in the format: 
    dv[@[wsn]] 
      or 
    UCmm 
    where 
    dv   -   specifies a two-character device type. 
    @   -   specifies that dv denotes a device name, not a file name, and is 
    required if wsn is specified.  If the wsn parameter is omitted, the user's 
    workstation of origin is assumed. 
    wsn   -   specifies a 1 to 8 character string designating the workstation 
    location of the specified device. 
    UCmm   -   specifies the name of a logical device into whose window 
    "lname" is to be directed. 
optionlist   -   specifies format attribute options to be applied when an 
attempt is made to output to the specified device.  Valid options are: 
BT[MBRDR]{[=YES]|=NO} 
CONC[URR]{[=YES]|=NO} 
CON[TINUE]{[=YES]|=NO} 
COP[IES]=value 
DV[FC]={'value'|O'value'} 
E[RASE]{[=YES]|=NO} 
FO[RM]=[']formname['] 
FW[INDOW]=name 
HBRDRC[HR]=c 
HBRDRS[IZ]=value 
HD[RHEIGHT]=value 
HE[ADER]=NO 
HOLD {[=YES]|=NO} 
HOLDCOPIES = value 
IN[DENT]=value 
LFT[BRDR]{[=YES]|=NO} 
LI[NES]=value 
LOGON 
MAR[GIN]=value 
MINL[ENGTH]=value 
MINW[IDTH]=value 
OPT[IONAL]{[=YES]|=NO} 
PO[SITION]= option 
P[AGECOLUMN]=value 
REM[OVE]{[=YES]|=NO} 
RES[ET]=YES 
RH[TBRDR]{[=YES]|=NO} 
SC[RUB]{[=YES]|=NO} 
SEQ{[=YES]|=NO} 
SEQC[OL]=value 
SEQI[D]='string' 
TA[B]={NO|tablist} 
TI[TLE]='string' 
TO[PBRDR]{[=YES]|=NO} 
VBRDRC[HR]=c 
VBRDRS[IZ]= value 
W[IDTH]=value 
WL[ENGTH]=value 
WW[IDTH]=value 
See LDEV_OPS. 
Description: 
LDEV defines logical devices and defines and modifies logical device 
attributes.  The LDEV command is used when the Logical Device Special Names 
and/or their default attributes cannot be used.  Typical uses of the LDEV 
command are to: 
o   Modify logical device attributes (e.g., the workstation, the device type 
    and/or format attributes). 
o   Define new logical devices including format attributes. 
o   Control timing of transmission of output for a logical device. 
o   Delete accumulated output for a logical device. 
o   Create multiple symbiont files within one job for different device types 
    or for the same device type. 
o   Set or modify window parameters. 
Examples: 
!LDEV LP01 LP@NORDOR,COPIES=7 
means, when LP or LP01 (which are synonymous) is used as an output device, the 
system should send that output to the line printer at workstation NORDOR, and 
generate seven copies. 
!LDEV CP01 CP@NUMENOR 
means direct card punch output (CP) to the card punch at workstation NUMENOR. 
!LDEV LP02 LP@LORIEN,TITLE='Lore' 
means direct line printer (LP02) to the lineprinter at workstation LORIEN. 
The title "Lore" will be attached to the output. 
Related Commands: 
PRINT, ERASE 
00002
00003
00001
00004
The options for the LDEV command are: 
BTMBRDR        HDREHEIGHT     OPTIONAL       TAB 
CONCURR        HEADER         PAGECOLUMN     TITLE 
CONTINUE       HOLDCOPIES     POSITION       TOPBRDR 
COPIES         INDENT         REMOVE         VBRDRCHR 
DVFC           LFTBRDR        RESET          VBRDRSIZ 
ERASE          LINES          RHTBRDR        WIDTH 
FORM           LOGON          SCRUB          WLENGTH 
FWINDOW        MARGIN         SEQ            WWIDTH 
HBRDRCHR       MINLENGTH      SEQCOL 
HBRDRSIZ       MINWIDTH       SEQUID 
Type HELP (IBEX) LDEV_OPS option 
  Opt        Meaning 
  BT[MBRDR]{[=YES]|=NO} 
        Specifies whether space is to be reserved at the bottom to separate 
        this window from the one below it.  The default is NO for a new 
        window, or causes this parameter to be ignored. 
  CONC[URR]{[=YES]|=NO} 
        YES specifies concurrent output mode, which means that output to the 
        logical device may start being transmitted concurrently with creation 
        of later output.  This option is of limited use, since the physical 
        device to which the output is directed must stand idle when it has 
        caught up to program output creation.  In specific cases with 
        semi-dedicated devices, however, it may decrease the elapsed data 
        processing time by overlapping physical output with internal computing 
        time.  (See CE34, Operations Reference, for more information 
        concerning concurrent output mode.) 
  CON[TINUE]{[=YES]|=NO} 
        Requests that the output stream to the logical device not be 
        terminated.  Used to specify new formatting attributes (e.g., TAB, 
        TITLE, LINES, MARGIN, PAGECOLUMN, SEQ, INDENT) without terminating the 
        output stream. 
        YES   -   specifies that the output stream is not to be terminated. 
        If CONTINUE=YES, FORM cannot be changed, and fid cannot be specified. 
        NO   -   specifies that the output stream to the logical device is to 
        be terminated and a new output stream started.  The existing output 
        stream is queued for output to its destination.  This is the default. 
  COP[IES]=value 
        Specifies the number of times that the output is to be transmitted to 
        the destination device. 
        value   -   is a decimal number from 1 to 511.  If CONTINUE=NO, the 
        number of copies pertains to subsequent output to the logical device 
        rather than to the current output stream.  Default is 1. 
  DV[FC]={'value'|O'value'} 
        Specifies the default vertical format control character for records 
        with no vertical format control. 
        value   -   specifies one of the vertical format control characters. 
        O'value'   -   specifies the DVFC character in octal. 
  E[RASE]{[=YES]|=NO} 
        Requests that the current accumulated output for the logical device is 
        deleted. 
        YES   -   requests that the accumulated output be deleted.  Meaningful 
        only when used with CONTINUE=NO. 
        NO   -   is the default. 
  FO[RM]=[']formname['] 
        Specifies the name of the form to be mounted on a unit record device. 
        formname   -   is an optionally quoted 1 to 6 character string.  The 
        name must have been defined to the system by the System Manager (via 
        the Form Definition File).  The default is blank which means standard 
        forms for the specified destination device. 
  FW[INDOW]=name 
        Specifies the four-character name of a stream in an adjacent window 
        that is to supply or receive any space indicated by the WWIDTH or 
        WLENGTH options. 
        name   -   is of the form 'UCnn' 
  HBRDRC[HR]=c 
        Specifies the single ASCII character to be used to mark the horizontal 
        border space(s).  It will fill every character position of the 
        farthest line of the border space.  The default causes this parameter 
        to be ignored. 
        c   -   is a single ASCII character. 
  HBRDRS[IZ]=value 
        Specifies the size in lines of the horizontal border space(s) (TOPBRDR 
        and BTMBRDR).  The default is zero, which causes this parameter to be 
        ignored.  Note that the border presence parameters must be used to 
        remove a border - HBRDRSIZ=0 won't work. 
        value   -   is a decimal integer from 0 to 15. 
  HD[RHEIGHT]=value 
        Specifies the height of the page header area. 
        value   -   is a decimal number from 0 to 15 that specifies the number 
        of lines (including the title line) in the header.  The default, 1, 
        specifies that no blank lines are to follow the title line. 
  HE[ADER]=NO 
        Specifies that no header is to be placed on pages of output.  Used to 
        remove the effect of a previous TITLE/HDRHEIGHT/INDENT/PAGECOLUMN 
        specification. 
  HOLD {[=YES]|=NO} 
        HOLD=YES specifies that output is not to be sent to the destination 
        device, but is to be held for later delivery (see the UNHOLD command.) 
        Multi-copy output may be held after zero or more copies have been 
        made; see the HOLDCOPIES option. 
  HOLDCOPIES = value 
        Specifies, when HOLD=YES, that this number of copies of the output are 
        to be transmitted to the destination device, and then any other 
        untransmitted copies are to be held for later delivery.  This option 
        might be useful if, for example, several copies of a report are to be 
        created but the user wishes to check one copy for accuracy before 
        printing the rest (HOLD=YES, HOLDCOPIES=1, COPIES=n).  The default 
        value of HOLDCOPIES is 0. 
        value    is a decimal value from 0 to 511. 
  IN[DENT]=value 
        Specifies the starting column for TITLE line text. 
        value   -   is a decimal number from 1 to 255 that indicates the 
        starting column relative to the leftmost column position.  The default 
        is column 1. 
  LFT[BRDR]{[=YES]|=NO} 
        Specifies whether space is to be reserved at the left to separate this 
        window from the one to the left.  The default is NO for a new window. 
  LI[NES]=value 
        Specifies the number of printable lines on a logical page of output. 
        value   -   is a decimal number from 1 to 32000 that specifies the 
        number of printable lines on a page.  If not specified, the default is 
        the number of lines contained in the FORM definition established by 
        the system manager.  The LINES on an LDEV do not override the FORM 
        definition. 
  LOGON 
        LOGON is meaningful when fid is UCnn.  LOGON causes the specified UCnn 
        to be disconnected from the current session and reconnected to CP-6 in 
        the logon state.  Once a session is created, its number does not 
        change.  A new session is allocated the lowest unused number. 
  MAR[GIN]=value 
        Specifies the lefthand margin for a logical page of output. 
        value   -   is a decimal number from 1 to 255 that specifies the 
        starting column.  (The value 1 specifies no indentation.)  The default 
        is no indentation. 
  MINL[ENGTH]=value 
        Specifies the minimum length for this window in lines.  The default is 
        255, which causes this parameter to be ignored unless this is a new 
        window, in which case it means the the length is to be fixed.  See 
        OPTIONAL also. 
        value   -   is a decimal integer from 0 to 254. 
  MINW[IDTH]=value 
        Specifies the minimum width for this window in columns.  The default 
        is 255, which causes this parameter to be ignored unless this is a new 
        window, in which case it means the the width is to be fixed.  See 
        OPTIONAL also. 
        value   -   is a decimal integer from 0 to 254. 
  OPT[IONAL]{[=YES]|=NO} 
        Specifies whether the window size is permitted to drop below MINWIDTH 
        or MINLENGTH.  If so, the window will be removed from the screen when 
        it is too small, but its context will be maintained.  The default is 
        NO for a new window. 
  PO[SITION]= option 
        Specifies the portion of FWINDOW that this (new) window is to occupy. 
        The options are TOP, BOTTOM, LEFT, and RIGHT.  This parameter is 
        ignored if the window already exists. 
  P[AGECOLUMN]=value 
        Requests that page numbering be included in the title line of the 
        header of each logical page of output, and specifies the starting 
        position of the page number. 
        value   -   is a decimal number that specifies the starting column of 
        the lefthand digit of the number.  The default is zero (which 
        specifies no page numbering). 
  REM[OVE]{[=YES]|=NO} 
        Cancels the logical device definition.  No new output can be written 
        to the logical device; any DCB open to the logical device is closed 
        automatically. 
        YES   -   cancels the logical device definition.  If specified and 
        other parameters to modify format are also specified, the other 
        parameters are ignored. 
        NO   -   is the default. 
  RES[ET]=YES 
        Reinitializes page numbering in the title line of logical page.  The 
        next page will be numbered 1. 
  RH[TBRDR]{[=YES]|=NO} 
        Specifies whether space is to be reserved at the right to separate 
        this window from the one to the right.  The default is NO for a new 
        window. 
  SC[RUB]{[=YES]|=NO} 
        Specifies that any previously defined attributes for the logical 
        device are to be removed.  Fid information returns to default values 
        unless specified. 
        YES   -   requests that the logical device be scrubbed.  If fid values 
        for dv and wsn are not specified in the command: 
        dv defaults to the first two characters in ldevname (i.e., the first 
        two characters must equal a device type). 
        wsn defaults to the user's workstation of origin. 
        Further, if FORM is not specified, it will default to the default form 
        defined by the system manager (in the workstation definition file for 
        this device type at the user's workstation of origin). 
        NO   -   is the default. 
  SEQ{[=YES]|=NO} 
        Specifies that sequencing is to occur on each output record. 
        (Normally used with punched card output). 
        YES   -   specifies that record sequencing is to be performed for 
        output to the logical device according to the SEQCOL and SEQID 
        parameters. 
        NO   -   specifies that record sequencing is not to be performed. 
        Normally used to discontinue record sequencing.  NO is the default. 
  SEQC[OL]=value 
        Specifies in which column sequencing of output records is to begin. 
        value   -   is a decimal number from 1 to 255 that specifies the 
        column number in which sequencing is to begin.  The sequence ID is 
        printed followed by the record sequence number.  The default is 73. 
  SEQI[D]='string' 
        Specifies that a four-character sequence identification is to be 
        appended to each output record when sequencing is requested. 
        string   -   is a four-character sequence identification.  The default 
        is blanks. 
  TA[B]={NO|tablist} 
        Controls horizontal tabulation. 
        NO   -   erase previously established tabs. 
        tablist   -   is 1 to 31 decimal numbers from 0 to 255 that specify 
        Horizontal Tab columns (HTs).  An HT character in output is replaced 
        by blanks up to the next tab column.  The tab specifications must be 
        in ascending numeric order and members of the list are separated by 
        commas.  The default is no tabulation (HT characters are replaced with 
        a single blank). 
        If MARGIN is also specified, tabulation is displaced such that the 
        MARGIN column on the output medium is TABS column 1. 
  TI[TLE]='string' 
        Specifies the text which is to be printed as a title on the top of 
        every page of output. 
        string   -   contains 1 to 144 characters of title text. 
  TO[PBRDR]{[=YES]|=NO} 
        Specifies whether space is to be reserved at the top to separate this 
        window from the one above it.  The default is NO for a new window. 
  VBRDRC[HR]=c 
        Specifies the single ASCII character to be used to mark the vertical 
        border space(s).  It will fill every character position of the 
        farthest column of the border space.  The default causes this 
        parameter to be ignored. 
        c   -   is a single ASCII character. 
  VBRDRS[IZ]= value 
        Specifies the size in columns of the vertical border space(s) (LFTBRDR 
        and RHTBRDR).  The default is zero, which causes this parameter to be 
        ignored.  Note that the border presence parameters must be used to 
        remove a border - HVBRDRSIZ=0 won't work. 
        value   -   is a decimal integer from 0 to 15. 
  W[IDTH]=value 
        Specifies the maximum width of lines. 
        value   -   is a decimal number from 1 to 255. 
  WL[ENGTH]=value 
        Specifies the size of the window, in absolute or incremental lines or 
        as a percentage of the full screen (or of the current size for an 
        existing window).  This option is ignored for a new window if 
        POSITION=LEFT or RIGHT.  The default is +0, which doesn't change an 
        existing window, but is specially interpreted for a new one as 99% 
  WW[IDTH]=value 
        Specifies the size of the window, in absolute or incremental columns 
        or as a percentage of the full screen (or of the current size for an 
        existing window).  This option is ignored for a new window if 
        POSITION=TOP or BOTTOM.  The default is +0, which doesn't change an 
        existing window, but is specially interpreted for a new one as 50%. 
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
00010
00011
00012
00014
00013
00015
00016
00017
00018
00019
00020
00021
00022
00024
00023
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
LDEV_OPS
Syntax: 
Form 1: 
LET [variable=expression][,variable=expression]...[variable=expression] 
    or 
LET DELETE [variable [,variable]...[variable]] 
Form 2: 
LET BANNER[TEXT][n] = expression (option) 
Form 3: 
LET BANNER[TEXT] RESET 
Parameters: 
variable   -   is a user defined variable or the system variable STEPCC. 
User-defined variables may be 1 to 31 characters and must begin with an 
alphabetic character.  Valid character set is: 
A-Z 
a-z 
0-9 
$_#@ 
expression   -   is a valid IBEX expression.  The format is: 
[unary]{variable|'string'|integer|function|system-variable} 
    [operator expression] 
See EXPRESSION for a complete description.\ 
n   -   is the line number (1-9) of the banner text.  Line number 0 
(registered name of the user) may not be changed by the user. 
option   -   may be any of the following: 
    PERM   -   sets the inserted textfield permanently in :USERS. 
    SESSION   -   sets the inserted textfield temporarily for the user's 
    session only. 
RESET  -   resets the 'session' textfield to the 'permanent' textfield. 
Description: 
Form 1 of the LET command assigns values to variables.  All values are stored 
as strings.  LET DELETE removes variable assignments; if no variables are 
specified, all variables are assumed. 
LET without any parameters displays the current variable assignments. 
Form 2 of the LET command allows the user to set or reset lines 1 through 9 of 
the banner text.  The PERM option sets the text permanently; the SESSION 
option sets the text for only that session. 
Form 3 of the LET command resets the session banner text to the permanent 
banner text. 
The DISPLAY command may be used to display the banner text. 
Examples: 
!LET STEPCC=A 
Set STEPCC equal to the value of the command variable A. 
!LET C=3 
Set command variable C equal 3. 
!LET X=STEPCC 
Set command variable X equal to the current contents of STEPCC. 
!LET A='123' 
!LET B=100 
!LET C=A+B 
All values are stored as strings.  Thus 123 is the same as '123'.  The final 
value of C is '223'. 
!LET A='123' 
!LET B=A || ' is a string. ' 
This example illustrates the use of concatenation.  The value of B is '123 is 
a string.'. 
!LET A=1 
!LET B=2 
!LET C=A&B 
This example shows the use of a TRUTH VALUE operator.  Any NUMERIC values may 
be operated on by AND, OR and NOT.  A numeric value is considered TRUE if 
greater than zero, and FALSE if zero or negative.  Thus in this example both A 
and B are considered TRUE and therefore the value of C is 1 (true). 
!LET CMD='DI' 
!%CMD 
In this example, the variable CMD is given a value of 'DI'.  Then the value of 
CMD is evaluated and put back into the second command and processed.  The 
result would be that a DISPLAY command would be executed. 
!LET FID='XYZ' 
!PL6 %FID OVER %(FID||':OU') 
This example is a bit more useful.  The result would be that PL6 would compile 
XYZ and create an object unit in XYZ:OU. 
Examples of Form 2: 
!LET BANNERTEXT3='Horatio Albatross' (PERM) 
!LET BANNERTEXT4='5250 West Century Blvd.' (PERM) 
!LET BANNERTEXT5='Los Angeles, Ca.' (PERM) 
!LET BANNERTEXT6='90045' (PERM) 
sets lines 3 through 6 of the user's banner text to the inserted text 
permanently.  The text can be displayed using the !DISPLAY command. 
Related Commands: 
IF, GOTO, DISPLAY 
00002
00003
00001
00004
Syntax: 
LIMIT [optionlist] 
Parameters: 
optionlist   -   specifies one or more of the following options in the format 
option[,option]... (If options omitted, current limits are printed.) 
    TI[ME]={hh:mm:ss|mm:ss|mm|:ss}   -   specifies the maximum execution time. 
    Note that the value can be expressed in hours, minutes and seconds, 
    minutes and seconds; minutes; or just seconds. 
    MEM[ORY]=value   -   specifies the maximum amount of memory to be 
    allocated for this job.  Value is an integer representing the number of 
    units of memory (each unit is 1024 36-bit words (1K) of memory) to be used 
    as the limit. 
    ABORT   -   tests the specified limit(s) before job step execution begins 
    and aborts the job if any of the options specified in the current LIMIT 
    command, when added to the cumulative job total for that option, exceeds 
    the total allowable option amount established for the job or allowed this 
    user. 
    STEP   -   specifies that the limits expressed in the current LIMIT 
    command are to apply to the following job step only. 
    LO=n   -   specifies the maximum number of printed pages (excluding 
    diagnostic output) that may be listed by subsequent job steps.  The number 
    must not exceed the maximum value assigned the user as part of his account 
    authorizations. 
    DO=n   -   specifies the maximum number of printed pages that may be 
    listed for diagnostics (via the M$DO DCB).  The maximum value is 
    determined for each user according to his account authorization. 
    PO=n   -   specifies the maximum number of punched cards that may be 
    output by subsequent job steps (may not exceed the maximum authorized for 
    the account). 
    TDIS=n   -   specifies the maximum number of temporary disk granules that 
    may be acquired by this job. 
    PDIS=n   -   specifies the maximum number of permanent disk granules that 
    may be generated by this job.  PDIS is also subject to limits established 
    for the account. 
    FPOOLS=n   -   establishes the maximum number of file management buffers 
    which the system may use for the job.  The minimum number of FPOOLS is 
    five. 
Description: 
LIMIT specifies maximum values for various system "consumables" required by a 
job step.  If the specified limit is exceeded during execution, the executing 
step is aborted.  More than one LIMIT command can be included in a job stream. 
The LIMIT command does not affect the scheduling of the job. 
Usage for the TIME and MEMORY options on the LIMIT command differs from their 
usage on the RESOURCE, ORESOURCE, and ACQUIRE commands.  The user may limit 
time or memory used by any given section of an executing program.  The maximum 
values allowed for the TIME and MEMORY options on the !LIMIT command are the 
values specified by the !RES command, or the default allocation, if none was 
specified. 
Note that there is no master LIMIT command; each occurrence is processed 
immediately, subject only to the restrictions established by the system 
manager for running account (or the RESOURCE or ORESOURCE requests for TIME). 
If STEP is specified, the limits revert to the last non-STEP LIMIT command. 
If the requested STEP LIMIT is more than that remaining for the item, the 
smaller value is used unless the ABORT option is specified, in which case the 
job is aborted. 
Note:  Limits used on the step following the STEP limit will not be deducted 
from the non-step limit specified previously. 
Usage Notes for Setting FPOOL Limits 
Sometimes a user may want to determine how many FPOOL buffers to use in order 
to achieve optimal performance with the minimum number of FPOOLs.  Perhaps the 
easiest way to determine how many FPOOLs to specify when running a 
user-written application is to use an experimental approach, i.e. run the 
application with a large FPOOL limit and examine it with ANLZ while running. 
The JIT display can be used to see total FPOOL's in use, and the DCB display 
to see the FPOOL's in use by each DCB.  A judgement must then be made as to 
which of these are routinely used, and the FPOOL limit set to accommodate the 
active DCBs. 
While there is no simple algorithm to predict exact FPOOL requirements, it is 
possible to formulate some general guidelines:  CONSEC and RELATIVE files 
require one FPOOL each while they are open.  KEYED and INDEXED files are more 
complex; the basic requirement is for two buffers, one for level 0 index and 
one for data.  In addition, if the file is large enough to have higher levels, 
one FPOOL is required for the top of the pyramid.  'Pyramid' refers to the 
buffer with the highest key indices.  When records are inserted causing a 
granule to be inserted at level 0 of a keyed or indexed file, a transient 
requirement for two more FPOOLs is present. 
In making these estimates, the transient buffer usage that occurs on the first 
read of a file may be in effect ignored.  Transient buffer usage refers to 
reading MAD, PAD, FD, and FIT when the file is opened. 
For routine activity with EDIT, PCL, various other compilers, etc., FPOOL 
limits set from five to ten are satisfactory. 
Examples: 
!LIMIT TIME=:05,LO=125 
Indicates that the current job is not to use more than 5 seconds of execution 
time or produce more than 125 pages of printed output. 
!LIMIT STEP,DO=50,FPOOLS=5,PDIS=18,TDIS=24 
Indicates that this LIMIT command is to apply to the following job step only, 
with these limits in effect:  50 pages of diagnostic output, 5 file management 
buffers, 18 permanent disk granules, and 24 temporary disk granules. 
Related Commands: 
DISPLAY, ORESOURCE, RESOURCE  
00002
00004
00001
00005
00003
{LINK|LOAD|LYNX} fid[,fid]...[,][tree] 
    [{ON|OVER} rununit[,listfid][(optionlist)]] 
Parameters: 
fid   -   specifies an object file, a run unit file, or a file of 
LINK commands.  If an object file is specified, all of the object 
units in the file are included.  If a run unit is specified, only 
information concerning defined symbols in the file is used;  no 
procedure or data is extracted from the run unit file.  Using run 
unit files, the LINK Processor can satisfy references to symbols 
that are offsets from defined memory images.  See the discussion of 
overlaid programs later in this Section for information on how to 
specify input file lists for an overlaid program. 
tree   -   optionally specifies a tree structure. 
ON   -   specifies that if the value for rununit identifies a file 
that already exists, the existing file is not to be overwritten. 
OVER   -   specifies that if the value for rununit identifies a file 
that already exists, the existing file is to be overwritten. 
rununit   -   identifies the file to contain the run unit.  If 
rununit is not specified, the default is "OVER *L." 
listfid   -   identifies file for listing output. 
optionlist   -   specifies valid LINK options in the form 
{option|(option[,option][,option]...)}.  Valid options are: 
ALT[SHARELIB]=libfid 
AS[LIB] 
B[REF]=value 
CONC{[=YES]|=NO} 
DB[IAS]=address 
DC[BSLOTS]=value 
{DCB1|SI[DCB]}=dcbname 
{DCB2|UI[DCB]}=dcbname 
{DCB3|OU[DCB]}=dcbname 
{DCB4|LO[DCB]}=dcbname 
DP[ATCH]=value 
DU[PLICATE] 
I[NCLUDE] ( (nodename,libfid,pen) [,(nodename,libfid,pen ...] ) 
IP[ATCH]=value 
IXT[NSIZE]=value 
LIBSR[CH](ac1[,ac2]...) 
LL[MU] 
LS[AU] 
M[AP]({N[AME]|V[ALUE]|L[DEF]|U[DEF]}[,{N[AME]|V[ALUE]|L[DEF]|U[DEF]}]...) 
NB[REF] 
{NDCB1|NSI[DCB]} 
{NDCB2|NUI[DCB]} 
{NDCB3|NOU[DCB]} 
{NDCB4|NLO[DCB]} 
NOALT[SHARELIB] 
NOC[HGPMEM] 
{NOD[EBUG]|ND} 
NOE[DITING] 
NOSH[ARELIB] 
{NOSY[SLIB]|NL} 
NPL[OVER] 
NWA[RN] 
OS[P] 
PB[IAS]=address 
PRI[VILEGES]{=priv|[=](priv[,priv]...)} 
PR[OCACC] 
PROMOTE 
PROMOTE_B[LANK] 
PROMOTE_L[ABEL] 
PSEUDO=(resnm[,decimal_number]) 
RE[PORT]=value 
SE[VERITY]=value 
{SHAREA[BLE]|NSHAREA[BLE]} 
SHAREL[IB]=libfid 
SL[IB] 
SLOCK(lock[,lock]...) 
SR[CH](ac1 [,ac2]...) 
ST[ART]=address 
STD[INVOC] 
SUR[CHARGE] 
SY[STEM] 
TC[B]=value 
UN[SAT]={libfid|(libfid,libfid[,libfid...])} 
V[ECTOR](option[,option]...) 
VER[SION]={version|(version)} 
WA[RN] 
WLOCK(lock[,lock]...) 
XT[NSIZE]=value 
Description: 
The LINK command (with synonyms LOAD and LYNX) creates an executable 
program (run unit) and, optionally, creates overlay programs. 
Examples: 
!LINK FIL.ACCT123.PAS OVER MOD (UNSAT=MY_LIB_FILE,SEVERITY=4,DBIAS=10000) 
In this example, the user specifies a library search list, a maximum severity 
level, and a bias: 
This command specifies: 
o   File FIL from account ACCT123 is the object unit to be retrieved. 
o   The library file MY_LIB_FILE is to be searched for external definitions 
    corresponding to unsatisfied primary references (if any exist after 
    linking has been accomplished from all other specified sources). 
o   The name MOD is to be associated with the run unit, which is to be a 
    permanent file in the user's account. 
o   Assuming that the user is authorized with a default read access of ALL, 
    any account may read the run unit, but none may write into it. 
o   Errors of severity level 4 are acceptable. 
o   A relocation bias of octal 10000 is to be used. 
o   No map is to be listed. 
Related Commands: 
See LINK HELP 
00002
00003
00001
00004
Syntax: 
LIST [{ON|INTO|OVER} fid] 
Parameters: 
fid   -   identifies a disk file, a line printer or other unit record device, 
the on-line terminal or logical device. 
Description: 
LIST enables the listing output of a processor.  If a fid is specified, then 
DCB #4 will be set to that file or device. 
Listing output is enabled by a flag in the JIT; it does not modify DCB #4. 
This means that processors can write to DCB #4 regardless of this flag.  The 
DONT LIST command resets this flag (it does not reset the DCB) so output may 
still occur at DCB #4 if a processor does not honor the flag. 
NOTE:  This command should not be confused with the PCL command LIST.  If a 
PCL list is to be executed in IBEX, the "L" form must be used to differentiate 
it from the IBEX LIST command. 
Examples: 
!LIST OVER MYFILE 
This command directs listing output to public disk file MYFILE.  If the file 
already exists, its contents are replaced. 
Related Commands: 
DONT LIST (to suspend listing); RESET #4 (to cancel LIST command). 
00002
00003
00001
00004
LINK
LINK
MESSAGE
Syntax: 
MAP rununit[ {ON|OVER|INTO} listfid](optionlist) 
Parameters: 
rununit   -   identifies a run unit. 
ON   -   specifies listing onto a newly created file. 
OVER   -   specifies replace any existing listing file. 
INTO   -   means append listing into existing listing file. 
listfid   -   specifies a file for LINK listing output. 
option   -   is any of the following values: 
    N[AME]   -   requests a map of defined symbols sorted by name. 
    V[ALUE]   -   requests a map of defined symbols sorted by value. 
    L[DEF]   -   requests that used library DEFs be included in the map. 
    U[DEF]   -   requests that all library DEFs (both used and unused) be 
    included in the map. 
Description: 
A map of an existing run unit is produced through the MAP command. 
See the VECTOR option for differences in the map produced at link 
time and that produced when specifying MAP to IBEX. 
Examples: 
!MAP FIL.ACCT123.PAS (NAME,UDEF) 
Requests a map of run unit FIL.ACCT123.PAS containing defined 
symbols sorted by name and all library DEFs. 
Related Commands: 
See LINK Help facility. 
00002
00003
00001
00004
Syntax: 
{M|MESSAGE} [(dest)] textstring 
Parameters: 
textstring   -   is a series of 1-110 characters to be sent to the 
installation operator's console. 
dest   -   specifies a particular console, i.e.: ADMIN, ADCOM, COMM, DEVICE, 
DISK, DELTA, LIBRN, NOSYS, SYS, TAPE, UR. 
Description: 
MESSAGE sends messages to the installation operator's console. 
Examples: 
!M HOWDY! 
Sends the message HOWDY! to the installation operator's console. 
!MESSAGE (TAPE) Mount LT#TUNA. 
Sends the above message to the tape operator's console. 
Related Commands: 
ACCEPT 
00002
00003
00001
00004
Syntax: 
{MOD|MODIFY|RENAME} sourcelist TO destination[,sourcelist TO destination]... 
Parameters: 
sourcelist   -   specifies a list of disk files or ranges of disk files, 
separated by commas.  The following input options may be used with 
with this command:  CRI, DATE, ORG, S, and TY.  Wildcard filenames 
are permitted. 
destination   -   specifies a file name, password, and or the 
attributes and access controls that are to be assigned to the disk 
files specified in the PCL source components.  The special format of 
the PCL destination component for the MODIFY command is: 
[{fid|wild}][(outopt[,outopt]...)] 
where 
fid   -   specifies a name and/or password to be associated with each 
modified file. 
wild   -   specifies a wildcard filename. 
outopt   -   specifies one of the following PCL output options:  ACC, ACS, 
BA, GH, LR, LS, NBA, NR, RD, REB, REL, SPAR, TYP, VRD, VWR, WR, and XTN. 
NOTE:  The following rules apply to the use of the ACC option: 
1.  If the command specifies a single ACC option, that option 
    will replace existing accesses. 
2.  If the command specifies more than one ACC option and the 
    first does not have a + or -, existing accesses will be 
    replaced by it.  Subsequent ACC options in the same command 
    that do not have a + or - will be treated as if they had a +. 
Description: 
MODIFY alters the attributes and access controls of specified disk files. 
Note that the source and destination fids for the MODIFY command 
differ substantially from the source and destination fids in other 
PCL commands. 
Examples: 
!MODIFY SHEEP TO GOATS 
means change only the name a file, SHEEP TO GOATS without having to 
wait for its contents to be copied. 
!MOD SECRET TO (ACC(?)) 
makes file unreadable by all other accounts. 
NOTE: The incantation MOD SECRET TO (RD=ALL) authorizes reading by all 
accounts. 
!RENAME ?_FORT TO ?_SI (TY=SF) 
means change the name of all files ending in _FORT so that they end in 
_SI, with the file type to be set to SF (source FORTRAN).  As 
each file is modified, the old and new names are displayed. 
<RENAME PERCH TO FISH, CHICKEN TO FOWL 
means change the names of PERCH to FISH, and CHICKEN to FOWL, 
with one command. 
Related Commands: 
See the PCL Help Facility 
00002
00003
00001
00004
Syntax: 
MOU[NT] fid {[DE[NSITY]{=n|(n)}][,{R[ING]|N[ORING]}] [,REEL=(reel[,reel]...)]} 
            {[REEL=(reel[,reel]...)                                         ]} 
Parameters: 
fid   -   is a CP-6 tape fid. 
DENSITY   -   specifies the tape density.  Meaningful only if the RING 
option is specified. 
RING   -   specifies that the tape is to be mounted with a write ring. 
NORING   -   specifies that the tape is to be mounted without a write 
ring.  This is the default setting. 
REEL=reel   -   specifies which physical reels are to be mounted. 
If only one reel is specified, the parenthesis may be omitted. 
The maximum number of reels is ten. 
Description: 
MOUNT requests that a certain tape be mounted on the system tape drives. 
When MOUNT is issued, the operator is informed of the request.  No 
further commands can be issued until the requested mount has taken 
place.  If the BREAK key is struck while a MOUNT request is active, 
the request is terminated, and a cancellation message is sent to the 
operator. 
Examples: 
!MOUNT FT#1234 REEL=3 
!MOUNT LT#ABCD 
means mount reel 3 of the free tape #1234 and the labeled tape #ABCD. 
Related Commands: 
See the PCL Help Facility 
00002
00003
00001
00004
Syntax: 
!NCTL {dv@[wsn][ (form)]|filename[.account]} 
Parameters: 
dv   -   specifies a device. 
wsn   -   specifies a workstation.  If unspecified, the device is assumed to 
be at the default workstation.  In either case, the device account must have 
access to the workstation. 
form   -   specifies a form to be used for processing the file. 
filename   -   specifies a file name that identifies the file.  This file must 
be consecutive.  If it exists, it will be extended, not overwritten.  If the 
filename ends with a "?", the "?" will be replaced with an 11-digit decimal 
UTS value.  The length of the filename (including the trailing "?") must not 
exceed 21 characters.  If it does, this substitution will not be performed and 
the NCTL M$OPEN will fail. 
account   -   specifies an account in which the file is to be created.  If 
this account is different from the device's account, the device's account must 
be authorized to create files in the specified account. 
Description: 
The NCTL control card allows a control input device to interpret non-control 
input.  Control input devices are local or remote card readers, bisynch input 
streams, or asynch devices logged on as symbiont input devices. 
Once a !NCTL is encountered, an End-of-File (EOF) is the only valid terminator 
for a file; this may be indicated with a !FIN card.  If the device is a 
non-control device, files read into the device are assigned a default !NCTL 
card, if one is not present.  A file created by the NCTL card has an 
expiration date equal to the creation date. 
NOTE:  Device accounts, default fids, and forms are installation-defined.  The 
ability of a control device to accept !NCTL cards can optionally be disabled 
by the system manager. 
Examples: 
!NCTL SYMFILE 
means create a file SYMFILE in the input device's default account. 
!NCTL SYMFILE.ROBINSON 
means create a file SYMFILE in account ROBINSON.  For this to be successful, 
the device's account must be able to create files in account ROBINSON. 
Related Commands: 
NONE 
00002
00003
00001
00004
Notation conventions used in command specifications and examples are listed 
below. 
  Convention          Meaning 
  CAPITAL LETTERS 
                      Capital letters must be entered as shown for input, and 
                      will be printed as shown in output. 
  lowercase letters 
                      Lowercase letters identify an element that must be 
                      replaced with a user-selected value. 
                      AP i could be entered as AP 2. 
  Special Characters 
                      Numbers that appear on the line (i.e., not subscripts), 
                      special symbols, and underlines appear as shown in 
                      output messages and must be entered as shown when input. 
                      #xxx could be entered as #011. 
  Brackets 
                      An element inside brackets ([]) is optional.  If 
                      elements are stacked vertically within brackets, the 
                      elements may be omitted or one of them may be entered. 
                      For example, 
                          [DISK] 
                          [TAPE] 
                      means that the user may omit this entry, or may enter 
                      DISK, or may enter TAPE. 
                      Alternatively, the vertical OR bar is used to separate 
                      the possible choices: 
                          [DISK|TAPE] 
                      When used to enclose keywords, brackets signify that the 
                      bracketed portion may be omitted, or truncated at any 
                      point.  For example, the notation K[EY] means that the 
                      user may enter K, KE, or KEY. 
  Braces 
                      Elements placed inside a pair of braces ({}) identify a 
                      required choice.  If elements are stacked vertically 
                      within braces, one of them must be entered.  For 
                      example, 
                          {id } 
                          {ALL} 
                      means that either a value for id or the word ALL must be 
                      entered. 
                      Alternatively, the vertical OR bar is used to separate 
                      the choices: 
                          {id|ALL}. 
  Or Bar 
                      The Or bar also separates elements in a required choice. 
                      {A|id}   -   means that either the letter A or the value 
                      of id must be entered. 
  Ellipsis 
                      The horizontal ellipsis indicates that a previous 
                      bracketed element may be repeated, or that elements have 
                      been omitted. 
                      option[,option]...   -   means that one or more options 
                      may be entered, with a comma inserted between each 
                      variable. 
  Careted Letters 
                      Letters inside carets indicate the keys on a physical 
                      terminal device. 
                      <ESC> <BS>   -   means press the escape key and then the 
                      backspace key. 
                      <CNTL-B>   -   means hold the control key down while 
                      pressing the B. 
                      Note that the control key is similar to the shift key: 
                      it does nothing on its own, but changes the meaning of 
                      the keys that are pressed while it is held down. 
  Keywords 
                      Keywords can be typed in uppercase or lowercase or a 
                      combination of both.  In this manual, keywords are 
                      always shown in uppercase. 
  Parameters 
                      Single parameters are connected to keywords in one of 
                      three ways: 
                      KEYWORD=parameter 
                      KEYWORD(parameter) 
                      KEYWORD=(parameter) 
                      A list of more than one parameter is connected to a 
                      keyword in one of two ways: 
                      KEYWORD(parameter,parameter) 
                      KEYWORD=(parameter,parameter) 
                      In this manual, the following forms are used: 
                      Single parameters:    KEYWORD=parameter 
                      Multiple parameters:  KEYWORD=(parameter,parameter) 
                                                       or 
                                            KEYWORD=(parameterlist) 
                      Multiple parameters are often referred to as lists, e.g. 
                      an optionlist is a list of options, separated by commas. 
  Double Quotes 
                      Comments within command streams are denoted by being 
                      enclosed in double quotes marks ("). 
  Apostrophe 
                      Strings that contain delimiters must be enclosed by 
                      apostrophes ('); if an apostrophe is part of a string, 
                      it is denoted by adjacent apostrophes (''). 
  Semicolon 
                      The semicolon is a continuation indicator for multiple 
                      line commands and for multiple commands on a single 
                      line.  The semicolon cannot be used for continuation 
                      inside a keyword or text string. 
00012
00005
00004
00001
00008
00011
00007
00009
00002
00006
00010
00013
00003
NOTATION
Syntax: 
NOTIFY [jobidlist] [[,](optionlist) 
Parameters: 
jobidlist - specifies one or more jobid in the format 
jobid[,jobid]...[,jobid], where jobid is one of the following: 
    sysid - is the job sysid assigned by the system and displayed in a message 
    sent to the user when the BATCH command that submitted the job was 
    processed. 
    jobname[.account] - is the alphanumeric job name which was defined with 
    the NAME option on the JOB command for the job to be checked.  If the user 
    does not have DISPJOB privilege, the named job must have been submitted 
    under the running account.  If account is not specified, the current 
    user's account name is the default. 
optionlist - specifies one or more of the following options in the format 
option[,option]...[,option]: 
    INPUT [suboption]   -   searches only the Input queue with the following 
    suboptions: 
        ALL   -   reports all the input jobs. 
        HELD   -   reports only those jobs held in the queue. 
        READY   -   reports only those jobs ready to run. 
        The default suboption is READY. 
    JOB  -  searches only the Running queue. 
    ME - searches the queue(s) for only job(s) under the user's account name. 
    OUTPUT  -  searches only the Output queue. 
    RUNNING  -  searches only the Running queue. 
    SYSTEM  -  searches the queue(s) for job(s) for any/everyone. 
    TERMINAL - searches the queue(s) for job(s) using the user's current 
    sysid. 
    USE - allows the user to specify a fid in which NOTIFY will store sysids 
    to be checked on later by the user.  If a file is named but no account is 
    specified, the default account (or default account and packset) will be 
    used as described in the CHECK/NOTIFY Options table.  The file name, 
    account name and optional packset name will be remembered for future use. 
    WAIT [suboption] - directs the system to wait a specified interval, then 
    report on BATCH jobs that have changed status since last checked.  <BREAK> 
    displays the status of all jobs being checked.  <CNTL-Y> or <ESC><ESC> 
    will abort the WAIT command.  The suboptions are as follows: 
        PRINT   -   wait until all jobs being checked are printing. 
        DONE   -   wait until all jobs being checked are done. 
        nnn   -   interval, in seconds, that CHECK is to sleep between 
        checking status of the jobs.  Default is 15 seconds. 
        The default is DONE. 
If neither jobid or optionlist is specified, all jobs in the current user's 
account which were BATCHed and not yet reported completed will be displayed. 
Upon being reported completed, the record(s) corresponding to the job sysid 
will be deleted from the USE file. 
These options are the same as those used for the CHECK command; See the 
CHECK/NOTIFY Options table for complete descriptions and syntax of the above 
options. 
Description: 
NOTIFY specifies that after each jobstep the user wishes to be notified of all 
jobs which have changed status.  DONT NOTIFY disables this feature, which is 
normally off.  If options are specified with NOTIFY, they will be remembered 
and used as defaults for future CHECKs and NOTIFYs (at job steps). 
Usage Notes: 
*$$JOB FILE 
Sysids of jobs batched during the current session, plus sysids CHECKed by the 
user will be stored in the star file *$$JOB, which is created by CHECK.  If 
the user wants to store this information in a permanent file, the USE option 
allows him to specify any file.  When the sysid job has completed, the 
corresponding record will be deleted from the USE file.  When all records have 
been deleted, the file will be deleted. 
PRIVILEGES NEEDED TO DO SPECIAL FUNCTIONS 
If the user wishes to see all the system input, output, and/or running job 
queues, he must be authorized for DISPJOB privilege. 
USER INTERACTION WITH CHECK AND NOTIFY 
All options specified by CHECK are treated as one-time, no-remember commands. 
If options are specified with NOTIFY, they will be remembered and used as 
defaults for future CHECKs and NOTIFYs (at job steps). 
Examples: 
!NOTIFY 
requests that the user be provided with a status display for all jobs which 
have changed status since the last display. 
Related Commands: 
CHECK, DISPLAY, DONT, BATCH 
00002
00004
00001
00005
00003
CHECK_OPS
CHECK_OPS
Syntax: 
OFF [{F[ULL]|S[UMMARY]|N[ONE]}] 
Parameters: 
F[ULL]   -   specifies full accounting information. 
S[UMMARY]   -   specifies summary of accounting information. 
N[ONE]   -   specifies no accounting information. 
The default is SUMMARY. 
Description: 
OFF terminates an on-line session; the user is logged off, a summary of 
accounting information is printed at the terminal, and the terminal is 
disconnected. 
Examples: 
!OFF 
means exit the system. 
Related Commands: 
BYE 
00002
00003
00001
00004
Syntax: 
{ORES|ORESOURCE} [resourcelist] 
Parameters: 
resourcelist - specifies a list of resources, separated by commas. Valid 
resources are: 
MEM[ORY]=VALUE 
TI[ME]={hh:mm:ss|mm:ss|mm|:ss} 
{MT|LT|FT}[dd][({1600,6250|800,1600|6250|1600|800}[BPI])][=n] 
DP[dd][({200|500|600|1000}[MEG])][=n] 
DP#name[({E[XCLUSIVE]|S[HARED]})] 
ACC[OUNT]=({a[,a]...|NO}) 
LP[dd][({APL|OVERPRINT|LC})][=n] 
CP[dd][({BIN|LC})][=n] 
Pseudo-resources can also be specified.  See RESOURCELIST for a complete 
description. 
Description: 
ORESOURCE is used to allocate memory, time, tape drives (spindles), packset, 
and pseudo resources for online or ghost jobs. 
Examples: 
!ORESOURCE MEM=256 
Indicates that 256K words of memory are to be allocated for this online 
session. 
Related Commands: 
RESOURCE, ACQUIRE 
00002
00003
00001
00004
Syntax: 
OUTPUT expression[,expression]... 
Parameters: 
expression   -   is a valid IBEX expression.  The format is: 
[unary]{variable|'string'|integer|function|system_variable} 
    [operator expression] 
See EXPRESSION for a complete description.\ 
Description: 
OUTPUT prints the value of expressions through the M$LL DCB, one expression 
per line. 
Examples: 
!OUTPUT A,B 
means print the values of variables A and B on separate lines. 
!OUTPUT 'A'||'B' 
means print 'AB' 
!OUTPUT STEPCC*20 
means print the current STEPCC value multiplied by 20. 
Related Commands: 
LET, IF 
00002
00003
00001
00004
Syntax: 
PASSWORD {OLD=oldpassword[,NEW=newpassword]|NEW=newpassword} 
Parameter: 
oldpassword   -   is the current password for the logon-id. 
newpassword   -   specifies a password to be assigned to the logon-id. 
If the logon-id has a password, both OLD and NEW must be specified to change 
the password.  If the logon-id has no password, only NEW is specified.  To 
delete the account's password, only OLD is specified. 
Description: 
PASSWORD creates, changes, or deletes the logon password.  In order to change 
or delete a password, the current password must be known. 
Examples: 
!PASSWORD OLD=SECRET,NEW=TOPSECRT 
changes the password of the logon-id from SECRET to TOPSECRT. 
!PASSWORD OLD=DANA 
deletes the logon-id password (DANA). 
!PASSWORD NEW=OCCULT 
defines the logon-id password as OCCULT.  Only legal if the logon-id has no 
current password. 
Related Commands: 
NONE 
00002
00003
00001
00004
Syntax: 
PLATEN [UCnn] [option[,option]...] 
Parameters: 
UCnn   -   specifies a particular stream (UCnn). 
option   -   is a valid option for the PLATEN command.  These options are 
described below. 
F[IRST]=value   -   specifies the number of lines between the perforation and 
the first printable line.  The default is 0.  Total page length is the sum of 
LENGTH, LIMBO, and FIRST. 
L[ENGTH]=value   -   specifies the number of printable lines in a page.  The 
default is continuous form paper.  The value of LENGTH cannot be less than 11. 
LI[MBO]=value   -   specifies the number of lines between the last printable 
line and the perforation at the bottom of the page. 
W[IDTH]=value   -   specifies number of characters in a terminal line.  The 
default is the physical platen width of the user's terminal, as defined in his 
current terminal profile. 
All values other than width must be decimal integers between 0 and 254 
inclusive.  Width value must be decimal integers between 0 and 508 inclusive. 
Description: 
PLATEN changes the maximum number of characters to be written per line on the 
terminal and the number of lines to be printed between each automatic page 
heading.  The PLATEN command with no options specifed executes as a DISPLAY 
PLATEN [UCnn] command. 
Examples: 
!PLATEN W=80 
means set the platen width to 80 characters. 
!PLATEN UC69 L=65,LI=0,FIRST=1 
means for stream UC69, skip one blank line at the top of each page and print 
65 lines per page. 
!PLATEN 
means display the current PLATEN settings of the user's console (UC01). 
Related Commands: 
NONE 
00002
00003
00001
00004
Syntax: 
PMD optionlist 
Parameters: 
optionlist   -   is any list of the following keywords: 
    AU[TO]               Auto segment (DS1) 
    CO[MMON]             Common segment (DS2) 
    DA[TA]               Data pages within Instruction Segment 
    DC[BS]               All DCBs 
    DS                   All data segments 
    DS1 through DS8      Data segments 1 through 8 
    D[YNAMIC]D[ATA]      Dynamic data pages within Instruction Segment 
    IS                   Entire Instruction Segment 
    JI[T]                User JIT 
    PR[OCEDURE]          Procedure pages within Instruction Segment 
    RO[SEG]              Entire Read-only segment 
    TC[B]                Task control block (TCB stack) 
Description: 
The PMD command invokes DELTA for post mortem dump functions.  A PMD will be 
performed only if an abort occurred during program execution or if the program 
has returned control to the Monitor through an M$XXX or M$ERR.  The PMD 
directive causes all or selected portions of a user's entire program image to 
be dumped.  Options allow for general selections of what areas to dump.  See 
the CP-6 DELTA Reference Manual, CE39, for further information. 
Examples: 
!PMD STATIC, AUTO, DCB 
means invoke DELTA for post mortem dump functions. 
Related Commands: 
DELTA, UNDER 
00002
00003
00001
00004
Syntax: 
POINT 
Description: 
The POINT command causes a caret (^) to be displayed as part of the syntax 
error message.  The POINT command is disabled by the use of !DONT POINT. 
Related Commands: 
DONT, EXPOUND, POSITION 
00001
00002
Syntax: 
POSITION 
Description: 
The POSITION command reactivates the automatic positioning of the cursor after 
the !DONT POSITION command has been used.  Automatic cursor positioning is 
part of the CP-6 syntax error message, and is the default unless the !DONT 
POSITION command has been used. 
Related Commands: 
DONT, POINT, EXPOUND 
00001
00002
    Preallocating file space is a good idea, especially for large databases. 
    The future growth of such files can often be anticipated and extra space 
    requested at initial file creation to allow more efficient operation by 
    CP-6 file management. 
    Typically controlled applications reserve file space via JCL or other 
    means.  At that time, the analysis performed in calculating file sizes is 
    used to select appropriate values for 
      IXTNSIZE - initial size of the file at creation. 
      XTNSIZE  - size of blocks added to the file when additional space 
                 is needed. 
      SPARE    - number of extra words to include in index blocks. 
    The defaults for these values are chosen so that users editing files 
    receive small increments when files need to be extended.  The assumption 
    is that controlled applications will systematically choose values 
    appropriate to those applications.  Please refer to "File Management 
    Performance", "M$OPEN and SET Options", later in this section which 
    discusses IXTNSIZE, XTNSIZE, and SPARE. 
    To determine how many granules are still available within a file, use 
    PCL's LIST command and observe the NGAV (number of granules available) 
    value. 
The IBEX PREPROCESSOR enables the user to define new commands by substitution 
into normal commands.  This is done by means of a preprocessor expression.  A 
preproceesor expression consists of a command variable which may be modified 
by a unary operator, and which may also be combined with an operator 
expression to perform a variety of functions.  The preprocessor expression is 
defined under EXPRESSION COMPONENT. 
IBEX preprocessor expressions can be used with any IBEX command.  Immediately 
after the command is read, IBEX looks for a single % sign. This character 
signals the start of a preprocessor expression.  IBEX then evaluates the 
expression and substitutes into the command variable. 
Please note that there are two types of substitutions which occur in IBEX: 1) 
BATCH/XEQ substitutions performed when a file is XEQed, BATCHed, or XMITed, 
and 2) preprocessor substitutions performed in the online IBEX command stream. 
When a file is XEQed, BATCHed, or XMITed, expressions may be defined by 
!DEFAULT, !GLOBAL, and the replacement components of the BATCH and XEQ 
commands.  As the file is read, a routine makes substitutions, checks syntax 
if requested (SCAN option), and prints the file (PRINT option) if requested. 
The resultant file is passed to IBEX for interpretation.  The !DEFAULT and 
!INCLUDE directives are stripped from the file at this time.  When IBEX 
interprets this file, it checks to see if a bang (!) is present, and alerts 
the user if it is not.  At this point, IBEX looks at the file for preprocessor 
expressions, and the file is processed in the same manner as an online command 
stream described below. 
For an online IBEX command stream, IBEX looks for preprocessor expressions, 
and, when one is found (on IBEX commands only), the routine is called which 
evaluates the expression and returns a resultant string.  This string is then 
inserted into the IBEX command in place of the preprocessor expression, the 
resultant command is parsed by IBEX, and interpreted.  Following is an example 
of preprocessor substitution: 
    !LET CMD='DI' 
    !%CMD 
In this example, the command variable CMD is given a value of 'DI'.  Then the 
substituted string ('DI') is processed as an IBEX command.  The result is that 
a DISPLAY command is executed.  Every subsequent occurrence of !%CMD in the 
command stream will be processed as a DISPLAY command. 
Another example: 
    !LET FID='XYZ' 
    !FORTRAN %FID OVER %(FID||':OU') 
The result is that FORTRAN compiles XYZ and creates an object unit in XYZ:OU. 
Notice that in this example the expression is enclosed in parentheses.  This 
is necessary for expressions which have multiple elements. 
    !FORTRAN %$INPUT('What fid?') OVER OU (NLS) 
In the above example, the user is prompted with 'What fid?'.  IBEX then waits 
for input and substitutes this input back into the command.  If the user had 
said 'KUHENBEAKER' then the command would be: 
    !FORTRAN KUHENBEAKER OVER OU (NLS) 
The next example shows how to use the preprocessor to abbreviate frequently 
used long commands. 
    !LET LINK='LINK A,B,C,D OVER FRED' 
    !%LINK 
The user needs only type %LINK and the contents of the variable LINK will be 
inserted into the command record and then executed. 
The final example shows where parentheses prevent ambiguities. 
    !LET FID='TEST' 
    !PL6 %FID OVER %(FID||':OU') (SR(.:LIB_D00),N4S) 
This results in PL6 compiling 'TEST' and creating a file 'TEST:OU'. 
User programs may access preprocessor command variables via the M$CMDVAR 
monitor service, and affect the execution of JCL. 
Since the percent sign (%) has been reserved as a special character for IBEX, 
if a percent character is actually needed it requires doubling the percent 
sign (%%) for each required character.  See EXPRESSION 
00001
00002
PREPROCESSING
Syntax: 
PRINT [ALL|ldevlist] 
Parameters: 
ALL   -   specifies that the accumulated outputs for all logical devices are 
to be sent to their destinations immediately.  This is the default. 
ldevlist   -   specifies that the accumulated outputs for the specified 
logical device or devices are to be sent to their destination(s) immediately. 
The list is entered in the format 
ldevname[,ldevname]... 
ldevname is a logical device name established through the LDEV command. 
Description: 
PRINT directs that output accumulated for logical devices be sent to its 
destination immediately. 
Examples: 
!PRINT LP01,LP02 
The above example causes the accumulated output associated with logical 
devices LP01 and LP02 to be sent immediately to the associated destinations. 
Related Commands: 
ERASE, LDEV 
00002
00003
00001
00004
Syntax: 
{PRIO|PRIORITY} value 
Parameters: 
value   -   specifies the default batch priority between 0 (lowest) and 15 
(highest) and cannot exceed the user's maximum. 
Description: 
PRIORITY establishes the default priority for a job entered into the batch 
queue by this user.  The default is utilized if a priority is not specified on 
the JOB command. 
Examples: 
!PRIORITY 8 
means set the default job priority to 8. 
Related Commands: 
None 
00002
00003
00001
00004
Syntax: 
PRIV optionlist 
Parameters: 
optionlist   -   specifies one or more options separated by commas. 
    ALL{[=YES]|=NO}   -   sets all privileges available to the user (if YES). 
    If NO these privileges are not in effect. 
    AS[AVE]{[=YES]|=NO}   -   requests the user's image to be saved 
    automatically if the terminal connection is lost.  Upon subsequent logon, 
    the user may reconnect to the save image, picking up at the point of 
    disconnect. 
    CF[EP]{[=YES]|=NO}   -   requests the user be permitted inspection of the 
    contents of a FEP (front-end processor). 
    DI[SPJOB]{[=YES]|=NO}   -   requests user be permitted to utilize 
    M$JOBSTATS service request. 
    EXM[M]{[=YES]|=NO}   -   requests the user be permitted to utilize a 
    special set of extended memory management monitor services. 
    EXP[M]{[=YES]|=NO}   -   requests the user be permitted to start and stop 
    the special performance monitoring function. 
    FMD[IAG]{[=YES]|=NO}   -   requests the user be permitted to access 
    packsets as unmanaged devices. 
    FMR[EAD]{[=YES]|=NO}   -   requests the user be permitted to override the 
    file management read-only check. 
    FMS[EC]{[=YES]|=NO}   -   requests the user be permitted to bypass all of 
    the file management security checks. 
    GP[P]{[=YES]|=NO}   -   requests the user to be permitted to override the 
    stealable-page limit and acquire physical memory pages. 
    IOQ{[=YES]|=NO}   -   requests the user be permitted the use of the M$IOQ 
    service request for reading only. 
    IOQW{[=YES]|=NO}   -   requests the user be permitted the use of the 
    M$IOQW service for writing only. 
    JI[T]{[=YES]|=NO}   -   requests the user be permitted to modify the JIT 
    (Job Information Table). 
    MA[XMEM]{[=YES]|=NO}   -   requests the user be permitted the allocation 
    of memory beyond his authorized limit. 
    MF[EP]{[=YES]|=NO}   -   requests the user be permitted to modify the 
    contents of a FEP (front-end processor). 
    MS[YS]{[=YES]|=NO}   -   allows the use of certain features of GOOSE. 
    P[M]{[=YES]|=NO}   -   requests the user be permitted to obtain 
    performance monitor reports. 
    SP[CLMM]{[=YES]|=NO}   -   requests the user be permitted the use of M$CVM 
    (read only) and M$ACCESS service requests. 
    SYSC[ON]{[=YES]|=NO}   -   requests the user be permitted the use of the 
    M$SYSCON service. 
    SYSL[OG]{[=YES]|=NO}   -   requests the user be permitted the use of the 
    M$RSYSLOG service. 
    TN[D]{[=YES]|=NO}   -   requests the user be permitted the use of the test 
    and diagnostic service requests. 
Description: 
PRIV requests authorization and deauthorization privileges.  To successfully 
obtain a privilege, the user must have been authorized by the system manager 
for that privilege; if not, the request is ignored. 
Examples: 
!PRIV ASAVE=ON 
means in the event of a disconnect, save the image of the terminal session. 
!PRIV ALL 
means set the maximum privilege for the current account. 
Related Commands: 
NONE 
00002
00003
00001
00004
Syntax: 
PROCEED 
Parameters: 
NONE 
Description: 
PROCEED (a synonym for the GO command) resumes an interrupted activity. 
PROCEED is only meaningful at the double-bang (!!)  prompt. 
Examples: 
!!PROCEED 
means continue the interrupted activity. 
Related Commands: 
GO, END, CONTINUE 
00002
00003
00001
00004
Syntax: 
PROFILE [profilename [(P[ERM])] 
        [NONE(P[ERM])         ] 
Parameters: 
profilename   -   specifies a terminal type as represented by a profile name. 
Profiles are defined and supported by the system manager.  A list of 
system-supported profiles can be obtained via a DISPLAY PROFILE command.  If 
no profilename is specified, then the user's current PROFILE will be 
displayed. 
PERM   -   specifies that the change will be permanent, i.e., used the next 
and subsequent times the user logs on to this account. 
NONE(PERM)   -   specifies that the user's permanent PROFILE field will be set 
to zero length blank character profile name, but that the PROFILE for the 
current session is not changed. 
Description: 
PROFILE sets the terminal profile for the on-line session.  This command can 
only be issued on-line. 
Note that entering an on-line PROFILE command that requests the profile of a 
device with no keyboard (such a PRU1002) will log the device off. 
The PROFILE command can also be issued at logon using the PRO option.  The 
syntax is: 
LOGON PLEASE:name,account,password PRO=profile 
Some attributes set by the profile can be modified with the TERMINAL command. 
Examples: 
!PROFILE VIP7205 
means set the terminal profile for a HONEYWELL VIP model 7205. 
!PROFILE NONE(PERM) 
means set the user's permanent PROFILE field to zero length blank character 
profile name, but do not change the PROFILE for the current session. 
!PROFILE NONE 
results in an error message. 
Related Commands: 
TERMINAL 
Resetting Profile Character Sets 
Profile character sets may be created and modified by the System Manager via 
SUPER (see System Support Reference, HA21).  For example, a special profile 
TI745A with CHARSETNAME=APLTF can be created for use with APL.  Then, using 
the IBEX PROFILE command and specifying TI745A gives the user the APL 
character set. 
However, to use the same terminal with another character set, it is necessary 
to reset the character set by entering <ESC>$.  For example, after exiting APL 
and before entering another profile, the user enters <ESC>$ to reset the 
character set.  The PROFILE command is then used to enter a new profile and 
associated character set.  To use the terminal for APL again, it is only 
necessary to enter the special APL profile.  The IBEX TERMINAL command may 
also be used to set or reset terminal character sets. 
00002
00003
00001
00004
00005
Syntax: 
PROTECT 
Parameters: 
NONE 
Description: 
The PROTECT command causes IBEX to issue a QUIT? message prior to executing 
any IBEX command which will make the user's interrupted process unresumable. 
This gives the user an opportunity to decide whether to terminate the 
interrupted activity or not.  The DONT command is used to terminate QUIT? 
prompting.  The default is DONT PROTECT. 
Examples: 
!PROTECT 
means issue a QUIT? message if a command is issued that would destroy the 
image at the interrupted activity. 
Related Command: 
GO, QUIT 
00002
00003
00001
00004
Syntax: 
{Q|QUIT|END|STOP} 
Parameters: 
NONE 
Description: 
QUIT terminates interrupt mode and prompts the user for an IBEX command.  The 
interrupted activity may not be resumed. 
When in a command file, QUIT terminates processing of the file.  The 
interrupted activity may not be resumed. 
Examples: 
!!QUIT 
means discard the interrupted activity. 
Related Commands: 
GO 
00002
00003
00001
00004
RESET
Syntax: 
{REL|RELEASE} releaselist 
Parameters: 
releaselist   -   specifies one or more of the following options in the format 
option[,option]... 
    ALL   -   releases all resources currently held by the job. 
    MT   -   releases all magnetic tapes currently held by the job. 
    DP   -   releases all spindles currently held by the job.  This option has 
    no effect if the disks are being shared. 
    MEM[ORY]=n   -   releases the amount of memory specified by n (in 1024 
    word (1K) units). 
    setname [(disp)] 
    where 
    setname   -   is a 1 to 6 alphanumeric packset name preceded by the 
    characters DP#. 
    disp   -   is one of the following suboptions. 
        REM[OVE]   -   means remove this setname from the user's ownership 
        list.  This is the default. 
        REL[EASE]   -   means release the spindle(s) on which this set is 
        mounted.  User still owns the setname.  Ignored if the set is PUBLIC 
        or SHARED. 
        {RELREM|REMREL}   -   means release the spindle(s) and the setname. 
        NOR[EL] - means make the spindle(s) available for use with another 
        packset.  User still owns the setname and the spindle(s). 
        All of the above suboptions attempt to break the association of the 
        set with the disk drive(s) on which it is mounted, which can be broken 
        only if no DCBs are open to files on the set, and the user is 
        exclusive. 
    resourcename   -   is always in the format rtdd (e.g., MT01, LP07, DP01). 
    Specifying rtdd releases the named resource. 
    pseudoname[=n]   -   is an installation defined value.  Specifying 
    pseudoname releases the n highest-numbered pseudo resources specified to 
    the system.  The default is 1. 
Description: 
RELEASE deallocates resources that have been allocated by the RESOURCE, 
ORESOURCE, or ACQUIRE commands.  If resources are not released via a RELEASE 
command, they remain assigned until the user logs off. 
Examples: 
!RELEASE DP01,DP02 
Releases two disk drives identified as DP01 and DP02. 
!RELEASE DP#LIBSET 
Releases the packset LIBSET. 
!RELEASE ALL 
Releases all resources associated with the current job. 
Related Commands: 
RESOURCE, ORESOURCE 
00002
00003
00001
00004
Syntax: 
REM[OVE] fid 
Parameters: 
fid   -   is a CP-6 tape fid. 
Description: 
REMOVE requests that a certain tape be removed from the system tape 
drives. 
Examples: 
<REMOVE FT#1234 
requests that the free tape be removed from the tape drive. 
Related Commands: 
See the PCL Help Facility 
00002
00003
00001
00004
MODIFY
Format: 
{field1|'string1'}={field2|'string2'} 
Parameters: 
field1   -   is the field to be replaced by either field2 or string2 
(whichever is specified). 
A field is a contiguous set of nondelimiter characters bounded on either side 
by a delimiter character or by the left or right record boundary. 
Nondelimiter characters and some sample delimiter characters are: 
    Delimiter              Nondelimiter 
    ---------              ------------ 
    ( )  +                 A-Z 
    /    ' '               a-z 
    '    =                 0-9 
    /    .                 - (hyphen) 
    ;                      ?   $   *   : 
                           _ (underscore) 
The list of nondelimiters is exhaustive; anything else is considered a 
delimiter. 
string1   -   is the string to be replaced by either field2 or string2 
(whichever is specified). 
A string can be a part of a field, contiguous parts of two fields, or one or 
more contiguous fields.  A string is designated in a REPLACEMENT component (or 
rep equation) by enclosing it in apostrophes. 
field2   -   is the field that replaces either field1 or string1. 
string2   -   is the string that replaces either field1 or string1. 
Description: 
Prior to submitting a command file for execution, the user can replace 
existing values with new ones.  He can: 
o   Define and modify data replacement parameters for a single BATCH, XMIT, or 
    XEQ file (through the DEFAULT command). 
o   Define and modify data replacement parameters for all BATCH, XMIT, and XEQ 
    files in the session (through the GLOBAL command). 
o   Override DEFAULT and GLOBAL data replacements for a file by specifying 
    data replacement parameters as part of the BATCH, XMIT, or XEQ command 
    that submits the file. 
Through data replacement parameters, the user specifies which string or field 
is to be changed, and what the new value is to be.  Every occurrence in the 
file of the specified field or string will be changed. 
As each record from a command file is read, it is searched for the occurrence 
of a field or string specified in the option list.  If found, the appropriate 
substitution is made, the process repeats for each replacement specified, and 
the modified record is then placed in the command stream (unless the test mode 
has been specified). 
Examples: 
1)  Field replacement:      ABC=DEF 
    Command file contents:  ABCABC ABC ABCABC 
    Modified command file:  ABCABC DEF ABCABC 
2)  'String' replacement:   'ABC'=DEF 
    Command file contents:  ABCABC ABC ABCABC 
    Modified command file:  DEFDEF DEF DEFDEF 
In example 1, the value to be replaced is the field ABC; in example 2, the 
value to be replaced is the string ABC. 
Rules: 
REPLACEMENTS are used in the BATCH, XEQ, XMIT, DEFAULT, and GLOBAL commands. 
Data replacement parameters (field2 or string2) are subject to various 
substitutions before they are assigned to the replacement field -- first 
explicit substitutions, then GLOBAL substitutions, and finally default 
substitutions. 
If a string or field is identified for replacement more than once, (i.e., the 
field or string specified on the left-hand side of the replacement expression 
is specified in more than one command) it will be modified only once in 
accordance with the following four rules of precedence: 
1.  Within a job command stream, XEQ and BATCH command data replacement 
    specifications have precedence over DEFAULT data replacement 
    specifications and GLOBAL replacements (i.e., they are always honored). 
2.  Within a session, GLOBAL data replacement specifications have precedence 
    over DEFAULT replacement specifications. An earlier GLOBAL specification 
    has precedence over a later one. 
3.  Within a file, an earlier DEFAULT replacement has precedence over a later 
    one. 
4.  If a later specification redefines a specification of the same type, then 
    the original is deleted and the new one has lower precedence than all 
    earlier defined specifications. 
00002
00003
00001
00004
REPLACEMENT
Syntax: 
REPORT {J[OB]|S[TEP]|P[ROPRIETARY]|A[LL]}={F[ULL]|S[UMMARY]|N[ONE]} 
Parameters: 
F[ULL]=  specifies full accounting information 
S[UMMARY]=  specifies summary of accounting information 
N[ONE]=  specifies no accounting information 
The default is NONE. 
Description: 
The REPORT command specifies the level of statistics to be displayed for a job 
at logoff time, job steps, or proprietary programs.  Statistics are displayed 
at job step time. 
Examples: 
!REPORT STEP=SUMMARY 
means generate an accounting summary. 
Related Commands: 
STATUS 
00002
00003
00001
00004
RESOURCE
Syntax: 
{R|RESET} {dcb|DCBS}[,optionlist] 
Parameters: 
DCBS   -   resets all DCB assignments back to their default values. 
dcb   -   identifies by dcb name or unit number the DCB whose assignments are 
to be reset. 
optionlist   -   specifies file and/or device attributes. 
Valid options are: 
ACC[ESS]           ALLT[RMS]          BLK[L]             COM[P] 
ACS                ALT[KEYS]          BLO[CKED]          COP[IES] 
ACSV[EH]           AN[YDCB]           BT[MBRDR]          CT[G] 
ALLD[CBS]          AU                 BU[PM]             CV[OL] 
DC[BCONLGL]        IM[SGTYP]          NO[FILE]           SEQC[OL] 
DEB[UG]            IN[DENT]           N[RECS]            SEQI[D] 
DE[NSITY]          INITI[ALIZE]       OLA[TCH]           SH[ARE] 
DIR[ONLY]          INITV[ALUE]        OLO[CK]            SN 
DIS[P]             INSTATTR           OM[SGTYP]          SPAN[NED] 
DV[FC]             IO[ERROK]          OPT[IONAL]         SPAR[E] 
EB[CDIC]           INSTATTRS[IZE]     OR[G]              TA[B] 
EOFN[ONE]          IS[TATION]         OS[TATION]         TE[RMCONLGL] 
EOFO[NE]           IX[TNSIZE]         PH[YSICAL]         TI[TLE] 
EOFT[IME]          JRNLB[YPASS]       PO[SITION]         TO[PBRDR] 
EV[ENT]            KEYL               PROCATTR           TY[PE] 
EXI[ST]            KEYX               PROCATTRS[IZE]     UATTR 
EXP[IRE]           LD[BYPRO]          PROF[ILE]          UATTRS[IZE] 
FO[RM]             LFT[BRDR]          P[AGECOLUMN]       UOPTn 
FP[RG_FID]         LI[NES]            Q[ISS]             VBRDRC[HR] 
FS[N]              LO[AD]             RD                 VBRDRS[IZ] 
FU[N]              LR[DLO]            REC[L]             VOLA[CCESS] 
FW[INDOW]          LST[AOR]           RES[ETPAGE]        V[OL] 
GH[STACS]          LS[LIDE]           RE[AD]             W[AS] 
HBRDRC[HR]         MAR[GIN]           RH[TBRDR]          WL[ENGTH] 
HBRDRS[IZ]         MAX[VOL]           SC[RUB]            WR[ITE] 
HD[RHEIGHT]        MINL[ENGTH]        SEE[D]             WW[IDTH] 
IG[NOREFSN]        MINW[IDTH]         SEGN[UM]           XTE[ND] 
ILA[TCH]           MI[NPHYS]          SEGS[IZE]          XTN[SIZE] 
ILO[CK]            MY[STATION]        SEQ 
Only keywords can be specified on a RESET command. 
Type HELP SET_OPS for complete descriptions. 
Description: 
RESET modifies DCB assignments at a job step.  Depending on the options 
specified on the command, RESET requests that: 
o   All DCB assignments for all DCBs be set back to their default values. 
o   The DCB assignments for a particular DCB be set back to its default 
    values. 
o   Specific DCB parameter values (options) for a particular DCB be modified, 
    as indicated in the command. 
Examples: 
!RESET DCBS 
This command resets all DCB assignments back to their default values at the 
next job step. 
!RESET M$SI 
This command resets M$SI back to its default values.  The command takes effect 
at the next job step. 
IO[ERROK] !RESET M$DATABASE,SHARE 
This command resets the sharing attributes of the DCB to its default.  No 
other attributes are affected.  The command takes effect at the next job step. 
Related Commands: 
SET 
00002
00003
00001
00004
Syntax: 
{RES|RESOURCE} [resourcelist] 
Parameters: 
resourcelist   -   specifies a list of resources, separated by commas.  Valid 
resources are: 
MEM[ORY]=VALUE 
TI[ME]={hh:mm:ss|mm:ss|mm|:ss} 
{MT|LT|FT}[dd][({1600,6250|800,1600|6250|1600|800}[BPI])][=n] 
DP[dd][({200|500|600|1000}[MEG])][=n] 
DP#name[({E[XCLUSIVE]|S[HARED]})] 
ACC[OUNT]=({a[,a]...|NO}) 
LP[dd][({APL|OVERPRINT|LC})][=n] 
CP[dd][({BIN|LC})][=n] 
NHPSN   -   specifies that the user's home packset is not required for this 
job.  NHPSN (No Home Packset Name) applies only to the RESOURCE command. 
Pseudo-resources can also be specified. 
See RESOURCELIST for a complete description. 
Description: 
RESOURCE allocates memory size, execution time, tape drives, disk drives 
(spindles), packsets, and pseudo resources for batch jobs.  It must 
immediately follow any JOB command. 
Examples: 
!RESOURCE DP(500MEG), DP02(200MEG), DP03(200MEG), LP(OVERPRINT) 
Indicates that the current job requires one 500MEG disk pack, two 200MEG disk 
packs, and a line printer with an overprint capability. 
!RESOURCE CP(BIN),MEM=4,TIME=04:20:13 
Indicates that the current job is to be allocated a binary card punch, 4K of 
memory, and the execution time is not to exceed 4 hours, 20 minutes and 13 
seconds. 
!RESOURCE ACC(.MARYACCT,.JOESACCT) 
Indicates that the packset containing the accounts MARYACCT and JOESACCT is a 
PUBLIC packset needed for this job. 
!RESOURCE DP#LIBSET(SHARED) 
Allocates the packset LIBSET as a PUBLIC packset for this job. 
Related Commands: 
ORESOURCE, RELEASE, LIMIT, ACQUIRE 
00002
00003
00001
00004
Format: 
resource[,resource]... 
Parameters: 
MEM[ORY]=VALUE   -   specifies the maximum amount of memory to be allocated 
for this job.  Value is an integer representing the number of units of memory 
(each unit is 1024 36-bit words or 1K of memory) to be used. 
TI[ME]={hh:mm:ss|mm:ss|mm|:ss}   -   specifies the total maximum CPU execution 
time. 
{MT|LT|FT}[dd][({1600,6250|800,1600|6250|1600|800}[BPI])][=n]   -    specifies 
the type of tape required.  MT is labeled or free, LT is labeled, and FT is 
free.  The "dd" is a two-digit decimal value (01 to 99) that assigns a unique 
identification to the tape drive; if not specified, dd assignments are made by 
the system in ascending order from 01.  The tape density (6250, 1600, or 800 
BPI) or tape densities (1600,6250 or 800,1600) can also be specified.  The "n" 
specifies the number of tape drives of that type that are required; the 
default is 1. 
DP[dd][({200|500|600|1000}[MEG])][=n]   -   specifies the number of disk 
spindles required.  The storage capacity (100, 200, 500, 600, or 1000 MEG) can 
also be specified.  The "dd" is a two-digit decimal value (01 to 99) that 
assigns a unique identification to the spindle; if not specified, dd 
assignments are made by the system in ascending order from 01.  The default 
for n is 1. 
    Note:  If several devices are acquired that have different attributes 
    (densities or capacities), they should be referenced by their full name 
    (i.e. MT05 not just MT) to assure getting the desired association between 
    attributes and drive. 
    Additionally, when acquiring such resources, it is preferable to fully 
    name the resource rather that letting the system assign the "dd" part of 
    the name.  This avoids having to compute the system-assigned name when 
    referring to the resource. 
    Example: 
         !JOB 
         !RES MT01(800),MT02(1600,6250),MT03(6250) 
         !PCL 
         PCL D00 here 
         <COPY MT01#XXXX/AFILE TO MT02#YYYY/BFILE(DEN=1600) 
         <REM #YYYY 
         <COPYALL MT02#ZZZZ TO MT03#AAAA 
    The RESource command acquires three drives.  MT01 is an 800bpi only drive. 
    MT02 is a 1600/6250 bpi dual density drive.  MT03 is a 6250 bpi only 
    drive.  The COPY command copies the file AFILE from the 800 bpi tape 
    #XXXX.  The COPYALL command copies all the files from the tape ZZZZ to the 
    6250 bpi tape #AAAA.  The #ZZZZ tape may have been written at either 1600 
    or 6250 bpi. 
DP#name[({E[XCLUSIVE]|S[HARED]})]   -   specifies a packset that is required. 
The "name" can be any six alphanumeric characters.  The type of access 
(EXCLUSIVE or SHARED) can be specified.  EXCLUSIVE (synonym PRIVATE) allocates 
the packset on a private basis.  SHARED (synonym PUBLIC) allocates the packset 
on a public bases.  Note that a packset is exclusive or shared depending on 
how it is mounted by the operator. 
ACC[OUNT]=({a[,a]...|NO})   -   specifies accounts that must be present on the 
system.  This is convenient for user's who are unfamiliar with the packset on 
which a particular account resides.  The default is the running account.  If 
even the running accounts home packset is not required, NO is specified. 
LP[dd][({APL|OVERPRINT|LC})][=n]   -   specifies the type and number of line 
printers.  LP01 or LP are permanently reserved and cannot be allocated as a 
resource by a user.  A combination of attributes (APL for an APL drum, 
OVERPRINT for a printer capable of true overstriking, and LC for 
Upper/Lowercase print element) can be specified, as long as each attribute is 
separated by commas.  The default for n is 1.  This is only required when a 
line printer is reserved as a resource. 
CP[dd][({BIN|LC})][=n]   -   specifies the type and number card punch or card 
image output devices (CP or CP01).  BIN names binary output.  LC means 
lowercase output.  The default for n is 1.  This is only required when a card 
punch or card image output device is reserved as a resource. 
Pseudo-resources, which are installation-defined resources used for special 
job-scheduling tasks may also be specified. 
Description: 
Resources are parts of the computer system that must be present for a 
particular job to successfully execute. 
Examples: 
!RESOURCE MEM=256,LT=2 
means the current batch job requires 256K memory and two labeled tapes (and 
thus two tape drives). 
!ORES ACC=NO,LP(OVERPRINT) 
means that the user's account need not be on the system when the job runs, and 
that a line printer with overstrike capability will be required. 
Usage: 
The RESOURCELIST component is used in the ACQUIRE, ORESOURCE, and RESOURCE 
commands. 
00002
00003
00001
00004
RESOURCELIST
Syntax: 
RESTORE fid 
Parameters: 
fid   -   specifies the name of the file to be restored.  This file must be in 
the user's logon account. 
Description: 
RESTORE (a synonym for the GET command) recalls an interrupted activity that 
has been saved in mid-execution via the SAVE command. 
Examples: 
!RESTORE EXECSAVEAREA 
means fetch an interrupted activity which has previously been SAVEd in the 
file EXECSAVEAREA. 
Related Commands: 
GET, SAVE 
00002
00003
00001
00004
Syntax: 
REW[IND] fid 
Parameters: 
fid   -   is a CP-6 tape fid. 
Description: 
REWIND rewinds a tape to its beginning or load point. 
Examples: 
!REW FT#1234 
!REW LT#ABCD 
means rewind free tape #1234 then rewinds the labeled tape #ABCD. 
Related Commands: 
See the PCL Help Facility 
00002
00003
00001
00004
Syntax: 
RUM fid 
Parameters: 
fid   -   identifies the run unit to be patched. 
Description: 
RUM fetches a run unit and invokes DELTA to process permanent patches against 
it. 
See the CP-6 DELTA Reference Manual (CE39) for further information on the 
methods available for patching. 
Examples: 
!RUM EXAMPLE 
Causes the run unit EXAMPLE to be fetched and allows permanent patches to be 
applied to it. 
Related Commands: 
DELTA, UNDER 
00002
00003
00001
00004
Syntax: 
RUN fid[,fid]...[,][tree][{ON|OVER} rununit,listfid[(option[,option]...)] 
Parameters: 
fid   -   specifies an object file or a run unit file.  If an object file is 
specified, all of the object units in the file are included.  If a run unit is 
specified, only information concerning defined symbols in the file is used; no 
procedure or data is extracted from the run unit file.  Using run unit files, 
the LINK Processor can satisfy references to symbols that are offsets from 
defined memory images. 
tree   -   optionally specifies a tree structure. 
ON   -   specifies that if the value for rununit identifies a file that 
already exists, the existing file is not to be overwritten. 
OVER   -   specifies that if the value for rununit identifies a file that 
already exists, the existing file is to be overwritten.  If neither ON nor 
OVER is specified the default is OVER. 
rununit   -   identifies the file to contain the run unit. 
listfid   -   identifies file for listing output. 
options   -   options are enclosed in a set of parentheses.  If more than one 
option is specified, options are separated by commas: 
ALT[SHARELIB]=libfid 
AS[LIB] 
B[REF]=value 
CONC{[=YES]|=NO} 
DB[IAS]=address 
DC[BSLOTS]=value 
{DCB1|SI[DCB]}=dcbname 
{DCB2|UI[DCB]}=dcbname 
{DCB3|OU[DCB]}=dcbname 
{DCB4|LO[DCB]}=dcbname 
DP[ATCH]=value 
DU[PLICATE] 
I[NCLUDE] ( (nodename,libfid,pen) [,(nodename,libfid,pen ...] ) 
IP[ATCH]=value 
IXT[NSIZE]=value 
LIBSR[CH](ac1[,ac2]...) 
LL[MU] 
LS[AU] 
M[AP]([{N[AME]|V[ALUE]|L[DEF]|U[DEF]} [,{N[AME]|V[ALUE]|L[DEF]|U[DEF]}]...]) 
NB[REF] 
{NDCB1|NSI[DCB]} 
{NDCB2|NUI[DCB]} 
{NDCB3|NOU[DCB]} 
{NDCB4|NLO[DCB]} 
NOALT[SHARELIB] 
NOC[HGPMEM] 
{NOD[EBUG]|ND} 
NOE[DITING] 
NOSH[ARELIB] 
{NOSY[SLIB]|NL} 
NPL[OVER] 
NWA[RN] 
OS[P] 
PB[IAS]=address 
PRI[VILEGES]{=priv|[=](priv[,priv]...)} 
PR[OCACC] 
PROMOTE 
PROMOTE_B[LANK] 
PROMOTE_L[ABEL] 
PSEUDO=(resnm[,decimal_number]) 
RE[PORT]=value 
SE[VERITY]=value 
{SHAREA[BLE]|NSHAREA[BLE]} 
SHAREL[IB]=libfid 
SL[IB] 
SLOCK(lock[,lock]...) 
SR[CH](ac1 [,ac2]...) 
ST[ART]=address 
STD[INVOC] 
SUR[CHARGE] 
SY[STEM] 
TC[B]=value 
UN[SAT]={libfid|(libfid,libfid[,libfid...])} 
V[ECTOR](option[,option]...) 
VER[SION]={version|(version)} 
WA[RN] 
WLOCK(lock[,lock]...) 
XT[NSIZE]=value 
Description: 
The RUN command creates an executable program (run unit), optionally creates 
overlays, and submits the run unit for immediate execution. 
Related Commands: 
See LINK Help facility. 
00002
00001
00003
Syntax: 
rununit [.[account]] [fid1][,fid2] [{TO|ON|OVER|INTO} [fid3][,fid4]] 
  [(optionlist)] 
Parameters: 
rununit   -   specifies the fid of a run unit created by the LINK processor. 
[.[account]]   -   If . is not specified, fid comes from :SYS account.  If . 
is specified without account, fid comes from user's account.  If .account is 
specified, fid comes from specified account. 
fid1   -   specifies the fid to be associated as the run unit source input 
(M$SI) file. 
fid2   -   specifies the fid to be associated as the run unit update input 
(M$UI) file. 
ON or TO   -   specifies that if an object or list file already exists, the 
existing file is not to be overwritten, and the run unit command is to be 
aborted. 
OVER   -   specifies that if an object or listout file already exists, the 
existing file is to be overwritten, and the rununit command is to be 
processed. 
INTO   -   specifies that if an object or listout file already exists, new 
output is to be added to that file.  If either of the files does not exist, it 
is created. 
fid3   -   specifies the fid to be associated as the run unit output (M$OU) 
file. 
fid4   -   specifies the fid to be associated as the run unit listing output 
(M$LO) file for source and object listing. 
optionlist   -   specifies the options the run unit expects to receive and 
process.  The optionlist is not processed by IBEX other than to pass it to the 
run unit. 
Description: 
Any run unit may be fetched into memory and started by issuing the name of the 
run unit as an IBEX command verb.  The syntax is the same as that used to 
invoke a compiler and follows: 
Assignments of the files source, update, object and listout to the DCBs M$SI, 
M$OU, and M$LO is established through the LINK command that creates the run 
unit.  Note that is is a convention only; any DCB may be associated with the 
above command files. 
Use of the third or fourth positional fid in connection with multiple 
invocations of a run unit in a single session or job will cause file 
management to perform automatic file extension to that fid.  Automatic file 
extension is documented elsewhere in this manual. 
Note:  Certain processors, such as SORT/MERGE accept non-standard run-unit 
calls.  These features are documented in the reference manual for the 
individual processor. 
Examples: 
!EXAMPLE. EXAMPSRCE,EXAMPUPDT INTO EXAMPOUT,EXAMPLIST 
This rununit command fetches the run unit EXAMPLE from the current directory 
account into memory and starts execution using EXAMPSRCE as the source input 
file, EXAMPUPDT as the run unit update file, EXAMPOUT as the run unit output 
file, and EXAMPLIST as the run unit listing file. 
!ADVENTURE.DEMO 
Fetches and starts execution of the run unit ADVENTURE from the file 
management account DEMO. 
Related Commands: 
START 
00002
00003
00001
00004
START
Syntax: 
SAVE {ON|OVER} fid 
Parameters: 
ON   -   specifies that if the file identified by fid already exists, the 
existing file is not to be overwritten, and the SAVE command is to be aborted. 
OVER   -   specifies that if the file identified by fid already exists, the 
existing file can be overwritten. 
fid   -   specifies the name to be assigned to the file to contain the memory 
image of the saved activity.  This must be a disk fid.  Note that DCBs are 
closed as the result of a SAVE. 
Description: 
To SAVE an interrupted activity, the user issues the SAVE command.  The 
activity is stored as a file, which may then be retrieved via GET or RESTORE. 
Execution can then be resumed.  Note that the SAVE command is valid only at 
the double bang (!!) prompt.  The original run-unit file must exist for a 
saved image to be restored.  Refer to the description of 'XCON: SAVE Files/GET 
Process' in the Monitor Services Reference (CE74) for more detail. 
Examples: 
!!SAVE ON EXECSAVEAREA 
Saves an interrupted activity in the file EXECSAVEAREA, unless a file with 
that name already exists, in which case the command is aborted. 
!!SAVE OVER OLDSAVEPROG 
Saves the user's interrupted process into the file OLDSAVEPROG.  If a file 
with that name does not already exist, a file with that name is created. 
Related Commands: 
GET, RESTORE 
00002
00003
00001
00004
SCHED_STATES
To obtain information about the host user scheduler states, enter: 
!HELP (IBEX) SCHED_STATE state 
where state is the state designator.  For example, 
     HELP SCHED_STATE STI 
provides information on user scheduler state STI. 
To list all the host user scheduler states, type ??<CR> 
at the next prompt. 
The table has the following format: 
  State               Meaning 
SC1           Compute queue 1 (highest) 
SC2           Compute Queue 2 
SC3           Compute queue 3 
SC4           Compute queue 4 
SC5           Compute queue 5 
SC6           Compute queue 6 
SC7           Compute queue 7 
SC8           Compute queue 8 
SC9           Compute queue 9 
SC10          Compute queue 10 
SC11          Compute queue 11 (lowest) 
SCU           Current user 
SCOB          Blocked, doing output 
SIOW          I/O wait 
SIOC          ComGroup I/O wait 
SMF           Master Function Count too high 
SW            Waiting (asleep) 
SDSC          Disconnected (going through logoff ) 
SQA           Queued for access 
STI           Terminal Inputting 
SQC           Queued for I/O cache I/O 
SCW           Communications (FEP) I/O Wait 
SNUL          Null (no user) 
QRCQ          Queued for space in communications circular queue 
QRMM          Queued for resource memory 
QRNQ          Queued for an M$ENQued resource 
QRIO          Queued for an IOQ packet 
QRAP          Queued for array processor 
00028
00024
00027
00025
00026
00001
00010
00011
00002
00003
00004
00005
00006
00007
00008
00009
00013
00012
00022
00018
00015
00014
00016
00023
00019
00021
00020
00017
Syntax: 
SE[T] [ dcb [fid][,optionlist] ] 
Parameters: 
dcb   -   specifies the DCB name. 
fid   -   specifies the file assignment of the DCB. 
optionlist   -   specifies file and/or device attributes.  If the fid is 
omitted, a previous SET command must have been issued that made a fid 
assignment; the attributes specified on this SET command are added to any 
previously specified ones.  If the fid is specified, the previous assignment 
is replaced, so that all effects of any previous SET commands for this DCB are 
removed. 
Valid options are: 
ACC[ESS]=({ALL|account|(accountlist)}[,controllist]) 
ACS={J[RNL]|D[IRECT]|S[EQUEN]} 
ACSV[EH]=((processorlist)[,controllist]) 
ALLD[CBS]{[=YES]|=NO} 
ALLT[RMS]{[=YES]|=NO} 
ALT[KEYS]=((altkey_spec) [,(altkey_spec)...]) 
AN[YDCB]{[=YES]|=NO} 
AU{[=YES]|=NO} 
BLK[L]=value 
BLO[CKED]{[=YES]|=NO} 
BT[MBRDR]{[=YES]|=NO} 
BU[PM]{[=YES]|=NO} 
COM[P]{[=YES]|=NO} 
COP[IES]=value 
CT[G]{[=YES]|=NO} 
CV[OL]{[=YES]|=NO} 
DC[BCONLGL]{[=YES]|=NO} 
DEB[UG]{[=YES]|=NO} 
DE[NSITY]={800|1600|6250}[BPI] 
DIR[ONLY]{[=YES]|=NO} 
DIS[P]={NA[MED]|SC[RATCH]} 
DV[FC]={'value'|O'value'} 
EB[CDIC]{[=YES]|=NO}[(CN[VRT]{[=YES]|=NO})] 
EOFN[ONE]{[=YES]|=NO} 
EOFO[NE]{[=YES]|=NO} 
EOFT[IME]=value 
EV[ENT]=value 
EXI[ST]={E[RROR]|N[EWFILE]|O[LDFILE]} 
EXP[IRE]={value|N[EVER]} 
FO[RM]='formname' 
FP[RG_FID]=fid 
FS[N]=value 
FU[N]={C[REATE]|I[N]|U[PDATE]} 
FW[INDOW]=name 
GH[STACS]={value|JRNLOPN|NONE} 
HBRDRC[HR]=c 
HBRDRS[IZ]=value 
HD[RHEIGHT]=value 
IG[NOREFSN]{[=YES]|=NO} 
ILA[TCH]{[=YES]|=NO} 
ILO[CK]{[=YES]|=NO} 
IM[SGTYP]=text 
IN[DENT]=value 
INITI[ALIZE]{[=YES]|=NO} 
INITV[ALUE]=value 
INSTATTR={attr_opt|(attr_opt [,attr_opt...])} 
INSTATTRS[IZE]=value 
IO[ERROK]{[=YES|=NO} 
IS[TATION]=station 
IX[TNSIZE]=value 
JRNLB[YPASS]{[=YES]|=NO} 
KEYL=value 
KEYX=value 
LD[BYPRO]=value 
LFT[BRDR]{[=YES]|=NO} 
LI[NES]=value 
LO[AD]{[=YES]|=NO} 
LR[DLO]=value 
LS[LIDE]=value 
LST[AOR]{[=YES]|=NO} 
MAR[GIN]=value 
MAX[VOL]=value 
MINL[ENGTH]=value 
MI[NPHYS]=value 
MINW[IDTH]=value 
MY[STATION]=station 
NO[FILE]{[=YES]|=NO} 
N[RECS]=value 
OLA[TCH]{[=YES]|=NO} 
OLO[CK]{[=YES]|=NO} 
OM[SGTYP]=text 
OPT[IONAL]{[=YES]|=NO} 
OR[G]=organization 
OS[TATION]=station 
P[AGECOLUMN]=value 
PH[YSICAL]=value 
PO[SITION]= option 
PROCATTR={attr_opt|(attr_opt[,attr_opt...)] 
PROCATTRS[IZE]=value 
PROF[ILE]=name 
Q[ISS]{[=YES]|=NO} 
{RD|RE[AD]}={ALL|account|(accountlist)} 
REC[L]=value 
RES[ETPAGE]=YES 
RH[TBRDR]{[=YES]|=NO} 
SC[RUB]{[=YES]|=NO} 
SEE[D]=(octstr|"charstr"|NONE) 
SEGN[UM]={VS1|VS2|VS3} 
SEGS[IZE]=value 
SEQ{[=YES]|=NO} 
SEQC[OL]=value 
SEQI[D]='string' 
SN={packsetname|(seriallist)} 
SH[ARE]={A[LL]|I[N]|N[ONE]} 
SPAN[NED]{[=YES]|=NO} 
SPAR[E]=value 
TA[B]=(tablist) 
TE[RMCONLGL]{[=YES]|=NO} 
TI[TLE]='string' 
TO[PBRDR]{[=YES]|=NO} 
TY[PE]=value 
UATTR={attr_opt|(attr_opt[,attr_opt...])} 
UATTRS[IZE]=value 
UOPTn{[=YES]|=NO} 
VBRDRC[HR]=c 
VBRDRS[IZ]= value 
V[OL]=value 
VOLA[CCESS]={A[LL]|I[N]|N[ONE]} 
WR[ITE]={ALL|account|(accountlist)} 
W[AS]{[=YES]|=NO} 
WL[ENGTH]=value 
WW[IDTH]=value 
XTE[ND]{[=YES]|=NO} 
XTN[SIZE]=value 
Type HELP SET_OPS for complete descriptions. 
Description: 
If no fid or optionlist is present in the command, then SET will display DCB 
SETs.  If a DCB is present in the command, only the SETs for that DCB will be 
displayed; otherwise, the SETs for all DCBs will be displayed. 
If a fid or optionlist is present in the command, then SET makes DCB and 
attribute assignments to disk, tape and unit record files, and exclusive 
devices.  Attribute values are assigned initially either in the processor 
(user program or system processor) or by the LINK Processor.  The SET command 
options are used to re-assign those initial values at job steps.  The DCB 
assignments and options values assigned by the SET command remain effective 
throughout the job or session unless modified: 
o   At a subsequent job step by another SET command. 
o   At a subsequent job step by a RESET command which resets some or all DCB 
    parameter values to the default assignments by deleting the existing 
    assignments. 
o   During the job step by the ADJUST command.  ADJUST assigns the specified 
    option values to the specified DCB; but, the assignment does not survive 
    the job step. 
Examples: 
!SET M$LO MYFILE.A.PSWRD 
Assigns the DCB named M$LO to disk file MYFILE, in account A with password 
PSWRD. 
!SET M$SI MT#FDATA,ORG=FIXED,RECL=80,BLKL=800,FUN=IN 
Assigns the M$SI DCB to a managed tape file named FDATA.  The user declares 
that the file contains fixed length records with no control information 
(ORG=FIXED), that each record is 80 bytes long, and that each block contains 
800 bytes.  The file will be opened for input only (FUN=IN). 
!SET M$LO LT#4003/MYFILE..PSWRD 
Assigns the DCB named M$LO to a file named MYFILE in the running account and 
defines the output media to be a labeled tape with the serial number 4003. 
!SET M$LO LT#VOLMA1#VOLMA2#VOLMA3/MYFILE 
Assigns the M$LO DCB to a labeled tape file named MYFILE on a volume set 
containing the volumes VOLMA1, VOLMA2 and VOLMA3. 
!SET M$LO LP@BOSTON,FORM='CHECKS' 
Assigns the M$LO DCB to a line printer device at workstation BOSTON as the 
destination for listing output and specifies that the form defined in the Form 
Definition File as CHECKS is to be mounted. 
!SET M$LO,TAB=(27,38,47,75),MAR=10,LI=55 
Re-assigns page formatting options for tabs, margins and number of lines per 
logical page of output. 
!SET M$EO OUTFILE,EXIST=OLDFILE,READ=(ACCTA,ACCTB) 
Assigns the M$EO DCB to disk file OUTFILE, and establishes that if OUTFILE 
already exists, new output is to be appended to the existing file.  Also, 
gives users in accounts ACCTA and ACCTB permission to read (but not write) the 
contents of the file. 
!SET M$DATABASE STUDENTS,; 
ACCESS=((ADMIN),READ,DELREC,WNEW,UPDATE,DELFILE),; 
ACCESS=((TEACHERS),READ,UPDATE),; 
ACCESS=((REGISTR),WNEW,DELREC,READ) 
Assigns the M$DATABASE DCB to the file STUDENTS and establishes three 
different file permission lists for the three accounts ADMIN, TEACHERS, and 
REGISTR. 
Related Commands: 
RESET, ADJUST 
00002
00003
00001
00004
SET_OPS
Syntax: 
SETUP {!command|RESET} 
Parameters: 
command   -   is any IBEX command.  The command prompt (!) must precede the 
command verb. 
RESET   -   clears all previous SETUP command entries. 
If more than one SETUP command is issued, the new SETUP command replaces 
previous SETUP commands. 
Description: 
SETUP specifies an IBEX command which is to be executed immediately following 
each logon to the system.  This gives the user the opportunity to have a 
command executed automatically whenever anyone logs on to the particular 
logon-id. 
Examples: 
!SETUP !XEQ SETUPS 
executes the file SETUPS which may contain multiple commands to be executed 
automatically after each logon. 
!SETUP !PROTECT 
specifies that the PROTECT command is to be executed automatically after each 
logon to the user account. 
!SETUP RESET 
deletes the previous SETUP command entry. 
Related Commands: 
NONE 
00002
00003
00001
00004
The options for the SET command can be categorized into the following groups. 
Alternate 
Keyed Files:         ALTKEYS 
Disk Files:          BUPM, COMP, CTG, DISP, EXIST, IXTNSIZE, LOAD, 
                     LRDL0, LSLIDE, SEED, SHARE, SPARE, XTNSIZE 
Disk and             ACCESS, ACS, ACSVEH, EXPIRE, FUN, KEYL, KEYX, 
Labeled Tape Files:  NRECS, ORG, READ, RECL, SN, TYPE, WRITE 
Labeled Tape:        BLKL, BLOCKED, FSN, IGNOREFSN, VOLACCESS, XTEND 
Labeled and/or 
Free Tape:           CVOL, DENSITY, EBCDIC, IOERROK, MAXVOL, SPANNED 
                     VOL 
Unit Record Devices 
(and Files:)         COPIES, DVFC, FORM, HDRHEIGHT, INDENT, INITIALIZE, 
                     INITVALUE, LINES, MARGIN, PAGECOLUMN, RESET, SEQ, 
                     SEQCOL, SEQID, TAB, TITLE 
Comgroups:           ALLDCBS, ALLTRMS, ANYDCB, AU, ILATCH, DEBUG, 
                     DCBONLGL, DIRONLY, EOFNONE, EOFONE, ILOCK, IMSGTYP, 
                     ISTATION, JRNLBYPASS, LSTAOAR, MYSTATION, OLATCH, 
                     OLOCK, OMSGTYP, OSTATION, QISS, WAS 
User Applications:   UOPT 
Virtual areas:       MINPHYS, PHYSICAL, SEGNUM, SEGSIZE 
Windows:             BTMBRDR, FWINDOW, HBRDRCHR, HBRDRSIZ, LFTBRDR, MINLENGTH, 
                     MINWIDTH, OPTIONAL, POSITION, RHTBRDR, TOPBRDR, VBRDRCHR, 
                     VBRDRSIZ, WLENGTH, WWIDTH 
FEP Prog (FPRG):     EVENT, FPRG_FID, HANDLER, LDBYPRO, PROFILE 
Miscellaneous:       EOFTIME, GHSTACS, NOFILE 
                      Type HELP (IBEX) SET_OPS option for complete 
                     description. 
The detailed meanings of these options can be found in the M$DCB, M$OPEN, 
M$READ, and M$WRITE descriptions in the Host Monitor Services Reference, CE74. 
  Opt         Meaning 
  ACC[ESS]=({ALL|account|(accountlist)}[,controllist]) 
        Establishes associated accounts and their permission. 
        ALL   -   specifies access control of all accounts. 
        account   -   specifies access control of text account. 
        accountlist   -   is one or more account names separated by commas. 
        The account names may include wildcard characters. 
        controllist   -   contains one or more of the following values 
        separated by commas: 
        Value           Access Authorized 
        -----           ----------------- 
        AU              Meaningful for comgroups only.  If set, this 
                        user is allowed to be the administrative user 
        AURD            Meaningful for comgroups only.  If set, this 
                        user is allowed to issue monitor services 
                        normally reserved for the administrative user 
                        that examine but do not change the comgroup. 
        DELR[ECORD]     Delete records. 
        DELF[ILE]       Delete files, change file name, password, 
                        ACCESS and ACSVEH. 
        E[XECUTE]    Means execute-only; access to a file depends on the 
                     process opening the file.  The opening process is 
                     defined as the name and account of the rununit 
                     associated with the execution domain (user, monitor, 
                     debugger, ASL, or command processor) that is 
                     performing the open request. If the execution domain 
                     is the monitor and the file is being opened for the 
                     purpose of executing it as a user program, then the 
                     process is to be referred to as FETCH[.:SYS]. 
                     If the opener is in the ACSVEH processorlist, then 
                     the ACSVEH controllist specifies the access the opener 
                     gets. 
                     If the opener is not in the ACSVEH processorlist, 
                     then one of two actions occurs: 
                     1)  if the opener is the monitor process called 
                         FETCH, then the program is allowed to run (i.e., 
                         for every file the ASCVEH list is presumed to 
                         include FETCH=READ.) 
                     2)  if the opener is not FETCH, the opener gets any 
                         other controls specified along with EXEC in 
                         controllist. 
        N[OLIST]        Suppress inclusion of file directory 
                        information from catalog listings. 
        READ            Read, or position and read a file. 
        TCTL            Meaningful for comgroups only.  If set, this 
                        user is allowed to issue terminal control 
                        monitor services (such as M$PROMPT and 
                        M$STRMATTR).  For ORG=FPRG comgroups, M$SETFP 
                        is allowed. 
        REAT[TRIBUTES]  Change file attributes with the 
                        exception of ACCESS and ACSVEH 
                        (see DELF above). 
        U[PDATE]        Replace existing records. 
        W[NEW]          Add new records to the file. 
        If controllist is omitted, the identified account or accounts are 
        denied all access.  The default permissions are attributes of the 
        file's account. 
        ACCESS applies to disk files.  The E, N, READ, and W permissions also 
        apply to labeled tapes. 
  ACS={J[RNL]|D[IRECT]|S[EQUEN]} 
        Defines how access will occur:  directly, sequentially, or in journal 
        mode. 
        D[IRECT]   -   specifies that when creating or updating a keyed or 
        indexed file, keys have no sequence restrictions. 
        J[RNL]   -   specifies that the file will be used in journal mode, 
        that is: 
        1.  The file is opened in create mode and the initial opener is the 
        owner. 
        2.  Subsequent opens by other users are in update mode. 
        3.  The file becomes unavailable for update when the owner closes the 
        file. 
        S[EQUEN]   -   specifies that when creating or updating a keyed file, 
        keys must be given in ascending order. 
        ACS applies to disk files.  Labeled tapes can be D, J, or S.  Free 
        tapes must be S. 
  ACSV[EH]=((processorlist)[,controllist]) 
        Defines a vehicle control list that allows the file creator to control 
        access by limiting it to processors.  ACSVEH applies only when the 
        effective access controllist for the opener's account includes the 
        EXECUTE control. 
        processorlist   -   identifies one or more processors by name. 
        Members of the list are separated by commas.  A processor is defined 
        as any run unit with optional account specification.  If the account 
        is not specified, :SYS is assumed (BASIC, EDIT, etc.).  If a period 
        follows the name, but no account is specified, the processor must 
        exist in the same account as the file.  See controllist below. 
        controllist   -   specifies the permissions to be granted to the 
        processor list.  Entries are the same as those listed under the ACCESS 
        option.  If the controllist is omitted, the processors identified in 
        the processor list are denied all access. 
        ACSVEH applies to disk files and labeled tapes. 
        In order to preclude file security problems, run units used as access 
        vehicles must reside in accounts which have been added to the Master 
        Account Directory (MAD), or the check for access vehicles will not be 
        performed when the file is opened, i.e., file management will open the 
        file as though it had no access vehicle control list. 
        Note:  For name wild-carding as applied to ACSVEH, only a trailing 
        question mark on the name portion is honored. 
  ALLD[CBS]{[=YES]|=NO} 
        Applies to comgroups.  Specifies the default value for ALLDCBS on 
        reads through this DCB.  If ALLDCBS is set here, ALLDCBS on the 
        M$WRITE is ignored. 
        ALLDCBS applies only on a write when STATION is wild-carded.  YES 
        specifies that the message is to be written to ALL DCB stations with 
        names that qualify with STATION.  NO, the default, says to send the 
        message to any one qualified station.  (unless ALLTRMS is YES). 
  ALLT[RMS]{[=YES]|=NO} 
        Applies to comgroups.  Specifies the default value for ALLTRMS on 
        reads through this DCB.  If ALLTRMS is set here, ALLTRMS on the 
        M$WRITE is ignored. 
        ALLTRMS applies only on a write when STATION is wild carded.  YES 
        specifies that the message is to be written to ALL terminal stations 
        with names that qualify with STATION.  NO, the default, says to send 
        the message to any one qualified station.  (unless ALLDCBS is YES). 
  ALT[KEYS]=((altkey_spec) [,(altkey_spec)...]) 
        Creates an area describing alternate index keys for indexed files. 
        Used on create opens or on closes. 
        altkey_spec   -   is the following: 
        [{KEYL|L}=l,[{KEYX|X}=x,[U[NIQUE]{[=YES]|=NO}] 
        KEYL=l   -   specifies the length of the key for this index as an 
        integer value from 1 to 255.  The default is one. 
        KEYX=x   -   specifies the byte offset into the record of the 
        beginning of this key as an integer value from 0 to 4000.  The default 
        is zero. 
        UNIQUE{[=YES]|=NO}   -   if YES, then the keys in this index must be 
        unique.  If a record is written which contains a key with the same 
        value as an existing key, the write will fail.  If UNIQUE=NO, 
        duplicate entries will be created if several records have the same key 
        value.  The order of the records for the duplicate keys is the order 
        of arrival of the records. 
  AN[YDCB]{[=YES]|=NO} 
        Applies to comgroups.  Specifies the default value for ANYDCB on reads 
        through this DCB.  If ANYDCB is set here, ANYDCB on the M$WRITE is 
        ignored. 
        When used with M$WRITE, YES specifies that this M$WRITE is directed to 
        any DCB station.  The message is treated as though it came in from a 
        terminal and STATION is ignored.  NO, the default, says to use STATION 
        to direct the write. 
  AU{[=YES]|=NO} 
        Applies to comgroups.  Indicates whether or not the user is to be the 
        administrative user. 
  BLK[L]=value 
        Specifies the maximum physical tape record size (in bytes) that will 
        be read from or written to a labeled tape. 
        value   -   is a decimal from 1 to 32764.  The default and maximum 
        value allowed vary by tape format.  See Appendix E, tables E-1 and 
        E-2, for format-dependent defaults and maximum values. 
        For labeled tape IN or UPDATE functions, the BLKL value is set to the 
        value of the file opened.  For managed tape, BLKL must be specified 
        for IN, UPDATE, and CREATE. 
        BLKL applies to fixed and variable files with blocked records on 
        labeled tape. 
  BLO[CKED]{[=YES]|=NO} 
        Controls packing of logical records into physical tape records. 
        YES   -   specifies that logical records and record segments are to be 
        packed into physical tape records.  This is the default. 
        NO   -   specifies that no more than one logical record or record 
        segment is to be included in a physical tape record. 
        For labeled tape IN or UPDATE functions, BLOCKED is determined from 
        the tape file opened.  For managed tape files, BLOCKED must be 
        specified for IN, UPDATE, and CREATE.  Blocked should be used in 
        conjunction with SPANNED for optimum tape record utilization. 
        BLOCKED applies to variable files with blocked records on labeled 
        tapes (VF tape formats). 
  BT[MBRDR]{[=YES]|=NO} 
        Specifies whether space is to be reserved at the bottom to separate 
        this window from the one below it.  The default is NO for a new 
        window. 
  BU[PM]{[=YES]|=NO} 
        YES   -   specifies that the file is to be backed up if modified. 
        NO   -   specifies that the file is not to be backed up. 
        The default is an attribute of the file's account. 
        BUPM applies only when creating a disk file. 
  COM[P]{[=YES]|=NO} 
        YES   -   specifies that records are to be written in compressed 
        format. 
        NO   -   specifies that records are not to be compressed.  This is the 
        default. 
        COMP applies only when creating CONSECUTIVE and KEYED disk files. 
  COP[IES]=value 
        Specifies the number of copies of this file to be printed.  Note that 
        at least one copy will be printed. 
        COPIES applies only to devices and when creating unit-record files. 
  CT[G]{[=YES]|=NO} 
        CTG determines whether a file is catalogued at open time. 
        YES   -   specifies that the file is catalogued at open time. 
        NO   -   specifies that the file is not to be catalogued until it is 
        closed (if at all).  This is the default. 
        CTG applies only when creating a disk file. 
  CV[OL]{[=YES]|=NO} 
        Specifies that the user is to be notified of end of volume conditions. 
        YES   -   specifies that the user is to control end of volume tape 
        processing. 
        NO   -   specifies that volume changes are to be done automatically. 
        This is the default. 
        CVOL applies to multi-volume tape files with trailing labels. 
  DC[BCONLGL]{[=YES]|=NO} 
        Applies to comgroups.  Meaningful only if ORG = CG.  Specifies whether 
        DCBs are allowed to open to this comgroup.  The default is YES.  See 
        HELP(HOSTMON)VLP_CGCP for further information. 
  DEB[UG]{[=YES]|=NO} 
        Applies to comgroups.  Specifies, if yes, that this FPRG is to be 
        debugged and therefore is not to be started, but is to be held 
        awaiting commands from a debugger such as: 
            DEBUG <station> ON <comgroup> 
        DEBUG is only honored for comgroup station connected FPRGs since 
        DCB-connected FPRGs will be debugged if their owner is running under 
        control of a debugger when this M$SETFP is issued.  The default is NO. 
  DE[NSITY]={800|1600|6250}[BPI] 
        Specifies the recording density at which a tape is to be written. 
        800, 1600 and 6250 specify the tape density. 
        All following files are created at the same density as the first.  For 
        IN or UPDATE opens, DENSITY is determined from the tape volume 
        containing the opened file. 
        DENSITY applies only when creating the first file of a tape volume. 
  DIR[ONLY]{[=YES]|=NO} 
        Applies to comgroups.  Specifies the default value for DIRONLY on 
        reads through this DCB.  If DIRONLY is set here, DIRONLY on the M$READ 
        is ignored. 
        YES specifies that an M$READ will only read messages written to this 
        station, not those in the comgroup readable by anyone.  NO, the 
        default, allows both directed and undirected messages to be read. 
  DIS[P]={NA[MED]|SC[RATCH]} 
        Specifies whether a new file can be catalogued or not. 
        NAMED   -   specifies it will be named and can be catalogued.  This is 
        the default. 
        SCRATCH   -   specifies that the new file is a scratch file. 
        DISP applies only when creating a disk file. 
  DV[FC]={'value'|O'value'} 
        Specifies the default vertical format control character for records 
        with no vertical format control. 
        value   -   specifies a vertical format control character. 
        O'value'   -   specifies the DVFC character in octal. 
        DVFC applies to unit record files, unit record and logical devices. 
  EB[CDIC]{[=YES]|=NO}[(CN[VRT]{[=YES]|=NO})] 
        YES   -   specifies that input/output translation of labels is to 
        occur. 
        NO   -   specifies that input/output translation of labels is not to 
        occur.  This is the default. 
        CNVRT   -   specifies whether data is to be translated (=YES) or not 
        (=NO).  The default is NO. 
        Note that EBCDIC controls conversion of tape file labels, user labels 
        and the data itself.  EBCDIC files cannot be created on ASCII volumes 
        and vice verse. 
        EBCDIC applies to tape files whose organization is FIXED, VARIABLE, 
        UNDEF.  EBCDIC can be explicitly established only when the tape file 
        is being created, and only if the file is the first file in the 
        volume.  Otherwise, EBCDIC is determined from the current volume. 
  EOFN[ONE]{[=YES]|=NO} 
        Applies to comgroups.  Specifies the default value for EOFNONE on 
        reads through this DCB.  If EOFNONE is set here, EOFNONE on the M$READ 
        is ignored. 
  EOFO[NE]{[=YES]|=NO} 
        Applies to comgroups.  YES specifies that only one message can be read 
        through this DCB.  After that message has been successfully read, all 
        subsequent M$READs will return END-OF-FILE.  EOFONE overrides EOFNONE 
        above or on the M$READ. 
        When used with M$READ, YES specifies that if a read cannot be 
        satisfied from data currently in the comgroup (as opposed to messages 
        received later from other sections) END-OF-FILE will be given on the 
        M$READ.  NO specifies that the read will remain active until an 
        appropriate message arrives in the comgroup.  EOFNONE has no effect on 
        M$WRITE.  The default is NO. 
  EOFT[IME]=value 
        Specifies the number of seconds to leave this read pending before 
        timing it out with END-OF-FILE.  If EOFTIME is set on the M$READ, 
        EOFTIME is ignored here. 
        The VLP field name of this parameter is VLP_SETSTA.ISTA.EOFTIME#. 
        The default is 0. 
        value   -   is a decimal integer from 0 to 262143. 
  EV[ENT]=value 
        Specifies an event number to be returned to the user of this 
        ASN=DEVICE DCB when B$COMIO events or FPRG-related events are returned 
        to the user.  Zero indicates not to return these events.  The default 
        causes this parameter to be ignored. 
        value   -   is a decimal integer from 0 to 2**35-1 (that is, any 
        reasonable size). 
  EXI[ST]={E[RROR]|N[EWFILE]|O[LDFILE]} 
        ERROR   -   specifies that if the named file already exists, the new 
        file is not to be created; error processing is initiated. 
        NEWFILE   -   specifies that if the named file already exists, the new 
        file is to replace the existing one.  This is the default. 
        OLDFILE   -   specifies that if the named file already exists, the new 
        file is to be appended to the existing file. 
        EXIST applies only when creating a disk file whose DISPOSITION is 
        NAMED. 
  EXP[IRE]={value|N[EVER]} 
        For disk files, determines how long to retain a file.  For EBCDIC and 
        ANS tapes, determines the expiration date of the volume set. 
        value   -   is a decimal number from 0 to the user's limit that 
        specifies the number of days to retain the file.  The upper limit and 
        default are established by the system manager for the user. 
        NEVER   -   specifies that the file is never to expire. 
        EXPIRE applies to CP-6 Disk files and the first file of labeled tape 
        volumes. 
  FO[RM]='formname' 
        Specifies the name of a form to be mounted on a unit record device. 
        formname   -   is a quoted 1 to 6 character string.  The name must 
        have been defined to the system by the system manager (via the Form 
        Definition File).  The default is blank, which means standard form for 
        unit record devices and form 'STDLP' for unit record files.  FORM 
        applies to unit record files and unit record devices. 
  FP[RG_FID]=fid 
        Specifies the name of the FEP program file to be loaded. 
        fid   -   is of the form 
            [DP[nn][#setname]/]name[.[account][.password]] 
        See CP-6 fid discussion in Section 2 for parameters. 
  FS[N]=value 
        Specifies the file sequence number for labeled tapes. 
        value   -   is a decimal number from 1 to 9999 that indicates the 
        position of the tape file relative to the beginning of the set.  The 
        first file of the volume set is numbered one. 
        If the function is CREATE, the user does not explicitly provide the 
        FSN.  If the function is IN or UPDATE and the file name is specified, 
        FSN specifies the number of the file at which to begin searching for 
        the named file.  If the function is IN or UPDATE and the file name is 
        not specified, FSN specifies, by number, the file. 
        FSN applies to labeled tape files whose function is IN or UPDATE. 
  FU[N]={C[REATE]|I[N]|U[PDATE]} 
        C[REATE]   -   specifies a new file is being created.  The file can be 
        read and modified.  An open with FUN=CREATE and EXIST=NEWFILE will be 
        interpreted as EXIST=NEWFILE if all of the following proves true: 
        1.  A filename is not specified. 
        2.  The previous open of this DCB in this session specifies 
        FUN=CREATE, EXIST=NEWFILE. 
        3.  A SET or RESET command for this DCB has not been issued since the 
        previous open. 
        IN   -   specifies that an existing file can be read, but not 
        modified.  This is the default.  An unlabeled tape opened with FUN=IN 
        may not be written. 
        UPDATE   -   specifies that an existing file can be read and modified. 
        FUN applies to disk or tape files, with a limited applicability for 
        devices. 
  FW[INDOW]=name 
        Specifies the four-character name of a stream in an adjacent window 
        that is to supply or receive any space indicated by the WWIDTH or 
        WLENGTH options. 
        name   -   is of the form 'UCnn' 
  GH[STACS]={value|JRNLOPN|NONE} 
        Specifies a function code to be passed to the system access ghost 
        prior to opening the DCB to a disk file.  The only currently 
        implemented code is JRNLOPN, which asks the ghost to open a journal, 
        either as the owner of this journal (see M$DCB.ACS) or to journal this 
        comgroup (see FPT_CGCTL.JRNLSTA).  The value NONE may be used to reset 
        to zero a previous non-zero value (either in the DCB for M$OPEN, or in 
        the file for M$CLOSE).  The default causes this parameter to be 
        ignored. 
        value   -   is a decimal integer from 0 to 15. 
  HBRDRC[HR]=c 
        Specifies the single ASCII character to be used to mark the horizontal 
        border space(s).  It will fill every character position of the 
        farthest line of the border space.  The default causes this parameter 
        to be ignored. 
        c   -   is a single ASCII character. 
  HBRDRS[IZ]=value 
        Specifies the size in lines of the horizontal border space(s) (TOPBRDR 
        and BTMBRDR).  The default is zero, which causes this parameter to be 
        ignored.  Note that the border presence parameters must be used to 
        remove a border - HBRDRSIZ=0 won't work. 
        value   -   is a decimal integer from 0 to 15. 
  HD[RHEIGHT]=value 
        Specifies the height of the page header area. 
        value   -   is a decimal number from 0 to 15 that specifies the number 
        of lines (including the title line) in the page header.  The default, 
        1, specifies that no blank lines are to follow the title line. 
        HDRHEIGHT applies to unit record files, and to unit record and logical 
        devices. 
  IG[NOREFSN] {[=YES]|=NO} 
        This option is meaningful only for labeled tape files.  If 
        IGNOREFSN=NO, each tape file is located by the file sequence number in 
        its HDR1 label before it is opened.  If such a file sequence number is 
        not correct, the file may not be found.  In addition, when 
        IGNOREFSN=NO, the first file section of each tape file is required, 
        and, if it is not present, the open will fail with an error message. 
        If IGNOREFSN=YES, tape file management will not check the file 
        sequence number of a tape file when it is being opened.  In addition, 
        if the first file section does not exist, the first file section found 
        (which may or may not be the earliest file section of the file) is 
        used.  With this capability, a user may successfully read all the 
        files on many types of malformed or partial tape sets. 
        IGNOREFSN=YES causes file sequence numbers to be ignored only when 
        used in combination with NXTF, or when opening a tape file by name. 
        If IGNOREFSN=YES when opening a tape file by file sequence number, 
        only the file section is ignored.  If IGNOREFSN=YES when opening a 
        tape file by name, the search will stop at the end of the tape (set). 
        Note that if a non-first file section is used and bad spanning 
        information is present (due to a record being spanned from a previous 
        section which is not present or was not found), TYC.DI will be set in 
        the DCB.  No error message will be generated, and the partial record 
        will be processed as if it were the first record in the file.  The 
        default causes this parameter to be ignored. 
  ILA[TCH]{[=YES]|=NO} 
        Applies to comgroups.  Specifies the default value for LATCH on reads 
        through this DCB.  If ILATCH is set, LATCH on the M$READ is ignored. 
  ILO[CK]{[=YES]|=NO} 
        Applies to comgroups.  ILOCK = NO specifies that the values given here 
        for IMSGTYP, ISTATION, DIRONLY, EOFNONE, and ILATCH are simply 
        defaults to be applied when an M$READ fails to specify their analogs. 
        ILOCK = YES specifies that these values are not only defaults but may 
        not be overridden on M$READ. 
        ILOCK = YES has the following specific effects:  If STATION is 
        specified on M$READ then the STATION and MSGTYP therein must either be 
        blank or match ISTATION and IMSGTYP respectively, at least up to the 
        wild-card character (if any) in the latter.  Specifying blanks for 
        ISTATION (respectively IMSGTYP) causes no restraint to be placed on 
        STATION (respectively MSGTYP) on M$READ.  For the control options 
        (EOFNONE, LATCH, and DIRONLY), the specifications given here are 
        honored instead of those specified on M$READ; furthermore, an M$READ 
        is illegal if it attempts to specify YES for a control option 
        specified as NO here. 
        ILOCK = NO has the following specific effects:  If an M$READ supplies 
        no station parameter, the values specified here are used.  If an 
        M$READ specifies blanks for STATION (respectively MSGTYP) the ISTATION 
        (respectively IMSGTYP) specified here is used.  For the control 
        options, the resultant specification is YES if YES is specified either 
        here or on M$READ.  In other words, if the control option is specified 
        as YES here, it is ignored on M$READ and treated as YES; if the 
        control option is specified as NO here, the value specified on M$READ 
        is honored.  The default is NO. 
  IM[SGTYP]=text 
        Applies to comgroups.  Specifies the default value for MSGTYP on reads 
        through this DCB. 
  IN[DENT]=value 
        Specifies the starting column for TITLE line text. 
        value   -   is a decimal number from 1 to 255 that indicates the 
        starting column relative to the leftmost column position.  The default 
        is column 1. 
        Applicable to unit record files, unit record, and logical devices. 
  INITI[ALIZE]{[=YES]|=NO} 
        YES specifies that any page that has not been accessed before, and 
        does not exist in the paging file, will be initialized to the value 
        specified in INITVALUE.  NO specifies that initialization will not be 
        done; the contents of the page is unchanged.  The default is NO. 
  INITV[ALUE]=value 
        Value will be used when INITIALIZE=YES is specified as the value that 
        the page is to be set to on the initial access of the page (if it does 
        not exist in the paging file). The default is 0. 
        value   -   is a decimal integer from 0 to 2**35-1 (that is, any 
        reasonable size). 
  INSTATTR={attr_opt|(attr_opt [,attr_opt...])} 
        attr_opt   -   is either: O'string' or 'string' 
        Specifies a value for the installation attributes.  Although the CP-6 
        system places no restrictions on setting this data, this parameter is 
        reserved for use by the installation manager.  The default is NIL. 
  INSTATTRS[IZE]=value 
        Specifies the size in words to reserve for the INSTATTR. 
        value   -   is a decimal integer from 0 to 262143. 
  IO[ERROK]{[=YES]|=NO} 
        Is meaningful only for tape files.  If IOERROK=NO, tape I/O errors 
        cause the tape position to be lost, and no further operations are 
        allowed except rewind or dismount.  (The user may then reissue the 
        failed read, write or position operation with IOERROK set in the FPT.) 
        If IOERROK=YES, tape file management will try to recover from I/O 
        errors as completely as possible.  The action taken depends on the 
        operation in progress at the time of the error.  In particular, no 
        errors will be returned during the processing of an I/O error. 
        Various bits in the TYC will, however, be set to indicate the I/O 
        error itself, as well as data inconsistencies or lost data.  The 
        default causes this parameter to be ignored. 
  IS[TATION]=station 
        Applies to comgroups.  Specifies the default value for STATION on 
        reads through this DCB. 
        station   -   is a valid station name, from one to eight characters. 
  IX[TNSIZE]=value 
        Specifies the initial extent of a new disk file. 
        value   -   is a decimal number from 1 to 2**35-1 (that is, any 
        reasonable size) that specifies the initial extent in number of 
        granules.  The default is 2. 
        IXTNSIZE applies only when creating a disk file. 
        IXTNSIZE is ignored for files whose organization is RELATIVE. 
  JRNLB[YPASS]{[=YES]|=NO} 
        YES specifies that for opens of comgroups that have the journaling 
        attribute, journaling is not to be done for this open.  AU=YES must 
        also be specified.  The default is NO. 
  KEYL=value 
        Specifies the length of a key for an indexed file. 
        value   -   is a decimal number from 1 to 255 that specifies (in 
        bytes) the length of the key. 
        KEYL applies when creating INDEXED disk and tape files. 
  KEYX=value 
        Specifies the key starting position for an indexed file. 
        value    is a decimal number from 0 to 32000 that specifies (in bytes) 
        the starting position of the key. 
        KEYX applies when creating INDEXED disk and tape files. 
  LD[BYPRO]=value 
        Specifies, if non-zero, that the FPRG is to be found from the 
        associated PROFILE, not from this VLP.  See PROFILE (below). 
        value    is a decimal integer from 0 to 511. 
  LFT[BRDR]{[=YES]|=NO} 
        Specifies whether space is to be reserved at the left to separate this 
        window from the one to the left.  The default is NO for a new window. 
  LI[NES]=value 
        Specifies the number of print lines on a logical page of output. 
        value    is a decimal number from 1 to 32000 that specifies the number 
        of printable lines on a page.  If not specified, the default is the 
        number of lines contained in the FORM definition established by the 
        system manager.  The LINES on a SET do not override the FORM 
        definition. 
        LINES applies to unit record files, unit record devices, and logical 
        devices. 
  LO[AD]{[=YES]|=NO} 
        Meaningful only for files written with alternate indices.  YES 
        specifies that when records are written keys are to be entered into 
        the primary index only - alternate indices are to be built or rebuilt 
        at a later time.  The default is NO. 
  LR[DL0]=value 
        Specifies the maximum number of contiguous blocks the level 0 key 
        index may be expanded to. 
        value    is a decimal number from 1 to 511 that specifies a maximum 
        number of blocks.  If this number is exceeded, the higher level index 
        will be rebuilt when the file is closed.  The value 511 specifies that 
        a maximum number of blocks is not to be used as a reason for 
        rebuilding the higher level index.  The default is 3. 
        LRDL0 applies to KEYED and INDEXED disk files. 
  LS[LIDE]=value 
        Specifies the maximum number of blocks the level 0 key index may be 
        expanded to. 
        value    is a decimal number from 1 to 511 that specifies a total 
        number of blocks.  If this number is exceeded, the higher level index 
        will be rebuilt when the file is closed.  The value 511 specifies that 
        a total number of blocks is not to be used as a reason for rebuilding 
        the higher level index.  The default is 510. 
        LSLIDE applies to KEYED and INDEXED disk files. 
  LST[AOR]{[=YES]|=NO} 
        Specifies, for comgroups only, when the VLP_STATION pointed to by 
        DCB.LASTSTA$ is to be updated.  If YES, it is updated only on reads. 
        If NO, it is updated on both reads and writes.  The default causes 
        this parameter to be ignored. 
  MAR[GIN]=value 
        Specifies the lefthand margin for output lines. 
        value    is a decimal number from 1 to 255 that specifies the starting 
        column.  (The value 1 specifies no indentation.) 
        MARGIN applies to unit record files, and to unit record and logical 
        devices. 
  MAX[VOL]=value 
        Specifies maximum number of tapes to be used as scratch tapes to 
        supplement the explicit volumes requested by serial number. 
        value    is a decimal number from 1 to 511 that specifies the number 
        of extra tape volumes that will be requested. 
        MAXVOL applies to labeled and free tapes. 
  MINL[ENGTH]=value 
        Specifies the minimum length for this window in lines.  The default is 
        255, which causes this parameter to be ignored unless this is a new 
        window, in which case it means the the length is to be fixed.  See 
        OPTIONAL also. 
        value    is a decimal integer from 0 to 254. 
  MI[NPHYS]=value 
        Specifies the minimum number of physical pages backing the virtual 
        area.  This parameter determines the least number of pages that are 
        held within memory at any given time.  The parameter has a great 
        effect on the access speed of the virtual segment. 
        value    is a decimal integer from one to 16384.  The default is 10 
        pages. 
  MINW[IDTH]=value 
        Specifies the minimum width for this window in columns.  The default 
        is 255, which causes this parameter to be ignored unless this is a new 
        window, in which case it means that the width is to be fixed.  See 
        OPTIONAL also. 
        value    is a decimal integer from 0 to 254. 
  MY[STATION]=station 
        Applies to comgroups.  Specifies the station name that the DCB will 
        have on the comgroup. 
        station    is a valid station name from one to eight characters.  If 
        unspecified, a unique name is assigned by the system. 
        Since the default station name will (due to system assignment) be 
        different on each open, MYSTATION should be specified explicitly if 
        the DCB is to be written to explicitly. 
  NO[FILE]{[=YES]|=NO} 
        Specifies if the user wants control of the missing page faults or not. 
        If YES is specified, whenever a page needs to be paged in, the user 
        will get an event.  The user then can use M$CVM or M$GVP to allocate 
        that page. 
  N[RECS]=value 
        Specifies the number of records in a relative file. 
        value    is a decimal number from 1 to 2**35-1 (that is, any 
        reasonable number) that specifies the number of records in a file. 
        NRECS applies only when creating RELATIVE disk or tape files. 
  OLA[TCH]{[=YES]|=NO} 
        Applies to comgroups.  Specifies the default value for LATCH on writes 
        through this DCB.  If OLATCH is set, LATCH on the M$WRITE is ignored. 
  OLO[CK]{[=YES]|=NO} 
        Applies to comgroups.  OLOCK = NO specifies that the values given here 
        for OMSGTYP, OSTATION, WAS, ALLTRMS, ALLDCBS, ANYDCB, and OLATCH are 
        simply defaults to be applied when an M$WRITE fails to specify their 
        analogs.  OLOCK = YES specifies that these values are not only 
        defaults but may not be overridden on M$WRITE. 
        OLOCK = YES has the following specific effects:  If STATION is 
        specified on M$WRITE, the STATION and MSGTYP therein must either be 
        blank or match OSTATION and OMSGTYP respectively, at least up to the 
        wild-card character (if any) in the latter.  Specifying blanks for 
        OSTATION (respectively OMSGTYP) causes no restraint to be placed on 
        STATION (respectively MSGTYP) on M$WRITE.  For the control options 
        (ANYDCB, LATCH, ALLTRMS, ALLDCBS, and WAS), the specifications given 
        here are honored instead of those specified on M$WRITE; furthermore an 
        M$WRITE is illegal if it attempts to specify YES for a control option 
        specified as NO here. 
        OLOCK = NO has the following specific effects:  If an M$WRITE supplies 
        no station parameter, the values specified here are used.  If an 
        M$WRITE specifies blanks for STATION (respectively MSGTYP), the 
        OSTATION (respectively OMSGTYP) specified here is used.  For the 
        control options, the resultant specification is YES if and only if YES 
        is specified either here or on M$WRITE.  In other words, if the 
        control option is specified as YES here, it is ignored on M$WRITE and 
        treated as YES; if the control option is specified as NO here the 
        value specified on M$WRITE is honored.  The default is NO. 
  OM[SGTYP]=text 
        Applies to comgroups.  Specifies the default value for MSGTYP (from 
        one to eight characters) on writes through this DCB. 
  OPT[IONAL]{[=YES]|=NO} 
        Specifies whether the window size is permitted to drop below MINWIDTH 
        or MINLENGTH.  If so, the window will be removed from the screen when 
        it is too small, but its context will be maintained.  The default is 
        NO for a new window. 
  OR[G]=organization 
        Defines the file organization. 
        where organization is one of the following values: 
        C[ONSEC] 
        Consecutive; each record will be processed sequentially.  This is the 
        default for disk and labeled tape files.  Applicable to disk files and 
        labeled tape files. 
        DBGDCB 
        DBGDCB is legal for ASN=DEVICE issued from the debugger domain only 
        and specifies that this DCB is to be opened as a pathway across which 
        the debugger will communicate with its FEP counterpart in order to 
        debug a FEP user.  The FEP user to debug is specified by the DBGDCBNO 
        (in the M$OPEN FPT) which specifies the DCB number to which the FEP 
        user is connected. 
        DBGCG 
        DBGCG is legal for ASN=DEVICE issued from the debugger domain only and 
        specifies that this DCB is to be opened as a pathway across which the 
        debugger will communicate with its FEP counterpart in order to debug a 
        FEP user.  The FEP user to debug is specified by the NAME, ACCT, PSN 
        and SETSTA parameters which are used to describe a STATION on a 
        COMGROUP that is to be debugged. 
        DBGSYSID 
        DBGSYSID is legal for ASN=DEVICE issued from the debugger domain only 
        and specifies that this DCB is to be opened as a pathway across which 
        the debugger will communicate with its FEP counterpart in order to 
        debug a FEP user.  The FEP user to debug is specified by the DBGSYSID 
        (in the M$OPEN FPT) which gives the FEP user's sysid and by RES='FEnn' 
        specifying that the user resides on node nn, or by RES='FE ' in 
        conjunction with the NODENAME (at M$OPEN) which gives the name of the 
        node on which the user resides. 
        FI[XED] 
        Fixed length records with no control information.  Applicable to ANS, 
        EBCDIC, and managed tape F format files. 
        FORM 
        FORM specifies that an FEP-attached terminal or line printer is to be 
        operated using a field-oriented form. 
        FPRG 
        FPRG is legal for ASN=DEVICE and specifies FEP program access.  The 
        user program reads and writes simple strings of data which are the 
        outputs of and inputs to FEP programs which control the actual 
        presentation of the data on the media.  If VFC is specified on an 
        M$WRITE, the first character of the buffer is discarded.  Any 
        character in the data (including TAB) is sent unmodified to the FEP 
        program.  Appropriate forms programs may be invoked via the M$SETFP 
        system service or via the FPRG variable on this FPT_OPEN. 
        FR[EE] 
        Distinguishes free tape from managed tape.  Applicable to free tapes. 
        HANDLER 
        HANDLER specifies a real device handler and is legal for ASN=DEVICE 
        only.  RES must be either 'FEnn' specifying the handler be started on 
        node nn, or RES is 'FE', specifying the NODENAME at M$OPEN to identify 
        the node on which the handler will reside.  FEP HANDLERS are described 
        in the FEP Monitor Services Reference Manual (CE66).  The FEP HANDLER 
        will continue to run even after this DCB is closed.  Starting of FEP 
        HANDLERS requires the MFEP privilege.  (NAME specifies the name of 
        this handler.) 
        ID[S] 
        RANDOM files created by the IDS processor.  Applicable to disk files 
        and labeled tape files. 
        IN[DEXED] 
        An embedded key file.  Applicable to disk files and labeled tape 
        files. 
        K[EYED] 
        An associated key file.  Applicable to disk files and CP-6 format 
        labeled tape files. 
        RA[NDOM] 
        A collection of granules devoid of system record information. 
        Applicable to disk files and CP-6 format labeled tape files. 
        REL[ATIVE] 
        A preallocated file (via NRECS) whose records are fixed length (via 
        RECL) and may be accessed either sequentially or by relative position 
        within the file.  Applicable to disk files and labeled tape files. 
        SE 
        Specifies that a video display terminal is to be operated in a 
        screen-editing mode. 
        T[ERMINAL] 
        Specifies terminal control type access.  Does not cause character and 
        space translation nor support the logical page control formatting 
        options available for unit record and logical record devices (except 
        TAB and VFC).  Applicable to devices. 
        UN[DEF] 
        Undefined length records with no control information.  Applicable to 
        ANS, EBCDIC, and U tape formats. 
        UR 
        Unit record formatted file.  All options available for formatting unit 
        record output and logical devices (such as TABS, VFC, HDR, FORM) are 
        available in UR files.  On writes, data is translated into the 96 
        ASCII graphics and tabs are translated into spaces.  This is the 
        default for device output.  Applicable to disk files and devices. 
        V[ARIABLE] 
        Used to identify variable ANS spanned and unspanned and EBCDIC 
        formats.  Applicable to ANS and D and S tape formats.  EBCDIC tape 
        format. 
        X364 
        Provides commands for functions such as cursor positioning and 
        erasure, which are a subset of functions defined by the ANSI 
        X3.64-1979 standard.  X364 allows the user to write applications 
        programs in a device-independent manner, as if for an X3.64-compatible 
        terminal.  The system translates the commands into those understood by 
        the user's terminal, which does not have to be X3.64-compatible. 
        Through windowing, multiple X364 virtual devices may simultaneously be 
        present, with some possibly connected to other host users or other 
        CP-6 host computers.  X364 virtual devices may also be present with 
        other types of virtual devices on the same screen.  For information on 
        the X364 functions available, see Appendix F. 
  OS[TATION]=station 
        Applies to comgroups.  Specifies the default value for STATION on 
        writes through this DCB.  Station is a valid station name (from one to 
        eight characters). 
  P[AGECOLUMN]=value 
        Requests page numbering in the title line of the header of each 
        logical page, and specifies the starting column of the page number. 
        value   -   is a decimal number from 0 to 255 that specifies the 
        column of the lefthand digit of the number.  The default is zero 
        (which specifies no page numbering). 
        PAGECOLUMN applies to unit record files, and to unit record and 
        logical devices. 
  PH[YSICAL]=value 
        Specifies the number of physical pages backing the virtual area.  This 
        parameter determines how many pages are held within memory at any 
        given time. The parameter has a great effect on the access speed of 
        the virtual segment. The default is ten pages. 
        value   -   is a decimal integer from one to 16384. 
  PO[SITION]= option 
        Specifies the portion of FWINDOW that this (new) window is to occupy. 
        The options are TOP, BOTTOM, LEFT, and RIGHT.  This parameter is 
        ignored if the window already exists. 
  PROCATTR={attr_opt|(attr_opt[,attr_opt...)] 
        attr_opt   -   is either: O'string' or 'string' 
        Specifies a value for the processor attributes.  Although the CP-6 
        system places no restrictions on setting this data, this parameter is 
        reserved for use by processors. 
  PROCATTRS[IZE]=value 
        Specifies the size in words to reserve for the PROCATTR. 
  PROF[ILE]=name 
        Specifies a profile name in TEXTC format when LDBYPRO is specified. 
        name   -   is a profile name in TEXTC format with a maximum of eleven 
        characters. 
  Q[ISS]{[=YES]|=NO} 
        Applies to comgroups.  Specifies type of tree for CREATE opens of 
        comgroups.  YES specifies that the station tree is to be the queue 
        tree.  NO specifies that the message-type tree is to be the queue 
        tree.  The default is NO. 
  {RD|RE[AD]}={ALL|account|(accountlist)} 
        Specifies the accounts that may read but not write the file. 
        accountlist   -   specifies one or more account names separated by 
        commas.  The account names may contain wildcard characters. 
        READ applies to disk files and labeled tape files. 
  REC[L]=value 
        The meaning of RECL depends on record organization as follows: 
        Organization           Specification (In Bytes) 
        ------------           ------------------------ 
        F, RELATIVE            Actual record length. 
        D, V (unspanned)       Maximum record length including 
                               the count field. 
        S, V (spanned)         Maximum record length.  In this 
                               case, a value of 0 indicates 
                               that the maximum record length 
                               may be greater than 99,999. 
        value   -   is a decimal number from 1 to 99999 that is a byte count. 
        See Appendix E, tables E-1 and E-2, for format-dependent defaults and 
        maximum values. 
        For unspanned files, at most one record segment is used per record. 
        Records exceeding this length are truncated.  All variable record 
        length TAPE formats include 4 bytes of control information with the 
        data record; except for format D (e.g., non-EBCDIC, SPANNED, 
        VARIABLE), which include 5 bytes of control information.  For labeled 
        tape and disk, IN or UPDATE functions, the RECL value is set to the 
        value of the file opened.  For managed tape, RECL must be specified 
        for IN, UPDATE, and CREATE. 
        RECL applies to RELATIVE and fixed length files. 
  RES[ETPAGE]=YES 
        Resets page numbering in the title line of the header of the next 
        logical page of output. 
        RESETPAGE applies to unit record files, and to unit record and logical 
        devices. 
  RH[TBRDR]{[=YES]|=NO} 
        Specifies whether space is to be reserved at the right to separate 
        this window from the one to the right.  The default is NO for a new 
        window. 
  SC[RUB]{[=YES]|=NO} 
        YES specifies that the DCB is to be completely erased and then 
        reinitialized with default conditions. The scrubbing of the DCB occurs 
        prior to the remerge of values from the SET command (if REASSIGN=YES) 
        and prior to the merge of parameters from this open FPT.  The default 
        is NO. 
  SEE[D]=(octstr|"charstr"|NONE) 
        Specifies whether or not the user wants a seed and if so, what type. 
        octstr   -   specifies an octal string from 0 to 777777777777. 
        "charstr"   -   specifies from 1 to 4 characters. 
        NONE   -   specifies that the user does not want a seed. 
  SEGN[UM]={VS1|VS2|VS3} 
        Specifies which of the three large virtual segments, VS1, VS2, or VS3, 
        is to be used for this file. 
  SEGS[IZE]=value 
        Specifies in words the size of the large virtual segment.  The actual 
        bounding of a virtual segment is done on a page basis so the SEGSIZE 
        will be rounded up to a number of virtual pages.  Any page access that 
        is not within bounds will cause a missing page fault. 
        value   -   is a decimal integer from one to 2097152. 
  SEQ{[=YES]|=NO} 
        Specifies that sequencing is to occur on each output record. 
        (Normally used with punched card output.) 
        YES   -   specifies that record sequencing is to be performed for 
        output to the logical device according to the SEQCOL and SEQID 
        parameters. 
        NO   -   specifies that record sequencing is not to be performed. 
        Normally used to discontinue record sequencing.  NO is the default. 
        SEQ applies to unit record files, and to unit record and logical 
        devices. 
  SEQC[OL]=value 
        Specifies in which column sequencing of output records begins. 
        value   -   is a decimal number from 1 to 255 that specifies the 
        column number in which sequencing is to begin.  The sequence ID is 
        printed followed by the record sequence number.  The default is 73. 
        Note that sequencing is controlled by the SEQ option. 
        SEQCOL applies to unit record files, and to unit record and logical 
        devices. 
  SEQI[D]='string' 
        Specifies that a four-character identification is to be appended to 
        each output record when record sequencing is requested. 
        string   -   is a four-character sequence identification.  The default 
        is blanks. 
        SEQID applies to unit record files, and to unit record and logical 
        devices. 
  SH[ARE]={A[LL]|I[N]|N[ONE]} 
        Determines what additional users can open a file and what they can do 
        with the file. 
        ALL   -   specifies that, depending on the associated functions, 
        qualified sharing users can open the file. 
        IN   -   specifies that qualified sharing users can open the file for 
        INPUT. 
        NONE   -   specifies that, unless qualified through the associated 
        function, no sharing users can open the file.  This is the default. 
        The ability of a user to open to a shared file depends on the FUN and 
        SHARE options he supplies in the SET command.  The following table 
        summarizes the response of the system to attempts to open to a shared 
        file: 
                                        Subsequent Users 
                                    FUN=IN              FUN=UPDATE 
        Initial User         SHARE  SHARE  SHARE    SHARE  SHARE  SHARE 
                             = ALL  = IN   =NONE    = ALL  = IN   =NONE 
        All users  SH=ALL      X      4      4        1      2      4 
        to date    SH=IN       X      X      X        4      4      4 
        opened     SH=NONE     X      X      X        4      4      4 
        FUN=IN 
        After a    SH=ALL      X      4      4        X      4      4 
        user has   SH=IN       3      4      4        4      4      4 
        opened     SH=NONE     4      4      4        4      4      4 
        FUN=UPDATE 
        X = Subsequent user allowed file access, no added restrictions. 
        1 = Subsequent user allowed access, but when this user enters the user 
        pool, the file is considered FUN=UPDATE for subsequent users. 
        2 = Subsequent user allowed access but when this user enters the user 
        pool, the file is considered FUN=UPDATE for subsequent users.  Note 
        that this condition can only take place if no other users have opened 
        FUN=UPDATE.  If the user closes, the FUN returns to IN. 
        3 = Subsequent user allowed access, but if the initial user closes, 
        the FUN is changed to IN. 
        4 = Subsequent user denied access. 
        If FUN=CREATE and the file has not been cataloged, SHARE has no 
        meaning. 
        If FUN=CREATE and the file has been cataloged, the same options apply 
        as for FUN=UPDATE. 
        FUN=CREATE users can open-create a file using the same name. 
        SHARE applies to disk files. 
  SN={packsetname|(seriallist)} 
        Specifies a list of tape serial numbers or a packset name. 
        packsetname   -   is an alphanumeric packset name. 
        seriallist   -   is a list of tape serial numbers whose members are 
        separated by commas.  The members must be specified in the same order 
        as when the volume set was created and cannot contain duplicate or 
        blank serial numbers.  SN applies to tapes and disk files. 
  SPAN[NED]{[=YES]|=NO} 
        Determines whether logical records may be divided between physical 
        tape records. 
        YES   -   specifies that records are to be spanned.  This is the 
        default. 
        NO   -   specifies that records are not to be spanned. 
        For labeled tape file IN or UPDATE opens, the SPANNED value is set to 
        the value for the file opened.  For managed tape files, SPANNED must 
        be specified for IN, UPDATE, and CREATE.  Spanned and unspanned files 
        may be intermixed on a tape volume.  SPANNED should be used with 
        BLOCKED to optimize tape utilization. 
        SPANNED applies to VARIABLE tape files. 
  SPAR[E]=value 
        Specifies the amount of space to be left unused at the end of each 
        index block while a KEYED or INDEXED disk file is being created or 
        updated with sequential access.  This spare space is reserved so that 
        additional keys can be inserted in a minimum time when updating the 
        file with direct access (as in EDIT). 
        value - specifies a decimal number from 1 to 511 that is the number of 
        words to be left unused.  If the file will never be updated with 
        direct access, a spare value of 1 should be specified.  A value of 0 
        means use the existing value in the DCB.  If a DCB has never been 
        opened by a program the default is 1. 
  TA[B]=(tablist) 
        tablist   -   is 1 to 31 decimal numbers from 0 to 255 that specify 
        Horizontal Tab columns (HTs).  An HT character in output is replaced 
        by blanks up to the next tab column.  The tab specification must be in 
        ascending numeric order and members of the list are separated by 
        commas.  The default is no tabulation (HT characters are replaced with 
        a single blank). 
        If MARGIN is also specified, tabulation is relative to it; that is, 
        the MARGIN column on the output medium is TABS column 1. 
        TAB applies to unit record files, and to unit record and logical 
        devices. 
  TE[RMCONLGL]{[=YES]|=NO} 
        Applies to comgroups.  Meaningful only if ORG = CG.  Specifies whether 
        terminals are allowed to open to this comgroup.  The default causes 
        this parameter to be ignored.  See HELP(HOSTMON)VLP_CGCP for 
        additional information. 
  TI[TLE]='string' 
        Specifies the text to be printed as a title on the top of every page 
        of output. 
        string   -   contains 1 to 114 characters of title text. 
        TITLE applies to unit record files, and to unit record and logical 
        devices. 
  TO[PBRDR]{[=YES]|=NO} 
        Specifies whether space is to be reserved at the top to separate this 
        window from the one above it.  The default is NO for a new window. 
  TY[PE]=value 
        Specifies the file type (normally assigned by the system processor 
        that creates the file). 
        value   -   is a two-character type.  If characters other than 
        alphanumeric characters or the characters $_#@ and * are used, the 
        value must be surrounded by quotes.  User-defined file types (e.g., MF 
        for Munged Funny) are legal. 
        TYPE applies to disk files and labeled tape files. 
  UATTR={attr_opt|(attr_opt[,attr_opt...])} 
        attr_opt   -   is either: O'string' or 'string' 
        Specifies a value for the user attributes.  Although the CP-6 system 
        places no restrictions on setting this data, this parameter is 
        reserved for use by processors. 
  UATTRS[IZE]=value 
        Specifies the size in words to reserve for the UATTR. 
  UOPTn{[=YES]|=NO} 
        Sets or resets a one-bit field in the DCB.  There are 9 UOPT flags 
        that the user can set to allow a user processor to pass information 
        between the DCB and his processor. 
        n   -   is a decimal integer from 0-8 that specifies the UOPT flag to 
        set or reset. 
        YES   -   specifies set the flag. 
        NO   -   specifies reset the flag. 
        UOPT is only used in user applications. 
  VBRDRC[HR]=c 
        Specifies the single ASCII character to be used to mark the vertical 
        border space(s).  It will fill every character position of the 
        farthest column of the border space. 
        c   -   is a single ASCII character. 
  VBRDRS[IZ]= value 
        Specifies the size in columns of the vertical border space(s) (LFTBRDR 
        and RHTBRDR).  The default is zero, which causes this parameter to be 
        ignored.  Note that the border presence parameters must be used to 
        remove a border - HVBRDRSIZ=0 won't work. 
        value   -   is a decimal integer from 0 to 15. 
  V[OL]=value 
        Specifies an initial tape volume. 
        value   -   is a decimal number from 1-511 that identifies tape 
        volume.  On open, VOL specifies which volume of the volume set (as 
        specified by the serial number list) is to be initially mounted.  A 
        value of 0 or 1 indicates the first volume, 2 the second, etc.  VOL is 
        used in conjunction with XTEND to determine which volume of the volume 
        set to extend.  If the DCB is open, VOL indicates which volume is 
        currently mounted. 
        VOL applies to tapes. 
  VOLA[CCESS]={A[LL]|I[N]|N[ONE]} 
        ALL   -   specifies any user may read or write the volume. 
        IN   -   specifies any user may read the volume, but only the owner 
        may write on it. 
        NONE   -   specifies only the owner of the volume set may access it. 
        VOLACCESS applies to labeled tapes. 
  W[AS]{[=YES]|=NO} 
        Applies to comgroups.  YES specifies the default value for WAS on 
        writes through this DCB.  If WAS is set here, WAS on the M$WRITE is 
        ignored.  (See WAS in VLP_STATION).  The VLP field name of this 
        parameter is VLP_SETSTA.OSTA.WAS#.  The default is NO. 
  WL[ENGTH]=value 
        Specifies the size of the window, in absolute or incremental lines or 
        as a percentage of the full screen (or of the current size for an 
        existing window).  This option is ignored for a new window if 
        POSITION=LEFT or RIGHT.  The default is +0, which doesn't change an 
        existing window, but is specially interpreted for a new one as 99%. 
  WR[ITE]={ALL|account|(accountlist)} 
        Specifies the accounts that may write but not read the file. 
        accountlist   -   specifies one or more account names separated by 
        commas.  The account names may contain wildcard characters. 
        WRITE applies to disk files and labeled tape files. 
  WW[IDTH]=value 
        Specifies the size of the window, in absolute or incremental columns 
        or as a percentage of the full screen (or of the current size for an 
        existing window).  This option is ignored for a new window if 
        POSITION=TOP or BOTTOM.  The default is +0, which doesn't change an 
        existing window, but is specially interpreted for a new one as 50%. 
  XTE[ND]{[=YES]|=NO} 
        Determines the position for CREATE opens of labeled tape. 
        YES   -   requests positioning after the last file of the volume set. 
        NO   -   requests that the next file is to be created at the current 
        volume position.  This is the default. 
        XTEND applies to labeled tape files. 
  XTN[SIZE]=value 
        Specifies the size of secondary extents. 
        value   -   is a decimal number from 1-32000 that specifies (in 
        granules) the size of secondary extents (used to add on extents).  The 
        default is 2. 
        XTNSIZE applies to keyed, indexed, consecutive and unit record disk 
        files. 
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
00019
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
00059
00060
00061
00062
00064
00063
00064
00065
00066
00068
00067
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
00107
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
SET_OPS
The following table shows special keys in use on the CP-6 system:  The 
notation <CNTL-H> indicates that the Control key is held down while the 
character 'H' is typed to generate the special character BS. 
  Key or Sequence          Function 
  <BREAK> 
                    Deletes type-ahead, any partial input record, any queued 
                    output, and returns the user to his break entry point. 
  <CNTL-H> or <BS> 
                    Moves the edit point left one column.  If at the beginning 
                    of the input record, the backspacing is ignored. 
  <CNTL-I> or <TAB> 
                    Moves the cursor to the next input tab stop. 
  <CNTL-J> or <LF> 
                    Same as <CR> except that if FULLDUXPAPERTAPE or 
                    HALFDUXPAPERTAPE is in effect, <LF> is ignored when the 
                    current input record is empty. 
  <CNTL-L> or <FF> 
                    Erases the window on a CRT.  Otherwise, same as <ESC> <L>. 
  <CNTL-M> or <CR> 
                    Echoes as a new-line after interpretation as a normal 
                    input character.  The new-line occurs only if echoing is 
                    enabled, or if <CR> is an activation character. 
  <CNTL-Q> or <DC1> or <XON> 
                    Enters full duplex paper tape mode. 
  <CNTL-R> or <DC2> 
                    If not at the end of the input record, moves the edit 
                    point right one column.  If at the end of the input 
                    record, a blank space is generated.  Resets the insertion 
                    window if the edit point moves out of it. 
  <CNTL-S> or <DC3> or <XOFF> 
                    Exits full duplex paper tape mode. 
  <CNTL-U> 
                    If not at the end of the input record, moves the edit 
                    point right one column.  If at the end of the input 
                    record, a blank space is generated.  Resets the insertion 
                    window if the edit point moves out of it.  Changes the 
                    case of the characters under the cursor. 
  <CNTL-W> or <ETB> 
                    Positions to the next or previous word.  The direction of 
                    movement is set by the last-received cursor-motion 
                    function (e.g., <BS>, <CNTL-R>, <TAB>, <CNTL-W>, 
                    <ESC> <I>, or <ESC> <V>) or by parameter 5. 
  <CNTL-X> or <CAN> 
                    Deletes type-ahead, any partially input record, and any 
                    queued output. 
  <CNTL-Y> or <EM> 
                    Deletes type-ahead, any partially input record, any queued 
                    output, and returns control to the command processor. 
  <CNTL-[> or <ESC> 
                    Introduces a CP-6 escape sequence. 
  <DEL> 
                    Deletes a column in the input record.  (ASCII DEL 
                    character) 
00001
00002
00012
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
00006
00007
00008
00009
00015
00013
00014
00011
00005
00004
00003
00009
00007
UR_SPECIAL_NAMES
STATUS
Syntax: 
S[TART] rununit [U|UNDER] [debuggername] 
Parameters: 
rununit   -   specifies the fid of the run unit to be fetched. 
U[NDER]   -   specifies that a debug processor is to be called and that 
control is to be passed to the debug processor. 
debuggername   -   specifies the name of a debug processor, either a 
user-developed debug processor or the CP-6 debug processor, DELTA.  If U[NDER] 
is specified but no debugger-name is supplied, the default debug processor is 
DELTA. 
Description: 
The START command fetches a run unit into memory, and depending on its syntax, 
either: 
o   Starts execution at its beginning address. 
o   Invokes a debug processor to process the run unit. 
Examples: 
!START EXAMPLE 
Starts execution of the run unit EXAMPLE without an associated debug 
processor. 
!S EXAMPLE UNDER 
Starts execution of the run unit EXAMPLE under control of DELTA. 
!START EXAMPLE U MYDEBUG 
Starts execution of the run unit EXAMPLE under control of the debug processor 
named MYDEBUG. 
Related Commands: 
INVOKING_RUNUNITS 
00002
00003
00001
00004
SCHED_STATES
Syntax: 
{ST|STATUS} {F[ULL]|S[UMMARY]|N[ONE]} 
Parameters: 
F[ULL]   -   specifies accounting information. 
S[UMMARY]   -   specifies summary of accounting information. 
N[ONE]   -   specifies no accounting information. 
The default is SUMMARY. 
Description: 
STATUS displays information about system usage during the current session. 
Examples: 
!ST 
displays information about system usage during the current session. 
Related Commands: 
REPORT 
00002
00003
00001
00004
    STEPCC is a one-byte field in the JIT that can take on values from 0 to 
    511, and can be set by the program using M$EXIT, M$ERR, and M$XXX monitor 
    services.  CP-6 processors use the values 0, 4, and 6 for exit control. 
    The default behavior of each of the exit monitor services is to set STEPCC 
    as follows: 
                        Default STEPCC 
    Monitor Service     Setting            Termination Type 
    ---------------     --------------     ---------------- 
    M$EXIT                     0           Normal 
    M$ERR                      4           Error Condition 
    M$XXX                      6           Program Abort 
Note that the STEPCC setting is under the programmer's control and can be set 
to any value between 0 and 511 for any case.  The form of exit (M$EXIT, M$ERR, 
or M$XXX) taken by the program at the last job step determines the settings of 
the OK, ERROR, and ABORT flags.  These one-bit indicators are either on or 
off.  The form of exit in relationship to the indicators and the type of 
termination is as follows: 
                          Flag Setting 
    Monitor Service       ------------       Termination Type 
    ---------------     OK  ERROR  ABORT     ---------------- 
                        ---------------- 
    M$EXIT              1     0      0       Normal 
    M$ERR               0     1      0       Error Condition 
    M$XXX               0     0      1       Program Abort 
The flag settings always refer to the type of exit chosen, independent of the 
value of STEPCC.  Both STEPCC and the exit flags (OK, ERROR, ABORT) may be 
tested with the IF command and appropriate action taken depending on the value 
or setting. 
Any trap not handled by the program results in an ABORT condition with STEPCC 
set to 6; in essence, this condition is identical to the program itself 
issuing an M$XXX.  Also, if the operator issues an ERROR keyin for a user 
running a program, the behavior will be as if the program that was running had 
performed an M$ERR.  (In the case of the X keyin, the user never regains 
control to do anything about it except for previously established exit 
control.) 
Syntax: 
STOP 
Parameters: 
NONE 
Description: 
STOP (a synonym for the QUIT command) terminates an interrupted activity. 
When issued in a command file, STOP terminates execution of the file. 
Examples: 
!!STOP 
means kill the current interrupted activity. 
Related Commands: 
QUIT, GO, CONTINUE 
00002
00003
00001
00004
Format: 
*ST[OW] [AC[TIVE]|IN[ACTIVE]]  fid1 [,fid2,...] 
Parameters: 
fid1, fid2    specify CP-6 file identifiers. 
Description: 
The STOW command requests that the specified file(s) be entered into the 
archive system, and has the following results: 
1.  The file is locked to prevent updating and is queued for STOW. 
2.  When the system manager performs an ARCHIVE run, the file is written to 
    tape and the FIT is updated with the time, date, and serial number of the 
    tape to which the file was copied. 
3.  Files designated ACTIVE are retained on disk and made accessible to users 
    (read only).  File(s) specified as INACTIVE are retained on tape only. 
Both ACTIVE and INACTIVE files may be removed from the queue for archiving via 
the UNSTOW command. 
If a file previously stowed ACTIVE and not UNSTOWed is made STOW INACTIVE, its 
disk granules are immediately released. 
If neither ACTIVE nor INACTIVE is specified, the default is INACTIVE. 
Usage Notes: 
1.  This command may be used only if:  a) the account is authorized with the 
    STOW attribute (see PIG, STOW|NOSTOW option) and the current user is the 
    file creator, or b) the account is authorized with the STOW attribute and 
    the current user has FMSEC privilege active. 
2.  While the file is queued for STOW or FETCH, it cannot be updated. 
00002
00001
00003
Syntax: 
SWITCH {n|ALL}[=ON]|=OFF][switchlist] 
Parameters: 
ALL   -   sets or resets all sense switches. 
switchlist   -   specifies one or more switch settings.  There are 36 
switches, numbered 0 to 35, which have two positions, ON and OFF.  The format 
for setting (turning ON) or resetting (turning OFF) a particular switch is: 
    n[={ON|OFF}] 
where n is the integer number of the switch (0-35).  If only the switch number 
is specified, ON is assumed.  Another method of setting or resetting the 
switches is to consider all together as a 36-bit word and designate an octal 
value (right-justified) to identify the switches being set or reset: 
    O'octal value' [={ON|OFF}] 
For example, !SWITCH O'5'=ON and !SWITCH 33=ON, 35=ON are equivalent methods 
of setting these two switches. 
Description: 
SWITCH sets and resets sense switches.  Sense switches may be interrogated by 
user programs for any purpose the user desires.  The sense switch is 'set' 
when it is on, and 'reset' when it is off. 
Examples: 
!SWITCH ALL 
Sets all sense switches. 
!SWITCH 4=ON,5=OFF,18=OFF,19,20=ON 
Sets sense switches 4,5, and 18, and resets sense switches 19 and 20. 
!SWITCH O'17' 
Sets sense switches 32, 33, 34, and 35.  These settings are determined by 
converting the octal number 17 into binary (001 111).  Each binary digit place 
that has a value of 1, sets the sense switch with the corresponding bit 
position in the 36-bit sense switch word (the most significant bit corresponds 
to sense switch 0, the least significant bit corresponds to sense switch 35). 
!SWITCH O'400000000000'=ON 
Sets sense switch 0. 
!SWITCH O'777777777777'=OFF 
Resets all sense switches. 
Related Commands: 
NONE 
00002
00003
00001
00004
NOTATION
TERMINAL
Syntax: 
TABS [s[,s]...] 
Parameters: 
s   -   is a column position where a tab stop is to be placed.  This value 
must be between 1 and 255.  If no stops are specified, the current stops are 
displayed. 
Description: 
Simulated tab stops for a terminal are set by the TABS command. 
Up to 32 tabs, in ascending sequence, may be set.  Whenever a tab character is 
sent to or received from a terminal, spaces are sent to the terminal to 
position the carrier to the next stop that is higher than the current 
position. 
Tab settings are disabled by the command: 
    TABS {0|NO|OFF} 
Examples: 
!TABS 5,10,30,50 
means set tab stops at columns 5, 10, 30, and 50. 
!TABS OFF 
means kill all current tab settings. 
Related Commands: 
See TA in EDIT and TABS in PCL. 
00002
00003
00001
00004
FID_TAPE
Syntax: 
{T|TERMINAL} [UCnn] [option[,option]...] 
Parameters: 
UCnn   -   directs TERMINAL command to a specific stream.  For a TERMINAL 
command with no options (i.e., a TERMINAL display command), default is UC98. 
For a TERMINAL command that sets parameters (options specified) the default is 
ALL streams.  For descriptions of use of UCnn with window options, see Section 
6, Using CP-6 Windows, or use HELP (IBEX) USING_WINDOWS. 
option   -   specifies a valid option for the TERMINAL command.  If no option 
is specified, a message is printed that displays the mode and port, the line 
speed, the name of the current profile, the window parameters, and the status 
of all options flags that are ON. 
Valid options are: 
AC[TONTRN]{[=YES]|=NO} 
AD[JTOPLFT]{[=YES]|=NO} 
APLL[CNRM]{[=YES]|=NO} 
AT[RSCRNPOS]{[=YES]|=NO} 
AUTOC[URSOR]{[=YES]|=NO} 
AUTON[L]{[=YES]|=NO} 
AUTOT[ABCLM]= value 
BI[N]{[=YES]|=NO} 
BL[ANKERASES]{[=YES]|=NO} 
BT[MBRDR]{[=YES]|=NO} 
CHARSETNAME=name 
CR[ISNL]{[=YES]|=NO} 
CURSORR[EAD]=[YES|NO} 
DC[HMOVFLD]{[=YES]|=NO} 
DEVICEB[S]{[=YES]|=NO} 
DEVICEC[R]{[=YES]|=NO} 
DEVICEL[F]{[=YES]|=NO} 
DEVP[OSOPTS]{[=YES]|=NO} 
DEVS[CROLL]{[=YES]|=NO} 
DI[SPINPUT]{[=YES]|=NO} 
DS[PHEIGHT]= value 
DV[CFLWCTRALG]= option 
EA[SYAPPEND]{[=YES|=NO} 
ED[ITOVR]{[=YES]|=NO} 
EN[BENTEXTSRDCHR]{[=YES]|=NO} 
FC[NTBL]={CP5|CP5S1|CP5S2|FRM1|SE1|SE2|NONE} 
FF[FLUSH]{[=YES]|=NO} 
FFI[NCCR]{[=YES]|=NO} 
FU[LLDUXPAPERTAPE]{[=YES]|=NO} 
FW[INDOW]=name 
HA[LFDUXPAPERTAPE]{[=YES]|=NO} 
HBRDRC[HR]= c 
HBRDRS[IZ]= value 
HE[IGHT]=value 
HSA[LL]{[=YES]|=NO} 
HSC[ROLL]{[=YES]|=NO} 
HSM[ARGIN]=value 
HSS[HIFT]=value 
IN[PUTIGNORE]{[=YES]|=NO} 
INS[ERTMODE]{[=YES]|=NO} 
KEE[PTYPAHD]{[=YES]|=NO} 
KEYI[NCR]= value 
KEYT[YPE]= option 
LFI[SNL]{[=YES]|=NO} 
LFT[BRDR]{[=YES]|=NO} 
LI[MBOCLM]{[=YES]|=NO} 
LOC[ALECHO]{[=YES]|=NO} 
LO[WERCASE]{[=YES]|=NO} 
LOWERCASEP[RINTS]{[=YES]|=NO} 
MA[XATRS]= value 
MIC[ROFPL]{[=YES]|=NO} 
MINL[ENGTH]=value 
MINW[IDTH]=value 
MSGH[ALT]{[=YES]|=NO} 
MSG[LINE]{[=YES]|=NO} 
NOF[LDTRM]{[=YES]|=NO} 
NO[OPTMIZ]{[=YES]|=NO} 
ONE[SPACEEDIT]{[=YES]|=NO} 
OPD[TAB{[=YES]|=NO} 
OPT[IONAL]{[=YES]|=NO} 
OU[TPUTDISCARD]{[=YES]|=NO} 
PAG[EHALT]{[=YES]|=NO} 
PAR[ITY]=option 
PAR[ITYCHECK]{[=YES]|=NO} 
PARK[CURSOR]{[=YES]|=NO} 
PR[INTHALT]{[=YES]|=NO} 
PRINTT[YPE]{[=YES]|=NO} 
PRO[GDTAB]{[=YES]|=NO} 
RC[RWRAP]{[=YES]|=NO} 
REL[PAGE]{[=YES]|=NO} 
RET[YPOVR]{[=YES]|=NO} 
RH[TBRDR]{[=YES]|=NO} 
SC[ROLL]{[=YES]|=NO} 
SE[NDBKSPACE]{[=YES]|=NO} 
SIM[PERF]{[=YES]|=NO} 
SI[NPUTSZ]=value 
SP[ACEINSERT]{[=YES]|=NO} 
SPC[BFRPRT]{[=YES]|=NO} 
SPE[ED]=value 
TABR[ELATIVE]{[=YES]|=NO} 
TABS[IM]{[=YES]|=NO} 
TE[XTEDIT]{[=YES]|=NO} 
TO[PBRDR]{[=YES]|=NO} 
TR[UNCATE]{[=YES]|=NO} 
TRUO[VRPRT]{[=YES]|=NO} 
TT[YTYPE]{[=YES]|=NO} 
UP[PERCASE]{[=YES]|=NO} 
VBRDRC[HR]=c 
VBRDRS[IZ]= value 
VSM[ARGIN]= value 
VSS[HIFT]= value 
WI[DTH]=value 
WL[ENGTH]=value 
WO[RDWRAPCLM]=value 
WR[APPAGE]={[YES]|NO} 
WW[IDTH]=value 
Type HELP T_OPS for complete description. 
Description: 
TERMINAL defines a terminal profile when used with one or more options, or 
results in a printed message when used with no options.  This command can only 
be issued on-line. 
Examples: 
!TERMINAL EDITOVR=NO 
means inserted characters are to be printed below the line and deletions are 
to marked with a backslash. 
Related Commands: 
PROFILE 
00002
00003
00001
00004
Valid options for the TERMINAL command are: 
ACTONTRN           DEVICEBS           FFINCCR            KEEPTYPAHD 
ADJTOPLFT          DEVICECR           FULLDUXPAPERTAPE   KEYINCR 
APLLCNRM           DEVICELF           FWINDOW            KEYTYPE 
ATRSCRNPOS         DEVPOSOPTS         HALFDUXPAPERTAPE   LFISNL 
AUTOCURSOR         DVCFLWCTRALG       HBRDRCHR           LFTBRDR 
AUTONL             DEVSCROLL          HBRDRSIZ           LIMBOCLM 
AUTOTABCLM         DISPINPUT          HEIGHT             LOCALECHO 
BIN                DSPHEIGHT          HSALL              LOWERCASE 
BLANKERASES        EASYAPPEND         HSCROLL            LOWERCASEPRINTS 
BTMBRDR            EDITOVR            HSMARGIN           MAXATRS 
CHARSETNAME        ENBENTEXTSRDCHR    HSSHIFT            MICROFPL 
CRISNL             FCNTBL             INPUTIGNORE        MINLENGTH 
CURSORREAD         FFFLUSH            INSERTMODE         MINWIDTH 
MSGHALT            PARKCURSOR         SINPUTSZ           UPPERCASE 
MSGLINE            PRINTHALT          SPACEINSERT        VBRDRCHR 
NOFLDTRM           PRINTTYPE          SPCBFRPRT          VBRDRSIZ 
NOOPTMIZ           PROGDTAB           SPEED              VSMARGIN 
ONESPACEEDIT       RCRWRAP            TABRELATIVE        VSSHIFT 
OPDTAB             RELPAGE            TABSIM             WIDTH 
OPTIONAL           RETYPOVR           TEXTEDIT           WLENGTH 
OUTPUTDISCARD      RHTBRDR            TOPBRDR            WORDWRAPCLM 
PAGEHALT           SCROLL             TRUNCATE           WRAPPAGE 
PARITY             SENDBKSPACE        TRUOVRPRT          WWIDTH 
PARITYCHECK        SIMPERF            TTYTYPE 
Type HELP (IBEX) T_OPS option 
  Opt        Meaning 
  AC[TONTRN]{[=YES]|=NO} 
        YES specifies that the activation (EOM) characters are to apply to 
        transparent reads to the terminal.  NO specifies that only activation 
        on byte count will be performed.  BREAK functions normally 
        independently of this option. 
  AD[JTOPLFT]{[=YES]|=NO} 
        Indicates the default direction for window size change requests.  YES 
        specifies that a window size change request for this window that does 
        not specify the FWINDOW parameter will prefer to move the top or left 
        boundary of the window.  NO specifies that such a request will prefer 
        to move the bottom or right boundary.  The ADJTOPLFT window attribute 
        is initialized for a new window based on the boundary of the new 
        window that was moved to create it.  Windows created with POSITION=TOP 
        or POSITION=LEFT will have ADJTOPLFT initially set to NO, and ones 
        created with POSITION=BOTTOM or POSITION=RIGHT will have it set to 
        YES. 
  APLL[CNRM]{[=YES]|=NO} 
        YES specifies that if lowercase characters are sent to the terminal 
        while it is in APL mode, they are printed as uppercase.  NO specifies 
        that they are to be uppercase underscored. 
  AT[RSCRNPOS]{[=YES]|=NO} 
        Specifies whether a field attribute definition occupies a printable 
        column on the terminal, such that a character cannot also be displayed 
        there. 
  AUTOC[URSOR]{[=YES]|=NO} 
        Yes specifies that the cursor is to move automatically from a 
        non-reading session when a read starts and is not completed by 
        typeahead.  The cursor is moved to the newly reading session.  NO 
        specifies that the cursor is to be moved only via the keyboard or 
        M$TRMPRG with CURSORHERE=YES. 
  AUTON[L]{[=YES]|=NO} 
        YES specifies that the terminal will itself perform a new line 
        function (CR+LF) immediately after printing in (or spacing through) 
        the right margin column.  NO means that the cursor will move to the 
        right of the right margin column to a column that cannot be printed 
        in. 
  AUTOT[ABCLM]= value 
        Specifies the initial cursor position to be used when a new record is 
        read (i.e., not rereading a line).  Any characters saved by the 
        wordwrap facility or in typeahead will, of course, be displayed 
        beginning at AUTOTABCLM as well.  A value of zero or one specifies 
        that the input data is to begin immediately after the prompt. 
        value    is a decimal value from 0 to 254. 
        In a screen-editing window, an attempt to move into a record (old or 
        new) in a position to the left of the autotab causes an autotab. 
  BI[N]{[=YES]|=NO} 
        Indicates whether binary output to this device is legal.  This option 
        does not apply to timesharing terminals. 
  BL[ANKERASES]{[=YES]|=NO} 
        YES means that a blank (Space) character displayed on the terminal in 
        a position occupied by another character erases the previous 
        character.  NO means that the previous character is unchanged. 
  BT[MBRDR]{[=YES]|=NO} 
        Specifies whether space is to be reserved at the bottom to separate 
        this window from the one below it.  The default is NO for a new 
        window. 
  CHARSETNAME=name 
        Specifies the name of the terminal character set; that is, how the 
        character sent to and received from the terminal are translated into 
        ASCII. 
        name    may be one to eight characters.  Current defined names are: 
        APLBF     APL bit-paired translation.  Lowercase ASCII characters are 
        printed as underscored uppercase characters.  Device: ASYNC 
        APLBP     APL bit-paired translation.  Lowercase ASCII characters are 
        printed as uppercase characters on output.  Device: ASYNC 
        APLTF     APL typewriter-paired translation.  Lowercase Device:  ASYNC 
        ASCII characters are printed as underscored uppercase characters on 
        output.  Device: ASYNC 
        APLTP     APL typewriter-paired translation.  Lowercase ASCII 
        characters are printed as uppercase characters on output.  Device: 
        ASYNC 
        ASC8      ASCII-95 variant translation that passes 8-bit output 
        characters (X'80' through X'FF') through unchanged rather than as '#'. 
        Device: ASYNC 
        ASC8I     ASCII-95 variant translation that passes 8-bit characters 
        (X'00' through X'FF') through on input rather than stripping the 
        parity bit.  Device: ASYNC 
        ASC64     ASCII-64 translation (the default).  Device: ASYNC URP 
        ASC64B    ASCII-64 variant translation for Teletype Model 35.  This 
        table interprets Altmode (X'7E', tilde) as escape on input.  Device: 
        ASYNC 
        ASC64C    ASCII-64 variant translation for Teletype Model 33, Xerox 
        7015, Hazeltine 2000, etc.  This table exchanges NOT (tilde) and OR 
        (vertical line) in CP-6 system with right bracket and left bracket at 
        the terminal.  It also interprets Altmode (X'7E', tilde) as escape on 
        input.  Device: ASYNC 
        ASC95     ASCII-95 translation (the default for RBTD and URP). 
        Device: ASYNC RBTD URP 
        ASC95M    ASCII-95 variant translation for CDI1203 Miniterms operating 
        in STD mode.  Converts the character generated by the ESC key (without 
        CTRL) to an ESC.  Device: ASYNC 
        BIT       EBC variant translation for BITNET.  The differences are: 
           EBCDIC                ASCII 
           Hex AD           <--> left-bracket 
           Hex BD           <--> right-bracket 
           solid-bar         --> broken-bar 
           Hex FA            --> broken-bar 
           Hex BF            --> hyphen 
           Hex 8B            --> left-brace 
           Hex 9B            --> right-brace 
           Hex 8F            --> semi-colon 
        Device: RBTD 
        EBCE     EBC variant fr RBTD European sites.  The differences are: 
           EBCDIC                ASCII 
           cent-sign        <--> dollar sign 
           solid-bar        <--> pound sign 
           backslash        <--> ampersand 
           ampersand        <--> backslash 
           pound-sign       <--> left-bracket 
           dollar-sign      <--> exclamation point 
           exclamation pt.  <--> left-bracket 
        Device: RBTD 
        EBCI      EBCDIC input is translated to CP-6 ASCII.  Device: RBTD 
        EBCO      CP-6 ASCII output is translated to EBCDIC.  Device: RBTD 
        HISI     Honeywell Bull (e.g., GCOS MOD400) EBCDIC input is translated 
        to CP-6 ASCII.  Device: RBTD 
        HISO     CP-6 ASCII output is translated to EBCDIC.  Device: RBTD 
        XDSI      Xerox extended EBCDIC input is translated to CP-6 ASCII. 
        Device: RBTD 
        XDSO      CP-6 ASCII output is translated to Xerox extended EBCDIC. 
        Device: RBTD 
        SDS7012   CP-6 ASCII operator console output is translated to an 
        uppercase EBCDIC subset; this should be specified for Xerox model 7012 
        operator consoles.  Device: RBTD 
        NONE      No translation to or from CP-6 ASCII will be performed. 
        Device: RBTD 
        3276STD   Standard EBCDIC-ASCII translation with all characters that 
        can be displayed by the 3276 type devices.  The following translation 
        is used for those characters not in both sets: 
           EBCDIC               ASCII 
           not-sign        <--> vertical-arrow 
           cent-sign       <--> left-bracket 
           solid-vert-line <--> right-bracket 
           field-mark      <--> escape 
        Note:  Not all translations hold for both input and output.  The 
        arrows indicate the direction of translation.  Device: 3270 
        3276LIM   Same as the previous table except useful for data-entry 
        keyboards that do not have all keys, or for others that prefer a more 
        obvious EBCDIC-ASCII translation at the expense of not being able to 
        enter or display square brackets: 
           EBCDIC                ASCII 
           not-sign         <--> tilde 
           solid-ver-line   <--> broken-vert-line 
           cent-sign        <--> vert arrow 
           left-paren       <--  left-bracket 
           right-paren      <--  right-bracket 
           broken-vert-line  --> broken-vert-line 
        Device: 3270 
        3270      For pre-IBM 3276 type device (limited character set).  Same 
        as previous table with the following differences: 
           EBCDIC            ASCII 
           right-paren  <--  right-brace 
           left-paren   <--  left-brace 
           pound-sign   <--  accent-grave 
           pound-sign   <--  backslash 
           Device: 3270 
        The default is blank. 
        3270EUR    Same as 3276STD except for the following differences needed 
        by European sites: 
        EBCDIC                ASCII 
           cent-sign        <--> dollar sign 
           solid-bar        <--> pound sign 
           backslash        <--> ampersand 
           ampersand        <--> backslash 
           pound-sign       <--> left-bracket 
           dollar-sign      <--> exclamation point 
           exclamation pt.  <--> left-bracket 
        Device: 3270 
  CR[ISNL]{[=YES]|=NO} 
        YES specifies that when a carriage return character is sent to the 
        terminal a new line function (CR+LF) is performed.  NO specifies that 
        CR has some other function (see DEVICECR). If CRISNL=YES is specified, 
        DEVICECR=YES must not be specified. 
  CURSORR[EAD]{[=YES]|=NO} 
        YES specifies that the "change sessions" input function (usually <ESC> 
        <.>) is to access only sessions for which a read is pending.  If NO is 
        specified, or if there are no reading sessions, all sessions are 
        accesssible. 
  CURSORUP 
        YES specifies that the terminal is capable of moving its cursor upward 
        (in the opposite direction of line feed).  NO specifies this feature 
        is not present. 
        NOTE:  This option is displayable, but may not be specified with the 
        TERMINAL command. 
  DC[HMOVFLD]{[=YES]|=NO} 
        YES specifies that the local character-editing functions (insert and 
        delete characters) cause fields to the right of their invocation to 
        slide along with the data contained in them.  NO specifies that such 
        fields remain stationary on the screen.  YES causes the use of such 
        functions to be disabled if a field begins or ends to the right of the 
        editing position. 
  DEVICEB[S]{[=YES]|=NO} 
        YES indicates that a BS character sent to the terminal causes a 
        backspace.  NO specifies that a BS character be processed normally, 
        which may or may not cause a backspace. 
  DEVICEC[R]{[=YES]|=NO} 
        YES specifies that a carriage return character sent to the terminal 
        causes exactly a carriage return (moves the cursor to left margin of 
        the same line).  NO means that CR has some other (or no) effect. 
  DEVICEL[F]{[=YES]|=NO} 
        YES specifies that a line feed character sent to the terminal causes 
        exactly a line feed (moves the cursor down one line without horizontal 
        movement.)  NO means that LF has some other (or no) effect. 
  DEVP[OSOPTS]{[=YES]|=NO} 
        Indicates whether the terminal combines contiguous horizontal 
        positioning requests into a single internal operation (device 
        positioning optimization).  YES implies that if a tab to column 10 
        followed by a backspace were sent to the terminal, the carriage would 
        go directly to column 9. 
  DEVS[CROLL]{[=YES]|=NO} 
        YES specifies that the terminal is self-scrolling.  This means it 
        prints on a continuous form or rolls old lines off its screen as new 
        ones are added at the bottom.  NO means that lines are overwritten 
        when the screen is filled or the device is not a CRT. 
  DI[SPINPUT]{[=YES]|=NO} 
        YES specifies that the system is to display input characters on the 
        terminal (ECHOPLEX).  NO specifies that input display is to be 
        inhibited. 
  DS[PHEIGHT]= value 
        Specifies the number of displayable lines on the screen for a screen 
        type terminal.  Display height should be specified only if it is 
        smaller than HEIGHT.  Causes the default scrolling operation of the 
        terminal to use the bottom DSPHEIGHT lines of the addressable memory 
        so that the rest functions as a capture buffer, and so that direct 
        cursor positioning can be used. 
        Legal values are 0 - 254.  A value of zero should be used to indicate 
        that DSPHEIGHT = HEIGHT. 
  DV[CFLWCTRALG]= option 
        Specifies the flow control algorithm used by a buffered device to 
        prevent overfilling its buffer.  Options may be: 
        NONE    specifies that no algorithm is used. 
        ENQACK or ETXACK    specifies that CP-6 is to send an ENQ or ETX and 
        wait for the device to respond with ACK whenever enough characters 
        have been sent to fill the buffer.  The size of the buffer is 
        specified in the profile for the device. 
        DC1DC3    specifies that the device sends DC3 to halt the flow of 
        characters, and DC1 to resume it.  This algorithm is also commonly 
        known as XON/XOFF. 
  EA[SYAPPEND]{[=YES]|=NO} 
        Specifies, if YES, that records may be appended to the end of a file 
        simply by moving the cursor down past the end-of-file position. 
        Otherwise, a non-empty record must be entered at the end-of-file 
        position first.  The default causes this parameter to be ignored. 
  ED[ITOVR]{[=YES]|=NO} 
        YES specifies that character insertions and deletions (other than at 
        the end of the line) are to cause the rest of the line to be 
        repositioned to reflect the updated line.  NO specifies that inserted 
        characters are to be printed below the line and deletions are to be 
        marked with a backslash. 
  EN[BENTEXTSRDCHR]{[=YES]|=NO} 
        YES specifies that when entering or exiting the Subordinate Real 
        Device(s) (SRDs) affected by this monitor service, a character string 
        should be sent transparently to the device.  When entering, the 
        character string specified on the last M$WRITE's KEY with KEYTYPE = 
        ENTSRDCHR is sent.  When exiting, the character string specified on 
        the EXTSRD_CHR option in the device's profile is sent.  This feature 
        is used for preserving the status of graphics devices. 
  FC[NTBL]={CP5|CP5S1|CP5S2|FRM1|SE1|SE2|NO} 
        Specifies the name of a table which tells the terminal handler how to 
        interpret control functions.  If a name unknown to the system is 
        specified, the current table is not changed.  CP5 identifies the full 
        input function table and is the default.  CP5S1 and CP5S2 identify 
        subset tables.  FRM1 identifies forms functions.  SE1 identifies 
        Read-Write screen editing functions; SE2 identifies Read-Only screen 
        editing functions.  NO is a table containing only necessary 
        line-control functions (e.g., disconnect).  The values for each tab 
        name are shown below: 
                                NO 
                               ---- 
        Escape             Special        Control         Numeric 
        Characters         Character      Strings         Escapes 
        ----------------   ------------   -------------   -------------- 
        None               None           DISCONNECT      None 
                               CP5 
                               --- 
         Escape            Special        Control         Numeric 
         Characters        Character      Strings         Escapes 
         ---------------   ------------   -------------   -------------- 
         SOH               BS             BREAK           HT 
         STX               HT             DISCONNECT      C 
         EOT               LF             OVERRUN         D 
         HT                FF             PARITY CHECK    H 
         LF                CR                             I 
         VT                DC1                            M 
         CR                DC2                            R-T 
         DC2               DC3                            ^ (caret) 
         DC4               ETB                            . (period) 
         ETB               CAN 
         ESC               EM 
         $                 NAK 
         ' (apostrophe)    DEL 
         ( 
         ) 
         * 
         - 
         . (period) 
         : 
         < 
         > 
         A-Y 
         ^ (caret) 
         DEL 
                               CP5S1 
                               ----- 
         Escape            Special        Control         Numeric 
         Characters        Character      Strings         Escapes 
         ---------------   ------------   -------------   -------------- 
         SOH               BS             BREAK           HT 
         STX               HT             DISCONNECT      C 
         HT                LF             OVERRUN         D 
         EOT               FF             PARITY CHECK    H 
         LF                CR                             I 
         VT                DC2                            M 
         CR                ETB                            R-T 
         DC2               CAN                            ^ (caret) 
         DC4               EM                             . (period) 
         ETB               DEL 
         DEL 
         $ 
         ' (apostrophe) 
         * 
         - 
         . (period) 
         : 
         < 
         > 
         A-B 
         D-O 
         Q-R 
         U-Y 
         ^ (caret) 
                               CP5S2 
                               ----- 
         Escape            Special        Control         Numeric 
         Characters        Character      Strings         Escapes 
         ---------------   ------------   -------------   -------------- 
         EOT               BS             BREAK           HT 
         HT                HT             DISCONNECT      C 
         LF                LF             OVERRUN         D 
         VT                FF             PARITY CHECK    I 
         CR                CR                             R-T 
         DC2               DC2                            ^ (caret) 
         DC4               ETB                            . (period) 
         ETB               CAN 
         ' (apostrophe)    DEL 
         * 
         . (period) 
         : 
         < 
         > 
         D 
         F 
         G 
         I-K 
         N 
         Q 
         R 
         V 
         X 
         ^ (caret) 
         DEL 
                               FRM1 
                               ---- 
         Escape            Special        Control         Numeric 
         Characters        Character      Strings         Escapes 
         ---------------   ------------   -------------   -------------- 
         STX               BS             BREAK           I 
         EOT               HT             DISCONNECT      R-T 
         LF                LF             OVERRUN         . (period) 
         VT                CR             PARITY CHECK 
         CR                DC2 
         DC2               ETB 
         ETB               CAN 
         ESC               EM 
         ' (apostrophe)    DEL 
         *                 NAK 
         ) 
         ( 
         - 
         . (period) 
         : 
         < 
         > 
         A 
         B 
         D 
         G-K 
         M-O 
         Q 
         R 
         U 
         V 
         X 
         Y 
         i 
         DEL 
                               SE1 
                               ---- 
         Escape            Special        Control         Numeric 
         Characters        Character      Strings         Escapes 
         ---------------   ------------   -------------   -------------- 
         STX               BS             BREAK           HT 
         EOT               HT             DISCONNECT      LF 
         BS                LF             OVERRUN         A-E 
         HT                CR             PARITY CHECK    H 
         VT                DC2                            I 
         DC2               ETB                            M 
         FF                CAN                            P 
         CR                EM                             R-T 
         ESC               DEL                            ^ (caret) 
         ' (apostrophe)                                   . (period) 
         ) 
         ( 
         * 
         - 
         . (period) 
         : 
         < 
         > 
         A-D 
         G-K 
         M-R 
         U 
         V 
         X 
         Y 
         ^ (caret) 
         DEL 
                               SE2 
                               ---- 
         Escape        Special       Control        Numeric 
         Characters    Characters    Strings        Escapes 
         STX    A-D    None          BREAK          HT   I 
         DC2    G-J                  DISCONNECT     A-E  R-T 
         HT     N,Q,R                OVERRUN        .    ^ (caret) 
         CR     V                    PARITY CHECK   H    M 
         ESC    Y 
         <      > 
         -      * 
         .      ^ (caret) 
  FF[FLUSH]{[=YES]|=NO} 
        YES specifies that the device (usually a plotter) needs to have a 
        form-feed operation performed to complete the display of any data 
        still buffered in the device.  NO specifies that a new line operation 
        is sufficient. 
  FFI[NCCR]{[=YES]|=NO} 
        YES specifies that the form-feed function for this terminal also 
        positions to the left margin.  NO specifies that it positions only 
        vertically. 
  FU[LLDUXPAPERTAPE]{[=YES]|=NO} 
        YES specifies that terminal input is handled using the following paper 
        tape conventions: 
        1.  If DISPINPUT = YES, DC3 (X-OFF) and DC1 (X-ON) characters are sent 
        to the terminal so that the input does not overflow available 
        buffering space. 
        2.  A DEL character on input is ignored. 
        3.  A LF character received as the first character of an input message 
        is ignored when M$READ is using the default input function table (CP5, 
        CP5S1, CP5S2). 
        NO specifies normal processing of terminal input. 
  FW[INDOW]=name 
        Specifies the four-character name of a stream in an adjacent window 
        that is to supply or receive any space indicated by the WWIDTH or 
        WLENGTH options. 
        name   -   is of the form 'UCnn' 
  HA[LFDUXPAPERTAPE]{[=YES]|=NO} 
        YES specifies that the FULLDUXPAPERTAPE conventions are to be followed 
        and that absolutely no characters are to be sent to the terminal for 
        either output or echoing.  NO specifies normal processing of terminal 
        input. 
  HBRDRC[HR]= c 
        Specifies the single ASCII character to be used to mark the horizontal 
        border space(s).  It will fill every character position of the 
        farthest line of the border space. 
        c    is a single ASCII character. 
  HBRDRS[IZ]= value 
        Specifies the size in lines of the horizontal border space(s) (TOPBRDR 
        and BTMBRDR).  The default is zero, which causes this Note that the 
        border presence parameters must be used to remove a border - 
        HBRDRSIZ=0 won't work. 
        value    is a decimal integer from 0 to 15. 
  HE[IGHT]=value 
        Indicates the number of lines on the screen of a screen-type terminal. 
        HEIGHT=0(zero) for non-screen-type terminals.  Value is a decimal 
        integer from 0 to 254.  The default is 255, which means that the 
        height is not altered. 
  HSA[LL]{[=YES]|=NO} 
        Specifies whether, if HSCROLL is YES, all the records of a screen 
        editing window are to be scrolled simultaneously whenever any 
        horizontal shift occurs.  NO specifies that only the record containing 
        the cursor is shifted by horizontal cursor motion and that a shifted 
        record is realigned with the rest of them when the cursor is away. The 
        repaint function, <ESC><->, may be used if HSALL=NO to align the other 
        records with the cursor record. 
        The context in which HSALL is stored only exists when a screen-editing 
        window is being used. 
  HSC[ROLL]{[=YES]|=NO} 
        Specifies, if RETYPOVR and EDITOVR are also true, that input editing 
        is to occupy only one line, even if the input record is longer than 
        the space remaining on the line after the prompt.  The HSMARGIN and 
        HSSHIFT parameters may be used to control the display characteristics 
        of this mode. 
  HSM[ARGIN]=value 
        Specifies, if HSCROLL=YES, the closest the cursor is to be allowed to 
        approach the edge of an input area without shifting a partially 
        displayed record to reveal more of it.  Values less than 128 specify 
        the distance in columns.  Higher values specify a percentage of the 
        width of the window as %SCROLL_PERCENT#+percent. 
        value   is a decimal value from 0 to 254. 
  HSS[HIFT]=value 
        Specifies, if HSCROLL=YES, the number of columns that an input image 
        is to be shifted when the user attempts to move the cursor closer than 
        HSMARGIN to an incompletely displayed end of the record.  The keyword 
        CENTER may be specified to request that the character under the cursor 
        be positioned as closely as possible to the center of the displayed 
        portion of the record when a shift occurs.  Otherwise, the value is 
        specified in columns or as a percentage of the width of the input 
        area. 
  IN[PUTIGNORE]{[=YES]|=NO} 
        YES sets input-ignore mode which specifies that characters input from 
        the terminal are not to be sent to the user program.  An M$READ issued 
        in input-ignore mode is processed as if nothing was input from the 
        terminal.  Characters are echoed to the terminal but they are not sent 
        to the program.  This function allows coupled terminals to converse 
        freely without sending any input to running programs or processors. 
        NO specifies normal processing of terminal input. 
  INS[ERTMODE]{[=YES]|=NO} 
        YES specifies insert mode is to be enabled.  In insertion mode, 
        characters that are typed are inserted to the left of the cursor; 
        also, the DEL key always deletes the character (if any) under the 
        cursor.  NO disables the insertion mode: characters that are typed 
        replace the character under the cursor, and the DEL key deletes the 
        character under the cursor, except that when the cursor is at the 
        right end of the insertion window, typed characters are inserted into 
        the input record, and the DEL key deletes the character to the left of 
        the cursor. 
  KEE[PTYPAHD]{[=YES]|=NO} 
        YES specifies that a session change as a result of the AUTOCURSOR 
        parameter is to move any typeahead from the old session to the new one 
        for use as input to the new session.  NO specifies that the typeahead 
        is to remain with the previous session.  The default causes this 
        parameter to be ignored. 
  KEYI[NCR]= value 
        Specifies default key increment to be used to insert new records.  See 
        KEYTYPE.  The maximum value 65535 requests that key incrementation is 
        to be disabled, requiring that record insertion be performed by the 
        host program. 
        value    is a decimal number from 1 to 65535.  The default is zero. 
        The context in which KEYINCR is stored only exists when a 
        screen-editing window is being used. 
  KEYT[YPE]= option 
        Specifies the key incrementation algorithm to be used to insert new 
        records.  The options are as follows: 
        BIN10    specifies that KEYINCR is to be divided by 10 until it fits. 
        If KEYINCR=1000, then the first of 1000, 100, 10, and 1 that fits is 
        used. 
        BINHLF    specifies that KEYINCR is to be halved.  If KEYINCR=32, then 
        the first of 32, 16, 8, 4, 2, and 1 that is small enough will be used. 
        BIN521    specifies that division by 5, 2.5, and 2 is to be repeated. 
        If KEYINCR=1000, then the sequence 1000, 500, 200, 100, 50, 20, 10, 5, 
        2, and 1 is used. 
        STRING    specifies that key incrementation is not possible. 
        The context in which KEYTYPE is stored only exists when a 
        screen-editing window is being used. 
  LFI[SNL]{[=YES]|=NO} 
        YES specifies that when a line feed character is sent to the terminal 
        a new line function (CR+LF) is performed.  NO specifies that LF has 
        some other function (see DEVICELF). If LFISNL=YES is specified, then 
        DEVICELF=YES must not be specified. 
  LFT[BRDR]{[=YES]|=NO} 
        Specifies whether space is to be reserved at the left to separate this 
        window from the one to the left.  The default is NO for a new window. 
  LI[MBOCLM]{[=YES]|=NO} 
        YES indicates that a backspace operation, immediately after displaying 
        a character in the rightmost column of the terminal, has the same 
        effect as for any other column.  NO specifies that the cursor remains 
        in the rightmost column after a character is displayed there. 
        Applicable only if AUTONL=NO. 
  LOC[ALECHO]{[=YES]|=NO} 
        YES indicates that any characters received from the terminal have 
        already been displayed on the terminal.  This option is especially 
        useful for very slow connections where the normal CP-6 echo mechanism 
        becomes distracting.  NO specifies normal processing. 
  LO[WERCASE]{[=YES]|=NO} 
        YES specifies that any uppercase alphabetic characters input from the 
        terminal are to be sent to the user program as lowercase letters.  In 
        addition, the following five characters are translated: 
        Character           Translation 
        ---------           ----------- 
            @                    ^ 
            [                    { 
            \                    | 
            ]                    } 
            ^                    ~ 
        NO specifies normal processing of terminal input.  This feature is 
        provided to enable terminals that are uppercase only to input 
        lowercase characters. 
  LOWERCASEP[RINTS]{[=YES]|=NO} 
        YES indicates that the terminal is capable of printing (displaying) 
        lower-case letters.  NO indicates that the terminal is not capable of 
        printing lower-case letters. 
  MA[XATRS]= value 
        Specifies the number of field definition positions permitted on any 
        line of the device. 
        value    is a decimal number from 0 to 254. 
  MIC[ROFPL]{[=YES]|=NO} 
        Indicates whether or not this terminal is a PC that is configured to 
        use microFPL programs. 
  MINL[ENGTH]=value 
        Specifies the minimum length for this window in lines.  The default is 
        255, which causes this parameter to be ignored unless this is a new 
        window, in which case it means the the length is to be fixed.  See 
        OPTIONAL also. 
        value    is a decimal integer from 0 to 254. 
  MINW[IDTH]=value 
        Specifies the minimum width for this window in columns.  The default 
        is 255, which causes this parameter to be ignored unless this is a new 
        window, in which case it means the the width is to be fixed.  See 
        OPTIONAL also. 
        value    is a decimal integer from 0 to 254. 
  MSGH[ALT]{[=YES]|=NO} 
        Specifies, if YES, that output to the terminal is to be halted after 
        an operator message until the user enters the customary output 
        continuation character. 
  MSG[LINE]{[=YES]|=NO} 
        Specifies, if YES and the profile indicates that the terminal has such 
        a facility, that the message line of the terminal is to be used to 
        display all operator messages. 
  NOF[LDTRM]{[=YES]|=NO} 
        Specifies whether an otherwise unterminated field definition extends 
        to the end of the device.  NO specifies that such a field extends only 
        to the end of the line. 
  NO[OPTMIZ]{[=YES]|=NO} 
        YES specifies that carriage positioning optimization is not to be 
        done.  This is useful for writing to mini-computers and paper tape 
        punches.  NO specifies that data is to be written as efficiently as 
        possible. 
  ONE[SPACEEDIT]{[=YES]|=NO} 
        Specifies whether one space or two spaces should be inserted between 
        sentences for joining operations.  NO specifies two spaces should be 
        used. 
        The context in which ONESPACEEDIT is stored exists only when a 
        screen-editing window is being used. 
  OPD[TAB]{[=YES]|=NO} 
        YES specifies that the terminal has device tabs which can be set by 
        the operator.  NO specifies that they are programatic (PROGDTAB) or 
        nonexistent. 
  OPT[IONAL]{[=YES]|=NO} 
        Specifies whether the window size is permitted to drop below MINWIDTH 
        or MINLENGTH.  If so, the window will be removed from the screen when 
        it is too small, but its context will be maintained.  The default is 
        NO for a new window. 
  OU[TPUTDISCARD]{[=YES]|=NO} 
        YES specifies that output is not sent to the terminal.  M$WRITE 
        requests appear to work to the user program but no characters are sent 
        to the terminal.  An M$READ that can be immediately satisfied by 
        typed-ahead input is processed normally.  AN M$READ that cannot be 
        satisfied by typed-ahead input turns off output-discard mode.  NO 
        specifies normal processing of output.  Performs same function as 
        <ESC> <W>, but pending output is not deleted. 
  PAG[EHALT]{[=YES]|=NO} 
        YES specifies that when the end of a page is reached, output is halted 
        until the user types a carriage return.  NO specifies that output 
        continues in this situation.  YES is often used to prevent a high 
        speed CRT from printing faster than its operator can read. 
  PAR[ITY]=option 
        Specifies the type of character parity at the terminal. 
        Possible options are: 
        Option  Parity 
        ------  ------ 
        NONE    On input the parity bit is ignored. 
                On output the parity bit of 
                translated characters is zero and 
                the parity bit of transparent 
                characters is unchanged. 
        ZERO    Parity is 0. 
        ODD     Parity is odd. 
        EVEN    Parity is even. 
        ONE     Parity bit is 1. 
        DC      Do not change parity. 
  PAR[ITYCHECK]{[=YES]|=NO} 
        YES specifies that characters input from the terminal are to be 
        checked for proper parity.  A character with bad parity is echoed as a 
        pound sign (#) and transmitted to the program as a SUB character; a 
        parity error completion type is reported on the M$READ.  NO specifies 
        that parity is not to be checked. 
  PARK[CURSOR]{[=YES|=NO} 
        YES specifies that the cursor is to be moved to the home position of 
        the window. 
  PR[INTHALT]{[=YES]|=NO} 
        YES specifies that if the terminal is being halted at the end of each 
        page of output that the message (CR TO GO) is to be printed to prompt 
        the user to continue the output.  NO specifies that no prompt be 
        issued in this situation. 
  PRINTT[YPE]{[=YES]|=NO} 
        YES specifies that the terminal prints on a form or screen such that 
        vertical positioning is sensible.  NO specifies that the terminal 
        produces records only (like a card punch) and vertical positioning is 
        meaningless. 
  PRO[GDTAB]{[=YES]|=NO} 
        YES indicates that the terminal device tabs are programmatic.  NO 
        indicates that the terminal device tabs are manual. 
  RC[RWRAP]{[=YES]|=NO} 
        Specifies whether editing position operations (like backspace, 
        word-skip, character-search) are to cross record boundaries. 
        The context in which RCWRAP is stored only exists when a 
        screen-editing window is being used. 
  REL[PAGE]{[=YES]|=NO} 
        YES specifies that if the terminal is being halted at the end of each 
        page of output, that the page boundary will be relative to the last 
        read which halted the terminal (and was not satisfied by type-ahead). 
        Thus the terminal would halt when the last input line had just 
        scrolled off the top of the screen.  NO specifies that the halts occur 
        every screen size of lines independent of whether there are inputs. 
  RET[YPOVR]{[=YES]|=NO} 
        YES specifies that retypes are to overprint the line being retyped. 
        NO specifies that they are to be printed on the next line. 
  RH[TBRDR]{[=YES]|=NO} 
        Specifies whether space is to be reserved at the right to separate 
        this window from the one to the right.  The default is NO for a new 
        window. 
  SC[ROLL]{[=YES]|=NO} 
        YES specifies that the terminal is to be scrolled, that is, treated as 
        though the media is a continuous form.  No specifies that when a page 
        has been filled, a screen erase is sent and a new page started. 
  SE[NDBKSPACE]{[=YES]|=NO} 
        YES specifies that when the user backspaces over a character (A) and 
        overstrikes it (with B), the original character, a backspace, and the 
        overstriking character are returned to the reading program (A - BS - 
        B).  NO specifies that in this situation only the overstriking 
        character is sent (B).  Note that no backspaces may be involved in the 
        above operation. 
  SIM[PERF]{[=YES]|=NO} 
        YES specifies that underscores will be printed where the perforation 
        would normally appear on the terminal form.  This gives the appearance 
        of perforated forms on terminals with continuous form paper.  NO 
        inhibits this printing. 
  SI[NPUTSZ]=value 
        Specifies the minimum length of lines typed which are to be remembered 
        by the system to be re-used <ESC> <D>. 
        value    is a decimal integer from 0 to 254.  A value of 0 or 1 
        specifies that all empty lines are saved.  The default is 3. 
  SP[ACEINSERT]{[=YES]|=NO} 
        YES specifies that horizontal tab (HT) characters input from the 
        terminal are to be replaced by an appropriate number of blanks based 
        on user input tabstop settings prior to being placed in the M$READ 
        buffer.  NO specifies that HT characters are to be placed in the 
        buffer unchanged.  (This can result in a significant space saving in 
        large files.) 
  SPC[BFRPRT]{[=YES]|=NO} 
        If SPCBFRPRT=NO then any VFC will be translated such that all paper 
        motion will follow print (e.g., space 4 and print VFCs will be 
        translated into write a blank line and space 4 followed by write the 
        read data and don't space).  If SPCBFRPRT=YES, then no special VFC 
        translation is done. 
        YES is the default. 
  SPE[ED]=value 
        Specifies the line speed of the terminal. 
        value    is a decimal integer indicating the actual baud rate to be 
        used.  Rates currently supported are: 
                110 
                150 
                200 
                300 
                600 
                1200 
                2400 
                4800 
                9600 
                19200 
  TABR[ELATIVE]{[=YES]|=NO} 
        YES specifies that on input and input echoing, user tab stops are 
        relative to the column where input was prompted.  NO specifies that 
        user tab stops are relative to column 1. 
  TABS[IM]{[=YES]|=NO} 
        Specifies positioning of horizontal tabs for output.  YES specifies 
        that when a horizontal tab (HT) character is sent to the terminal, the 
        cursor is positioned to the next logical tab stop.  If no tabstops are 
        set, each tab character is replaced by a single blank.  NO specifies 
        that HT characters are sent to the terminal unchanged.  (This can 
        result in the cursor being positioned one space or several spaces 
        depending on the device tabs of the terminal.) 
  TE[XTEDIT]{[=YES]|=NO} 
        Specifies whether joining operations are to insert or delete blanks in 
        order preserve normal text-like appearance (e.g., one blank except 
        after sentence-ending punctuation). 
        The context in which TEXTEDIT is stored only exists when a 
        screen-editing window is being used. 
  TO[PBRDR]{[=YES]|=NO} 
        Specifies whether space is to be reserved at the top to separate this 
        window from the one above it.  The default is NO for a new window. 
  TR[UNCATE]{[=YES]|=NO} 
        YES specifies that output lines which exceed the platen width will be 
        truncated to fit on one line.  NO specifies that such lines will wrap 
        to the next line. 
  TRUO[VRPRT]{[=YES]|=NO} 
        YES specifies that the terminal performs overprinting.  NO specifies 
        that the terminal is not capable of overprinting (that is, upspace 
        cannot be inhibited or multiple characters cannot be displayed in one 
        position).  NO specifies that the terminal is not capable of 
        overprinting.  Currently ignored by VDH, but used by APL. 
  TT[YTYPE]{[=YES]|=NO} 
        YES specifies that the terminal is capable of displaying what it 
        sends.  YES is typically specified for a device such as a keyboard 
        printer or CRT.  NO specifies that input is not displayed. 
  UP[PERCASE]{[=YES]|=NO} 
        YES specifies that any lowercase alphabetic characters input from the 
        terminal are to be sent to the user program as uppercase letters.  NO 
        specifies normal processing of terminal characters. 
  VBRDRC[HR]=c 
        Specifies the single ASCII character to be used to mark the vertical 
        border space(s).  It will fill every character position of the 
        farthest column of the border space. 
        c    is a single ASCII character. 
  VBRDRS[IZ]= value 
        Specifies the size in columns of the vertical border space(s) (LFTBRDR 
        and RHTBRDR).  The default is zero.  Note that the border presence 
        parameters must be used to remove a border - HVBRDRSIZ=0 won't work. 
        value    is a decimal integer from 0 to 15. 
  VSM[ARGIN]= value 
        Specifies the closest that the cursor is to be allowed to approach the 
        top or bottom of the window without shifting the image to reveal more 
        of the file.  Values less than %SCROLL_PERCENT# (128) specify the 
        distance in lines.  Higher values specify a percentage of the height 
        of the window as %SCROLL_PERCENT#+percent. 
        value    is a decimal number from 0 to 254. 
        The context in which VSMARGIN is stored only exists when a 
        screen-editing window is being used. 
  VSS[HIFT]= value 
        Specifies the lines to shift the image when the user attempts to move 
        the cursor closer than VSMARGIN to an incompletely displayed end of 
        the file.  The keyword CENTER may be specified to request that the 
        line under the cursor be positioned as close as possible to the center 
        of the displayed portion of the file when a shift occurs.  Otherwise, 
        the value is specified in lines or as a percentage of the height of 
        the window.  The preprocessor equates %SCROLL_PERCENT# and 
        %SCROLL_CENTER# may be used to set the value at runtime. 
        value    is a decimal number from 0 to 254. 
        The context in which VSSHIFT is stored only exists when a 
        screen-editing window is being used. 
  WI[DTH]=value 
        Specifies the number of printable columns on the terminal. 
        value    is a decimal integer from 0 to 510. 
  WL[ENGTH]=value 
        Specifies the size of the window, in absolute or incremental lines or 
        as a percentage of the full screen (or of the current size for an 
        existing window). 
  WO[RDWRAPCLM]={value|NO|OFF} 
        Specifies the maximum length of lines containing blanks that will be 
        returned to the reading program.  If a longer line is entered, the 
        characters past the space before WORDWRAPCLM will be saved for use in 
        the next read operation.  A value of zero, NO, or OFF disables this 
        facility. 
        value    is a decimal number from 0 to 254. 
  WR[APPAGE]={[YES]|NO} 
        YES specifies for CRTs with SCROLL=NO that the screen is to be erased 
        one line at a time, such that the line below the cursor is always 
        blank.  NO specifies that the entire screen is to be erased after 
        using the bottom line. 
  WW[IDTH]=value 
        Specifies the size of the window, in absolute or incremental columns 
        or as a percentage of the full screen (or of the current size for an 
        existing window). 
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
00044
00045
00046
00047
00049
00048
00049
00050
00051
00052
00053
00054
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
00067
00068
00069
00070
00071
00072
00073
00074
00075
00077
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
TERMINAL_OPS
TERMINAL_OPS
Syntax: 
TIME 
Parameters: 
NONE 
Description: 
TIME displays the current time and date.  The format of the display is: 
mmm dd 'yy hh:mm    (month)(day)(year)(hours)(minutes) 
Examples: 
!TIME 
displays the current time and date. 
Related Commands: 
DATE 
00002
00003
00001
00004
Syntax: 
TITLE string 
Parameters: 
string   -   specifies the heading text.  Any ASCII characters including 
blanks can be specified.  If non-printing ASCII characters are included, they 
are translated as blanks.  Title text cannot be continued. 
Description: 
TITLE inserts a heading at the beginning of each logical page listed on LP01 
(LP). 
Examples: 
!TITLE STRESS-ENERGY TENSOR ANALYSIS 
The above example causes the title string to be output at the top of each 
logical page listed on LP01 by the executing program. 
Related Commands: 
SET, LDEV 
00002
00003
00001
00004
TERMINAL_OPS
UNDER
Format: 
UNA[RCHIVE] fid1[, fid2] ... 
Parameters: 
fid1, fid2    specify CP-6 file identifiers. 
Description: 
This command modifies the FIT of the specified files to remove them from the 
archive system.  (Only the TERMINATE (reserved) flag in the FIT remains set, 
indicating that the file is no longer maintained in the archive system.) 
Usage Notes: 
Before EFT does an unarchive on any file, it performs the following checks: 
1.  Is this file ready to be unarchived? 
2.  If this file is ready to be unarchived, then who can unarchive it? 
The rules of determining whether a file is ready for unarchiving are: 
1.  An actively archived file can be unarchived right away. 
2.  If a FETCH has been issued for an actively archived file, it must be 
    retrieved from tape before it can be unarchived. 
3.  An inactively archived file must be fetched and retrieved before it can be 
    unarchived.  However, anyone with FMSEC priv can unarchive an inactively 
    archived file immediately.  The result is similar to a cleanup operation 
    and results in the complete deletion of the file from disk. 
After determining that the file is ready, EFT checks whether the account from 
which the UNARCHIVE command is issued fits any of the following: 
1.  The account is the original creator. 
2.  The account has FMSEC priv. 
3.  The account has DELF file access permission to that file (thru PIG). 
00002
00001
00003
Syntax: 
{U|UNDER} [debuggername] 
Parameters: 
debuggername   -   is DELTA or a user-supplied debuggger. 
Description: 
UNDER calls a debug processor under which the next rununit will execute.  If 
debuggername is not specified, DELTA is the default. 
Examples: 
!U 
indicates that the run unit specified in the next command is to be executed 
under control of DELTA. 
!UNDER MYDEBUG 
indicates that the run unit specified in the next command is to be executed 
under control of the debug processor named MYDEBUG. 
Related Commands: 
DELTA, RUM 
00002
00003
00001
00004
Format: 
UNF[ETCH] fid1[, fid2] ... 
Parameters: 
fid1, fid2    specify CP-6 file identifiers. 
Description: 
This command rescinds a FETCH request, unlocking the specified files.  For any 
specified file not currently queued for FETCH, an error is reported.  UNFETCH 
can be used on a file only by the creator of the respective FETCH request or 
by persons with active FMSEC privileges. 
00002
00001
Syntax: 
UNHOLD jobid [output-file-spec] [(number[,number...])]... 
Parameters: 
jobid   -   is the symbiont output job id and may be in either of the 
following forms: 
    sysid    the job sysid assigned by the system and displayed in a message 
    sent to the user when the BATCH command that submitted the job was 
    processed. 
    jobname[.account]    the alphanumeric job name which was defined with the 
    NAME option on the JOB command for the job to be aborted.  The named job 
    must have been submitted under the running account.  Account specifies the 
    account in which the named job is to be found. 
    output-file-spec   -   takes one of the following forms: 
        -1 or (1)   -   allows the specification of one subfile. 
        (1[2,...])   -   allows the specification of a list of subfiles. 
    Note: Since JOB allows a jobname of just digits, whenever a sysid or a 
    jobname is allowed, if IBEX encounters a 6 or less digits number, it 
    treats this as a sysid.  Anything of greater length is treated as a 
    jobname.  If a jobname exists that can be treated as a sysid, the user 
    must put the jobname inside single quotes to indicate to IBEX that this is 
    a jobname.  Some examples are 'jobname'-1, '1234'-1, '1234'(1), 
    'jobname'(1). 
number   -   specifies a symbiont output file number. 
Description: 
The UNHOLD command removes a job's symbiont output from HOLD status (via the 
HOLDCOPIES option on the LDEV command, a user can specify that a certain 
number of copies of an output symbiont file are to be printed, after which the 
file is put in HOLD state).  The job is identified as for CHECK.  If the job 
has no current output, an error is returned.  If the job's account does not 
match that of the service call issuer, an error is returned and no action 
taken.  Otherwise, the job's output is removed from HOLD and becomes a 
candidate for printing. 
Examples: 
UNHOLD 12345 
UNHOLD 12345(1) 
UNHOLD 12345 (1,3) 
UNHOLD STARJOB, PL6_CMPL (1,4) 
Related Commands: 
HOLD, LDEV 
00002
00003
00001
00004
Format: 
UNS[TOW] fid1[, fid2] ... 
Parameters: 
fid1, fid2    specify CP-6 file identifiers. 
Description: 
This command unlocks the specified files, previously queued for STOW, to 
permit further update activity.  For any specified file not currently queued 
for STOW, an error is reported. 
Usage Notes: 
1.  This command may be used only if:  a) the account is authorized with the 
    STOW attribute and the current user is the file creator or b) the account 
    is authorized with STOW and the current user has FMSEC privilege active. 
2.  While the file is queued for STOW or FETCH, it cannot be updated. 
00002
00001
00003
FID_UR
    The following table describes special names of unit record devices:\ 
  fid   Description              Batch Meaning     On-line Meaning 
LO    An output device. The    LP01              On-line terminal 
      destination for listing 
      output. 
CR    The current command      Command           Command 
      stream input source:     stream            stream 
      an XEQ file, the 
      on-line terminal, or 
      the job stream. 
ME    For input requests,      Command           Command 
      equivalent to CR.        stream            stream 
      For output requests,     LP01              On-line terminal 
      equivalent to LO. 
UC    In on-line mode, the     NO                On-line terminal 
      user terminal. 
LP    An abbreviation for      LP01              LP01 
      LP01, denoting a 
      line printer. 
CP    An abbreviation for      CP01              CP01 
      CP01, denoting a card 
      punch. 
GR    An abbreviation for      GR01              GR01 
      GR01,generally denot- 
      ing a spooled output 
      graphics device. 
JF    An output pseudo- 
      device.  When the JF 
      DCB is closed, with 
      DISP=SAVE, the records 
      that have been written 
      to JF are inserted at 
      the head of the command 
      stream, and executed 
      when the current 
      command finishes. 
JE    An output pseudo-device. 
      Records written to JE 
      are submitted as a new 
      batch job when the JE 
      DCB is closed (with 
      DISP=SAVE). 
NO    An input/output pseudo- 
      device.  Returns an 
      end-of-file when read; 
      discards all records 
      written to it. 
The user logging on to time sharing is assigned three streams by default: 
     o   UC98    displays the command processor stream 
     o   UC01    displays the user program stream 
     o   UC99    displays the debugger stream 
It is possible to see the window characteristics of these default streams by 
using the DISPLAY command with the LDEV UC option.  This displays the status 
of all defined terminal streams for a user. 
Additional streams can be created by using the LDEV command (or its equivalent 
monitor service - M$LDEV). 
Streams created by LDEV remain associated with the user until removed by an 
LDEV REMOVE or LOGON option.  A stream is also created when a DCB is opened to 
a stream (RES=UCnn) that is not currently defined.  A stream created by 
opening a DCB is automatically removed when the last DCB open to it is closed. 
A stream may be directed through any desired window by specifying the "fid" 
portion of the LDEV command: 
!LDEV UCnn UCmm 
The above command directs UCnn through the window currently displaying the 
UCmm stream. 
CP-6 windows are also exclusively created by the LDEV function or by the 
opening of a DCB.  Once created, windows may have their characteristics 
modified by all three mechanisms: LDEV, OPEN, and the TERMINAL command (whose 
equivalent monitor service is M$STRMCTL). 
Usage Notes: 
Window manipulation is subject to the following rules: 
1.  Every window occupies a rectangular area on the screen.  No irregular 
    shapes. 
2.  Every window size adjustment must be accomplished by adjusting only one 
    border and only any other windows adjacent to that border, while still 
    maintaining rule 1. 
3.  A window exists as long as any stream is associated with it. 
    A new window is created by dividing an existing window into two parts, 
    either vertically or horizontally, depending on the POSITION option used. 
    WLENGTH or WWIDTH may be used to specify how big to make the new window. 
    All other window characteristics are copied from the window being divided. 
    The FWINDOW option may be used to specify which window to divide, 
    overriding the default, which is UC01 or UCmm from the most recent LDEV 
    command specifying it. 
4.  The border options permit the user to delineate the windows with rows 
    and/or columns of spaces and/or border characters.  The TOPBRDR, BTMBRDR, 
    LFTBRDR, and RHTBRDR options indicate which edges of the windows are to 
    have borders.  The HBRDRSIZ and VBRDRSIZ options specify how many lines or 
    columns the borders are to occupy.  The HBRDRCHR and VBRDCHR options 
    specify which character is to be displayed in the borders. 
Examples: 
The following example is for a Honeywell VIP7801 terminal. 
!DISPLAY LDEV UC 
   Ldev assignments: 
UC98 Position=(1,1), WLength=24, WWidth=80, MinWidth=0, MinLength=0, 
     HBrdrSIZ=1, HBrdrChr=' ', VBrdrSiz=1, VBrdrChr=' ' 
UC01 Position=(1,1), WLength=24, WWidth=80, MinWidth=0, MinLength=0, 
     HBrdrSIZ=1, HBrdrChr=' ', VBrdrSiz=1, VBrdrChr=' ' 
UC99 Position=(1,1), WLength=24, WWidth=80, MinWidth=0, MinLength=0, 
     HBrdrSIZ=1, HBrdrChr=' ', VBrdrSiz=1, VBrdrChr=' ' 
Using the DISPLAY command with the LDEV UC option displays the characteristics 
of the three default streams assigned to the user.  For each stream (UC98, 
UC01, and UC99): 
    Position = 1,1    the starting position is row 1, column 1 
    WLength=24    window length is 24 lines 
    WWidth=80    window width is 80 characters 
Initially the window occupies all of the displayable space for this terminal. 
The three streams (command, user, and debugger) are all displayed in this 
window. 
A second window may be created by using the LDEV command: 
!LDEV UC98,POS=TOP,WL=2 
The above command creates a separate window for UC98 of length 2.  This also 
results in a reduction of length for the UC01/UC99 window to 22 lines.  As a 
result, all command processor stream data will appear on the first 2 lines 
(for example, IBEX data), while user program stream data (e.g., EDIT) and 
debugger stream data (e.g.  DELTA) will appear on the bottom 22 lines. 
The characteristics of a window may be changed by using the LDEV or TERMINAL 
command: 
!LDEV UC98,WL=10   or    !TERMINAL UC98 WL=10 
Either of the above commands changes the window size (length) of UC98 from 2 
to 10.  This also results in a reduction of length for the UC01/UC99 window to 
14 lines.  As a result, all command processor stream data will appear on the 
first 10 lines, while user program stream data and debugger stream data will 
appear on the bottom 14 lines. 
By creating a fourth window and using the LDEV LOGON option, the user can 
perform more than one task at the same time.  Note that the LOGON option can 
not be used with the three default-assigned window streams.  The following 
command shows the creation of a new window using the LOGON option: 
!LDEV UC05,POS=BOTTOM,WL=10,LOGON 
The following example demonstrates how every size change (WW or WL option) 
requires that exactly one border be adjusted: 
         +-------------------+ 
         |                   | 
         |       UC01        | 
         +---------+---------+ 
         |         |         | 
         |  UC98   |  UC99   | 
         +---------+---------+ 
Once the above configuration has been created, the WL option is inoperative 
for UC98 and UC99 until they are 'combined'.  This can be done by using: 
  !LDEV UC99 UC98 
which results in the following configuration: 
         +-------------------+ 
         |                   | 
         |       UC01        | 
         +-------------------+ 
         |     Combined      | 
         |    UC98 & UC99    | 
         +-------------------+ 
See WINDOW_OPS 
00002
00001
To obtain information about vertical format control characters, enter: 
!HELP (IBEX) VFC character 
where character is: 
    A character or mnemonic (for unprintables) 
    An octal value in the form          O'ooo' 
    A decimal value in the form         D'ddd' 
    A hexadecimal value in the form     X'xx' 
NOTE:  The following must be enclosed in single quotes: 
              greater than ('>'). 
To list the entire VFC character set, type ??<CR> at the next prompt. 
The table has the following format: 
  CODE   OCTAL     DECIMAL   HEX      MEANING 
 A     O'101'    D'065'    X'41'    Print, then upspace 1 line. 
 B     O'102'    D'066'    X'42'    Print, then upspace 2 lines. 
 C     O'103'    D'067'    X'43'    Print, then upspace 3 lines. 
 D     O'104'    D'068'    X'44'    Print, then upspace 4 lines. 
 E     O'105'    D'069'    X'45'    Print, then upspace 5 lines. 
 F     O'106'    D'070'    X'46'    Print, then upspace 6 lines. 
 G     O'107'    D'071'    X'47'    Print, then upspace 7 lines. 
 H     O'110'    D'072'    X'48'    Print, then upspace 8 lines. 
 I     O'111'    D'073'    X'49'    Print, then upspace 9 lines. 
 J     O'112'    D'074'    X'4A'    Print, then upspace 10 lines. 
 K     O'113'    D'075'    X'4B'    Print, then upspace 11 lines. 
 L     O'114'    D'076'    X'4C'    Print, then upspace 12 lines. 
 M     O'115'    D'077'    X'4D'    Print, then upspace 13 lines. 
 N     O'116'    D'078'    X'4E'    Print, then upspace 14 lines. 
 O     O'117'    D'079'    X'4F'    Print, then upspace 15 lines. 
 `     O'140'    D'096'    X'60'    Print (no vertical motion); 
                                    position to beginning of line. 
 a     O'141'    D'097'    X'61'    Upspace 1 line, then print. 
 b     O'142'    D'098'    X'62'    Upspace 2 lines, then print. 
 c     O'143'    D'099'    X'63'    Upspace 3 lines, then print. 
 d     O'144'    D'100'    X'64'    Upspace 4 lines, then print. 
 e     O'145'    D'101'    X'65'    Upspace 5 lines, then print. 
 f     O'146'    D'102'    X'66'    Upspace 6 lines, then print. 
 g     O'147'    D'103'    X'67'    Upspace 7 lines, then print. 
 h     O'150'    D'104'    X'68'    Upspace 8 lines, then print. 
 i     O'151'    D'105'    X'69'    Upspace 9 lines, then print. 
 j     O'152'    D'106'    X'6A'    Upspace 10 lines, then print. 
 k     O'153'    D'107'    X'6B'    Upspace 11 lines, then print. 
 l     O'154'    D'108'    X'6C'    Upspace 12 lines, then print. 
 m     O'155'    D'109'    X'6D'    Upspace 13 lines, then print. 
 n     O'156'    D'110'    X'6E'    Upspace 14 lines, then print. 
 o     O'157'    D'111'    X'6F'    Upspace 15 lines, then print. 
 P     O'120'    D'080'    X'50'    Print, then advance to bottom of 
                                    page. 
 0     O'060'    D'048'    X'30'    Advance to top of page, then print. 
 Q     O'121'    D'081'    X'51'    Print, then advance to channel 1. 
 R     O'122'    D'082'    X'52'    Print, then advance to channel 2. 
 S     O'123'    D'083'    X'53'    Print, then advance to channel 3 . 
 T     O'124'    D'084'    X'54'    Print, then advance to channel 4. 
 U     O'125'    D'085'    X'55'    Print, then advance to channel 5. 
 V     O'126'    D'086'    X'56'    Print, then advance to channel 6. 
 W     O'127'    D'087'    X'57'    Print, then advance to channel 7. 
 X     O'130'    D'088'    X'58'    Print, then advance to channel 8. 
 Y     O'131'    D'089'    X'59'    Print, then advance to channel 9. 
 Z     O'132'    D'090'    X'5A'    Print, then advance to channel 10. 
 [     O'133'    D'091'    X'5B'    Print, then advance to channel 11. 
 \     O'134'    D'092'    X'5C'    Print, then advance to channel 12. 
 ]     O'135'    D'093'    X'5D'    Print, then advance to channel 13. 
 ^     O'136'    D'094'    X'5E'    Print, then advance to channel 14. 
 _     O'137'    D'095'    X'5F'    Print, then advance to channel 15. 
 1     O'061'    D'049'    X'31'    Advance to channel 1, then print. 
 2     O'062'    D'050'    X'32'    Advance to channel 2, then print. 
 3     O'063'    D'051'    X'33'    Advance to channel 3, then print. 
 4     O'064'    D'052'    X'34'    Advance to channel 4, then print. 
 5     O'065'    D'053'    X'35'    Advance to channel 5, then print. 
 6     O'066'    D'054'    X'36'    Advance to channel 6, then print. 
 7     O'067'    D'055'    X'37'    Advance to channel 7, then print. 
 8     O'070'    D'056'    X'38'    Advance to channel 8, then print. 
 9     O'071'    D'057'    X'39'    Advance to channel 9, then print. 
 :     O'072'    D'058'    X'3A'    Advance to channel 10, then print. 
 ;     O'073'    D'059'    X'3B'    Advance to channel 11, then print. 
 <     O'074'    D'060'    X'3C'    Advance to channel 12, then print. 
 =     O'075'    D'061'    X'3D'    Advance to channel 13, then print. 
 >     O'076'    D'062'    X'3E'    Advance to channel 14, then print. 
 ?     O'077'    D'063'    X'3F'    Advance to channel 15, then print. 
 @     O'100'    D'064'    X'40'    Print with no vertical motion 
                                    while maintaining column position. 
 p     O'160'    D'112'    X'70'    Advance to top of page, then print. 
 q     O'161'    D'113'    X'71'    Advance to top of page, print, 
                                    upspace 1 line. 
 r     O'162'    D'114'    X'72'    Advance to top of page, print, 
                                    upspace 2 lines. 
 s     O'163'    D'115'    X'73'    Advance to top of page, print, 
                                    upspace 3 lines. 
 t     O'164'    D'116'    X'74'    Advance to top of page, print, 
                                    upspace 4 lines. 
 u     O'165'    D'117'    X'75'    Advance to top of page, print, 
                                    upspace 5 lines. 
 v     O'166'    D'118'    X'76'    Advance to top of page, print, 
                                    upspace 6 lines. 
 w     O'167'    D'119'    X'77'    Advance to top of page, print, 
                                    upspace 7 lines. 
 x     O'170'    D'120'    X'78'    Advance to top of page, print, 
                                    upspace 8 lines. 
 y     O'171'    D'121'    X'79'    Advance to top of page, print, 
                                    upspace 9 lines. 
 z     O'172'    D'122'    X'7A'    Advance to top of page, print, 
                                    upspace 10 lines. 
 {     O'173'    D'123'    X'7B'    Advance to top of page, print, 
                                    upspace 11 lines. 
 |     O'174'    D'124'    X'7C'    Advance to top of page, print, 
                                    upspace 12 lines. 
 }     O'175'    D'125'    X'7D'    Advance to top of page, print, 
                                    upspace 13 lines. 
 ~     O'176'    D'126'    X'7E'    Advance to top of page, print, 
                                    upspace 14 lines. 
 DEL   O'177'    D'127'    X'7F'    Advance to top of page, print, 
                                    upspace 15 lines. 
 SUB   O'032'    D'026'    X'1A'    For hard-copy devices, advance to 
                                    bottom of page unless already 
                                    there.  For scrollong windows, 
                                    positions to the bottom line of 
                                    the window. 
 GS    O'035'    D'029'    X'1D'    Erase the current window 
                                    (or the screen, if no window) 
                                    and position cursor to home 
                                    position.  Interpreted as SUB 
                                    for hard-copy devices. 
 RS    O'036'    D'030'    X'1E'    Advance, if needed, to a blank 
                                    line, print, upspace 0. 
 US    O'037'    D'031'    X'1F'    Advance, if needed, to a blank 
                                    line, print, upspace 1. 
00033
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
00059
00060
00061
00062
00063
00064
00001
00002
00003
00004
00081
00082
00083
00084
00033
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
00059
00060
00061
00062
00063
00064
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
00032
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
00065
00066
00067
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
00080
00005
00006
00007
00082
00008
00009
00010
00011
00012
00013
00014
00015
00081
00082
00083
00084
00033
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
00059
00060
00061
00062
00063
00064
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
00032
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
00065
00066
00067
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
00032
00034
00035
00083
00036
00081
00037
00038
00084
00039
00040
00041
00081
00082
00083
00084
00033
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
00059
00060
00061
00062
00063
00064
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
00032
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
00065
00066
00067
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
00042
00043
00033
00044
00045
00046
00047
00048
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
00065
00066
00067
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
VFC_CHARS
Syntax: 
WHEN [ [(LEVEL 0)] expression THEN IBEX-command] 
Parameters: 
LEVEL 0   -   allows the user to set the WHEN command for the level 0, i.e., 
IBEX command level, anytime. 
expression   -   is a valid IBEX expression; the format is: 
[unary]{variable|'string'|integer|function|system_variable} 
    [operator expression] 
See EXPRESSION for a complete description. 
command   -   is any valid IBEX command. 
Description: 
The WHEN command allows the user to establish a command to be evaluated and 
executed at each JOBSTEP.  If the expression evaluates false, IBEX will then 
process the next command in the command stream.  If the expression evaluates 
true, the command portion of the WHEN command is executed.  If the command 
portion does not alter the flow of the JCL, IBEX will then process the next 
command in the command stream.  Once activated, the WHEN command remains in 
effect until the end of the session or until the DONT WHEN command is 
processed.  The WHEN key word alone with a carriage return means activate the 
previously defined WHEN command.  If none exists an error message will be 
output. 
The LEVEL 0 option allows the user to set the WHEN command for the level 0, 
i.e., IBEX command level, anytime.  This allows the user to set his level 0 
WHEN command from a SETUP file.  Therefore, everytime the user logs on, he can 
have a WHEN command setup for him. 
CAUTION:  While the WHEN command is activated, IBEX will not give automatic 
aborts on error conditions.  Users may want to allow for this in the 
executable portion of the WHEN command.  Otherwise, job stream will continue 
with the next record.  The WHEN command has the effect of IF commands at each 
JOBSTEP. 
USAGE NOTES: 
1.  The WHEN command will be parsed at JOBSTEP, not when it is entered. 
2.  The use of preprocessor variables within the WHEN command calls for using 
    double percent signs.  For example, to specify %$DATE in the WHEN command, 
    the user must input %%$DATE. 
    Example: 
    !WHEN '%%$DAY'='MON' THEN OUTPUT 'THE TIME IS %%$TIME' 
    !DI WHEN 
        When: 
          !WHEN '%$DAY'='MON' THEN OUTPUT 'THE TIME IS %$TIME' 
    ! 
    !WHEN '%$DAY'='MON' THEN OUTPUT 'THE TIME IS %%$TIME' 
    !DI WHEN 
        When: 
          !WHEN 'MON'='MON' THEN OUTPUT 'THE TIME IS %$TIME' 
3.  In dealing with nested procedures IBEX considers each new procedure call 
    (i.e., !XEQ newproc) a step to a new level. 
4.  Level 0 is at the IBEX command level.  The WHEN command affects the level 
    that it is issued at and all subsequent levels unless superseded by 
    another WHEN (or !DONT WHEN) command. 
    Example: 
    If the user inputs: 
    !WHEN (LEVEL 0) 
    IBEX will not give the user a syntax error at the time of the command is 
    input.  But at the time of execution, the user will receive an error 
    message stating that the user did not specify a WHEN command . 
At any level the user can either specify a WHEN command, specify that WHEN is 
to be halted (!DONT WHEN), or not specify a WHEN command.  If the user 
specifies a WHEN command, then while IBEX is executing the commands at that 
level, the WHEN remains in effect.  If the user specifies that the WHEN 
command is to be halted (!DONT WHEN), then while IBEX is executing the 
commands at that level there is no WHEN command in effect.  If the user does 
not specify either a WHEN nor a DONT WHEN, IBEX will use the WHEN state that 
was in effect before this level was entered.  Upon exiting any level of nested 
XEQ files, the WHEN state will be reset to its previous state. 
Upon returning to job step, IBEX will check to see if a WHEN command is in 
effect.  If so, IBEX will test the WHEN command expression.  If the expression 
evaluates to true, the 'command' portion will be executed.  If false, IBEX 
will continue by reading the next command in the job stream.  If there is no 
WHEN command in effect IBEX will continue by reading the next command in the 
job stream. 
If returning to job step under an abort condition, IBEX will check to see if a 
WHEN command is in effect.  If so, the expression test will be executed as 
above.  If there is no WHEN command in effect, IBEX will read the next command 
to see if it is an IF command.  If the command is an IF, it will be executed. 
Otherwise, an abort will result. 
Examples: 
!WHEN STEPCC>0 THEN XEQ ABORT_STEP 
When IBEX is entered at JOBSTEP, STEPCC will be evaluated.  If it is greater 
than zero, IBEX will transfer flow to the command XEQ ABORT_STEP.  Otherwise, 
IBEX will process the next command in the command stream. 
!WHEN '%%$DAY' = 'FRI' THEN GOTO LONG_LUNCH 
This illustrates the use of double percent signs for command variables. 
The following example illustrates the concept of "levels".  Each nested XEQ 
calls a new level of the IBEX command.  Note the range of the various WHEN 
commands. 
!DONT WHEN 
!DI WHEN 
   When: none 
!XEQ *1 
....."Executing *1"..... 
$DI WHEN 
   When: none 
$WHEN 1=1 THEN OUTPUT 'In file *1' 
$DI WHEN 
   When: 
     !WHEN 1=1 THEN OUTPUT 'In file *1' 
$XEQ *2 
....."Executing *2"..... 
$DI WHEN 
   When: 
     !WHEN 1=1 THEN OUTPUT 'In file *1' 
$DONT WHEN 
$DI WHEN 
   When: none 
$XEQ *3 
....."Executing *3"..... 
$DI WHEN 
   When: none 
$WHEN 1=1 THEN OUTPUT 'In file *3' 
$DI WHEN 
   When: 
     !WHEN 1=1 THEN OUTPUT 'In file *3' 
....."Returns to *2"..... 
$DI WHEN 
   When: none 
....."Returns to *1"..... 
$DI WHEN 
     !WHEN 1=1 THEN OUTPUT 'In file *1' 
!DI WHEN 
   When: none 
Related Commands: 
DONT, IF 
00002
00003
00001
00004
WINDOWS
CP-6 windowing allows the user at most CRTs the capability to divide the 
display area into more than one 'window' or work area.  The number of windows 
and the size of each is determined by options used with the IBEX SET, 
TERMINAL, and LDEV commands. 
Each window is associated with some number of UCnn names as CP-6 logical 
streams. 
See USING_WINDOWS, WINDOW_OPS and WINDOW_CONTROL 
The various command options and parameters that affect CP-6 windows may be 
window-specific, stream-specific, session-specific, or non-specific, i.e. 
global.  For more information, type ?? <CR> at the next prompt. 
Window-specific Parameters 
-------------------------- 
Each window has independent values for any IMP definitions and the following 
TERMINAL command options, window options, PLATEN command options, and 
screen-editing parameters: 
                    TERMINAL Command Options 
                    ------------------------ 
ADJTOPLFT       HSMARGIN        PRINTHALT       SPACEINSERT 
APLLCNRM        HSSHIFT         RELPAGE         TABRELATIVE 
CHARSETNAME     INSERTMODE      RETYPOVR        TABSIM 
DISPINPUT       LOWERCASE       SCROLL          TRUNCATE 
EDITOVR         NOOPTMIZ        SENDBKSPACE     UPPERCASE 
FCNTBL          PAGEHALT        SIMPERF         WRAPPAGE 
HSCROLL         PARKCURSOR 
                         Window Options 
                         -------------- 
BTMBRDR         MINLENGTH       RHTBRDR         VBRDRSIZ 
HBRDRCHR        MINWIDTH        TOPBRDR         WLENGTH 
HBRDRSIZ        OPTIONAL        VBRDCHR         WWIDTH 
LFTBRDR 
                         PLATEN Options 
                         -------------- 
LENGTH          WIDTH           LIMBO           FIRSTLINE 
                    Screen-editing Parameters 
                    ------------------------- 
EASYAPPEND      KEYINCR         RCRWRAPT        VSMARGIN 
HSALL           KEYTYPE         TEXTEDIT        VSSHIFT 
                                                       . 
Stream-specific Parameters 
-------------------------- 
Each stream has independent values for the prompt string, activation 
characters and timeout, saved input record, and the TERMINAL options ACTONTRN, 
WORDWRAPCLM, and AUTOTABCLM. 
                                                      . 
Session-specific Parameters 
--------------------------- 
Each session has independent values for these parameters: 
LDEV header 
type-ahead input 
MSGHLT 
MSGLIN 
OUTPUTDISCARD 
SINPUTSZ 
SUPPHALT (from M$EOM)) 
                                                      . 
Global Parameters 
----------------- 
The following global parameters can still be altered when windows are present: 
<ESC> <*> string 
AUTOCURSOR 
CURSORREAD 
FULLDUXPAPERTAPE 
HALFDUXPAPERTAPE 
KEEPTYPAHD 
MICROFPL 
PARITY 
PARITYCHECK 
SPEED 
The remaining TERMINAL command settings are global parameters which cannot be 
modified if more than one window is defined on the screen.  This affects the 
operation of the PROFILE command in a curious way, in that those portions of 
the profile definition that are permitted to operate will do so.  For example, 
invoking the TTY profile with windows defined will cause EDITOVR and RETYPOVR 
to be reset, but will not change the profile name itself or any of the 
settings that control the operations of the terminal. 
00004
00003
00002
00001
Window options may be classified as follows: 
Options used to create windows and manipulate window size:  FWINDOW, 
MINLENGTH, MINWIDTH, POSITION, OPTIONAL, WLENGTH, WWIDTH. 
Border options:  BTMBRDR, HBRDRCHR, HBRDRSIZ, LFTBRDR, RHTBRDR, TOPBRDR, 
VBRDRCHR, VBRDRSIZ. 
Miscellaneous options:  LOGON, REMOVE. 
Window options are listed in the following table.  For detailed syntactical 
information, see HELP LDEV_OPS option, HELP SET_OPS option or HELP 
TERMINAL_OPS option. 
  Option     Characteristic                    Remarks 
BTMBRDR    Specifies whether space is to 
           be reserved at the bottom to 
           separate this window from the 
           one below it. 
FWINDOW    Specifies the name of a stream 
           associated with the window from 
           which a new window is to be 
           created, or whose size is to 
           be adjusted to compensate for 
           the size adjustment being made 
           to the window. 
HBRDRCHR   Specifies an ASCII character      Character must be 
           to be used to mark the edge of    enclosed in single 
           the horizontal border space(s).   quotes. 
HBRDRSIZ   Specifies the size in lines 
           of the horizontal border 
           space(s) (TOPBRDR and BTMBRDR). 
LFTBRDR    Specifies whether to reserve 
           space at the left to separate 
           this window from the one to 
           the left. 
LOGON      Causes the specified stream to    Can be used only with 
           be disconnected from the current  the LDEV command, and not 
           session and reconnected to CP-6   for UC98, UC01, or UC99. 
           in the logon state. 
MINLENGTH  Specifies the minimum length 
           for this window in lines. 
MINWIDTH   Specifies the minimum width 
           for this window in columns. 
POSITION   Specifies portion of FWINDOW      Useful only for LDEV 
           that this (new) window is to      and SET.  Required 
           occupy.  The options are TOP,     to create a new window. 
           BOTTOM, LEFT, and RIGHT. 
OPTIONAL   Specifies whether the window 
           size is permitted to drop 
           below MINWIDTH or MINLENGTH. 
           If so, window is removed 
           from screen when too small, 
           but its context is maintained. 
REMOVE     Cancels the stream definition.    Can not be used with 
           If the stream is the only one     UC98, UC01, or UC99. 
           associated with its window,       Used only with LDEV 
           the window is also removed.       command. 
RHTBRDR    Specifies whether to reserve 
           space at the right to separate 
           this window from the one to 
           the right. 
TOPBRDR    Specifies whether to reserve 
           space at the top to separate 
           this window from the one 
           above it. 
VBRDRCHR   Specifies the single ASCII        Character must be 
           character to be used to mark      enclosed in single 
           the vertical border space(s).     quotes. 
VBRDRSIZ   Specifies the size in columns 
           of the vertical border space(s) 
           (LFTBRDR and RHTBRDR).  The 
           default is zero, which causes 
           this parameter to be ignored. 
WLENGTH    Specifies window length,          For a new window with 
           including any borders:            POS=TOP or POS=BOTTOM, 
           (1) in absolute lines             WLENGTH defaults to 99% 
           (2) in incremental lines          (all but one line). 
           (3) as % of full screen or 
               of current window if 
               window exists. 
           NOTE: Only (1) above is 
           implemented. 
WWIDTH     Specifies window width,           For a new window with 
           including any borders:            POSITION=LEFT or RIGHT, 
           (1) in absolute columns           WWIDTH defaults to 50% 
           (2) in incremental columns        (half the screen). 
           (3) as % of full screen, or 
               of current screen if 
               window exists. 
            NOTE: Only (1) is implemented 
            in IBEX. 
WINDOW_OPS
Syntax: 
XEQ  fid[(optionlist)][,fid[(optionlist)]]... 
Parameters: 
fid   -   identifies an XEQ file generally created through EDIT or PCL. 
optionlist   -   specifies one or more of the following options in the format 
option[,option]... 
   P[RINT]   -   directs that while the file is being submitted for execution, 
   every record is printed (echoed) on the output destination. 
   CRPT=(octstr|"charstr")   -   specifies a SEED to be applied to the XEQ 
   file if it is encrypted. 
        octstr   -  specifies an octal string from 0 to 777777777777. 
        charstr  -  specifies from 1 to 4 characters. 
    S[CAN]   -   checks the contents of the command file for syntax errors. 
    If an error is found, appropriate diagnostics are written to the user's 
    console, and the XEQ aborted. 
    T[EST]   -   directs IBEX to inhibit submitting the file for execution and 
    instead to print each record as it is altered through the data replacement 
    specifications contained in the REPLACEMENT component equations in the 
    command.  Only altered records are displayed.  This test mode allows the 
    user to examine the effects of data replacement requests before submitting 
    the job for execution. 
    START=record specifier   -   identifies the record at which command 
    execution is to start.  If the START option is not selected, command 
    execution begins with the first record in the file.  Record specifier may 
    be a record number, a record EDIT key, or a label.  A record EDIT key is 
    distinguished from a record number by the inclusion of a period. 
    END=record specifier   -   identifies the record at which command 
    execution is to end.  If not specified, command execution ends with the 
    last record.  Record specifier is defined as for START. 
    NG[SUBS]   -   specifies that GLOBAL replacements are not to be used in 
    processing this file. 
    rep   -   specifies a replacement specification in the format: 
        {field1|'string1'}={field2|'string2'} 
    See the REPLACEMENT component for a complete description. 
Description: 
The XEQ command inserts all or part of an XEQ file into the command stream and 
initiates execution of the contents of the file. 
Examples: 
START= 123.   means key 123 
START= 123    means record 123 
START= FRED   means label FRED 
!XEQ RUNPL6JOB(START=10,P,'/*'=' ','*/'=' ') 
Inserts the disk file RUNPL6JOB starting at record 10 into the command stream. 
In addition each record of the file is printed on the output destination and 
each occurrence of string '/*' or '*/' is converted to a blank. 
!XEQ STRTFORTCOMPILE(TEST,COMMON=GLOBAL) 
Prints each record of the file STRTFORTCOMPILE that is altered by the 
replacement specification COMMON=GLOBAL.  The file is not submitted for 
execution. 
Related Commands: 
BATCH 
00002
00003
00001
00004
Syntax: 
XMIT fid[(optionlist)][,fid[(optionlist)]]...{TO|ON|OVER|INTO} fid 
Parameters: 
fid   -   identifies an XEQ file generally created through EDIT or PCL.  The 
output fid may be a device. 
optionlist   -   specifies one or more of the following options in the format 
option[,option]... 
    P[RINT]   -   directs that while the file is being submitted for 
    execution, every record is printed (echoed) on the output destination. 
    CRPT=(octstr|"charstr")   -   specifies a SEED to be applied to the XEQ 
    file if it is encrypted. 
        octstr   -  specifies an octal string from 0 to 777777777777. 
        charstr  -  specifies from 1 to 4 characters. 
    S[CAN]   -   checks the contents of the command file for syntax errors. 
    If an error is found, appropriate diagnostics are written to the user's 
    console, and the XMIT aborted. 
    T[EST]   -   directs IBEX to inhibit submitting the file for execution and 
    instead to print each record as it is altered through the data replacement 
    specifications contained in the REPLACEMENT component equations in the 
    command.  Only altered records are displayed.  This test mode allows the 
    user to examine the effects of data replacement requests before submitting 
    the job for execution. 
    START=record specifier   -   identifies the record at which command 
    execution is to start.  If the START option is not selected, command 
    execution begins with the first record in the file.  Record specifier may 
    be a record number, a record EDIT key, or a label.  A record EDIT key is 
    distinguished from a record number by the inclusion of a period. 
    END=record specifier   -   identifies the record at which command 
    execution is to end.  If not specified, command execution ends with the 
    last record.  Record specifier is defined as for START=record specifier. 
    NG[SUBS]   -   specifies that GLOBAL replacements are not to be used in 
    processing this file. 
    rep   -   specifies a replacement specification in the format: 
        {field1|'string1'}={field2|'string2'} 
    See the REPLACEMENT component for a complete description. 
Description: 
The XMIT command performs the same data replacement as the XEQ and BATCH 
commands, but does not submit the file directly for batch or XEQ processing. 
It is commonly used to submit a file to the job entry stream of some other 
system connected as a HASP workstation. 
Examples: 
!XMIT RUNPL6JOB TO JE@LADC 
Transmits the disk file RUNPL6JOB to the job entry device on the system LADC. 
Related Commands: 
INCLUDE, DEFAULT, GLOBAL 
00002
00003
00001
00004
