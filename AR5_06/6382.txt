The ARCOM processor is the archive compactor.  Its function is to create new 
archive tapesets from old archive tapesets or old archive optical disksets, or 
create new optical disksets from old archive tapesets or old archive optical 
disksets.  While doing so, ARCOM skips all files on the old archive tapeset or 
optical diskset which are not currently in the archive system (files that have 
either been unarchived since the old archive tapeset or optical diskset was 
created, or files that have been modified and rearchived since they were 
previously archived). 
ARCOM is invoked directly from IBEX by the !ARCOM command. 
To obtain more HELP information, see 
HELP (ARCOM) TOPICS               Displays topics. 
?                                 Displays next level of 
                                  HELP messages. 
??                                Displays all levels of 
                                  HELP messages. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
DO
ARCOM modifies the EFT :ARCHIVE file to include a record of the controlled 
tapeset or optical diskset designated by the ARCOM COMPACT command for 
subsequent ARCHIVE operations. 
The PPRIV EFT privilege must be authorized via SUPER to enable the use of 
ARCOM by an individual user.  ARCOM runs with FMSEC turned on, which allows 
ARCOM to write on any tape, changing labels if necessary. 
Format 1 (Optical Diskset to Optical Diskset): 
CO[MPACT] [SEL[ECT]] DP#psn1 [,DP#psn2,...] 
    [FROM od_source] [(sopt_list)] [OMIT od_source] 
    TO CD#arcsn1 [(dopt_list)] 
Format 2 (Tapeset to Optical Diskset): 
CO[MPACT] [SEL[ECT]] DP#psn1 [,DP#psn2,...] 
   [FROM tape_source] [(sopt_list)] [OMIT tape_source] 
   TO CD#arcsn1 [(dopt_list)] 
Format 3 (Optical Diskset to Tapeset): 
CO[MPACT] [SEL[ECT]] DP#psn1 [,DP#psn2,...] 
    [FROM od_source] [(sopt_list)] [OMIT od_source] 
    TO CT#arcsn1 [,CT#arcsn2,...CT#arcsnN] [(dopt_list)] 
Parameters: 
psn    is a packset name. 
od_source    is an optical disk volume set specification of the form: 
    OD#odsn1[#odsn2...#odsn3] 
        or 
    CD#odsn 
        where odsn is a standard EFT-style controlled optical diskset 
        designation. 
arcsn1    is a standard EFT-style controlled tapeset or optical diskset 
designation.  Optionally, multiple output tapesets may be specified as arcsn2, 
arcsn3, etc.  Multiple output optical disksets may not be specified. 
tape_source    is a tape volume set specification of the form: 
    LT#tsn1[#tsn2...#tsnN] 
        where tsn is a tape serial number. 
        or 
    CT#ctsn 
        where ctsn is a standard EFT-style controlled tapeset designation. 
sopt_list    is one or more of the following separated by commas. 
    FSN = n    specifies a file sequence number (n), within the set of EFT 
    tapes or optical disk cartridges, at which to begin COMPACTing. 
    IO[ERROR] C[ONTINUE] {[=Y[ES]]|=N[O]}    specifies that processing should 
    continue after the occurrence of an irrecoverable tape read or write 
    error.  By default, when IOERROR CONTINUE is not specified, COMPACTing is 
    terminated.  Valid for Format 2 only. 
