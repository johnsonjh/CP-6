The SPIDER (Shared Processor Install, Delete and Replace) routine is a 
maintenance tool for permanently-shared (permanently memory-resident) 
processors and shared libraries. 
To obtain more HELP information, see: 
HELP (SPIDER) TOPICS              Displays available topics. 
HELP (SPIDER) COMMANDS            Displays a list of SPIDER 
                                  commands. 
HELP (SPIDER) command PARAM       Displays parameters associated 
                                  with a particular command. 
HELP (SPIDER) command DESC        Displays description associated 
                                  with a particular command. 
?                                 Displays next level of HELP 
                                  messages. 
??                                Displays all levels of HELP 
                                  messages. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
A list of SPIDER commands and their definitions can be accessed by typing a ? 
or a ??.  To obtain definitions of individual commands, type 
HELP (SPIDER) COMMANDS command 
where command is any of the following: 
DELETE, END, HELP, INSTALL, LIST, QUIT, REPLACE. 
  Command        Description 
  DELETE 
                 Removes a processor entry from processor tables. 
  {END|QUIT} 
                 Terminates SPIDER. 
  HELP 
                 Lists information about the SPIDER commands. 
  INSTALL 
                 Installs a new shared processor. 
  LIST 
                 Lists a subset of attributes of specified processors. 
  REPLACE 
                 Replaces an indicated processor with a specified run unit. 
00001
00002
00003
00004
00005
00002
00006
Format: 
D[ELETE] procname[, PERM] 
Parameters: 
procname    is the name of the processor to be deleted. 
PERM    deletes corresponding file from :SYS. 
Description: 
The DELETE command removes the processor entry from processor tables.  The 
corresponding run unit is deleted from :SYS if PERM is specified.  This 
prevents further user association with the processor.  Users associated with 
the processor at the time this command is issued will continue to have use of 
it until they disassociate.  If there are no users currently associated with 
the processor, the pages will be released. 
00002
00001
Format: 
{E[ND]|Q[UIT]} 
Description: 
The END or QUIT command terminates SPIDER. 
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
  DELETE Command - 
      HELP DELETE 
  DELETE Command (SPIDER) - 
      HELP DELETE FORMAT: 
E 
  END Command - 
      HELP END 
H 
  HELP Command - 
      HELP HELP 
I 
  INSTALL Command - 
      HELP INSTALL 
  INSTALL Command (SPIDER) - 
      HELP INSTALL FORMAT: 
  Invoking SPIDER - 
      HELP INVOKING_SPIDER 
L 
  LIST Command - 
      HELP LIST 
  LIST Command (SPIDER) - 
      HELP LIST FORMAT: 
P 
  Privileges for Use of SPIDER - 
      HELP PRIVILEGES 
  processor in :SYS - 
      HELP END DESCRIPTION: 
      HELP REPLACE PARAMETERS: 
R 
  REPLACE Command - 
      HELP REPLACE 
  REPLAY -   
    HELP Command - 
      HELP HELP FORMAT: 
S 
  SPIDER -   
    DELETE - 
      HELP DELETE FORMAT: 
    END - 
      HELP END FORMAT: 
    INSTALL - 
      HELP INSTALL FORMAT: 
    LIST - 
      HELP LIST FORMAT: 
    REPLACE - 
      HELP REPLACE FORMAT: 
00001
00002
00003
00004
00005
00006
00007
HELP_INDEX
Format: 
I[NSTALL] procname, {ASL|CP|DB|LIB} FROM fid 
Parameters: 
procname    is the name assigned to the new shared processor. 
ASL   for alternate shared library 
CP    for command processor 
DB    for debugger 
LIB   for shared library 
fid    is the file identification of the run unit from which the processor is 
taken. 
Description: 
The INSTALL command is used to install a new shared processor which did not 
previously exist on the system. 
Note:  The run unit is automatically copied into the :SYS account if it is not 
already there, and the user can copy files into :SYS, via the FMSEC privilege 
or WRITE access to :SYS. 
00002
00001
SPIDER may be run as a batch or on-line job.  It is invoked by the command 
!SPIDER.  The DCBs used by SPIDER are: 
o   M$SI for input 
o   M$LO for output 
When run as an on-line job, SPIDER solicits commands with the > character. 
Format: 
L[IST] [procname|*A[UTO]] 
Parameters: 
procname    specifies the name of the processor to be listed. 
*AUTO    specifies that all automatically shared processors and their overlays 
be listed. 
If no parameter is specified, all processors will be listed. 
Description: 
The LIST command lists a subset of the attributes of the specified processor, 
or of all automatically shared processors, or of all processors currently in 
the system. 
00002
00001
Use of SPIDER requires that the users be authorized for the SPIDERD processor 
privileges in order to use the LIST command, and for the SPIDERC privilege if 
the INSTALL, DELETE, or REPLACE commands are to be used.  These privileges are 
authorized by the SUPER processor (see HELP (SUPER)).  The user must also have 
write access to any processors in :SYS which are to be modified. 
END
Format: 
R[EPLACE] procname WITH fid[,PERM] 
Parameters: 
procname    is the name of the processor to be replaced. 
fid    is the file identification of the run unit that will replace the 
specified processor, copying it into the :SYS account if PERM is specified. 
PERM    specifies that the processor is to be copied to the :SYS account. 
Empty slots must be available in the processor tables.  In the case of an 
alternate shared library, debugger, or command processor, the only means of 
guaranteeing that the latest version is available after a system crash is to 
specify the processor name in the TIGER SPROC command.  In the case of a 
permanently-shared processor, that is not specified in the TIGER SPROC 
command, the processor will be a candidate for auto-sharing but not 
permanently memory-resident after a system crash. 
Description: 
The REPLACE command is used to replace the indicated processor with the run 
unit specified by 'fid'.  It is copied into the :SYS account if the PERM 
parameter is entered.  When REPLACE is used, new users get only the new 
processor version; users associated with the old version continue to use the 
old copy until they become disassociated from the processor.  Processor type 
is preserved; processor privileges are set to those of the new run unit. 
00002
00001
