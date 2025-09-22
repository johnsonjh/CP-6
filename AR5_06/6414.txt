The journaling (JAYS) processor takes ownership responsibility for a journal, 
performs journaling, and related utility functions. 
To obtain more information, type: 
HELP (JAYS) COMMANDS      For a brief description of the 
                          commands. 
HELP (JAYS) TOPICS        For a list of JAYS HELP topics. 
HELP (JAYS) command       For the format of a specific command. 
                          Then type ? or ?? for more. 
HELP (JAYS) command PARAM For only the parameters for a 
                          specific command. 
HELP (JAYS) command DESC  For the description of a specific 
                          command. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
Format: 
CA[NCEL] fid 
Parameters: 
fid    specifies the CP-6 file identifier of a journal file. 
Description: 
This command terminates journaling to the specified file and closes the file. 
If JAYS is journaling comgroup messages on this file, the comgroup's journal 
station DCB is also closed.  Messages are output to the system operator 
console indicating that journaling for the comgroup is terminated. 
Usage Note: 
The user requesting this command must have DELF access to the journal file. 
00002
00001
00003
  Command     Meaning 
CANCEL      Terminate journaling to the specified file. 
CREATE      Establish attributes for a journal. 
END         Exit JAYS.  EXIT, QUIT, and Carriage Return also exit 
            JAYS. 
HELP        Displays information on the JAYS processor and other 
            processors. 
LIST        Display a list of all open journals and comgroups that the 
            user can see (i.e., to which the user has read access). 
RENAME      Rename the specified journal file to permit continued 
            journaling to a new physical file using the original 
            name. 
Enter: HELP (JAYS) command for information about a specific command. 
COMMANDS
Format: 
CR[EATE] fid[, optionlist] 
Parameters: 
fid    is a legal CP-6 file identifier. 
optionlist    is the list of options permitted for the IBEX SET command. 
Although all legal SET command options may be present, only the serial number 
specification (SN=LT#sn1,sn2,... or SN=sn1,sn2,...) is meaningful. 
For additional information on the SN option, enter: 
HELP (IBEX) SET_OPS option, where option is the option name. 
Description: 
The CREATE command creates a file with the name, account and password 
specified by fid, on the current file management packset, replacing any 
existing old file.  The UATTR area of the created file will contain the serial 
number list specified in the optionlist. 
Usage Note: 
The CREATE command is used to define a list of serial numbers of magnetic tape 
volumes, when the journal is a magnetic tape file, and to preserve them for 
later use in the UATTR area of the file.  The serial numbers will be used by 
JAYS when opening volumes of the magnetic tape for journal output. 
It is not necessary to use the CREATE command if the journal is to be a disc 
file, as the information required to open the file is provided by the opening 
user. 
00002
00001
00003
Format: 
E[ND] 
Description: 
This command causes an exit from JAYS. 
Usage Note: 
Entering Q[UIT], EX[IT], X[IT], or Carriage Return also causes an exit from 
JAYS. 
00001
00002
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
C 
  CANCEL Command - 
      HELP CANCEL 
  CREATE Command -   
    JAYS - 
      HELP CREATE FORMAT: 
  CREATE Command - 
      HELP CREATE 
E 
  END Command - 
      HELP END 
H 
  HELP Command - 
      HELP HELP 
I 
  Invoking JAYS - 
      HELP INVOKING_JAYS 
J 
  JAYS -   
    CANCEL Command - 
      HELP CANCEL FORMAT: 
    CREATE Command - 
      HELP CREATE FORMAT: 
    LIST Command - 
      HELP LIST FORMAT: 
    RENAME Command - 
      HELP RENAME FORMAT: 
L 
  LIST Command -   
    JAYS - 
      HELP LIST FORMAT: 
  LIST Command - 
      HELP LIST 
R 
  RENAME Command - 
      HELP RENAME 
00001
00002
00003
00004
00005
00006
HELP_INDEX
To invoke the command-executing portion of JAYS, the format is 
!JAYS 
Note:  Users who invoke the TRADER processor to request journaling for 
Transaction Processing systems do NOT invoke JAYS directly. 
Format: 
L[IST] 
Description: 
This command displays a list of all open journals and comgroups known to JAYS. 
00001
END
Format: 
RE[NAME] fid TO file_name 
Parameters: 
fid    specifies a CP-6 file identifier of an existing journal file. 
file_name    specifies the name to be assigned to the file that is replaced as 
the journal. 
Description: 
This command renames an existing journal file.  Renaming a journal file 
permits the original journal file name to remain open and available to receive 
items written to the journal by other users. 
Usage Note: 
The user requesting this command must have DELF access to the journal. 
00002
00001
00003
END