dopt_list    is one or more of the following separated by commas. 
    BLOCK = nn    specifies the maximum physical tape block size in pages 
    (4096 bytes each).  The maximum is 21.  The default is 4. 
    IO[ERROR] C[ONTINUE] {[=Y[ES]]|=N[O]}    specifies that processing should 
    continue after the occurrence of an irrecoverable tape read or write 
    error.  By default, when IOERROR CONTINUE is not specified, COMPACTing is 
    terminated.  Valid for Format 3 only. 
    IM[MEDIATE] [U[PDATE]]    specifies that all files should be listed and 
    their FITs updated for an EFT_RESTRICT_FILE (FSN) immediately after all 
    files contained within that FSN have been successfully copied to their 
    destination.  Only files that are entirely contained within a FSN are 
    considered.  A file that continues on the next FSN is updated when that 
    FSN is subsequently written.  By default, when IMMEDIATE UPDATE is not 
    specified, files are not listed and their FITs are not updated until after 
    all files have been COMPACTed to their destination. 
    VOLA[CCESS] = {N[ONE]|A[LL]|I[N]}    indicates labeled tape or optical 
    disk volume set access limitations. 
        NONE    specifies that only the owner of the volume set (account of 
        user creating first file on the volume set) will be allowed access to 
        this volume set. 
        ALL    specifies that all may read or write the volume set. 
        IN    specifies that all may read the volume set but only the owner 
        may write on it. 
        The system default is ALL. 
