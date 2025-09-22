To run the STARLOG processor requires 128K of memory and, for batch runs, the 
STAR pseudo resource.  (Use the IBEX command ORES MEM=128 for online sessions 
or RES STAR=1, MEM=128 for batch jobs.)  To initiate a STARLOG session after 
logging on to the LADC support computer simply enter: 
        !STARLOG [optionlist] 
  where 
  optionlist    consists of one option or two options separated by a comma. 
  The options are 
    NFC    for "no first command", causes the first command in the user's 
    LOGON record not to be executed. 
    LOGON | NA    causes the automatic logon information to be skipped. 
    Instead, STARLOG prompts for a full logon.  This option is primarily for 
    use by Starlords. 
STARLOG replies with a greeting, for example: 
         STARLOG B02B 09:45:03 FRI MAR 20 '87 
        - 
        # 
For additional information on STARLOG's HELP facility, enter a question mark 
and carriage return. 
Topics within the STARLOG HELP facility include: 
AREA - describes STARLOG's database, STARBASE.  Related 
       topics describing areas in STARBASE are ASTAR, ANOTE, 
       ALOGON, ACUSTOMER, APRODUCT, ACATEGORY, APRODUCT, 
       APROGRAMMER. 
       For example, enter 
           HELP ASTAR 
       for information on fields in a STAR. 
COMMAND - describes the types of STARLOG commands.  For each 
       command there is a separate topic.  For example to 
       see information on the BUILD command, enter 
           HELP BUILD 
CRITERIA - describes elements within the STARLOG command 
       syntax.  Related topics are FIELD, LITERAL, LOGIC, 
       RELATION, SEVERITY, SUBJECT, STATUS. 
To display all topics in STARLOG HELP, enter 
  HELP TOPICS 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1992 
  ************************************************************** 
The CATEGORY area contains records which describe subject names.  Type ? or ?? 
to see the fields in this area. 
  NA[ME] 
  PROD[UCT] product-field-name 
  TY[PE] 
00001
00002
00003
The CUSTOMER area data describes the characteristics of CP-6 customers.  Type 
? or ?? to see the fields in this area. 
  COMP[UTER] INFO[RMATION] 
  COMP[UTER] [SIGN[ON]] ACC[OUNT] 
  COMP[UTER] [SIGN[ON]] NA[ME] 
  COMP[UTER] [SIGN[ON]] PASS[WORD] 
  COMP[UTER] TEL[EPHONE] 
  CONT[ACT] NA[ME] 
      Name of the primary contact at the site. 
  CONT[ACT] TEL[EPHONE] 
      Phone number of the primary contact at the site. 
  COST CEN[TER] 
      The Honeywell Bull cost center associated with the site. 
  DEL[IVERY] AD[DRESS] 
  F[IELD] E[NGINEER] NA[ME] 
      Name of the CSD Field Software Support Specialist assigned to the site. 
  F[IELD] E[NGINEER] TEL[EPHONE] 
      Phone number of the CSD Field Software Support Specialist assigned to 
      the site. 
  LA[ST] PA[TCHES] 
  OP[ERATOR] NA[ME] 
      Name of the site's operator. 
  OP[ERATOR] TEL[EPHONE] 
      Phone number of the site's system console. 
  RE[PLY] AD[DRESS] 
  SITE NA[ME] 
      The name of the customer.  The contents of this field will appear in the 
      heading of each STAR submitted by the site. 
  SYS[TEM] {NO | NUM[BER]} 
      The customer's system number, e.g., LX0001. 
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
Syntax: 
AL[L] [ area: ] [ criteria ] 
Parameters: 
area    identifies an area within STARBASE.  If area: is not specified, then 
the area to which the user is currently positioned is used. 
criteria    is a logical expression composed of field names, relational or 
logical operators, or literals that specify which records are to be selected. 
The criteria specified become the current selection criteria.  If no criteria 
are specified, then the current selection criteria are used. 
Description: 
The ALL command steps through all of the records in the specified area which 
meet the selection criteria specified. 
The action taken when STARLOG steps to each record is defined by the user via 
the WHEN command. 
Example: 
The commands necessary to obtain a list of all COBOL STARs are 
    #WHEN STAR:STARSUM          "Instructs STARLOG to produce the STARSUM 
                                "report whenever the user steps to a STAR 
    #ALL STAR:SUNA IS COBOL     "Instructs STARLOG to step through to all 
                                "STARs with a SU/JECT NA/ME of COBOL. 
A more desirable alternative for obtaining the same results is shown as an 
example in the REPORT command section. 
00002
00003
00001
The LOGON area contains records that describe valid logon identifiers. 
Customers may view only their own LOGON record.  Type ? or ?? to see the 
fields in this area. 
  FIRST {COMM[AND] | CMND} 
      A one line command (up to 80 characters) that is to be executed whenever 
      the user logs on to STARLOG. 
  LA[ST] {OFF | LOGOFF} [TI[ME]] 
      Time user last logged off from STARLOG. 
  LA[ST] {ON | LOG[ON]} [TI[ME]] 
      Time user last logged on to STARLOG. 
  MY ST[UFF] 
      User field. 
  MY TI[ME] 
      Contains the LOGON TIME of the last session that was terminated normally 
      (without using the HOLD option). 
  NA[ME] 
      Name user wishes to appear in STARs and NOTEs. 
  PRIV[ILEGES] 
      User's privileges as determined by the STARLOG administrator. 
  PROG[RAMMER] pfn 
      LADC used field.  pfn points to the PROGRAMMER record. 
  [SI[GNON]] ACC[OUNT] 
      Logon account. 
  SI[GNON] NA[ME] 
      Logon name. 
  [SI[GNON]] PASS[WORD] 
      Logon password. 
  SITE {NO | NUM[BER]} 
      User's site number, e.g., LX0001. 
  TEL[EPHONE] 
      Phone number at which the user may be contacted. 
  THIS {ON | LOG[ON]} [TI[ME]] 
      Time user logged on for the current session. 
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
ASTARNOTE
The PRODUCT area contains records describing products.  Type ? or ?? to see 
the fields in this area. 
  [ MAR[KETING] ] ID[ENTIFICATION] 
      Honeywell Bull Marketing identifier. 
  NA[ME] 
      Name commonly used in referring to product. 
  REL[EASE] VERS[ION] 
      Current product version. 
