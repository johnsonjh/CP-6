The Packset Initializer (PIG) processor performs several functions:  It turns 
scratch packs into usable packs, creates and deletes accounts, and sets the 
defaults and attributes of accounts.  For HELP messages, type: 
HELP (PIG) COMMANDS      For a categorized list of commands 
HELP (PIG) COMMAND_SUMM  For a brief description of all commands 
HELP (PIG) TOPICS        For a list of topics 
HELP (PIG) command       For the format of a specific command. 
                         Then type ? or ?? for more. 
HELP (PIG) command PARAM For parameter information for a 
                         specific command. 
HELP (PIG) command DESC  For the description of a specific 
                         command. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
ACCOUNT
To display all information on access permissions, type ??.  To display a 
subset of that information, type: 
HELP (PIG) ACCESS_PERM name 
Valid names are ACCOUNT_PERM, FILE_ACCESS_PERM, HYBRID_ACCESS_PERM. 
  Type     Permission 
  Account Permissions 
           C[REATE]    New files may be created in the account. 
           Note:  If CREATE is used alone, i.e., with no file permissions, it 
           also prevents any access to files created by others (they appear 
           not to exist even if access controls on the individual files might 
           seem to allow access). 
           NONE    Account appears not to exist.  (It appears not to exist 
           even if access controls on the individual files might seem to allow 
           access.  For example, if a file in the account has the READ 
           attribute, it is not accessible in a NONE account.) 
           Note:  NONE must not be combined with other permissions as a single 
           string.  For example, the options NONE=?, READ=?DN are permissible, 
           but NONEREAD=?DN is not. 
  File Access Permissions 
           R[EAD]    Records may be read. 
           W[NEW]    New records may be written. 
           U[PDATE]    Existing records may be overwritten. 
           D[ELR]    Existing records may be deleted. 
           {DELF[ILE]|S[CRATCH]}    Files may be deleted, renamed, or 
           repassworded and the ACCESS and ACSVEH attributes may be changed. 
           {F[ITMOD]|REAT[TR]}    File attributes except ACCESS and ACSVEH may 
           be modified. 
           E[XECUTE]    Files may be executed only; access to files depends on 
           the process opening the file.  The opening process is defined as 
           the name and account of the rununit associated with the execution 
           domain (user, monitor, debugger, ASL, or command processor) that is 
           performing the open request.  If the execution domain is the 
           monitor and the file is being opened for the purpose of execution 
           it as a user program, then the process is to be referred to as 
           FETCH[.:SYS]. 
           If the opener is in the ACSVEH processorlist, then the ACSVEH 
           controllist specifies the access the opener gets. 
           If the opener is not in the ACSVEH processorlist, then one of two 
           actions occurs: 
           1.  If the opener is the monitor process called FETCH, then the 
               program is allowed to run (i.e., for every file the ACSVEH list 
               is presumed to include FETCH=READ). 
           2.  If the opener is not FETCH, the opener gets any other controls 
               specified along with EXEC in controllist. 
           N[OLIST]    Files appears not to exist.  (However, if a file in the 
           account has the READ attribute, it is accessible in a NOLIST 
           account.) 
           Note:  NOLIST may be meaningfully combined only with EXECUTE.  For 
           example, the combined access permission NOLISTEXECUTE or NE is 
           permissible, but NOLISTREAD or NR is not. 
  Hybrid Access Permissions 
           {READ|RD}    Specifies that the account attribute CREATE and NONE 
           are both off and the file access permissions are all off except 
           READ which is on.  This specification causes users to have the 
           ability to list file names and to read files (unless otherwise 
           specified at file creation or via a PCL MODIFY command).  All READ 
           synonyms are treated the same with the exception of RD, which must 
           stand alone.  If combined with other permissions, RD is interpreted 
           as DR (delrec-read). 
           WR[ITE]    Specifies that the account attribute CREATE is on and 
           NONE is off, and the file access permissions READ, WNEW, UPDATE. 
           DELR, DELFILE, and FITMOD are on; EXECUTE and NOLIST are off.  (In 
           other words WRITE is equivalent to the permission string RWUDSFC.) 
           This specification causes users to have total access to files 
           within the account (unless otherwise specified at file creation or 
           via a PCL MODIFY command). 
00001
00002
00003
Format: 
AC[COUNT] [DP]#psn 
Parameters: 
psn    is the name of the packset to be accounted. 
Description: 
The ACCOUNT command accumulates granule accounting information into the system 
accounting log for all the files on a packset.  If exclusive access to the 
packset is obtained, a RECONSTRUCT operation is performed simultaneously.  If 
SHELFTIME has been specified, the ACCOUNT function occurs automatically at 
SHARED or PUBLIC MOUNT time. 
The ACCOUNT command should precede any installation accounting processing. 
00002
00001
Format: 
AT[TR] [={ON|YES}] 
       [={OFF|NO}] 
Parameters: 
ON|YES    specifies that the list function reports time information. 
OFF|NO    specifies the list function does not report time information. 
Description: 
The ATTR command controls whether the list function is to report time 
information, which includes packset mount, dismount, accounting, modification 
(DEFAULT command), creation times, account creation times, and modification 
(MODIFY command) times.  The LIST function is performed following the MODIFY, 
CREATE, and DEFAULT commands and in the LIST command. 
00002
00001
Format: 
B[UILD] [DP]#psn [F[ROM] vsn1[, vsn2] ... ] [optlist] 
Parameters: 
psn    specifies the packset name.  Up to six characters, at least one of 
which must be non-numeric, are permitted. 
vsn1[, vsn2]    are the volume serial numbers of the packs to be included. 
vsn is made up of one to eight decimal digits and may be followed by a single 
upper-case letter to designate which section of a split volume to use. 
Omitting FROM vsn1[, vsn2] ... requests reinitialization of an existing 
packset. 
optlist    specifies one or more options separated by commas.  Type 
HELP (PIG) OPTIONS for a list of these options. 
Description: 
The BUILD command is used to initialize or reinitialize a packset; that is, to 
create a Packset Account Directory (PAD), assign the packset a name, establish 
the serial numbers of the packs constituting the set, establish packset 
options (i.e., packset attributes and account defaults). 
Usage Notes: 
1.  Default packset options at packset initialization are GRAN=1000 and 
    READ=?, unless altered via a prior DEFAULT BUILD command; the defaults can 
    be displayed via the command DEFAULT BUILD (without parameters). 
