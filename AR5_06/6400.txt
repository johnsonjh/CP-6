Format: 
Form 1: 
FEPLINK [ou_fid [, ou_fid] ... [{ON|OVER} ru_fid]] [(opt[,opt] ... )] 
Form 2: 
FEPLINK l_fid 
Parameters: 
ou_fid    specifies a CP-6 file identifier of an object unit to be linked. 
ru_fid    specifies the CP-6 file identifier of the run unit to be created. 
opt    specifies any of the FEPLINK options.  Type HELP (FEPLINK) OPTIONS for 
a list of these options. 
l_fid    specifies a CP-6 file identifier that contains a Form 2 FEPLINK 
command. 
Description: 
This command links the specified object units to create a run unit which is 
stored as a CP-6 file.  This command may be invoked at the IBEX level or after 
invoking FEPLINK by entering !FEPLINK.  To display more information about 
FEPLINK, type: 
HELP (FEPLINK) OPTIONS 
HELP (FEPLINK) FEPMAP 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
FEPLINK is a 2-pass linker designed to link 16-bit object units to produce a 
run unit that can execute in a Front-end Processor. 
The FEPLINK processor is invoked at the command processor level via the 
!FEPLINK command.  The mapping feature of FEPLINK can be invoked separately 
via the !FEPMAP command, also entered at the command processor level. 
  Option         Description 
  FEPLINK 
                 Links object units to create a FEP run unit. 
  FEPMAP 
                 Creates map for a FEP run unit. 
00001
00002
Format: 
FEPMAP ru_fid [(mopt [, mopt] ... )] 
Parameters: 
ru_fid    specifies the file identifier that contains the run unit to be 
mapped. 
mopt    specifies any map options as defined for the MAP option of the FEPLINK 
command (enter HELP (FEPLINK) OPTIONS MAP). 
Description: 
This command creates a map for an existing FEP run unit.  This command may be 
entered at the IBEX level or after invoking FEPLINK. 
00002
00001
A 
  accounting surcharge option - 
      HELP OPTIONS SURCHARGE 
B 
  big AUTO segment option, FEPLINK - 
      HELP OPTIONS LAUTO 
D 
  data patch space option - 
      HELP OPTIONS DPATCH_ 
F 
  FEP run unit - 
      HELP CONCEPTS 
  FEPLINK -   
    FEPLINK Command - 
      HELP INVOKING_FEPLINK FORMAT: 
    FEPMAP Command - 
      HELP FEPMAP FORMAT: 
  FEPLINK Options - 
      HELP OPTIONS 
  FEPLINK Processor - 
      HELP CONCEPTS 
I 
  instruction patch space option - 
      HELP OPTIONS IPATCH_ 
  Invoking FEPLINK - 
      HELP INVOKING_FEPLINK 
  Invoking FEPMAP - 
      HELP FEPMAP 
L 
  LAUTO option, FEPLINK - 
      HELP OPTIONS LAUTO 
  linker - 
      HELP CONCEPTS 
  lock linker option - 
      HELP OPTIONS SLOCK 
      HELP OPTIONS WLOCK 
P 
  privileges option - 
      HELP OPTIONS PRIVILEGES 
  processor accounting option - 
      HELP OPTIONS PROCACC 
  pseudo resource option - 
      HELP OPTIONS PSEUDO 
S 
  shared library option - 
      HELP OPTIONS SHARELIB 
00001
00002
00003
00004
00005
00006
00007
HELP_INDEX