Each PRODUCT record may contain the sub-area VERSION. 
00001
00002
00003
The PROGRAMMER area contains a record for each person who is recognized as an 
LADC programmer.  Only Starlords and LADC programmers may view the contents of 
the programmer area.  Type ? or ?? to see the fields in this area. 
  EMP[LOYEE { NO | NUM[BER] } 
  MAIL SLOT 
      Honeywell Bull internal mailing address 
  { MAN[AGER] | MGR } 
  NA[ME] 
00001
00002
00003
00004
The major areas are STAR, PRODUCT, CUSTOMER, PROGRAMMER, CATEGORY, and LOGON. 
The [STAR] NOTE area is a sub-area of the STAR area, the [PRODUCT] VERSION 
area is sub-area of the PRODUCT area.  Pictorially, this is represented below. 
                           STARBASE 
                              | 
  ____________________________|__________________________ 
  |          |          |           |         |         | 
  |          |          |           |         |         | 
STAR     CUSTOMER    PRODUCT   PROGRAMMER   LOGON   CATEGORY 
  |                     | 
  |                     | 
NOTE                 VERSION 
Position is established in any of these areas by finding or locating a record 
within the area.  It may be assumed that each area contains a record of the 
same name as the area.  For example, the STAR record is the only record in the 
STAR area.  The major areas are independent of one another in that current 
position may be established for each simultaneously.  The current position in 
a sub-area, however, is dependent on the current position of the area to which 
it is subordinate.  For example, the current position for the NOTE area must 
be a NOTE record in the current STAR. 
Also, position may be established in a major area through use of a field in 
another area.  For example, you'll see that the STAR record contains a pointer 
to the customer record in the CUSTOMER area for the STAR's submitter.  STARs 
may be positioned to on the basis of the name field in the LOGON area (by 
ORIGINATOR NAME). 
The current position in the STAR area may be determined via the STARSUM report 
and in the NOTE area via the NOTE report. 
STARLOG maintains a "default area" which changes whenever a FIND, SELECT or 
step command is executed.  Subsequent commands which do not specify an area 
are defaulted to this area.  The initial default area upon logging on is STAR. 
Each of the areas' records have fields that may be referenced by users in 
STARLOG commands that retrieve information on the basis of user specified 
criteria.  The areas and their corresponding records that are of concern to 
customers interested in pursuing their normal day to day CP-6 support 
responsibilities are STAR, NOTE, CUSTOMER and LOGON.  For more information see 
the topics ACUSTOMER, ALOGON, ASTAR, ASTARNOTE, and also ACATEGORY, APRODUCT, 
APROGRAMMER. 
AREA
The STAR area contains a number of fields in its record that describe the 
entire content of a STAR except for the notes.  Type ? or ?? for the 
description of STAR record fields.  Note that each field name is shown with 
the minimum abbreviation that STARLOG accepts. 
  [AS[SIGNED]] PROG[RAMMER] pfn 
      This field points to the appropriate record in the PROGRAMMER area that 
      identifies the LADC developer who has responsibility for the STAR. 
      pfn represents the programmer field name through which STARs may be 
      positioned. 
  [CUR[RENT]] STAT[US] 
      Current state of the STAR (see STAR statuses under the HELP topic 
      STATUS). 
  DESC[RIPTION] 
      Detailed description of the reported difficulty.  The description may 
      consist of multiple lines. 
  MOD[IFICATION] DA[TE] 
      Date at which any of the following were changed: 
              DESCRIPTION 
              SEVERITY 
              CURRENT STATUS 
              ASSIGNED PROGRAMMER 
              NOTE:TEXT 
        or    the STAR was built or a NOTE appended. 
  {NUM[BER]|NO} 
      STAR number (assigned by STARLOG) 
  NOT[E] snfn 
      This field points to the NOTEs for this STAR contained in the NOTE area. 
      snfn represents any STAR note field name by which STARs may be 
      referenced.  For example, STARs may be positioned to on the basis of 
      NOTEs that have your NAME (i.e., NOTE:NAME) 
  OR[IGIN] DA[TE] 
      STARLOG supplied data representing the date the STAR was submitted. 
  OR[IGINATOR] CU[STOMER] cafn 
      The field points to the record in the CUSTOMER area that identifies the 
      submitter of the STAR. 
      cafn represents any CUSTOMER area field name.  STAR(s) may be referenced 
      by any field in the CUSTOMER record of the submitter.  For example, it 
      is possible to find all STARs with an OR CU SITE NAME of 'XYZ'. 
  OR[IGINATOR] NA[ME] 
      Name of the STAR submitter as supplied at the time the STAR was created. 
  SEV[ERITY] 
        1-4 indicates the user's perceived impact of problem (see the list of 
            STAR severities under the HELP topic SEVERITY.) 
          5 indicates a desired improvement request. 
          A is an ANALYST ALERT providing technical information or warnings. 
          D is used for discussions or status STARs. 
  SU[BJECT] NA[ME] 
      Problem's subject category, e.g., FORTRAN, FILE.  For the list of 
      subject names, see the HELP topic SUBJECT. 
  SU[BJECT] VERS[ION] 
      Problem's subject version, e.g., D00 for the D00 operating system, B06 
      for the B06 version of a compiler or processor, 01 for the 01 version of 
      a reference manual. 
  ST[ATUS] CO[DE] 
      Internal code representing the STAR's current state. 
  TI[TLE] 
      One line description of the problem containing up to 60 characters. 
  VIS[IBILITY] DA[TE] 
      Date the STAR was reviewed (i.e., made visible to other customers. 
00001
00002
00003
00004
00005
00006
00005
00008
00009
00007
00010
00013
00011
00012
00014
00015
The NOTE area, as has already been mentioned, is a sub-area of the STAR area. 
The records in the area contain the data that users append to STARs as 
additional information.  Type ? or ?? to see the fields in the NOTE record. 
  DA[TE] 
      Date the NOTE was entered or reviewed. 
  LOG[ON] lfn 
      This field points to the LOGON record for the NOTE's originator. 
      lfn represents any LOGON field name that may be used to position to 
      NOTEs. 
  NA[ME] 
      Name entered when the NOTE was created. 
  {NUM[BER]|NO} 
      Number of the NOTE as assigned by STARLOG. 
  TEXT 
      Multiple lines of text. 
  TY[PE] 
      Code entered at the time the NOTE is entered in response to the "Type:" 
      prompt: 
            blank         - indicates a NOTE that may be entered by any user 
                      with added information or questions. 
            F[ORGET]       - indicates that STAR is to be ignored and may be 
                      entered by the originator only. 
            R[ESPONSE]     - provides the LADC developer a means of 
                      acknowledgement. 
            D[ISPOSITION]  - indicates the NOTE provides a resolution for the 
                      problem reported.  Entered by LADC programmers or CP-6 
                      TAC. 
            A[VOID]        - provides a means to avoid or work-around the 
                      problem.  Entered by LADC programmers or CP-6 TAC. 
            I[NVISIBLE]    - indicates that the NOTE is visible only to LADC 
                      programmers and CP-6 TAC.  These are used for internal 
                      discussions related to the problem reported.  These and 
                      "H" type NOTEs cause the customers to see "gaps" in the 
                      successive NOTE numbers that appear in STAR displays. 
            H[ONEYWELL]    - indicates a NOTE entered by and only visible to 
                      Honeywell Bull personnel. 
            X              - indicates that the NOTE is to be ignored and may 
                      be entered the originator only. 
00001
00002
00003
00004
00005
00006
Syntax: 
BU[ILD] { STAR | NOTE } [ FROM fid ] 
Parameters: 
FROM fid    specifies that information for the STAR or NOTE is stored in a 
file.  The information in the file must be arranged exactly as if it were 
typed in from a terminal. 
If no FROM fid is specified, STARLOG will prompt for the various fields 
necessary to build either the new STAR record or new NOTE. 
Description: 
The BUILD command is used to create a new STAR or to append a new NOTE to a 
STAR.  It's necessary, of course, to first position to a STAR via the FIND or 
SELECT command prior to issuing the BUILD NOTE command. 
Examples: 
1.  Building a STAR 
    After entering the BUILD STAR command, the following prompts are issued: 
        Subject name:           A subject category known to STARLOG (see 
                                SUBJECT for a list) and owned by the 
                                customer is required here. 
        Subject version:        The version of the product for which the 
                                problem is being reported. 
        Originator name:        The name of the submitter.  If a carriage 
                                return is entered here, the name as stored 
                                in the user's LOGON record is used. 
        Severity:               The user's perceived severity of the problem 
                                (see SEVERITY for suggested guidelines). 
        Title:                  The title for the problem report up to 60 
                                characters. 
    After the above data is entered, STARLOG outputs the STAR number as 
    follows: 
        Star number: nnnnn 
    Then, the user is prompted for the description of the problem by 
        Description: 
        - 
    A null response to the successive "-" prompts terminates the BUILD STAR 
    process. 
2.  Building a NOTE 
    After entering the BUILD NOTE command, the following prompts are issued: 
        Name:                   The name of the submitter.  If a carriage 
                                return is input here, the name as stored in 
                                the user's LOGON record is used. 
        Type:                   For all customer supplied notes, a carriage 
                                return would suffice.  See STATUS for a 
                                list of valid NOTE types. 
    At this point, the NOTE's number is output and the user is prompted for 
    the text of the NOTE as follows: 
        NOTE number: nn 
        - 
    The NOTE building process is terminated by a carriage return in response 
    to one of the successive "-" prompts. 
3.  Building STAR in a file 
    It may also be convenient to build STAR entries in an edit file, before 
    logging on to the support system.  In this case, use a template file of 
    the form: 
      1.000 subject name 
      2.000 subject version 
      3.000 
      4.000 severity 
      5.000 title 
    When building a STAR, use EDIT to merge or copy the template file into the 
    beginning of the STAR file.  Then re-read (RR) the five lines.  Replace 
    the non-blank lines with correct STARLOG responses.  For example, the 
    subject could become FORTRAN, subject version could become D00, severity 
    could become 3, and title would be whatever is appropriate.  Then enter 
    the description of the STAR following the title line.  When the STAR 
    description is complete, use the command BUILD STAR FROM fid command in 
    STARLOG to build the actual STAR.  (The originator name is supplied for 
    line 3 when the BUILD STAR command is executed.) 
    To create a file containing multiple STARs, use a similar template, 
    inserting the STAR description after the title, but instead of using the 
    BUILD command, use the READ command.  Separate the description of the STAR 
    from the following BUILD command by ".END".  A file containing two build 
    STAR sequences is as follows: 
      1.000 BUILD STAR 
      2.000 subject name 
      3.000 subject version 
      4.000 
      5.000 severity 
      6.000 title 
      7.000 description (may be multiple lines) 
      8.000 .END 
      9.000 BUILD STAR 
     10.000 subject name 
     11.000 subject version 
     12.000 
     13.000 severity 
     14.000 title 
     15.000 description (may be multiple lines) 
     16.000 .END 
    Using this file as a template, the first of two STARs could appear as 
    follows: 
      1.000 BUILD STAR 
      2.000 CENTRAL 
      3.000 C01 
      4.000 
      5.000 2 
      6.000 <XYZ> UDE-501-7 @ KQT$TREES+.2222 
      7.000 The screech occurred during a ZAP of the system.  After recovery 
      7.100 another ZAP proceeded without incident.  Preliminary analysis 
      7.200 information will be beamed to .ZZZTEST.  The dump @XYZ will 
      7.300 be star_A005.:SYSTAC2.  We're running on week 702 patches. 
      8.000 .END 
       . 
       . 
       . 
00002
00003
00001
OFF
Syntax: 
CH[ANGE] [ area: ] fldn {{ TO | = } { literal | INPUT } | FROM fid } 
Parameters: 
area    identifies an area within STARBASE.  If area: is not specified, then 
the area to which the user is currently positioned is used. 
fldn    represents a field name which exists in the area being modified. 
literal    represents a valid literal as described in the HELP topic LITERAL 
that matches the data type of the field being modified. 
INPUT    specifies multi-line text fields.  STARLOG will prompt the user for 
successive lines of input. 
fid    specifies a file containing the replacement field (i.e., the literal or 
INPUT).  The special symbol ".END" signals the end of multi-line text input. 
Description: 
The CHANGE command is used to alter the contents of specific fields of the 
current record.  The EDIT command is recommended for altering STAR 
descriptions or NOTE text. 
Example: 
Change the subject name of an existing STAR, 1234, to FORTRAN. 
    #1234                   "FIND command to position to STAR 1234 
    #CH SUNA TO FORTRAN     "Changes SUBJECT NAME to FORTRAN 
00002
00003
00001
The STARLOG commands can be classified in one of three categories:  Record, 
Step, and Miscellaneous commands. 
o   Record 
    The Record commands give users the ability to enter problem reports 
    (STARs), to provide additional information for existing problem reports 
    (NOTEs), or to modify any data that exists in a STAR or NOTE they've 
    previously entered.  Record commands include: 
        BUILD 
        CHANGE 
        EDIT 
o   Step 
    The Step commands instruct STARLOG how to "walk through" and extract 
    information from the STARBASE.  The Step commands include: 
    To set very selective criteria for reports/displays: 
        FIND        ALL        REST 
        SELECT      FIRST      THIS 
        WHEN        NEXT 
    To extract selected information from the STARBASE: 
        DISPLAY 
        REPORT 
o   Miscellaneous 
    This set of commands allows users control of I/O during their STARLOG 
    sessions as well as providing an access to CP-6 utilities during their 
    sessions.  These commands include: 
        DATE        END        LINK         MY           PAGE 
        DIRECTORY   ERASE      LOGON        OFF          PRINT 
        DO          HELP       MODE         OUTPUT       READ 
STARLOG permits users to position to or locate a record or set of records 
based on some user-specified selection criteria.  This criteria is a logical 
expression made up of the field names, relational and logical operators, and 
literals.  See the HELP topics FIELD, LITERAL, LOGIC, RELATION for more 
information. 
CRITERIA
Syntax: 
{ DATE | TIME } 
For information on dates entered as literals in STARLOG commands, see the HELP 
topic LITERAL. 
Description: 
DATE (and its synonym TIME) displays the current date and time.  The format of 
the display is: 
mmm dd 'yy hh:mm   (month)(day)(year)(hours)(minutes) 
Examples: 
#DATE 
requests a display of the current date and time.  A sample display is: 
MAR 02  '86  11:03 
00001
00002
DISPLAY
Syntax: 
{ DIR[ECTORY] } [ fid | R[ESET ]] 
Parameters: 
fid    specifies the new default account fid, and may consist of an account or 
a packset name and an account. 
RESET    specifies that the default account is to be reset to the running 
account. 
Description: 
This command changes the default account and packset.  The default account and 
set are the account and associated packset that are selected if an account is 
not supplied as part of a disk file fid specification.  Initially, the default 
account is the logon or running account and the packset name is nil.  When 
used without parameters, DIRECTORY displays the current directory pointer. 
Examples: 
#DIRECTORY .ZZZCUST 
This command directs that subsequent fids that do not include an account are 
to default to the .ZZZCUST account and the packset associated with that 
account. 
#DIRECTORY RESET 
This command re-establishes the running account and its associated packset as 
the default. 
00002
00003
00001
Syntax: 
DI[SPLAY] [ area: ] { displaylist | ALL } [ step ] [ criteria ] 
Parameters: 
area    identifies an area within STARBASE.  If area: is not specified, then 
the area to which the user is currently positioned is used. 
displaylist | ALL    specifies one or more fields in either a STAR or NOTE to 
be displayed.  The items in the displaylist are identified by field name and 
are separated by commas.  If ALL is specified, all major fields are displayed. 
step    specifies which records are to be stepped to for the desired report. 
Valid step specifications are 
   FIRST    - step to the first record satisfying the selection 
              criteria. 
   NEXT     - step to next record satisfying the selection criteria. 
   REST     - steps through all the records satisfying the selection 
              criteria starting after the record to which the user 
              is currently positioned. 
   ALL      - steps through all the records satisfying the selection 
              criteria.  This is the default, if step is not 
              specified. 
criteria    is a logical expression composed of field names, relational or 
logical operators, or literals that specify which records are to be selected. 
The criteria specified become the current selection criteria.  If no criteria 
are specified, then the current selection criteria are used. 
Description: 
The DISPLAY command is entered following the SELECT or FIND command to 
generate displays of specified fields of selected STARs/NOTEs.  If a step 
command is specified, the DISPLAY command becomes the new default WHEN 
command.  The DISPLAY command applies only to the immediately preceding FIND 
or SELECT command.  A global DISPLAY command is enabled through the WHEN 
command. 
Examples: 
1.  To display just the STAR number field of STAR 8821 and the NOTE types 
    attached to it, the STARLOG user enters: 
        #FIND STAR:NUMBER=8821 
        #DISPLAY NUMBER, (NOTE:TYPE) 
2.  To display all STARs whose subject name is FEP, the STARLOG user enters: 
        #SELECT STAR:SUBJECT NAME IS FEP 
        #DISPLAY ALL 
3.  To display the number, title and status of a STAR, the STARLOG user 
    enters: 
        #FIND STAR:NUMBER=8821 
        #DISPLAY NUM, TITLE, STATUS 
00002
00003
00001
Syntax: 
{ DO | ! } IBEX-command 
Parameters: 
IBEX-command    any legal IBEX command.  Enter HELP (IBEX) COMMANDS for more 
information. 
Description: 
The DO command allows the user to execute an IBEX command without exiting the 
current processor. 
Note:  The ! (exclamation point) may be used instead of the word DO.  It 
should be noted however that if the ! is used in an XEQ file, it will 
terminate the current processor session unless preceded by at least one blank, 
or entered as a double ! (!!). 
Examples: 
1.  To display the current system status enter 
    #DO DI 
2.  To set up a title and page number for a report destination enter 
    #!LDEV LP09 TITLE='report title',PAGE=100,COPIES=3 
00002
00003
00001
Syntax: 
ED[IT] [ area: ] fldn 
Parameters: 
area    identifies an area within STARBASE.  If area: is not specified, then 
the area to which the user is currently positioned is used. 
fldn    represents a field name which exists in the area being modified. 
Description: 
The EDIT command works in one of two ways depending on the type of field being 
edited.  If the field is not a multi-line text field, then the field is output 
to the user's terminal with the cursor left at the end of the field.  The user 
at that point is free to use the standard CP-6 backspace editing commands to 
correct the data as desired. 
If the field to be modified is a multi-line text field, then the data is 
written to a temporary file, *STAREDIT, and the CP-6 editor, EDIT, is given 
control with the file open for modification. 
Examples: 
1.  To edit the body of a STAR, enter: 
          starnumber.ED DESC 
    which positions to the specified star number at the description 
    portion and prompts for entry of edit commands.  *STAREDIT is the 
    temporary file that contains the STAR description. 
2.  To edit the title of a STAR, enter: 
          starnumber.ED TITLE 
    which displays the title and positions the cursor at the end of the 
    title line.  You may then delete and retype characters as needed. 
3.  To edit a NOTE, enter: 
          starnumber.:notenumber.ED TEXT 
    which positions to the specified star number at the specified note 
    number and prompts for entry of edit commands.  *STAREDIT is the 
    temporary file that contains the NOTE text. 
00002
00003
00001
Syntax: 
{ EN[D] | X | Q[UIT] }  [ HO[LD] ] 
Parameters: 
HOLD    causes the field MY TIME in the user's LOGON record not to be updated 
when the session is terminated.  Normally, MY TIME is updated to be the same 
date and time as the field LAST LOGON TIME in the LOGON record.  The HOLD 
option is convenient when the LAST LOGON TIME needs to be preserved for use in 
a later session. 
Description: 
The END command is used to exit STARLOG and return to the IBEX level. 
00002
00001
Syntax: 
ERASE [ ALL | ldevlist ] 
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
#ERASE ALL 
deletes all output accumulated for all logical devices defined for the session 
or job. 
00002
00003
00001
FIND
A field is a basic unit of information within a record.  Each field has a name 
unique to its area.  Fields may be specifically accessed by their names in 
CHANGE, DISPLAY and EDIT commands as well as being used in specification of 
selection criteria in FIND and SELECT commands.  Refer to Appendix A for a 
description of the more commonly used field names. 
There are five types of fields, all of which have fixed length.  They are 
1.  Decimal 
    Consists solely of numeric characters.  On display, leading zeroes are 
    suppressed.  STAR:NUMBER, i.e., the NUMBER field in the STAR area record, 
    is an example of a decimal field. 
2.  Text 
    Consists of any printable characters.  On display, trailing blanks are 
    suppressed.  STAR:TITLE is an example of such a field. 
3.  Multi-line text 
    Consists of one or more lines of printable characters.  STAR:DESCRIPTION 
    is an example. 
4.  Code 
    Consists of text fields that are restricted to specific characters. 
    NOTE:TYPE is such an example. 
5.  Pointer 
    Consists of a pointer to another record.  The field itself contains no 
    displayable data.  Its name is used in conjunction with field names within 
    the record to which it points.  An example of such a field is 
    STAR:ORIGINATOR CUSTOMER.  It points to the record that describes the 
    customer that originated the STAR.  Since SITE NAME is a field within the 
    CUSTOMER record, a fully qualified pointer field name would be 
    STAR:ORIGINATOR CUSTOMER SITE NAME. 
Syntax: 
FI[ND] [ step ] [ area: ] criteria                   (Format 1) 
             - or - 
{ n1 [:n2] | :n3 }                                   (Format 2) 
Parameters: 
step    represents either FIR/ST or NE/XT.  If neither is specified, NEXT is 
assumed. 
area    identifies an area within STARBASE.  If area: is not specified, the 
area to which the user is currently positioned is used. 
criteria    is a logical expression composed of field names, relational or 
logical operators, or literals that specify which records are to be selected. 
The criteria specified become the current selection criteria.  If no criteria 
are specified, then the current selection criteria are used. 
n1    is a STAR number. 
n2    is a NOTE number. 
n3    is a NOTE number within the current STAR. 
Description: 
The FIND command positions to the first or next occurrence of a record fitting 
the specified criteria independent of the current selection criteria defined 
by the SELECT command. 
The second form of the FIND command, probably the more useful of the two, is 
used to position to STARs or NOTEs. 
Note:  If the response to a FIND command for a specific STAR is the message 
"*** Nothing found", that STAR is probably closed and archived.  To view such 
STARs, invoke the processor ARCHLOG.STAR which accepts STARLOG commands. 
Examples: 
The following pairs of command sequences are identical: 
    Format 1                  Format 2    Description 
    #FIND STAR:NUMBER=1234    #1234       Positions to STAR 1234 
    #FIND STAR:NUMBER=1234    #1234:5     Positions to NOTE 5 of STAR 1234 
    #FIND NOTE:NUMBER=5 
    #FIND NOTE:NUMBER=10      #:10        Positions to NOTE 10 of the 
                                          STAR to which the user is 
                                          currently positioned 
00002
00003
00001
Syntax: 
FIR[ST]  [ area: ] [ criteria ] 
Parameters: 
area    identifies an area within STARBASE.  If area: is not specified, then 
the area to which the user is currently positioned is used. 
criteria    is a logical expression composed of field names, relational or 
logical operators, or literals that specify which records are to be selected. 
The criteria specified become the current selection criteria.  If no criteria 
are specified, then the current selection criteria are used. 
Description: 
The FIRST command causes a sequential search for the first record in the area 
which meets the specified selection criteria. 
The action taken when STARLOG steps to each record is defined by the user via 
the WHEN command. 
Example: 
The commands necessary to produce a STAR report for the first STAR submitted 
by the user are 
    #WHEN STAR:STAR             "Instructs STARLOG to produce the STAR 
                                "report whenever the user steps to a STAR. 
    #FIRST STAR:ORNA IS ME      "Instructs STARLOG to step through to the 
                                "first STAR with a OR/IGINATOR NA/ME of ME 
                                "(i.e., the name specified in LOGON:NAME). 
00002
00003
00001
Syntax: 
H[ELP] [ (fid) ] [ TOPICS ] [ keyword1 [ - ] [ keyword2 ] ] 
Note:  The following elements can be specified in any order: 
         (fid) 
         TOPICS 
         [ keyword1 ] [ - ] [ keyword2 ] ] 