Description: 
Format 1 is used to create new archive optical disksets from old archive 
optical disksets.  Multiple output optical disksets may not be specified. 
Format 2 is used to create new archive optical disksets from old archive 
tapesets.  Multiple output optical disksets may not be specified. 
Format 3 is used to create new archive tapesets from old archive optical 
disksets.  Optionally, multiple output tapes may be specified. 
SELECT tells ARCOM that only the selected packsets are to be included in the 
new archive set.  The first packset specified will be made the new master 
packset. 
If SELECT is not specified, ARCOM will include all packsets from all archive 
sets that are identified as master packsets. 
FROM od_source or FROM tape-source tells ARCOM that only the selected optical 
disk or tape volumes contain files which are to be included on the new archive 
tapeset or optical diskset.  If FROM is not specified, ARCOM will include all 
tape or optical disk volumes on which disk files are archived. 
OMIT od_source or OMIT tape-source tells ARCOM that files on the specified 
optical disk or tape volumes are not to be included on the new archive optical 
diskset or tapeset. 
TO CD#arcsn1 tells ARCOM the optical diskset designation(s) of the new optical 
diskset. 
TO CT#arcsn1 [,CT#arcsn2,...,CT#arcsnN] tells ARCOM the controlled tapeset 
designation(s) of the new archive tapeset(s).  If multiple output tapes are 
specified, only the first two controlled tapesets will be remembered in EFT's 
:ARCHIVE file for subsequent ARCHIVE operations. 
00002
00001
Format: 
CO[MPACT] [SEL[ECT]] DP#psn1 [,DP#psn2,...] 
    [FROM tape_source] [(sopt_list)] [OMIT tape_source] 
    TO {CT#arcsn1 [,CT#arcsn2,...,CT#arcsnN]} [(dopt_list)] 
Parameters: 
psn    is a packset name. 
tape_source    is a tape volume set specification of the form: 
    LT#tsn1[#tsn2...#tsnN] 
        where tsn is a tape serial number. 
        or 
    CT#ctsn 
        where ctsn is a standard EFT-style controlled tapeset designation. 
sopt_list    is one or more of the following separated by commas. 
    DU[PLICATE] [T[APESET]]    indicates the source tape specified is a 
    duplicate archive tapeset.  The check to determine if the correct archive 
    tapeset has been specified for compacting files, by comparing with the 
    STOW tape in a file's FIT, is bypassed. 
    FSN = n    specifies a file sequence number (n) within the set of EFT 
    tapes at which to begin COMPACTing. 
    IO[ERROR] C[ONTINUE] {[=Y[ES]]|=N[O]}    specifies that processing should 
    continue after the occurrence of an irrecoverable tape read or write 
    error.  By default, when IOERROR CONTINUE is not specified, COMPACTing is 
    terminated. 
arcsn1    is a standard EFT-style controlled tapeset designation.  Optionally, 
multiple output tapesets may be specified as arcsn2, arcsn3, etc. 
dopt_list    is one or more of the following separated by commas. 
    BLOCK = nn    specifies the maximum pages in 3K increments (from 2 to 21) 
    to be used per call to the M$WRITE monitor service.  The default is 4K 
    words. 
    DEN[SITY] = {800|1600|6250}    specifies tape recording density. 
    EXP[IRE] = {ddd|NEV[ER]}    specifies the days remaining until expiration. 
    IM[MEDIATE] [U[PDATE]]    specifies that all files should be listed and 
    their FITs updated for an EFT_RESTRICT_FILE (FSN) immediately after all 
    files contained within that FSN have been successfully copied to their 
    destination.  Only files that are entirely contained within a FSN are 
    considered.  A file that continues on the next FSN is updated when that 
    FSN is subsequently written.  By default, when IMMEDIATE UPDATE is not 
    specified, files are not listed and their FITs are not updated until after 
    all files have been COMPACTed to their destination. 
    IO[ERROR] C[ONTINUE] {[=Y[ES]]|=N[O]}    specifies that processing should 
    continue after the occurrence of an irrecoverable tape read or write 
    error.  By default, when IOERROR CONTINUE is not specified, COMPACTing is 
    terminated. 
    VOLA[CCESS] = {N[ONE]|A[LL]|I[N]}    indicates labeled tape volume set 
    access limitations. 
        NONE    specifies that only the owner of the volume set (account of 
        user creating first file on the volume set) will be allowed access to 
        this volume set. 
        ALL    specifies that all may read or write the volume set. 
        IN    specifies that all may read the volume set but only the owner 
        may write on it. 
        The system default is ALL. 
Description: 
COMPACT is used to create new archive tapesets from old archive tapesets. 
Optionally, multiple output tapes may be specified. 
SELECT tells ARCOM that only the selected packsets are to be included in the 
new archive set.  The first packset specified will be made the new master 
packset. 
If SELECT is not specified, ARCOM will include all packsets from all archive 
sets that are identified as master packsets. 
FROM tape_source tells ARCOM that only the selected tape volumes contain files 
which are to be included on the new archive tapeset.  If FROM is not 
specified, ARCOM will include all tape volumes on which disk files are 
archived. 
OMIT tape_source tells ARCOM that files on the specified tape volumes are not 
to be included on the new archive tapeset. 
TO CT#arcsn1 [,CT#arcsn2,...,CT#arcsnN] tells ARCOM the controlled tapeset 
designation(s) of the new archive tapeset(s).  If multiple output tapes are 
specified, only the first two controlled tapesets will be remembered in EFT's 
:ARCHIVE file for subsequent ARCHIVE operations. 
00002
00001
Format: 
{DATE|TIME} 
Description: 
DATE (and its synonym TIME) displays the current date and time.  The format of 
the display is: 
mmm dd 'yy hh:mm (month)(day)(year)(hours)(minutes) 
Examples: 
*DATE 
requests a display of the current data and time.  A sample display is: 
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
    terminate the current processor session unless preceded by at least one 
    blank, or by a double ! (!!). 
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
The END command (and its synonyms EXIT and QUIT) exits the ARCOM processor. 
00001
END
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
C 
  COMPACT Command (Optical Diskset) - 
      HELP COMPACT_OPTDISK 
  COMPACT Command (Tapeset) - 
      HELP COMPACT_TAPESET 
  Continuation after Tape I/O Error - 
      HELP TAPE_IO_ERROR 
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
  ENTER Command - 
      HELP ENTER 
  ERASE Command - 
      HELP ERASE 
  exclamation point (!) - 
      HELP DO DESCRIPTION: 
F 
  Files Created by ARCOM - 
      HELP ARCOM_FILES 
  FROM - 
      HELP COMPACT_TAPESET DESCRIPTION: 
      HELP COMPACT_OPTDISK DESCRIPTION: 
I 
  IBEX command - 
      HELP DO DESCRIPTION: 
L 
  LDEV command - 
      HELP ERASE PARAMETERS: 
O 
  OMIT - 
      HELP COMPACT_TAPESET DESCRIPTION: 
      HELP COMPACT_OPTDISK DESCRIPTION: 
  optical diskset options -   
    BLOCK - 
      HELP COMPACT_TAPESET PARAMETERS: 
      HELP COMPACT_OPTDISK PARAMETERS: 
    VOLACCESS - 
      HELP COMPACT_TAPESET PARAMETERS: 
      HELP COMPACT_OPTDISK PARAMETERS: 
  OUTPUT Command - 
      HELP OUTPUT 
P 
  PRINT Command - 
      HELP PRINT 
  Privileges for Use of ARCOM - 
      HELP ARCOM_PRIVS 
R 
  RESET option - 
      HELP DIRECTORY PARAMETERS: 
S 
  SELECT - 
      HELP COMPACT_TAPESET DESCRIPTION: 
      HELP COMPACT_OPTDISK DESCRIPTION: 
  SYSLIB account - 
      HELP DIRECTORY EXAMPLES: 
T 
  tapeset options -   
    DENSITY - 
      HELP COMPACT_TAPESET PARAMETERS: 
    EXPIRE - 
      HELP COMPACT_TAPESET PARAMETERS: 
  TO CT# - 
      HELP COMPACT_OPTDISK DESCRIPTION: 
U 
  UTIL packset - 
      HELP DIRECTORY EXAMPLES: 
Y 
  Y account - 
      HELP DIRECTORY EXAMPLES: 
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
HELP_INDEX
Format: 
         [[OVER] LP[@location]] 
OUT[PUT] [[INTO] fid          ] [(option [,option]...[)]] 
         [[ON  ] ME           ] 
         [[TO  ]              ] 
Parameters: 
fid    any valid CP-6 file identifier. 
ON or TO    indicates to only honor the OUTPUT command if the file does not 
already exist. 
OVER    indicates to honor the OUTPUT command whether or not the file exists. 
INTO    indicates to merge the result of the OUTPUT command into the file if 
it exists, or to create a new one if it does not. 
LP    directs output to the default line printer; @location specifies a line 
printer. 
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
The OUTPUT command is used to direct all processor output to a destination. 
OUTPUT with no options redirects output to the original output destination. 
Output can be directed to any valid file name (fid).  If none of ON, TO, OVER, 
or INTO is specified, ON will be assumed. 
00002
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
00002
00003
00001
ARCOM_PRIVS
END
The ARCOM option IOERROR CONTINUE = YES must be used to enable ARCOM to 
continue after irrecoverable tape read or write errors.  By definition, read 
errors include E$IOERR, E$BLNKTP, and E$NOTANS errors. 
When an irrecoverable tape read error occurs, reading continues from the 
current volume depending whether or not data exists beyond where the error is 
encountered.  If data exists, ARCOM continues by skipping over the bad part of 
the tape, reading the next good block, and searching for the beginning of the 
next file.  If data does not exist, ARCOM rolls over to the next volume of the 
tapeset.  The output listing reflects the name of the file(s) that could not 
be completely copied, followed by an error message stating that a number of 
files may have been skipped. 
When an irrecoverable write error occurs, the operator is informed that ARCOM 
is having difficulty writing to tape and is queried whether to abort or to 
continue writing to the next volume of the tapeset.  If the operator elects to 
abort, the message "Job aborted by operator" is written to the output listing. 
If the operator elects to continue, ARCOM rolls over to the next volume of the 
tapeset.  If data already exists in the current EFT_RESTRICT_FILE on tape, the 
last block of the EFT_RESTRICT_FILE is read and written to the next volume. 
This is performed to enable ARCOM to write an EFT_CVOL_FILE to an error-free 
portion of the tape.  The following error message is output to the output 
listing to reflect this activity:  "Due to the preceding error, filename.acct 
was rewritten to LT#tsn".  The FITs of the rewritten files are updated to 
reflect the new file sequence and serial numbers.  If a write error occurs at 
the beginning of tape, the previous tape is mounted (if one exists) and the 
EFT_CVOL_FILE is rewritten.  The operation continues after requesting a 
replacement tape. 
DATE
END