Enter ? or ?? to display FEPLINK options.  To obtain HELP messages about 
individual options, type:  HELP (FEPLINK) OPTIONS option 
For a list of option names, enter HELP (FEPLINK) OPTIONS TOPICS 
The options are displayed in the following format: 
  Option               Meaning 
  B[IAS] {= hhhhh|[=] (hhhhh)} 
                       Specifies the absolute address (hexadecimal 0-FFFFF) of 
                       the first word which FEPLINK is to allocate.  If the 
                       BIAS option is not specified, the first word allocated 
                       is at location 10000. 
  DC[BSLOTS]=value 
                       Specifies a decimal value that specifies how many spare 
                       slots are to be reserved in the DCB pointer list so 
                       that DCBs can be added dynamically during program 
                       execution. 
  DE[BUGGER] 
                       Specifies that the formed run-unit is a debugger. 
  DP[ATCH] {= n|[=] (n)} 
                       Specifies the number (0-65535) of words of data patch 
                       space to allocate in the target run unit.  If DPATCH is 
                       not specified, no data patch space is allocated. 
  IP[ATCH] {= n|[=] (n)} 
                       Specifies the number (0-65535) of words of instruction 
                       patch space to allocate in the target run unit.  If 
                       IPATCH is not specified, no instruction patch space is 
                       allocated. 
  LA[UTO] 
                       Specifies that the program is to run with AUTO in small 
                       segments instead of .A0000.  This option allows use of 
                       the big AUTO segment at .A0000 as a normal data 
                       segment.  Programs that need more than 12K AUTO should 
                       not use this option. 
  L[IST] 
                       Displays a list of object units included in the run 
                       unit. 
  M[AP] {= mopt|[=] (mopt [, mopt] ... )} 
                       Requests a map of the newly created run unit.  The 
                       following can be specified as map options (mopt): 
                           N[AME]    Sort external symbols by name. 
                           V[ALUE]    Sort external symbols by value. 
                           U[DEF]    Include unused external symbols. 
                           E[MPTY]    Include empty control sections. 
                       At least one of NAME or VALUE must be specified in 
                       order to produce a map of external symbols.  If neither 
                       NAME nor VALUE is specified, only a protection type 
                       summary and control section map are produced. 
  NOC[HGPMEM] 
                       Specifies that if the run-unit resides in :SYS, then 
                       procedure pages will not be charged for regardless of 
                       whether the program is shared or not. 
  NOE[DITING] 
                       Suppresses the inclusion of most of the system 
                       information in the run unit, including the read-only 
                       segment, the association of shared libraries, the 
                       FEPLINK defined pointers (G$JIT$, G$TCB$, G$ROS$), the 
                       debugger work area, and the user fault location.  This 
                       option will not generate a usable FEP run-unit. 
  NOD[EBUG] 
                       Inhibits inclusion of debug schema in the target run 
                       unit. 
  NOSHAREL[IB] 
                       Inhibits the automatic association of any shared 
                       library. 
  PRI[VILEGES](priv[,priv]...) 
                       Specifies the special privileges that are to be 
                       associated with the run unit.  These privileges are 
                       effective only if the run unit resides in the :SYS 
                       account.  The privileges are: 
                       CQ    allows the user to use the Circular Queue. 
                       EXMM    allows the user to utilize a set of EXtended 
                       Memory Management services.  M$CVM (read/write access) 
                       is the only one available to date. 
                       EXPM    allows the user to start and stop the monitor 
                       performance monitor. 
                       GPP    allows a user to override the stealable page 
                       limit and acquire physical memory pages. 
                       INTCON    allows the user to use the M$INTCON monitor 
                       service. 
                       MAXMEM   allows the user to allocate memory beyond his 
                       authorized limit. 
                       MSYS    allows the user to use the M$SYS monitor 
                       service and to execute his interrupt processing 
                       routines in Ring 1. 
                       SCREECH    allows the user to use M$SCREECH to dump and 
                       reboot the Front End. 
                       SPCLMM    allows the user to utilize a set of SPeCiaL 
                       Memory Management services.  M$CVM (read only access) 
                       is the only one available to date. 
                       SYSLOG    allows the user to use the M$WRSYSLOG monitor 
                       service request. 
                       TND    allows the user to use the Test aNd Diagnostic 
                       monitor services. 
  PR[OCACC] 
                       Specifies that if the run-unit resides in :SYS, 
                       processor accounting, rather than user accounting, is 
                       to be in effect when this run-unit is put into 
                       execution. 
  PSEUDO=(resnm[,decimal_number]) 
                       Specifies a pseudo resource to be associated with a 
                       run-unit, thereby limiting the number of users of a 
                       specific processor, 
                       resnm    is the name of a pseudo resource; it may be 
                       from 1 to 8 characters. 
                       decimal_number    is the number (1-511) of resnm 
                       required; the default is 1. 
  SE[VERITY] {= n|[=] (n)} 
                       Sets the maximum severity level (0-15) which FEPLINK is 
                       to tolerate.  The default is 4. 
                       Severity levels may be passed to FEPLINK by the 
                       language processor by setting a field in the head 
                       record of an object unit.  The linker assigns severity 
                       levels to certain FEPLINK detected errors as follows: 
                         ERROR                                SEVERITY 
                         -----                                -------- 
                         Unresolved secondary entry or            0 
                         data references 
                         Unresolved primary entry or data         7 
                         references 
                         Multiply defined symbols                 4 
                         Object language errors                  16 
                         Source language errors               severity set 
                                                              by language 
                                                              processor 
                       Because the maximum legal severity level is 15, object 
                       language errors cannot be suppressed; instead they 
                       cause the link to be unconditionally aborted.  If the 
                       final severity level of the run unit is greater than 
                       the maximum severity level specified, the run unit is 
                       not created.  If an old run unit is to be replaced and 
                       the final severity is greater than the maximum severity 
                       level specified, the old run unit is not replaced. 
  {SHAREA[BLE]|NSHAREA[BLE]} 
                       Specifies if the run unit is shareable or not. 
                       SHAREABLE is the default. 
  SHAREL[IB]=libfid 
                       Specifies the name of the shared library to be 
                       associated with the run unit.  Libfid can be any file 
                       (the account defaults to :SYS if not specified).  The 
                       SHARELIB option inhibits any default shared library 
                       association established within any object files. 
  SL[IB] 
                       Specifies that the formed run unit is a shared library. 
  SLOCK(lock[,lock]...) 
                       Specifies a strong series of 'locks' or access controls 
                       to the run unit.  A lock is a decimal integer from 1 to 
                       72.  Each user has a set of keys as established by the 
                       system manager.  SLOCK specifies that the user must 
                       have all the keys to access the run unit.  Also see 
                       WLOCK.  Only one of SLOCK or WLOCK may be specified. 
  SR[CH](ac1 [,ac2]...) 
                       Specifies the accounts the Linker can access when 
                       searching for an object unit file.  If the SRCH option 
                       is specified and a file is encountered in the link 
                       command that does not contain an account, then the 
                       linker will search for the file in the accounts given 
                       in the SRCH option.  The search is performed in the 
                       order specified on the SRCH option, from left to right. 
  STA[RT] {= hhhhh|[=] (hhhhh)} 
                       Overrides any default start address (hexadecimal 
                       0-FFFFF) passed in an object unit. 
  SUR[CHARGE] 
                       Specifies that, if the run-unit resides in the :SYS 
                       account, a processor accounting record will be written 
                       to :ACCTLG when the run-unit is terminated. 
  TC[B]=value 
                       Specifies, in decimal, the maximum number if 
                       environments that may be stacked on the Task Control 
                       Block.  The default is 0. 
  V[ECTOR](option[,option]...) 
                       Specifies that a transfer vector be generated for a 
                       shared library. 
                       The VECTOR option causes the values of entry 
                       definitions to be changed.  A map produced at link time 
                       will reflect the values before change.  A map produced 
                       subsequently will reflect the values after change. 
                       The options are: 
                       RF=file    specifies that the transfer vector in the 
                       specified run unit file should be used. 
                       E[NTRIES](entry,[,entry]...)    specifies entries in 
                       the transfer vector, where entry may be: 
                           an ENTDEF name 
                           a range of ENTDEF names e.g., A - Z, 
                           (note that the hyphen must be 
                           enclosed by blanks) 
                           EMPTY=decimal, where decimal is the 
                           number of empty slots to reserve 
                           in the transfer vector. 
                       REMOVE_E[NTDEF]    specifies that the linker should 
                       remove all ENTDEF's from the run unit that are not 
                       included in the transfer vector. 
                       REMOVE_S[YMDEF]    specifies that the linker should 
                       remove all SYMDEF's from the run unit. 
  VER[SION]{=version|(version)} 
                       Specifies version to be displayed on map generated, 
                       where version may be 1 to 6 characters. 
  WLOCK(lock[,lock]...) 
                       Specifies a weak series of 'locks' or access controls 
                       to the run unit.  A lock is a decimal integer from 1 to 
                       72.  Each user has a set of keys as established by the 
                       system manager.  WLOCK specifies that the user needs 
                       only any one of the keys to access the run unit.  Also 
                       see SLOCK.  Only one of SLOCK or WLOCK may be 
                       specified. 
00001
00002
00003
00004
00005
00006
00007
00008
00009
00011
00010
00012
00017
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