For example, HELP (fid) keyword1  - keyword2 TOPICS is acceptable. 
Parameters: 
(fid)    specifies the processor name (for example, STARLOG).  If (fid) is 
omitted, the current processor is assumed.  The processor name can be ? to 
request a listing of processors that have HELP facilities available. 
TOPICS    requests a list of topic or subtopic names, rather than an 
information message. 
keyword1 [-] [keyword2]    specifies a topic, a range of topics, or a topic 
and subtopic to identify what HELP information is requested.  keyword1 and 
keyword2 may be abbreviated (by truncation). 
FORM                                     RESULT 
-------------------                      -------------------- 
HELP (fid) TOPICS                        Lists all topics 
HELP (fid) TOPICS keyword1 - keyword2    Lists all topics in the range 
                                         specified by keyword1 - keyword 2 
HELP (fid) TOPICS keyword1?              Lists all topics beginning with 
                                         the prefix specified by keyword1 
HELP (fid) TOPICS keyword1               Lists all subtopics for the 
                                         topic specified by keyword1 
HELP (fid) keyword1                      Displays the first level 
                                         information message for 
                                         the topic keyword1 
HELP (fid) keyword1 keyword2             Displays the information 
                                         message for keyword1, but only 
                                         the level identified by the 
                                         subtopic keyword2 