2.  The DEFAULT DP#psn command permits changes to packset options for an 
    existing packset.  At reinitialization or any other time, packset options 
    can be displayed via DEFAULT DP#psn (without additional parameters). 
Examples: 
B #BACK FROM 105 G=1000,DEFAULT BACKUP,NO ACUP,WRITE=?MCS,OWNER=CSM/50LU 
This command establishes packset BACK from volume 105, specifies that by 
default file management accounts on the packset are to have 1000 granules and 
the DEFAULT BACKUP and NO ACUP attributes; specifies that by default user 
logon accounts ending in MCS are permitted WRITE access to the accounts (other 
users are permitted READ access by default since no DEFAULT command was used); 
and specifies that the packset owner is the user logon CSM,50LU. 
00002
00004
00001
00003
Format: 
                                      [PU[BLIC]   ] 
CAT[ALOG] {vsn                      } [SH[ARED]   ] 
          {[DP]#psn[vsn[, vsn] ... ]} [EX[CLUSIVE]] 
                                      [SC[RATCH]  ] 
                                      [OP[ERATOR] ] 
Parameters: 
vsn    if vsn is not specified, the packset must be currently accessible. 
OPERATOR    is the default and requires an operator keyin before any mounting 
will occur. 
SCRATCH    permits a set to be destroyed (via BUILD or SCRATCH) without 
confirmation .  An operator keyin is also required before any mounting will 
occur. 
Description: 
The CATALOG command adds entries to the system packset catalog.  The catalog 
contains one entry for each volume or packset that is cataloged.  A volume 
entry catalogs the volume serial number, associated packset name, if any, size 
in granules, and device model number.  A packset entry catalogs the setname, 
the volumes that make up the set, and the mode of mounting to be used in the 
absence of an operator keyin prior to the readying of the last volume of the 
set. 
00002
00001
Format: 
CATD[ELETE] {vsn          } 
            {[DP]#psn[vsn]} 
Parameters: 
psn    specifies the packset name. 
Description: 
The CATDELETE command removes an entry from the system packset catalog. 
00002
00001
Format: 
CATL[IST] [{vsn      } [>]] 
          [{[DP]#psn }    ] 
Parameters: 
>    indicates that all psns and vsns following the first matching one are to 
be listed. 
Description: 
The CATLIST command lists entries in the system packset catalog. 
00002
00001
Format: 
                            [PU[BLIC]    ] 
CATM[ODIFY] {vsn          } [SH[ARED]    ] 
            {[DP]#psn[vsn]} [EX[CLUSIVE] ] 
                            [SC[RATCH]   ] 
                            [OP[ERATOR]  ] 
Description: 
The CATMODIFY command changes an entry in the system packset catalog. 
00001
COUNT
    PIG commands can be categorized functionally as follows: 
    Packset management commands:  ACCOUNT, ATTR, BUILD, COUNT, CREATE, 
    DEFAULT, DELETE, DISMOUNT, DISPLAY, EXTEND, LIST, MODIFY, MOUNT, 
    RECONSTRUCT, SCRATCH. 
    Master Account Directory commands:  MADADD, MADDELETE, MADLIST. 
    System Packset Catalog commands:  CATALOG, CATDELETE, CATMODIFY, CATLIST. 
    Project Administrator command:  MAKEME. 
    Volume identification command:  SCRATCH. 
    Miscellaneous commands:  END, EXIT, HELP, QUIT.  For a full information on 
    a specific command, type: 
    HELP (PIG) command 
    for the format, then type ?? for additional information.  For a brief 
    description of a specific command, type: 
    HELP (PIG) COMMAND_SUMMARY command 
    PIG commands may contain a maximum of one command per record.  Each record 
    may contain a maximum of 256 bytes.  A semicolon (;) must be used to 
    continue the command on the next line.  Commentary may be entered in 
    double quotation marks. 
    To list a brief description of all PIG commands, type ??. To list a brief 
    description of a specific command, type 
    HELP (PIG) COMMAND_S command 
    Valid command names are ACCOUNT, ATTR, BUILD, CATALOG, CATDELETE, CATLIST, 
    CATMODIFY, COUNT, CREATE, DEFAULT, DELETE, DISMOUNT, DISPLAY, END, EXIT 
    EXTEND, HELP, LIST, MADADD, MADDELETE, MADLIST, MAKEME, MODIFY, MOUNT, 
    RECONSTRUCT, SCRATCH. 
  Command     Description 
  ACCOUNT 
              Accumulates granule accounting information into the system 
              accounting log for all files on the packset. 
  ATTR 
              Controls reporting of time information from the LIST function. 
  BUILD 
              Initializes, or reinitializes, a packset. 
  CATALOG 
              Adds entries to the system packset catalog. 
  CATDELETE 
              Removes an entry from the system packset catalog. 
  CATLIST 
              Lists entries in the system packset catalog. 
  CATMODIFY 
              Changes an entry in the system packset catalog. 
  COUNT 
              Displays current directory information for a packset. 
  CREATE 
              Creates an account on the packset and assigns account attributes 
              and file defaults. 
  DEFAULT 
              Displays or modifies the default packset options for BUILD; 
              displays or modifies the default packset options for a specific 
              packset; modifies the default mode of mounting for a packset. 
  DELETE 
              Removes an account from a packset. 
  DISMOUNT 
              Releases a packset. 
  DISPLAY 
              Displays the status of a pack, or of a specified packset, or of 
              all packsets. 
  {END|EXIT|QUIT} 
              Exits from the Packset Initializer. 
  EXTEND 
              Adds a volume or volumes to an existing packset. 
  HELP 
              Displays information about commands. 
  LIST 
              Displays the current status of a packset or specified 
              account(s). 
  MADADD 
              Adds an entry or a group of entries to the Master Account 
              Directory. 
  MADDELETE 
              Deletes an entry or a group of entries from the Master Account 
              Directory. 
  MADLIST 
              Lists the entries in the Master Account Directory. 
  MAKEME 
              Allows project administrator to administer a project. 
  MODIFY 
              Modifies account or file usage attributes of the specified 
              account(s). 
  MOUNT 
              Causes a packset to be mounted. 
  RECONSTRUCT 
              Reconstructs the free extent list of a packset. 
  SCRATCH 
              Establishes the volume serial number of a pack; splits physical 
              volumes into logical volumes and establishes the volume serial 
              number; or reinitializes pack(s) as scratch packs. 
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
00014
00024
00025
Format: 
CO[UNT] [DP]#psn 
Parameters: 
psn    specifies the packset name. 
Description: 
The COUNT command displays current directory information for all accounts on 
the packset.  This information includes:  NAMES, the number of file names in 
the account (including deleted files not yet recognized by EFT); GRANS, the 
number of granules in use; FD, the number of granules occupied by the 
directory (FD). 
00002
00001
Format: 
CR[EATE] [DP]#psn.acct [optlist] 
Parameters: 
psn    specifies the packset name. 
acct    specifies the name of the account to be created. 
optlist    specifies one or more options separated by commas.  Any PIG packset 
and account option be specified (except {NON[EWFDS]|N[EWFDS]} and 
{NOSH[ELFTIME]|SH[ELFTIME]} which apply to packsets only).  Type 
HELP (PIG) OPTIONS for a list of these options. 
Description: 
The CREATE command is used to create a file management account on the packset 
and to endow the account with account attributes and file defaults.  The 
account created is entered into the Packset Account Directory as a result of 
this command. 
Usage Notes: 
1.  The default account attributes assumed when an account is created are 
    established via BUILD, but may be modified via an intervening DEFAULT 
    DP#psn command.  The defaults are taken from the Packset Account 
    Directory. 
2.  To display the defaults assumed when an account is created, enter the 
    command DEFAULT DP#psn (without other parameters).  To display the 
    attributes for an existing account enter the command LIST #psn.acct . 
Examples: 
B #BACK FROM 105 G=1000,DEFAULT BACKUP,NO ACUP,WRITE=?MCS,OWNER=CSM/50LU 
CREATE #BACK.XB0LS NOLIST=?,READ=(?RN,?PL,?CO),WRITE=?MSC 
The CREATE command establishes unique attributes for the file management 
account XB0LS on #BACK, the packset established by the BUILD command.  The 
file management account XB0LS assumes the defaults established in the BUILD 
command:  1000 granules, DEFAULT BACKUP, NO ACUP.  However, the access 
permission is replaced.  The CREATE command specifies that this account is to 
be NOLIST to all other users, is allowed to be read by users whose accounts 
end in RN, PL and CO, and is allowed to be written by users whose accounts end 
in MSC.  Note that access permission options specified in the CREATE command 
replace all existing default access permissions (unless the first access 
permission option in the CREATE command is preceded by a plus).  Also note 
that as the OWNER attribute has different meanings on BUILD and CREATE, OWNER 
from the BUILD command does not provide the default OWNER attribute for XB0LS. 
00002
00004
00001
00003
DISPLAY
Format: 
Form 1: 
DEF[AULT] B[UILD] [optlist] 
Form 2: 
DEF[AULT] [DP]#psn [optlist] 
Form 3: 
DEF[AULT] M[OUNT] {NONE|P[UBLIC]|SH[ARED]} 
Parameters: 
optlist    specifies a list of options separated by commas.  Type 
HELP (PIG) OPTIONS for a list of these options. 
psn    is the packset name. 
Description: 
Form 1 of the command specified without options displays the account defaults 
and default packset attributes assumed when the BUILD command is performed. 
If the DEFAULT BUILD command specifies an option list, those options replace 
the defaults assumed at initialization via the BUILD command. 
Form 2 of the command specified without options displays the account defaults 
or default packset attributes assumed when the CREATE command is performed. 
If Form 2 specifies an option list, those options modify the existing defaults 
for the packset.  This command overrides the options specified when the 
packset was initialized by the BUILD command. 
Form 3 of the command specifies the default mode of mounting (to be used in 
the absence of an operator keyin) for uncataloged packsets. 
Usage Notes: 
1.  Specifying options in Form 1 of the DEFAULT command has no effect on 
    existing packsets or on subsequent invocations of PIG. 
2.  Specifying options in Form 2 of the DEFAULT command has no effect on 
    existing accounts on the packset. 
Examples: 
DEF B G=500,NOLIST=? 
B #BACK FROM 105 WRITE=?MCS,OWNER=CSM/50LU 
 . 
 . 
 . 
DEF B G=1000 
The first DEFAULT BUILD command establishes default attributes for any packset 
to be built.  As a result, at the BUILD command the attributes for the #BACK 
packset include a default granule allocation limit of 500, and file 
permissions that prohibit any user from being able to list or access any files 
unless access permission(s) for a user account are explicitly specified when 
the file or account is created.  One exception added via the BUILD command is 
that users whose account name ends in MCS are given default WRITE permission. 
The second DEFAULT BUILD command modifies one default specified in the first 
DEFAULT BUILD command so that the default granule allocation is 1000.  Any 
accounts created on #BACK during the session are not affected by the second 
DEFAULT BUILD command; it affects only packsets built during the session after 
it. 
00002
00004
00001
00003
Format: 
DELETE [DP]#psn.acct 
Parameters: 
psn    is the name of the packset on which the account to be deleted resides. 
 .acct    is the designation of the account to be deleted.  Use of the 
wildcard character is not permitted. 
Description: 
The DELETE command is used to remove an account from a packset. 
00002
00001
DISPLAY
Format: 
DISM[OUNT] [DP]#psn 
Parameters: 
psn    specifies the packset name. 
Description: 
The DISMOUNT command can be used in place of a !RELEASE command. 
Usage Notes: 
1.  The DISMOUNT command saves a few keystrokes on-line.  It is exactly 
    equivalent to !RELEASE DP#psn. 
00002
00001
00003
Format: 
          [DPnn    ] 
D[ISPLAY] [SETS    ] 
          [[DP]#psn] 
Parameters: 
nn    is the number of the disk drive for which status is to be displayed. 
SETS    denotes that the status of all packsets is to be displayed. 
psn    is the packset identification of the packset to be displayed. 
Description: 
The DISPLAY command is used to display the status of a specified pack, or of a 
specified packset, or of all packsets. 
The status information displayed includes all of the packsets currently known 
to the Packset Initializer.  The information includes the packset serial 
number, the packset name, the device address for the device on which the pack 
is mounted, and information concerning the packset status; that is, shared, 
available, waiting for dismount, or reserved exclusively for a specific user. 
Status information for Mirrored Disk devices is also shown. 
00002
00001
Format: 
{E[ND]|[E]X[IT]|Q[UIT]} 
Description: 
This command terminates PIG. 
00001
EXTEND
END
Format: 
EX[TEND] [DP]#psn W[ITH] vsn1[, vsn2] ... 
Parameters: 
psn    is the name of the packset to be extended. 
vsn1[, vsn2] ...    are the volume serial numbers of the volumes to be added. 
Description: 
The EXTEND command is used to add a volume or volumes to an existing packset. 
A RECONSTRUCT operation, described below, is required in order to use the new 
volumes.  The RECONSTRUCT operation will occur automatically the next time the 
set is mounted, or immediately if it is currently mounted exclusively for the 
user of EXTEND.  Only the system set (DP#SYS) may be EXTENDed without 
exclusive access. 
00002
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
A 
  access permission - 
      HELP ACCESS_PERMISSIONS ACCOUNT_PERMISSIONS 
  access permission (PIG) - 
      HELP OPTIONS PERM 
  ACCOUNT Command -   
    PIG - 
      HELP ACCOUNT FORMAT: 
  ACCOUNT Command - 
      HELP ACCOUNT 
  account defaults - 
      HELP BUILD DESCRIPTION: 
      HELP DEFAULT DESCRIPTION: 
  account permissions - 
      HELP ACCESS_PERMISSIONS ACCOUNT_PERMISSIONS 
  accounting (PIG) - 
      HELP ACCOUNT DESCRIPTION: 
  ACUP option -   
    PIG - 
      HELP OPTIONS ACUP 
  ATTR Command - 
      HELP ATTR 
B 
  BACKUP option (PIG) - 
      HELP OPTIONS BACKUP 
  BUILD Command - 
      HELP BUILD 
C 
  CATALOG Command - 
      HELP CATALOG 
  CATDELETE Command - 
      HELP CATDELETE 
  CATLIST Command - 
      HELP CATLIST 
  CATMODIFY Command - 
      HELP CATMODIFY 
  CGMEM option (PIG) - 
      HELP OPTIONS CGMEM 
  CHECKWRITE option (PIG) - 
      HELP OPTIONS CHECKWRITE 
  COUNT Command - 
      HELP COUNT 
  CREATE Command -   
    PIG - 
      HELP CREATE FORMAT: 
  CREATE Command - 
      HELP CREATE 
D 
  DATACHECKWRITE option (PIG) - 
      HELP OPTIONS DATACHECKWRITE 
  DEFAULT Command - 
      HELP DEFAULT 
  default packset attributes - 
      HELP DEFAULT DESCRIPTION: 
  DEFAULTBACKUP option (PIG) - 
      HELP OPTIONS BACKUP 
  DELETE Command -   
    PIG - 
      HELP DELETE FORMAT: 
  DELETE Command - 
      HELP DELETE 
  directory - 
      HELP COUNT DESCRIPTION: 
  DISMOUNT Command - 
      HELP DISMOUNT 
  DISPLAY Command -   
    PIG - 
      HELP DISPLAY FORMAT: 
  DISPLAY Command - 
      HELP DISPLAY 
E 
  END Command - 
      HELP END 
  EXTEND Command - 
      HELP EXTEND 
F 
  FD - 
      HELP COUNT DESCRIPTION: 
  file access permissions - 
      HELP ACCESS_PERMISSIONS FILE_ACCESS_PERMISSIONS 
  File Directory - 
      HELP COUNT DESCRIPTION: 
G 
  GRANLIM option (PIG) - 
      HELP OPTIONS GRANLIM 
  granule accounting - 
      HELP ACCOUNT DESCRIPTION: 
H 
  HELP Command - 
      HELP HELP 
  hybrid access permissions - 
      HELP ACCESS_PERMISSIONS HYBRID_ACCESS_PERMISSIONS 
I 
  Invoking PIG - 
      HELP INVOKING_PIG 
L 
  LIST Command -   
    PIG - 
      HELP LIST FORMAT: 
  LIST Command - 
      HELP LIST 
M 
  MADADD Command - 
      HELP MADADD 
  MADDELETE Command - 
      HELP MADDELETE 
  MADLIST Command - 
      HELP MADLIST 
  MAKEME Command - 
      HELP MAKEME 
  Master Account Directory (MAD) - 
      HELP MADLIST DESCRIPTION: 
  MERGEACCESS option (PIG) - 
      HELP OPTIONS MERGEACCESS 
  Mirrored Disk - 
      HELP BUILD USAGE_NOTES: 
      HELP DISPLAY DESCRIPTION: 
      HELP SCRATCH USAGE_NOTES: 
  MODIFY Command -   
    PIG - 
      HELP MODIFY PARAMETERS: 
  MODIFY Command - 
      HELP MODIFY 
  MOUNT Command - 
      HELP MOUNT 
N 
  NEWFDS option (PIG) - 
      HELP OPTIONS NONEWFDS 
  NOBACKUP option (PIG) - 
      HELP OPTIONS BACKUP 
O 
  OWNER option (PIG) - 
      HELP OPTIONS OWNER 
P 
  Packset Account Directory (PAD) - 
      HELP BUILD DESCRIPTION: 
  packset attributes - 
      HELP BUILD DESCRIPTION: 
  PIG -   
    ACCOUNT Command - 
      HELP ACCOUNT FORMAT: 
    ATTR Command - 
      HELP ATTR FORMAT: 
    BUILD Command - 
      HELP BUILD FORMAT: 
    CATALOG Command - 
      HELP CATALOG FORMAT: 
    CATDELETE Command - 
      HELP CATDELETE PARAMETERS: 
    CATLIST Command - 
      HELP CATLIST FORMAT: 
    CATMODIFY Command - 
      HELP CATMODIFY FORMAT: 
    COUNT Command - 
      HELP COUNT FORMAT: 
    CREATE Command - 
      HELP CREATE FORMAT: 
    DEFAULT Command - 
      HELP DEFAULT FORMAT: 
    DELETE Command - 
      HELP DELETE FORMAT: 
    DISMOUNT Command - 
      HELP DISMOUNT FORMAT: 
    DISPLAY Command - 
      HELP DISPLAY FORMAT: 
    EXTEND Command - 
      HELP EXTEND FORMAT: 
    LIST Command - 
      HELP LIST FORMAT: 
    MADADD Command - 
      HELP MADADD FORMAT: 
    MADDELETE Command - 
      HELP MADDELETE FORMAT: 
    MADLIST Command - 
      HELP MADLIST FORMAT: 
    MAKEME Command - 
      HELP MAKEME FORMAT: 
    MODIFY Command - 
      HELP MODIFY PARAMETERS: 
    MOUNT Command - 
      HELP MOUNT FORMAT: 
    RECONSTRUCT Command - 
      HELP RECONSTRUCT FORMAT: 
    SCRATCH Command - 
      HELP SCRATCH FORMAT: 
  PIG Command Summary - 
      HELP COMMANDS 
  PROTECTED option (PIG) - 
      HELP OPTIONS PROTECTED 
  PURGE option (PIG) - 
      HELP OPTIONS PURGE 
R 
  RECONSTRUCT Command - 
      HELP RECONSTRUCT 
S 
  SCRATCH Command -   
    PIG - 
      HELP SCRATCH FORMAT: 
  SCRATCH Command - 
      HELP SCRATCH 
  SHELFTIME - 
      HELP ACCOUNT DESCRIPTION: 
  SHELFTIME option (PIG) - 
      HELP OPTIONS NOSHELFTIME 
  split volume (disk) - 
      HELP SCRATCH PARAMETERS: 
  STOW option (PIG) - 
      HELP OPTIONS STOW 
T 
  $$TRACKER file - 
      HELP INVOKING_PIG 
V 
  volume serial number (VSN) - 
      HELP SCRATCH DESCRIPTION: 
  volume, split - 
      HELP SCRATCH PARAMETERS: 
  VSN - 
      HELP SCRATCH DESCRIPTION: 
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
    To invoke PIG, enter: 
    !PIG 
    PIG may be run as a console ghost job, with commands keyed in at the 
    operator's console; output occurs at the operator's console. 
    Note:  Any account that is built automatically on the system pack (DP#SYS) 
    at boot-time should not be moved to another packset. 
    If a $$EFT account exists on the packset, a record of every DEFAULT, 
    CREATE, MODIFY, and DELETE command executed by PIG will be maintained in a 
    file called $$TRACKER. 
Format: 
       {[DP]#psn.acct[>]} 
L[IST] {[DP]#psn        } 
       {.acct[>]        } 
Parameters: 
psn    is the name of the packset to be displayed. 
 .acct    is the name of the account to be displayed.  The .acct field may 
include one or more question mark characters used as wildcard characters.  It 
may be followed by a greater-than character (>) to indicate that all accounts 
following the first matching one are to be listed. 
Description: 
The LIST command is used to display the current attributes of a specified 
packset or of a specified account.  The displayed information includes all the 
attributes of the specified packset and its accounts, as set by the BUILD and 
DEFAULT commands, or all the attributes of the specified accounts, as set by 
the CREATE and MODIFY commands. 
00002
00001
MODIFY
Format: 
MADA[DD] [DP]#psn[.acct] 
Parameters: 
psn.acct    is the packset and account designation to be entered into the 
Master Account Directory.  If .acct is omitted, all accounts in the packset 
will be added to the MAD if not already present.  acct may be wildcarded. 
Description: 
The MADADD command is used to add an entry to the Master Account Directory. 
Note:  Changing an entry on the Master Account Directory requires two steps. 
The erroneous or obsolete entry must first be deleted via MADDELETE and then 
the corrected form entered via MADADD. 
00002
00001
Format: 
MADD[ELETE] {[DP]#psn[.acct]|.acct} 
Parameters: 
psn    is the name of a packset on which the designated account resides.  If 
this variable is used without an .acct variable, all entries concerning the 
named packset are deleted from the Master Account Directory. 
 .acct    is the designation of the account entry to be deleted.  acct may be 
wildcarded. 
Description: 
The MADDELETE command is used to delete an entry or group of entries from the 
Master Account Directory. 
00002
00001
Format: 
MADL[IST] [{[DP]#psn|.acct|.acct>}] 
                    [{.acct[>]}] 
Parameters: 
psn    is the name of the packset whose MAD entries are to be listed. 
 .acct    is the designation of the account whose MAD entries are to be 
listed.  .acct may include wildcard characters.  It may be followed by the > 
character to indicate that all accounts following the first matching one are 
to be listed. 
Description: 
The MADLIST command is used to list the entries in the Master Account 
Directory (MAD).  These entries denote accounts that may be accessed by 
specifying the account designation only (i.e., the packset of residence need 
not be specified), and show where they are resident. 
The list resulting from entering the command in the form:  MADLIST .acct will 
indicate on which packset the system expects to find the designated account. 
The list resulting from entering the command in the form:  MADLIST #psn will 
show all entries in the MAD for all accounts in psn's Account Directory. 
A sample output, resulting from entering the command in the form MADL, is 
shown below. 
#SYS     .:SYMI      #SYS     .:SYMO   #SYS    .:SYS 
#YOX     .CHK        #YOX     .CS      #SYS    .DELTA 
#YOX     .FELDMAN    #YOX     .FJJ     #YOX    .GGH 
#YOX     .HEYING     #YOX     .IWG     #YOX    .JEFF 
#YOX     .JPC        #YOX     .JRC     #YOX    .JTA 
#YOX     .KRASNY     #YOX     .LEM     #YOX    .LLA 
#YOX     .PEGGY      #YOX     .PKT     #YOX    .PLA 
#YOX     .PRYOU      #YOX     .PRYSU   #YOX    .PRYTX 
#YOX     .TANDD      #SYS     .TEST123 
00002
00001
Format: 
MAK[EME] [.acct/name] 
Parameters: 
 .acct/name    identify the project.  The account/name must be a project for 
which the user is an administrator. 
Description: 
The MAKEME command is used to establish a project administrator mode wherein 
only the account manipulation commands are available and they can be used only 
for the accounts defined in the project (see SUPER). 
A project administrator is automatically in this mode when he enters PIG and 
may escape from it by using a null MAKEME command. 
00002
00001
Format: 
M[ODIFY] [[DP]#psn].acct optlist 
Parameters: 
psn    specifies the packset name. 
 .acct    specifies the account designation and may contain one or more 
question mark wildcard characters. 
optlist    specifies one or more options separated by commas.  Type 
HELP (PIG) OPTIONS for a list of these options. 
Description: 
The MODIFY command is used to modify the account attributes and file defaults 
applicable to the specified account(s).  This command overrides the account 
attributes and file defaults specified for the account when it was created via 
the CREATE command. 
Usage Notes: 
1.  To display the existing attributes for the account, enter the command LIST 
    [#psn].acct. 
2.  MODIFY alters attributes that are stored in the account's File Directory, 
    thus changing the accessibility of all files in the account. 
Examples: 
B #BACK FROM 105 G=1000,DEFAULT BACKUP,NO ACUP,WRITE=?MCS,OWNER=CSM/50LU 
CREATE #BACK.XB0LS NOLIST=?,READ=(?RN,?PL,?CO),WRITE=?MSC 
  . 
  . 
  . 
MODIFY #BACK.XB0LS +WRITE=?DN 
The MODIFY command alters the existing attributes for file management account 
XB0LS on #BACK, the packset established by the BUILD command.  Unique 
attributes for XB0LS were first established by the CREATE command shown. 
Later, the user enters the MODIFY command, specifying that the WRITE access 
permission for user accounts ending in DN is to be added to the existing 
access permissions for the account XB0LS. 
00002
00004
00001
00003
Format: 
MOU[NT] [DP]#psn [PU[BLIC]|SH[ARED]|EX[CLUSIVE]] 
Parameters: 
psn    specifies the packset name. 
Description: 
The MOUNT command attempts to cause a packset to be mounted in exclusive mode 
if is not already mounted (the option is ignored in this case).  Except in 
batch mode, resources are acquired automatically and will be returned 
automatically when the packset is released.  Except in batch mode, all volumes 
must be spinning; the operator will not be asked to mount them.  If the 
packset is already mounted, the command attempts to associate the user with 
the packset in the specified mode. 
Usage Note: 
The MOUNT command is useful when creating a batch job of PIG commands, to 
cause operator mount requests for the volumes of a packset.  Note that !RES 
must be used to allocate the required resources. 
00002
00001
00003
To display all Packset and Account options, type ??.  To display a specific 
option, type: 
HELP (PIG) OPTIONS option 
Valid option names are: ACUP, BACKUP, CGMEM, CHECKWRITE, DATACHECKWRITE, 
DEFAULTBACKUP, GRANLIM, MERGEACCESS, NEWFDS, NONEWFDS, NOBACKUP, NOCHECKWRITE, 
NODATACHECKWRITE, NOMERGEACCESS, NOPURGE, NOSHELFTIME, NOSTOW, NOT_PROTECTED, 
SHELFTIME, OWNER, perm (for access permissions), PROTECTED, PURGE, and STOW. 
  Option     Use 
  {A[CUP]|NOA[CUP]} 
             Specifies whether or not a file's access date should be updated 
             when a read-only operation is performed.  Default is ACUP. 
  {B[ACKUP]|D[EFAULT]B[ACKUP]|NOB[ACKUP]} 
             For tape backup eligibility (via EFT's SAVE or BACKUP command). 
             B[ACKUP] specifies that files in the account are eligible for 
             backup but explicit user action is required.  A file in a BACKUP 
             account is backed up (1) if the file has has been modified (or 
             created) since the last backup, save, or dual operation and has 
             the BUPM attribute set YES (it can be set via PCL's BACKUP output 
             option, via !SET BUPM=YES, etc.) or (2) if the IBEX BACKUP 
             command is used to request one-time backup of the file. 
             D[EFAULT]B[ACKUP] specifies that files in the account are 
             eligible for backup by default.  Without user intervention files 
             are backed up if modified (or created) since the last EFT backup, 
             save, or dual operation.  (Files in DEFAULTBACKUP accounts have 
             the BUPM attribute set ON by default.  Thus there is usually no 
             reason to use the IBEX BACKUP command.) To prevent a file in a 
             DEFAULTBACKUP account from being backed up, the file's BUPM 
             attribute can be set to NO (via PCL's NBACKUP output option, via 
             !SET with BUPM=NO, etc.) 
             NOB[ACKUP] specifies that files in the account are not eligible 
             for backup.  The account is ignored at EFT save or backup 
             operations. 
             The default is BACKUP. 
  CG[MEM]=n 
             Specifies the number of pages (1024 words) of CP-6 main memory 
             that may be in use at any time by open comgroups in the account. 
             The specified value is rounded up to the next multiple of eight 
             pages.  The default is 0. 
  {C[HECKWRITE]|NOC[HECKWRITE]} 
             Specifies whether or not disk read-and-compares after write 
             (checkwrite) operations should be performed on the directory 
             granules.  Default is NOCHECKWRITE. 
  {D[ATACHECKWRITE]|NOD[ATACHECKWRITE]} 
             Same as CHECKWRITE on all granules.  Default is NODATACHECKWRITE. 
  G[RANLIM]=n 
             For establishing the granule limit for the account.  Default is 
             1000. 
             Note:  A default granule limit (GRAN=1000) is assumed by PIG, but 
             may be overridden by PIG commands.  See BUILD, DEFAULT, CREATE, 
             and MODIFY commands for details. 
  {M[ERGEACCESS]|NOM[ERGEACCESS]} 
             Specifies whether or not access permissions on a given file in 
             the account are to be concatenated onto the default permissions 
             or to replace them .  Default is NOMERGEACCESS. 
             The following example is provided to clarify how the 
             MERGEACCESS|NOMERGEACCESS option is used.  Assume an account with 
             the file access permissions: 
             READ=?,NOLIST=ZZZ? 
             contains a file with the attribute: 
             WRITE=?. 
             In this case: 
             If a user is running under an account with a name that does not 
             begin with ZZZ, the user will have WRITE access to the file 
             regardless of the MERGEACCESS|NOMERGEACCESS option. 
             If a user is running under an account with a name that does begin 
             with ZZZ, access to the file depends on the 
             MERGEACCESS|NOMERGEACCESS option for the account. 
             o   With NOMERGEACCESS (replacement of permissions), the access 
                 controls on the file appear to be: 
                     WRITE=? 
                 Thus the ZZZ? user has WRITE access to the file. 
             o   With MERGEACCESS (concatenation of permission), the access 
                 control on the file appear to be: 
                     READ=?,NOLIST=ZZZ?,WRITE=? 
                 Thus for the ZZZ? user the NOLIST option prevails; that is, 
                 the file in question appears not to exist to the ZZZ? user. 
                 (To accomplish the effect of NOMERGEACCESS for a particular 
                 file in a MERGEACCESS account, the access specifications for 
                 the account should be repeated for the file, in this case, 
                 the options WRITE=?,WRITE=ZZZ? .) 
  {NON[EWFDS]|N[EWFDS]} 
             Specifies whether or not new accounts may be created on the 
             packset without the use of PIG (e.g., by a PCL COPY).  The 
             default is NONEWFDS.  This option is valid for packsets only and 
             may be specified only on the BUILD or DEFAULT commands. 
             Note:  FMSEC privilege is required to create a new account with a 
             name other than the current logon account or on a packset other 
             than the user's home set, if the NEWFDS attribute is in effect. 
  {NOSH[ELFTIME]|SH[ELFTIME]} 
             Specifies whether or not SHELFTIME is to be accounted for 
             separately from mounted time. 
             The default is NOSH.  This option is valid for packsets only and 
             may be specified only on the BUILD or DEFAULT commands. 
  O[WNER] [= (acct/name[, acct/name] ... )] 
             This option has two meanings: 
             As a packset option on BUILD and DEFAULT commands, this option 
             establishes the packset owner(s).  This provides to the specified 
             users full use of PIG commands for the packset being built. 
             As an account option on the CREATE and MODIFY commands, this 
             option establishes account owners.  This allows the specified 
             users to invoke the MODIFY and CREATE commands to change certain 
             account attributes and all file defaults for the account(s) being 
             MODIFied.  The attributes subject to change are restricted to 
             PROTECTED, NOTPROTECTED, BACKUP, DEFAULTBACKUP, MERGEACCESS, and 
             NOMERGEACCESS.  Note that NOBACKUP cannot be changed to either 
             BACKUP or DEFAULTBACKUP and vice versa. 
             acct/name    refers to a user's SUPER authorized account and 
             name.  Name (but not acct) may be a single question mark to 
             indicate all users authorized for acct.  If no acct/name is 
             specified, the current owner is removed. 
  {perm|+perm|-perm} = {uacctlist|ALL|?} 
             This form is used to define access permissions for file 
             management accounts. 
             perm    specifies any access permission(s) that can be displayed 
             by typing HELP (PIG) ACCESS_PERM.  Perm may consist of 
             o   A single account permission, e.g., NONE. 
             o   A single file default permission, e.g., E[XECUTE]. 
             o   A hybrid specification, READ or WRITE, that incorporates the 
                 most frequently used settings for account permissions and 
                 file defaults. 
             o   A string that may combine one or several file default 
                 permissions or the account permission C[REATE], e.g., 
                 READWNEW (access permissions, READ and WNEW), RU (access 
                 permissions R[EAD] and U[PDATE], abbreviated). 
                 Note:  C[REATE] can be abbreviated C, CR, etc.  Thus CRU is 
                 equivalent to CREATEUPDATE (not CREATEREADUPDATE), whereas 
                 RCU is equivalent to READCREATEUPDATE. 
                 Note:  Default access permissions (READ=?) are provided by 
                 PIG, but may be overridden by PIG commands.  See the BUILD, 
                 DEFAULT, CREATE, and MODIFY commands for details. 
             uacctlist    specifies the user logon accounts that are given the 
             specified access permission.  If multiple accounts are specified, 
             they must be enclosed in parentheses and separated by commas; if 
             one account is specified parentheses are not required.  Account 
             names can include wildcard characters anywhere in the string.  If 
             more than one access permission option is specified and wildcard 
             characters are used in uacctlist, user matches may occur for more 
             than one account list.  (Note that a similar situation can occur 
             if MERGEACCESS is specified.)  In this case, the user is given 
             the permissions associated with the list in which the most 
             non-wildcard characters match.  If the same number of 
             non-wildcard characters match, the match is against the last 
             specified account list.  A total of 200 account names may be 
             specified. 
             {ALL|?}    specifies that all users are to be given the specified 
             access permission (unless a "closer match" is specified as 
             discussed above). 
             Note:  In general, any access control option(s) specified in a 
             DEFAULT BUILD, BUILD, CREATE, or MODIFY command replace all 
             default access control options.  Exceptions are (1) the + and - 
             symbols which are described below, and (2) the default perm=?. 
             The perm=? default is replaced by any other perm=? option, but 
             not by the option perm=uacctlist.  For instance if the default is 
             READ=? and BUILD specifies WRITE=?, the result is WRITE=?. 
             However, if the default is READ=? and WRITE=?MCS is specified on 
             BUILD, the result is READ=?, WRITE=?MCS. 
              + or -    is useful only if the first access permission option 
             entered in a command specifies one of them and only in reference 
             to a file management account having default or explicit access 
             permissions already established. 
             o   Using + adds more user accounts to the existing access 
                 permissions.  For example, if existing permissions are 
                 NOLIST=?, READ=?MCS, entering a command with +WRITE=?DN, 
                 READ=?RN results in these access permissions:  NOLIST=?, 
                 READ=?MCS, WRITE=?DN, READ=?RN . 
             o   Using + replaces the access permission for a user already 
                 included in the existing access permissions.  For example, if 
                 the existing permissions are NOLIST=?, READ=?MCS, entering a 
                 command with +WRITE=?MCS results in the access permissions: 
                 NOLIST=?, WRITE=?MCS. 
             o   Omitting + replaces access permission options for specific 
                 accounts except those specified as perm={ALL|?} as discussed 
                 in the note above. 
             o   Using - removes the specified permissions from the current 
                 set for the specified accounts when used in the form: 
                 -perm=uacctlist.  For example, if the existing permissions 
                 include READCREATE=?DN, entering a command with -CREATE=?DN 
                 would change that specification to READ=?DN. 
             o   Using - with no permission list removes the specified 
                 uacctlist entries from the existing access permission list. 
                 For example, if the current list includes READ=?DN, entering 
                 a command with -=?DN will remove that specification from the 
                 list. 
                 Note; The acct ? cannot be removed from the list. An attempt 
                 to do so, e.g., -=?, is interpreted as +NONE=? (all 
                 permissions are removed for ?).  Note also that wildcard 
                 matching is not used to find existing specifications for 
                 modification.  ?DN will find a specification only for ?DN, 
                 not for XDN, for example. 
  {PR[OTECTED]|NO[T] PR[OTECTED]} 
             For identification protection.  If PROTECTED is selected, 
             unlimited access is given to a file in the specified account only 
             to the file's creator (that is, access is limited to an 
             account/name match).  If NOT PROTECTED is selected, unlimited 
             access is given to any user whose account is the same as that in 
             which the file resides.  Default is NOT PROTECTED. 
  {PU[RGE]|NOPU[RGE]} 
             Specifies whether or not files in the account can be purged via 
             EFT's PURGE command.  Default is PURGE. 
  {ST[OW]|NOST[OW]} 
             Specifies whether or not files in the account can be archived, 
             i.e., can be queued for STOW via EFT's STOW command.  Default is 
             STOW. 
00001
00002
00004
00003
00004
00005
00002
00002
00006
00007
00008
00001
00002
00004
00005
00007
00008
00013
00009
00014
00012
00010
00011
00012
00013
00009
00014
OPTIONS
  Function       Command      PPRIV        Privilege 
Packset        ACCOUNT      PIGC         FMDIAG and FMSEC or setowner 
Management                               plus SYSLOG 
               BUILD        PIGC         FMDIAG and FMSEC or setowner 
               DEFAULT      PIGC         FMDIAG, or setowner 
               DISPLAY      PIGD         SPCLMM 
               EXTEND       PIGC         FMDIAG and FMSEC or setowner 
               RECONSTRUCT  PIGC         FMDIAG and FMSEC or setowner 
               SCRATCH      PIGC         FMDIAG 
ACCOUNT        CREATE       PIGC         FMDIAG, PADMIN, or setowner 
               DELETE       PIGC         FMDIAG, PADMIN, or setowner 
               LIST         PIGD         FMSEC, PADMIN, or setowner if 
                                         '?' is used; Access to 
                                         account; FMSEC or setowner if 
                                         creator or owner is to be 
                                         seen. 
               MODIFY       PIGC         FMDIAG, PADMIN, or acct owner; 
                                         FMSEC, PADMIN, or setowner 
                                         if '?' used. 
MAD            MADADD       PIGC         FMDIAG 
               MADDELETE    PIGC         FMDIAG 
               MADLIST      PIGC         FMSEC (if more than 1 account) 
CATALOG        CATALOG      PIGC         FMSEC, FMDIAG 
               CATDELETE    PIGC         FMSEC 
               CATLIST      PIGC         FMSEC 
               CATMODIFY    PIGC         FMSEC 
Project        MAKEME       PIGC         PADMIN, FMSEC, or FMDIAG 
Management                  or SUPER 
END
Format: 
REC[ONSTRUCT] [DP]#psn 
Parameters: 
psn    is the name of the packset to be reconstructed. 
Description: 
The RECONSTRUCT command is used to reconstruct the free extent list (the 
internal representation of the remaining unused space) of the specified 
packset.  It also fixes incorrect granule counts in files and directories. 
The packset must be mounted exclusive. 
Note: The actual (physical) layout of the in-use and free extents on the pack 
are not in any way affected. 
00002
00001
Format: 
          {vsn1[, vsn] ...                     } 
SCR[ATCH] {DPnn AS vsn2 [(size1[, size2] ... )]} 
          {vsn3 [(size1 [, size2] ... )]       } 
          {[DP]#psn                            } 
Parameters: 
vsn1, [vsn] specifies a collection of existing logical volumes to be 
scratched.  Each volume serial number is made up of one to eight decimal 
digits and may be followed by a single upper-case letter to designate which 
section of a split volume to use. 
nn    is the number of the disk drive on which the pack is mounted. 
vsn2    specifies the volume serial number to be assigned to an uninitialized 
physical volume.  vsn2 is made up of one to eight decimal digits.  This field 
is required if the pack is uninitialized. 
vsn3    specifies the vsn to assign when dividing a physical volume into 
logical volumes.  vsn3 is made up of 1 to 8 decimal digits. 
size1    is used to create a split volume.  Each size is a number of granules 
to be occupied by a portion of the volume.  If the sum is not the size of the 
volume, another section will be added to use the remaining space.  The maximum 
value for size is 262143, or the size of the disk volume itself, whichever is 
smaller. 
psn    is the name of a packset of which all volumes are to be scratched.  The 
packset must not be in use unless it is necessary to scratch DP#SYS. 
Description: 
The SCRATCH command is used to establish the volume serial number of a pack on 
the specified drive, to change the volume serial number of a specified pack, 
to set the sizes of the logical volumes on a pack, or to reinitialize a 
specified pack or all the volumes of a packset as scratch packs. 
Usage Notes: 
1.  Before scratching a previously initialized and cataloged pack, the packset 
    should be deleted from the catalog via the CATDELETE command. 
2.  The maximum size of a logical volume on a disk is 262143 granules.  PIG 
    does not accept a SCRATCH command that does not properly divide a 
    large-capacity disk into legal logical volumes. 
3.  The SCRATCH command can be used to SCRATCH only a primary Mirrored Disk 
    device -- not a secondary device. 
00002
00001
00003
END