keyword1 may include the wild-card (?) character as the rightmost character, 
if TOPICS is specified. 
Description: 
HELP displays information. 
HELP messages have levels.  Once the initial level has been displayed, 
entering a question mark displays the next level, usually containing greater 
detail.  Entering two question marks displays the entire message. 
Examples: 
HELP (STARLOG) BUILD 
displays the syntax of the BUILD command.  Entering ?? displays additional 
information on the BUILD command. 
HELP (STARLOG) SUBJECT 
displays the available STAR subjects. 
HELP (STARLOG) SEVERITY 
displays the meaning of STAR severity codes. 
HELP (STARLOG) ASTAR TOPICS 
displays all fields within the STAR area. 
00002
00003
00001
A 
  ALL Command - 
      HELP ALL 
  archived STARs - 
      HELP FIND DESCRIPTION: 
  ARCHLOG.STAR - 
      HELP FIND DESCRIPTION: 
B 
  BUILD Command - 
      HELP BUILD 
C 
  CATEGORY Area - 
      HELP ACATEGORY 
  CHANGE Command - 
      HELP CHANGE 
  Commands - 
      HELP COMMANDS 
  CUSTOMER Area - 
      HELP ACUSTOMER 
D 
  DATE Command - 
      HELP DATE 
  DIRECTORY Command - 
      HELP DIRECTORY 
  DISPLAY Command - 
      HELP DISPLAY 
  DO Command - 
      HELP DO 
E 
  EDIT Command - 
      HELP EDIT 
  END Command - 
      HELP END 
  ERASE Command - 
      HELP ERASE 
F 
  Field Names - 
      HELP FIELD 
  FIND Command - 
      HELP FIND 
  FIRST Command - 
      HELP FIRST 
H 
  HELP Command - 
      HELP HELP 
I 
  Invoking STARLOG - 
      HELP INVOKING_STARLOG 
L 
  LINK Command - 
      HELP LINK 
  Literals - 
      HELP LITERAL 
  Logical Operators - 
      HELP LOGIC 
  LOGON Area - 
      HELP ALOGON 
  LOGON Command - 
      HELP LOGON 
M 
  MODE Command - 
      HELP MODE 
  MY Command - 
      HELP MY 
  MY TIME in LOGON record - 
      HELP ALOGON MY_TIME 
N 
  NEXT Command - 
      HELP NEXT 
  NOTE Area - 
      HELP ASTARNOTE 
  NOTE type codes - 
      HELP ASTARNOTE TYPE 
O 
  OFF Command - 
      HELP OFF 
  OUTPUT Command - 
      HELP OUTPUT 
P 
  PAGE Command - 
      HELP PAGE 
  Positioning and Record Selection - 
      HELP RECORD 
  PRINT Command - 
      HELP PRINT 
  PRODUCT Area - 
      HELP APRODUCT 
  PROGRAMMER Area - 
      HELP APROGRAMMER 
R 
  READ Command - 
      HELP READ 
  Relational Operators - 
      HELP RELATION 
  REPORT Command - 
      HELP REPORT 
  REST Command - 
      HELP REST 
S 
  SELECT Command - 
      HELP SELECT 
  Selection Criteria - 
      HELP CRITERIA 
  Severity, STAR - 
      HELP SEVERITY 
  STAR Area - 
      HELP ASTAR 
  STAR Severities - 
      HELP SEVERITY 
  STAR Statuses - 
      HELP STATUS 
  STAR Subjects - 
      HELP SUBJECT 
  Status, STAR - 
      HELP STATUS 
  Subject, STAR - 
      HELP SUBJECT 
T 
  THIS Command - 
      HELP THIS 
  type codes for NOTEs - 
      HELP ASTARNOTE TYPE 
W 
  WHEN Command - 
      HELP WHEN 
  wild-carding in CONTAINS clause - 
      HELP RELATION 
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

Syntax: 
LINK  fid 
Parameters: 
fid    specifies the CP-6 processor to which control is to be transferred 
Description: 
The LINK command causes an M$LINK to be issued to the processor specified by 
fid.  When the processor receiving control is terminated, control returns to 
STARLOG. 
00002
00001
Literals may be decimal strings, quoted strings, symbols (unquoted words), 
dates, phone numbers and special names.  Two special keyword names are 
       ME    - depending on the associated field, it refers to the 
               user's CUSTOMER:SITE NAME or the user's LOGON:NAME. 
       INPUT - is used with the CHANGE command.  It instructs 
               STARLOG to prompt for the literal when needed; it is 
               used only with multi-line fields. 
The format for dates on input is 
       mm[/dd]/yy [hh:mm] 
or 
       hh:mm [mm[/dd]/yy] 
where mm is the month number, dd is the day of the month, yy is the year's 
last two digits, hh is the hour and mm is the minute of the hour.  If only 
hh:mm is specified, then the date defaults to the current date. 
The format for dates as a literal in comparisons and modifications is 
       mm[/dd]/yy [hh:mm] 
       hh:mm [mm[/dd]/yy] 
       LAST YEAR                    - any time during the previous year 
       LAST MONTH                   - any time during the previous month 
       {LAST DAY | YEST[ERDAY]}     - any time during the previous day 
       NOW                         - current time and date 
       WEEK AGO                    - time 7 days ago 
       YEAR AGO                    - time 365 1/4 days ago 
       MONTH AGO                   - time 30 1/2 days ago 
       DAY AGO                     - time 1 day ago 
       TODAY                       - any time today 
       L[AST] {LOG[ON] | ON} [TI[ME]] - time of previous session logon 
       L[AST] {LOGOFF | OFF} [TI[ME]] - time of previous session logoff 
       T[HIS] {LOG/ON | ON} [TI[ME]] - time of current session logon 
       MY TI[ME]                   - contents of LOGON:MY TIME field (see 
                                     END command) 
The format of a phone number for input or comparison is 
       (acd) pre-numb [Xexten] 
or 
        HVN  pre-numb [Xexten] 
where acd is a three digit area code, pre is a three digit prefix, numb is 
four digit number and exten is an up to five character extension.  Use the 
characters "HVN" instead of area code designation for HVN phone numbers. 
LITERAL
LOGON
The logical operators are 
                         { NOT  |  ~ } 
                         { AND  |  & } 
                         {  OR  |  | } 
Parentheses, as commonly used in arithmetic expressions, may be used to 
influence the evaluation of terms of logical expressions.  The field name or 
relational operator need not be respecified in successive terms if it is the 
same as used in the previous term.  For example, 
    NUMBER < 5 OR = 7 OR 8 
has the same meaning as 
    NUMBER < 5 OR NUMBER = 7 OR NUMBER = 8 
Parentheses may also be used for sub-area criteria by following the left 
parentheses with a sub-area name and a colon.  All field names that appear 
within the parentheses must describe fields within the sub-area record.  For 
example, 
    SUBJECT NAME IS COBOL AND (NOTE:NA IS 'Jim Smith') 
is a logical expression which is true if a STAR has a SUBJECT NAME of COBOL 
and has any NOTE that was originated by 'Jim Smith'. 
LOGIC
Syntax: 
LO[GON] [ HO[LD] ] 
Parameters: 
HOLD    specifies that the value stored in MY TIME, a STARLOG user-profile 
parameter that contains the logon time for the previous STARLOG session, not 
be updated. 
Description: 
The LOGON command ends the current STARLOG session and permits the user to 
logon to STARLOG with a different account name.  Specifying HOLD notifies 
STARLOG not to change the value of the MY TIME parameter.  HOLD is specified 
when the STARLOG user wishes to treat multiple STARLOG sessions as continuous 
sessions, usually for tracking purposes. 
Examples: 
To logon with a different account name, the STARLOG user enters: 
    #LOGON 
The system responds: 
     STARLOG B02B 15:05:18 WED JUN 10 '87 
     Please log on: 
The user may respond with: 
  1.  account,name,password [ (option) ] 
  2.  account,name [ (option) ] 
  3.  password [ (option) ] 
  4.  [ (option) ] 
For responses 3 and 4, the account, name are taken from the JIT.  The logon 
option permitted is NFC, meaning don't execute the FIRST COMMAND. 
00002
00003
00001
Syntax: 
MODE [ BE[GINNER] | EX[PERT] ] 
Parameters: 
BEGINNER    directs STARLOG to prompt with STAR> or NOTE> depending on the 
current default location (set by a FIND or SELECT command). 
EXPERT    directs STARLOG to prompt with #, the default. 
Description: 
The MODE command allows the user to change the STARLOG prompt mode.  If the 
MODE command is issued and neither BEGINNER or EXPERT are specified, STARLOG 
will display the current mode. 
Examples: 
To request prompting in Beginner's mode, the STARLOG user enters: 
    #MODE BEGINNER 
    STAR> 
To position to a NOTE, STARLOG prompts as follows in Beginner mode: 
    STAR>FIND STAR:NUMBER=1234 
    STAR>FIND NOTE:NUMBER=1 
    NOTE>REPORT NOTE 
00002
00003
00001
Syntax: 
MY fldn { = | IS } literal [ , fldn { = | IS } literal ] ... 
Parameters: 
fldn    represents a field name which exists in the area being modified. 
literal    represents a valid literal as described in the HELP topic LITERAL 
that matches the data type of the field being modified. 
Description: 
The MY command is used to change the user's image as viewed by STARLOG.  The 
user may change NAME, SITE, etc. in order to create STARs and NOTEs as the 
proper entity.  This facility is primarily to be used by support personnel 
when reporting problems experienced by their customers. 
00002
00001
Syntax: 
{ NE[XT] | > } [ area: ] [ criteria ] 
Parameters: 
area    identifies an area within STARBASE.  If area: is not specified, then 
the area to which the user is currently positioned is used. 
criteria    is a logical expression composed of field names, relational or 
logical operators, or literals that specify which records are to be selected. 
The criteria specified become the current selection criteria.  If no criteria 
are specified, then the current selection criteria are used. 
Description: 
The NEXT command causes a sequential search starting from the current position 
in the area for the first record which meets the specified selection criteria. 
The action taken when STARLOG steps to each record is defined by the user via 
the WHEN command. 
Example: 
The commands necessary to produce a STAR report for the all the STARs 
submitted by the user in step mode are 
    #WHEN STAR:STAR             "Instructs STARLOG to produce the STAR 
                                "report whenever the user steps to a STAR 
    #FIRST STAR:ORNA IS ME      "Instructs STARLOG to step through to the 
                                "first STAR with a OR/IGINATOR NA/ME of ME 
                                "(i.e., the name specified in LOGON:NAME) 
    #NEXT                       "Instructs STARLOG to step to the next STAR 
                                "that meets the current selection criteria 
                                "of ORNA IS ME.  This action is performed 
                                "each subsequent NEXT that is entered. 
00002
00003
00001
Syntax: 
{ OFF | BYE } [ HO[LD] ] 
Parameters: 
HOLD    specifies that the value stored in MY TIME, a STARLOG user-profile 
parameter that contains the logon time for the previous STARLOG session, not 
be updated. 
Description: 
The OFF command is used to exit STARLOG and terminate the current CP-6 
session.  Specifying HOLD notifies STARLOG to not change the value of the MY 
TIME parameter.  HOLD is specified when the STARLOG user wishes to treat 
multiple STARLOG sessions as continuous sessions, usually for tracking 
purposes. 
Examples: 
To exit STARLOG and log off the CP-6 system, the STARLOG user enters: 
    #OFF 
00002
00003
00001
Syntax: 
         [[ ON   ] LP[@location ]] 
OU[TPUT] [[ OVER ] fid           ] 
         [[ INTO ] ME            ] 
         [[ TO   ]               ] 
Parameters: 
{ON|TO|OVER|INTO}    directs file output processing.  OVER causes an existing 
file to be overwritten.  INTO causes file extension.  ON and TO are synonyms 
used to create a new file.  If the file exists, 
an error will occur.  The default is ON. 
fid    any valid CP-6 file identifier. 
LP    directs output to the default line printer.  @location identifies a 
specific line printer. 
ME    redirects output to the user's terminal. 
Description: 
This command sends subsequent output to the specified destination. 
Examples: 
#OUTPUT ON OUTPUTFILE 
#OUTPUT ON ME 
00002
00003
00001
Syntax: 
PA[GE] 
Description: 
The PAGE command causes a page eject to occur. 
Examples: 
To specify page ejects between STAR reports, the STARLOG user enters, for 
example: 
    #SELECT STAR:(SUBJECT NAME IS FEP) AND (NOTE:DATE > 04/08/87) 
    #REPORT STARSUM 
    #PAGE 
    #SELECT STAR:(SUBJECT NAME IS VDH) AND (NOTE: DATE > 04/08/87) 
    #REPORT STARSUM 
00001
00002
LITERAL
Syntax: 
PRINT [ ALL | ldevlist ] 
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
#PRINT LP01,LP02 
The above example causes the accumulated output associated with logical 
devices LP01 and LP02 to be sent immediately to the associated destinations. 
00002
00003
00001
END
REPORT
Syntax: 
REA[D]  fid 
Parameters: 
fid    is a file containing commands exactly as would be entered at a terminal 
during an interactive STARLOG session. 
Description: 
The READ command reads and executes commands stored in a file.  As each 
command is executed, it is echoed. 
00002
00001
Before any operation is performed on an existing STARLOG record, it's 
necessary to be positioned to that record.  A user accomplishes this by means 
of the FIND or SELECT/STEP commands.  Most often the records that customers 
will be positioning to will be STAR, NOTE or LOGON records.  In the case of a 
NOTE record, since it's in a sub-area of the STAR area, it will be necessary 
to first position to the STAR record to which the NOTE belongs and then 
position to the appropriate NOTE. 
STARLOG permits users to identify sets of records by means of the SELECT 
command that allows multiple selection criteria to be specified.  The set of 
records thus selected may subsequently be acted upon by either the REPORT 
command to produce a variety of reports or by a "stepping facility" that 
automatically positions to each record in the set to perform some pre-defined 
user task.  The WHEN command is used to specify the pre-defined user task. 
Relations are used in selection criteria to position to a single record or 
locate a set of records based on the contents of specific fields.  The 
relational operators are: 
       { LESS [THAN] | LT | < | BEF[ORE] } 
       { GREAT[ER] [THAN] | GT | > | AFT[ER] } 
       { E[QUAL] [TO] | IS | = } 
       { NOT [EQUAL [TO]] | IS NOT | ~= } 
       { LESS [THAN] [OR] EQU[AL] [TO] | LE | <= } 
       { GREAT[ER] [THAN] [OR] EQU[AL] [TO] | GE | >= } 
       { CONTAINING | CON[TAINS] | HAV[ING] | WITH } 
       NOT { CONTAINING | CON[TAINS] | HAV[ING] | WITH } 
A relation is a field name followed by a relational operator followed by a 
literal.  For example, 
       NUMBER = 6600 
or 
       TITLE CONTAINS COMP? | CALC? 
Note that the second example above demonstrates that relations may be combined 
with logical operators to form logical expressions.  All comparisons are made 
after translating lower case characters to upper case.  This example also 
shows the use of wild-carding; that is, it requests STARs containing the 
strings COMP or CALC in the title.  (Wild-carding is permitted only in the 
CONTAINS clause.) 
RELATION
Syntax: 
[ RE[PORT] ]  rptname  [ step ]  [ criteria ] 
Parameters: 
rptname    represents the name of the desired report.  Possible report names 
are 
   STARSUM  - one line description of a STAR 
   NOTE     - a formatted display of a NOTE record 
   STARNOTE - a STARSUM report for a STAR followed by NOTE reports 
              for each NOTE associated with the STAR 
   STARONLY - a formatted display of a STAR 
   STAR     - a STARONLY report for a STAR followed by NOTE reports 
              for each NOTE associated with the STAR 
   STARPAGE - STAR report preceded by a page eject 
step    specifies which records are to be stepped to for the desired report. 
Valid step specifications are 
   FIRST    - step to the first record satisfying the selection 
              criteria. 
   NEXT     - step to next record satisfying the selection criteria. 
   REST     - steps through all the records satisfying the selection 
              criteria starting after the record to which the user 
              is currently positioned. 
   ALL      - steps through all the records satisfying the selection 
              criteria.  This is the default, if step is not 
              specified. 
criteria    is a logical expression composed of field names, relational or 
logical operators, or literals that specify which records are to be selected. 
The criteria specified become the current selection criteria.  If no criteria 
are specified, then the current selection criteria are used. 
Description: 
The REPORT command generates formatted displays of STARs and NOTEs.  It is the 
primary vehicle by which customers extract information from the STARBASE. 
Examples: 
1.  To list all the COBOL STARs, enter 
    #STARSUM ALL SUNA IS COBOL 
2.  To display your site's STARs for which there has been activity since your 
    last logon, enter the following command.  The field MY TIME is usually 
    used instead of LAST LOGON TIME (see the description of the END command's 
    HOLD option). 
    #STAR ALL ORCU SITE NA IS ME & MOD DA >= MYTI 
    The above command instructs STARLOG to step to all STARs whose ORIGINATOR 
    CUSTOMER SITE NAME is ME (i.e., that which is stored in the user's 
    CUSTOMER record) AND whose MOD/IFICATION DA/TE is greater than or equal to 
    the user's LOGON:MY TI/ME and to produce the STAR report for each. 
00002
00003
00001
Syntax: 
RES[T]  [ area: ] [ criteria ] 
Parameters: 
area    identifies an area within STARBASE.  If area: is not specified, then 
the area to which the user is currently positioned is used. 
criteria    is a logical expression composed of field names, relational or 
logical operators, or literals that specify which records are to be selected. 
The criteria specified become the current selection criteria.  If no criteria 
are specified, then the current selection criteria are used. 
Description: 
The REST command steps through all of the records, starting after the one to 
which the user is currently positioned, which meet the selection criteria 
specified. 
The action taken when STARLOG steps to each record is defined by the user via 
the WHEN command. 
Example: 
The commands necessary to list all FORTRAN STARs that were submitted that have 
a number greater than 30000 and have either the word ENCODE or DECODE in the 
title are 
    #30000.STARSUM REST SUNA IS FORTRAN & (TI CONTAINS ENCODE | DECODE) 
The first command above, a form of the FIND command, positions the user to 
STAR #30000.  The second steps through all the STARs after 30000 that meet the 
specified criteria and produces the STARSUM report for each. 
Note that this is a frequently used feature since, if a user knows 
approximately where a STAR that's being searched for exists, then it's 
desirable to begin the search well into the STARBASE rather than wasting time 
searching unnecessary STARs. 
00002
00003
00001
Syntax: 
SE[LECT]  [ area: ]  [ criteria | ALL ] 
Parameters: 
area    identifies an area within STARBASE.  If area: is not specified, then 
the area to which the user is currently positioned is used. 
criteria    is a logical expression composed of field names, relational or 
logical operators, or literals that specify which records are to be selected. 
The criteria specified become the current selection criteria.  If no criteria 
are specified, then the current selection criteria are used. 
ALL    specifies that all the records are selected. 
Description: 
The SELECT command identifies a particular set of records within the specified 
area.  The command simply establishes the selection criteria which will be 
used by the user stepping through the STARBASE.  It does not position itself 
position to any record.  Positioning is accomplished by means of a step or 
FIND command. 
If a SELECT command is in effect for an area of the STARBASE and you issue 
another SELECT command for the same area, the new selection criteria replace 
the previous selection criteria. 
Example: 
Type HELP WHEN EXAMPLES for a SELECT usage example. 
00002
00003
00001
For each STAR a customer submits, a severity level will be requested.  The 
severities may be a numerical value from 1 to 5, D or A.  The lower the 
numerical value used for a STAR's severity, the higher the impact of the 
problem on the customer's operation.  A severity 1 problem is the most severe 
and should be used only when conditions so indicate.  Below is a list of 
guidelines for the various severity possibilities. 
  Severity   Guidelines for Use 
    1      System is down or is crashing so frequently so as to hamper 
           productive work. 
           Major application won't run. 
           Signifies a request by the customer for immediate attention 
           from the TAC and/or LADC. 
           Customer should follow up with a call to the CP-6 TAC. 
           Customer should have available problem documentation or 
           testcases to duplicate the difficulty. 
    2      Problem has a serious impact on customer, e.g., can't compile 
           a program that's under development. 
           Signifies a request by the customer for a patch and/or a 
           usable work-around. 
           Customer would like confirmation that a problem does exist. 
           Customer should have available problem documentation or 
           testcases to duplicate the difficulty. 
    3      Problem moderately impacts the customer. 
           A work-around already exists. 
           Indicates that the customer would be satisfied with a "fixed 
           in the next release" resolution. 
    4      Problem has little impact. 
           Used to report discrepancies between existing documentation 
           and current CP-6 behavior. 
           Used to report errors in existing documentation. 
           Fast response is not critical to the customer. 
    5      Signifies a request for product improvement. 
           The fact that a product is working as designed but not as a 
           customer would like is NOT grounds for a severity other than 
           5. 
    D      Used for discussion STARs, i.e., general discussion or 
           technical questions. 
           Used for reporting problems with programs that reside in the 
           X account. 
           Used for purposes of tracking (status STAR) critical customer 
           events, e.g., BETA testing, installation of new release of 
           software.  STARs of this nature have been extremely useful in 
           providing a highly visible status reporting vehicle for such 
           events. 
    A      Analyst Alert STAR 
           Used to warn customers about major pitfalls that are 
           discovered with either hardware or software. 
Below is a list of the statuses a STAR may assume. 
  Status     Description 
CLDUP      Problem resolved as a duplicate of another STAR. 
CLOSED     Problem resolved with information supplied.  Usually the 
           problem was the result of a misinterpretation of existing 
           documentation or a user error. 
CLPATCH    Problem corrected with the release of a patch.  TATTLE 
           normally assigns this status to the STAR when a note is added 
           indicating the availability of the patch in an incremental 
           patch file automatically shipped to customers. 
CLPEND     Problem resolved with a fix to source that will be available 
           to customers with the next release. 
CLPREL     Problem resolved by the previous release of the software. 
CLREL      Problem resolved by the current release of the software. 
CPANS      Problem corrected by a local patch AND no source updates 
           are required.  This seldom-used status is used for a STAR 
           previously in TPANS status. 
UNREV      STAR has yet to be reviewed by the Starlord. 
DOCUM      Additional documentation is required for problem analysis to 
           proceed.  Further work on the problem is normally suspended 
           until the receipt of the requested information. 
OPEN       STAR has been reviewed and, a programmer is assigned to the 
           problem. 
TPANS      Problem has been identified, a patch is available for 
           testing, AND there are no source (NS) updates required for 
           this STAR. 
TPATCH     Problem has been identified and a patch is available for 
           testing.  At this point, the patch is not generally available 
           to customers until it's been through the patch testing 
           procedures at LADC.  Customers may request a pre-release of 
           the patch through the STAR; however, be aware that it's 
           made available on a use-at-your-own-risk basis. 
Below is a list of available STARLOG subject categories for which STARs may be 
submitted.  Before a customer is permitted to submit a STAR against a 
particular subject, the customer's site must be licensed for it. 
3270          6EDIT         ADAPT         ANLZ          ANVIL 
APL           ARCOM         ARES          ARGENT        ASYNC 
BASIC         BISYNC        C             CAP           CE? 
CENTRAL       COBOL         COBOLE        COBOL85       COMGROUP 
CONTROL       DELTA         DEMO          DH03          DMIVTP 
DOG           EDIT          EFT           ELAN          ELF 
ELSIE         FEP           FEPLINK       FILE          FIRMWARE 
FORGE         FORTRAN       FPL           FPS           FROG 
GMAP          GMAP6         GOOSE         GRAPHICS      HA? 
HARDWARE      HDLCX25       IBEX          IDP           IDS 
IMP           INIT          INSYM         IO            JAYS 
KEYIN         LABEL         LEMUR         LIBRARY       LINK 
LOGON         MAIL          MM            NODEADMN      NETCON 
OPER          OUTSYM        PARTRGE       PACT          PASCAL 
PCL           PCT           PIG           PIGETTE       PIGLET 
PL6           PLOVER        PRESCAN       QUAC          RATES 
RCVR2         REPLAY        RPG           SCHED         SHARED_SYSTEM 
SLUG          SORT          SPIDER        STARLOG       STATS 
SUPER         SUPPORT       SYSCON        TEXT          TOLTS 
TP            TPA           TPCP          TRADER        TURTLE 
UNITREC       VDH           VARIPORT      VOLINIT       X 
X29 
SUBJECT
Syntax: 
{ TH[IS] | * } [ STAR|NOTE ] 
Parameters: 
STAR    changes the location to STAR. 
NOTE    changes the location to NOTE. 
Description: 
The THIS command "resteps" to the current position letting the user see the 
previous position again.  The THIS command is primarily useful if a WHEN 
command has been specified.  The THIS command can be used to help locate the 
current processing position by "revisiting" the last executed WHEN REPORT or 
WHEN DISPLAY command. 
Examples: 
To display a STAR again which has just been stepped to, the STARLOG user 
enters: 
    #WHEN STAR: REPORT STAR 
    #SELECT STAR: ORIGINATING CUSTOMER NAME IS ME 
    #FIRST 
      . 
      . 
      . 
    #NEXT 
      . 
      . 
      . 
    #THIS 
00002
00003
00001
LITERAL
Syntax: 
WH[EN]  [ operation ]  [ area: ]  [ command ] 
Parameters: 
operation    is one of the following: 
FIND    - indicates that the command specified is to be performed when 
          a successful FIND is executed 
SELECT  - indicates that the command specified is to be performed when 
          a successful SELECT is executed 
STEP    - indicates that the command specified is to be performed for 
          each record the user steps.  This is the default, if 
          operation is not specified. 
area    identifies an area within STARBASE.  If area: is indicated, then 
either STAR: or NOTE: must be specified.  It indicates the type of record the 
user is to position via a FIND, SELECT or step operation. 
If no area: is specified, then the area of the record to which the user is 
currently positioned is used.  To avoid confusion, it's recommended that this 
specification always be made. 
command    must be a REPORT command (e.g., STARSUM) or a DISPLAY command.  If 
no command is specified, the indicated WHEN is reset. 
Description: 
The WHEN command is used to define a REPORT command to be automatically 
executed whenever a STEP, FIND and/or SELECT command is successfully 
performed. 
If a WHEN command is in effect for an area of the STARBASE and you issue 
another WHEN command for the same area, the new WHEN command replaces the 
previous WHEN command. 
Examples: 
1.  The commands necessary to output a STARSUM report whenever a STAR is 
    positioned to via a FIND or STEP operation are 
    #WH STAR:STARSUM      "Instructs STARLOG to perform a STARSUM report 
                          "whenever the user steps to a STAR. 
    #WH FI STAR:STARSUM   "Instructs STARLOG to perform a STARSUM report 
                          "whenever the user positions to a STAR via the 
                          "FIND command. 
    In this case, a STARSUM report would be produced for the first two 
    commands that follow but not the third: 
    #1234                 "FIND STAR number 1234 
    #NEXT                 "STEP to the NEXT STAR following 1234 
    #SE STAR:NUM=1234     "SELECT STAR number 1234 
2.  The following shows the commands necessary to step unconditionally through 
    all the STARs submitted by the user's site with a number > 20000, 
    producing a STARONLY report (STAR description with no NOTEs) for each.  In 
    addition, commands are shown that permit the user, after positioning to 
    each STAR, to display only those NOTEs that have been added/modified since 
    the user last logged on. 
    #WH STAR:STARONLY           "Instructs STARLOG to produce a STARONLY 
                                "report each time the user steps to STAR. 
    #SE STAR:ORCU SITE NA IS ME "Sets the selection criteria for the STAR 
                                "area to ORIGINATOR CUSTOMER SITE NAME 
                                "equal ME (i.e., all STARs submitted with 
                                "an ORCU SITE NA equal to that stored in 
                                "the user's CUSTOMER record). 
    #SE NOTE:DA >= MYTI         "Sets the selection criteria for the NOTE 
                                "area to DATE greater than or equal to 
                                "MY TIME (see the HOLD option of the END 
                                "command). 
    #20000.NEXT STAR.NOTE       "Three commands are used here: 
                                " 
                                " 20000     - positions (FIND) to the STAR 
                                "             with number = 20000. 
                                " NEXT STAR - starting from STAR 20000, 
                                "             search forward for a STAR 
                                "             meeting the current selection 
                                "             criteria for the STAR area. 
                                "             Note if one is found, a 
                                "             STARONLY report is produced. 
                                " NOTE      - produces a NOTE report for 
                                "             each NOTE that meets the 
                                "             current selection criteria 
                                "             for the NOTE area. 
                                " 
                                "After the appropriate displays are output, 
                                "it is possible for the user to append 
                                "information to the currently positioned 
                                "STAR without impacting the STAR and NOTE 
                                "current selection criteria. 
    #NEXT STAR.NOTE             "To repeat the process for the next STAR. 
00002
00003
00001
END
