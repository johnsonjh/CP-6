The Efficient File Transfer (EFT) processor provides flexible file maintenance 
safeguards to prevent the loss of data due to natural disasters, hardware 
malfunctions and human error.  In addition to providing protection from loss 
of data, EFT provides the capability for transferring files by account or 
accounts from one system to another.  To display information about EFT, type 
any of the following\ 
HELP (EFT) COMMANDS         For a list of commands by category 
HELP (EFT) command          For the format of a specific command. 
                            Then type ? or ?? for more. 
HELP (EFT) command PARAM    For only parameter information on a 
                            specific command. 
HELP (EFT) command DESC     For only the description of a 
                            specific command. 
HELP (EFT) TOPICS           For a list of all EFT HELP topics. 
HELP (EFT) COMMAND_SUMMARY  For a brief description of commands. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
DO
Format: 
ADD DP#psn [TO] [ARC[HIVE]] FOR DP#mpsn 
Parameters: 
psn    specifies the new packset to be added to the existing group of 
packsets. 
mpsn    specifies the master of the packset group. 
Description: 
For archiving purposes, the ADD command adds a new packset to an existing 
group of packsets.  EFT creates (or modifies) the :ARCHIVE file on the new 
packset.  EFT updates the :ARCHIVE file as new packsets are added. 
Usage Notes: 
1.  The master of the set (mpsn) must be mounted whenever an ARCHIVE operation 
    is performed for any of the member packsets. 
2.  A packset cannot be a member of more than one archive set. 
Example: 
ADD DP#LJF TO ARCHIVE FOR DP#MEFTY 
00002
00004
00001
00003
Format: 
ARC[HIVE] [FOR DP[nn]#psn1[, DP[nn]#psn2] ... ] [(topt_list)] 
Parameters: 
nn    is a 2-digit, user-defined disk resource identifier. 
psn1,psn2    specify the packsets to be searched. 
topt_list    specifies a list of options describing how the ARCHIVE is to be 
performed.  (topt_list) is of the form (option1[,option2]...) where option can 
be any of the following: 
    CHECK    specifies automatic tape checking for the archive tape.  By 
    default, tape checking is performed depending on whether it was specified 
    on the ESTABLISH command. 
    IOERROR CONTINUE    specifies that processing should continue after the 
    occurrence of an irrecoverable tape write error.  By default, continuation 
    is performed according to the setting established via the ESTABLISH 
    command. 
    See TAPE_OPS, for a complete description of these options. 
Description: 
The ARCHIVE command causes a search for files to be STOWed and appends a copy 
of those files to the proper archive tapeset.  The archive operation applies 
to the specified packsets, or to all packsets if no packsets are specified. 
Usage Note: 
The master of the set (mpsn) must be mounted whenever an ARCHIVE operation is 
performed for any of the member packsets. 
Example: 
*ARCHIVE FOR DP#EFTY 
stores files from DP#EFTY that are queued for stow and displays a formatted 
listing of packsets and accounts, and the files written to the archive 
tapeset. 
00002
00004
00001
00003
The CP-6 archive compactor (ARCOM) enables the user to "compress" archive data 
by eliminating superseded or unwanted files.  Enter: HELP (ARCOM) for details. 
Format: 
BAC[KUP] DP[nn]#psn1[,DP[nn]#psn2] ... [(sopt_list)]  [/(sel_list) ] 
    {OVER  } {CT#nnnn0  [,CT#nnnn0] } 
    {EXTEND} {CT#nnnn00 [,CT#nnnn00]} [(topt_list) ] 
             {LT#tsn1[#tsn2] ... } 
Parameters: 
nn    is a 2-digit, user-defined disk resource identifier. 
psn1,psn2    specify the packsets to be backed up. 
sopt_list    specifies source options describing how the BACKUP is to be 
performed.  (sopt_list) is of the form (so[,so]...) where options can be any 
of the following: 
    ACUP 
    IDS 
    CLEANUP    This option is the default if there is no dual packset. 
    SHARED 
See SOURCE_OPS for complete descriptions. 
sel_list    specifies criteria for file selection when a subset of files on a 
packset is to be backed up.  sel_list is in the form [/(ss[, ss] ... )].  See 
SEL_OPS for format. 
{CT#nnnn0  [,CT#nnnn0 ]} 
{CT#nnnn00 [,CT#nnnn00]}    specifies the controlled tapeset to receive the 
saved files.  Insert CONTROLLED_TAPESETS for additional information.  If two 
tapesets are specified, a duplicate tapeset is created. 
{LT#tsn1[#tsn2] ... }    specifies a labeled tapeset in which the user assumes 
complete responsibility for assignment of volume numbers (e.g., #tsn1#tsn2). 
topt_list    specifies options pertaining to storage of the backup files on 
tape.  (topt_list) is of the form (op[,op]...) where op can be any of the 
following: 
    BLOCK 
    CHECK 
    DENSITY 
    EXPIRE 
    EXTEND 
    IOERROR CONTINUE 
    VOLACCESS 
    VOLUME 
See TAPE_OPS for complete descriptions. 
Description: 
The BACKUP command creates a tape copy of qualified files and deleted files on 
the specified packsets since the last SAVE, DUAL, or BACKUP operation. 
Current packset attributes, account attributes, and deleted accounts are 
always written to the tape.  Each time BACKUP is requested, the data written 
to tape is considered an increment.  BACKUP creates a new tapeset if OVER is 
specified or extends an existing tapeset if EXTEND is specified. 
Note:  Packset attributes, account attributes and deleted accounts are always 
written to tape and are not considered an increment. 
When RESTORE is used later, a specified occurrence of a file can be referenced 
by identifying the backup increment. 
BACKUP writes changes to tape according to the selection criteria, using the 
same criteria as SAVE with respect to account eligibility.  If select options 
(sel_list) are omitted, qualified files from the complete packset are written 
to tape.  If select options included range specifications, only those files 
are backed up. 
For each file copied to tape, the file is closed with modification to the 
extended attributes specifying the time and date of the backup, and the serial 
number of the tape to which it was copied. 
00002
00001
Format 1: 
CAT[ALOG] {OVER|INTO|TO|ON|ONTO|IS} fid 
Format 2: 
CAT[ALOG] OFF 
Parameters: 
OVER    indicates that a new catalog file is to be created, replacing any old 
catalog file with the same name. 
INTO    indicates that new cataloging information is to replace old cataloging 
information in the specified file. 
ON or TO    indicates that a new catalog file is to be created only if an old 
catalog file of the same name does not already exist. 
ONTO    indicates that new cataloging information is to be included with old 
cataloging information in the specified file. 
IS    indicates that the catalog file is to be opened for input only for use 
with the EFT WHERE command. 
fid    identifies a catalog file on disk to which (or from which) cataloging 
information is to be written (or read). 
Description: 
Format 1 of the CATALOG command specifies an EFT catalog file and requests 
cataloging be performed during EFT operations (e.g., SAVE, BACKUP, ARCHIVE). 
Format 2 turns off cataloging. 
Usage Notes: 
1.  A catalog file may be created during a tape check operation by specifying 
    a CATALOG command before a CHECK command. 
2.  Cataloging generally is used with SAVE, BACKUP, ARCHIVE, or PURGE 
    operations. 
3.  The EFT catalog file can be interrogated by the WHERE command. 
Related Commands: 
ARCHIVE, BACKUP, CHECK, PURGE, SAVE 
00002
00001
00004
00003
Format: 
        [{CT#nnnn0           }] 
CHE[CK] [{CT#nnnn00          }] [(sopt_list)] 
        [{LT#tsn1[#tsn2] ... }] 
Parameters: 
{CT#nnnn0           } 
{CT#nnnn00          } 
{LT#tsn1[#tsn2] ... }    specifies an EFT tapeset.  Insert CONTROLLED_TAPESETS 
for additional information. 
sopt_list    specifies the source option pertaining to the specified tapeset. 
sopt_list is of the form so[, so] ... where so can be any of the following: 
    DENSITY 
    FSN 
    IOERROR CONTINUE 
    VOLUME 
See SOURCE_OPS and TAPE_OPS 
for complete descriptions. 
Description: 
The CHECK command reports the contents of a tapeset generated by EFT, and 
verifies the readability of the tape. 
Note:  It is important that every tape be CHECKed (by means of either the 
CHECK command or the EFT CHECK option) before it is assumed to be valid.  If a 
tape is found to be improperly recorded, the REQUALIFY command can be used to 
allow the just-performed operation to be re-performed without losing any data. 
Usage Note: 
Note that EFT leaves the last tape it just SAVEd/BACKedUP/ARCHIVEd on the tape 
drive for any subsequent operation.  If a check of the tape is made right 
after the SAVE/BACKUP/ARCHIVE operation, be aware that one of the tape drives 
is already taken. 
00002
00001
00003
Format: 
        {CD#nnnn0             } 
CH[ECK] {CD#nnnn00            } [(odopt_list)] 
        {OD#odsn1[#odsn2] ... } 
Parameters: 
{CD#nnnn0             } 
{CD#nnnn00            } 
{OD#odsn1[#odsn2] ... }  specifies an EFT optical diskset. 
CD#nnnn0[0]    specifies a five or six digit controlled optical diskset number 
ending in 0 through 99. 
OD#odsn    specifies an optical diskset. 
odopt_list    specifies options pertaining to storage of files on optical 
disk.  (odopt_list) is of the form (option1[,option2]...)  where option is any 
of the following: 
    FSN 
    VOLUME 
See Table 6-10, EFT Optical Diskset Options, for descriptions of these 
options. 
Description: 
The CHECK command reports the contents of a diskset generated by EFT and 
verifies the readability of the optical disk (see OPT_DISK_OPS). 
00002
00001
Format: 
CLO[SE] [(REM[OVE])] 
Description: 
The CLOSE command, which is used in conjunction with an OPEN command, returns 
to the normal mode of EFT and causes the * prompt to be displayed.  (REMOVE) 
requests the tapeset to be dismounted, but does not release the tape drive; 
this allows the user to enter another OPEN command for another 
transport/transfer operation, if desired. 
00001
EFT commands can be categorized as follows: 
Cataloging commands                 CATALOG, WHERE 
Disk to disk save commands:         DUAL ALL, DUAL INCREMENTAL 
Disk to tape save commands:         SAVE, BACKUP 
File or account recovery command:   RESTORE 
Maintenance/                        STATUS, SCAN, CHECK, VALIDATE, 
Miscellaneous commands:             REQUALIFY, MOUNT, END, EXIT, QUIT, HELP, 
                                    DATE, TIME, DIRECTORY, DO, ENTER, ERASE, 
                                    ERROR, OUTPUT, PRINT, REWIND 
Packset purging command:            PURGE 
Packset recovery command:           REBUILD 
System manager archiving commands:  ESTABLISH, ARCHIVE, RETRIEVE, 
                                    ADD, REMOVE 
System to system transport/ 
packset transfer commands:          OPEN, CLOSE 
User archiving commands:            STOW, UNSTOW, FETCH, UNFETCH, 
                                    UNARCHIVE, MODIFY 
Enter: HELP (EFT) COMMAND_SUMMARY for a brief description of 
each command. 
  Command            Description 
ADD                Adds a new packset to an existing group of 
                   packsets. 
ARCHIVE            Archives all files for which STOW is requested on 
                   the specified packset(s). 
BACKUP             Copies to tape the qualified files since the last 
                   SAVE, DUAL or BACKUP. 
CATALOG            Creates a catalog file, or updates an existing 
                   catalog file. 
CHECK              Verifies readability and reports the content of 
                   an EFT tapeset. 
CLOSE              Returns to EFT at the * prompt level after entry 
                   of transfer/transport subcommands. 
{DATE|TIME}        Displays the current time and date 
{DIRECTORY|DIR}    Changes the default account and packset. 
{DO|!}             Enables IBEX command execution. 
DUAL ALL           Copies a complete packset to a newly initialized 
                   packset. 
DUAL               Copies to dual packset the qualified files since the 
INCREMENTAL        last DUAL. 
{END|EXIT|QUIT}    Exits the EFT processor. 
ENTER              Invokes a CP-6 ADAPT dialog from within this 
                   processor. 
ERASE              Deletes accumulated output for logical devices. 
ERROR              Causes EFT to reprint the last error summary. 
ESTABLISH          Establishes tapeset for archiving of packsets. 
FETCH              Requests return of specified file(s) to disk from 
                   the archive tapeset. 
HELP               Displays information about commands. 
MODIFY             Modifies archive tapeset or its attributes. 
MOUNT              Directs the operator to mount a magnetic tape. 
OPEN               OPEN specifies transfer or transport media and 
                   functions; prompts with + for subcommands, i.e. 
                   the transfer/transport subcommands and CLOSE 
                   subcommand. 
OUTPUT             Directs output to a specified destination. 
PRINT              Directs that output accumulated for logical 
                   devices be sent to destinations immediately. 
PURGE              Deletes files from specified packset and writes 
                   purged files to tape. 
REBUILD            Reconstructs a complete packset, updates a dual 
                   packset, or reconstructs IDS files from multiple 
                   file increments from BACKUP (and possibly SAVE) 
                   tapesets. 
REMOVE             Removes the specified packset from an existing 
                   group of packsets, or removes a magnetic tape from 
                   a tape drive. 
REQUALIFY          Forces a replication of information previously 
                   written to an archive tape or backup tape. 
RESTORE            Restores specified files or accounts to disk from 
                   tape or dual disk. 
RETRIEVE           Retrieves all archived files for which FETCH is 
                   requested on the specified packset(s). 
REWIND             Rewinds a specified magnetic tape. 
SAVE               Copies eligible files to tape. 
SCAN               Scans a packset and reports the extended 
                   attributes of files meeting specified criteria. 
STATUS             Generates specified EFT reports from EFT control 
                   files. 
STOW               Requests to enter files into the archive system. 
UNARCHIVE          Removes specified files from archive records; 
                   once this is done, no record of the archive copy 
                   exists. 
UNFETCH            Rescinds previous FETCH request for specified 
                   files. 
UNSTOW             Rescinds a previous STOW request for specified 
                   files. 
VALIDATE           Validates a complete packset or specified files 
                   on a packset. 
WHERE              Retrieves information from a catalog file. 
Enter: HELP (EFT) command for information on a specific command. 
    EFT provides controlled tapesets in consecutive volumes identified by the 
    prefix CT followed by a serial number.  The controlled tapeset 
    specification CT#xxxxn begins with LT#xxxxn and ends with LT#xxxx9.  The 
    specification CT#xxxxnn begins with LT#xxxxnn and ends with LT#xxxx99. 
    For example, CT#ABCD5 means LT#ABCD5 through LT#ABCD9.  CT#ABCD84 means 
    LT#ABCD84 through LT#ABCD99. 
Format: 
{DATE|TIME} 
Description: 
DATE (and its synonym TIME) displays the current date and time.  The format 
for the display is: 
mmm dd 'yy hh:mm   (month)(day)(year)(hours)(minutes) 
Examples: 
*DATE 
requests a display of the current data and time.  A sample display is: 
AUG 10  '88  11:03 
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
DUAL_INCREMENTAL
Format: 
DUAL A[LL] DP[nn]#psn [(sopt_list)] [/(sel_list)] OVER DP[nn]#vsn 
Parameters: 
nn    is a 2-digit, user-defined disk resource identifier. 
psn    specifies the source packset. 
vsn    specifies the volume serial number of the destination packset for which 
PIG SCRATCH and BUILD have been performed.  Note that this packset has the 
same name as the source packset, but is identified in the EFT command by its 
volume serial number (and it has been AVR'ed after the source packset). 
sopt_list    specifies source options, and is of the form (so[, so] ... ) 
where so can be any of the following: 
    CLE[ANUP]    specifies removal of deleted files and accounts from the 
    included file directories.  This option is the default if there are no 
    BACKUP or SAVE tapes (indicated by the lack of a :BACKUP.$$EFT control 
    file). 
    SWI[TCH] [IF ERR[ORS]] < nn    specifies that the destination packset is 
    to become the prime and the source packset is to become the dual following 
    the copy of the source to the destination if the number of bad file errors 
    is less than nn. 
These are the only source options that can be used in a DUAL ALL command. 
sel_list    specifies the accounts to be skipped and consists of SKI[P] 
(fid_specifier).  See Table 6-4, EFT Selection List options for the format of 
sel_list. 
Description: 
The DUAL ALL command generates a copy of the source packset on the destination 
packset.  Unless SWITCH is specified, the source becomes the prime packset and 
the destination becomes the dual packset.  The prime packset can be made 
accessible to users as a public packset.  Public access to the dual packset is 
prevented and that packset is held in reserve.  In case of destruction of the 
prime packset, the dual packset can be substituted to provide quick access by 
users to the files contained on the packset.  Public access to the dual 
packset is made possible by deleting the :DUAL.$$EFT file on the dual packset. 
If continued usage as a dual packset is desired, deletion of the :DUAL.$$EFT 
file from the dual packset should be avoided as it is required for DUAL 
INCREMENTALs. 
CAUTION:  If changes are made to the dual packset, for example, if a user 
requests the packset for exclusive use and accesses or updates files on the 
dual packset, EFT cannot guarantee its later use as a prime packset or as the 
source for RESTORE operations. 
The copy performed by DUAL assures that the destination packset is identical 
to the source packset in all important respects. 
Example: 
DUAL ALL DP#LJF /(SKIP(.:SYMI,.:SYMO)) OVER DP#D75310 
copies the contents of DP#LJF to DP#D75310, skipping two accounts. 
00002
00003
00001
Format: 
DUAL I[NCREMENTAL] DP[nn]#psn [(sopt_list)] [/(sel_list)] 
Parameters: 
nn    is a 2-digit, user-defined disk resource identifier. 
psn    specifies a prime packset as the source for the DUAL INCREMENTAL. 
sopt_list    specifies source options.  sopt_list is of the form 
(so[, so] ... ) where so can be any of the following: 
    CLE[ANUP]     specifies the removal of deleted files and accounts from the 
    included file directories.  This option is the default if there are no 
    BACKUP or SAVE tapes (indicated by the lack of a :BACKUP.$$EFT control 
    file). 
    SWI[TCH] [IF ERR[ORS]] < nn     specifies that the destination packset is 
    to become the prime, and the source packset is to become the dual, 
    following the copy of the source to the destination if the number of bad 
    file errors is less than nn. 
    IDS ({FULL|FAST})    specifies how to copy IDS files. 
    ACUP    specifies that if only the access date of a file on the primary 
    packset has changed, the entire file is not moved to the dual packset. 
    Instead, the access date of the file on the dual packset is updated to 
    reflect the change. 
See SOURCE_OPS for complete descriptions.  Note, however, that the options 
listed above are the only options that can be used in a DUAL INCREMENTAL 
command. 
sel_list    specifies the accounts to be skipped and consists of SKI[P] 
(fid_specifier).  See Table 6-4, EFT Selection List options for the format of 
sel_list. 
Description: 
The DUAL INCREMENTAL command copies to the dual packset all changes since the 
last DUAL operation.  If the dual packset is not currently mounted, DUAL 
INCREMENTAL requests the operator to mount that packset.  As a result of DUAL 
INCREMENTAL, the files on the dual are logically identical to the files on the 
prime packset. 
In the case that the source and destination packsets are requested for 
EXCLUSIVE use by EFT and the destination packset AVRs before the source 
packset, the packsets appear reversed to the system.  However, EFT can perform 
the DUAL INCREMENTAL operation correctly using the packset containing :PRIME 
as the source. 
To avoid the problem of running out of disk space in the middle of DUAL, EFT 
will do a first pass which deletes from the DUAL pack the files that have 
already been deleted from the PRIME pack.  EFT then DUALs the rest of the 
PRIME pack.  The DUAL output listing will reflect the two-pass DUAL run.  The 
first pass lists the files and times they were deleted.  However, deletion 
times are unknown for files in a "no backup" account or for files removed from 
file directories as a result of a prior SAVE operation; hence "unknwn" is 
output in lieu of the deletion time. 
If creating a dual packset for DP#SYS in order that a system packset be 
available in case of destruction of the prime packset, the :DUAL.$$EFT file on 
the dual packset must not exist so that the dual packset can be made 
accessible to users as a public packset (PIG prevents a packset from being 
shared if a :DUAL.$$EFT file exists).  The following method is suggested so 
that the :DUAL file exists during not after DUAL completion:  rename :DUAL to 
::DUAL after a DUAL and then rename it back to :DUAL prior to a subsequent 
DUAL. 
Example: 
DUAL INCR DP#LJF (SWITCH IF ERRORS < 1) 
copies all changes since the last DUAL to the dual packset and changes the 
location of the :PRIME and :DUAL files if no errors exist. 
00002
00003
00001
EFT_OPTIONS
EFT commands are modified through the use of EFT options, which fall into the 
following categories: 
o   selection options    in the form of sel_list specify criteria for file 
    selection.  See: HELP (EFT) SEL_OPS. 
o   tape options    tape options in the form of topt_list specify options 
    pertaining to storage of backup files on tape.  See: HELP (EFT) TAPE_OPS. 
o   source options    in the form sopt_list specify source options.  See: HELP 
    (EFT) SOURCE_OPS. 
o   search options    in the form srch_list specify search criteria.  See: 
    HELP (EFT) SEARCH_OPS. 
o   optical disk options in the form odopt_list specify storage files on 
    optical disk.  See: HELP (EFT) OPT_DISK_OPS. 
EFT_OPTIONS
    Most EFT output listings are similar.  They usually contain one line of 
    information about the account and one line of information about the file. 
    The following example illustrates a listing output as a result of a SCAN 
    command. 
 !EFT 
  EFT E02 14:50 WED AUG 15 '90 
 *SCAN REV_AFARCHIVE_C.:REVIEWS 
 :REVIEWS  DP#KING   08/15/88  14:51 
     REV_AFARCHIVE_C                     * CON /F  A  B  3  179 821209 *** 
Total files                 1 
Total granules              3 
Elapsed time      00:00:00.39 
The listing above contains the following data, reading from left to right: 
First line: 
-  The account is :REVIEWS, disk pack DP#KING, current 
   date 08/15/88, current time 14:51. 
Second line: 
-  name of file is REV_AFARCHIVE_C 
-  Asterisk indicates that during copy of file to tape, 
   there has been a volume change.  A blank would indicate 
   no volume change. 
-  File organization is CON (consecutive). 
-  File type is F (or can be blank). 
-  Descriptor flag is A; can be: 
       blank - ordinary file 
       D  - deleted 
       A  - archived (actively) 
       I  - archived (inactively) 
       SA - queued for active archiving 
       SI - queued for inactive archiving 
       FA - queued for fetch; file is inactive 
-  B indicates bad file (or can be blank). 
-  Number of granules is 3. 
-  Number of records is 179. 
-  Applicable date is 881508.  This is the 
       o  archive date for inactively archived files 
       o  deletion date for deleted files 
       o  modification date for all others 
-  Asterisks (***) indicates error during file access. 
   A blank would indicate no error. 
The next three lines (total files, total granules, elapsed time) are 
self-explanatory. 
The following example illustrates a listing which was output as the result of 
a BACKUP command.  (A similar listing is output for a SAVE command.) 
!EFT 
 EFT E02 22:37 THU SEP 13 '90 
*BACKUP DP#KING/.:REVIEWS(ACUP) OVER LT#B38B03 
:REVIEWS  DP#KING  09/16/88  22:37  315 LT#B38B03 
    NAP$POSTER                      315 KEY/06          7      26 860918 fit 
Total files                1 
Total granules             7 
Elapsed time     00:00:02.39 
The above listing contains the following data, reading from left to right: 
First line: 
-  The account is :REVIEWS on disk pack DP#KING, the current date is 
   09/16/88, the current time is 22:37, the file sequence number 
   (FSN) of the first file written to tape during this operation is 
   315, and the tapeset used for the backup operation is LT#B38B03. 
Second line: 
-  File name is NAP$POSTER. 
-  FSN for the file on tape is 315. 
-  File organization is KEY (keyed). 
-  File type is 06 (or can be blank). 
-  Number of granules in the file is 7. 
-  Number of records in the file is 26. 
-  Applicable date is 880916.  This is the 
   o  archive date for inactively archived files 
   o  deletion date for deleted files 
   o  modification date for all others 
-  'fit' indicates that only the FIT of the file was written to 
   tape.  This only appears if the ACUP source option is specified 
   for a BACKUP operation and only the access date of the file 
   has changed since the last SAVE or BACKUP operation was performed.  This 
   field is blank otherwise. 
The next three lines (total files, total granules, elapsed time) are 
self-explanatory. 
The SCAN command with Extended Attributes (EA) provides three extra lines of 
information about a specific file as follows: 
*SCAN REV_AFARCHIVE_C.:REVIEWS(EA) 
:REVIEWS  DP#KING  07/17/88 14:51 
    REV_AFARCHIVE_C                   *CON /F A  B  3     179 
        12/09/82 07:01:36   12/09/82 08:12:50 03/12/84 13:55:27 - 
        URACCT ,106USERNAME 07/11/84 05:31:15 02/03/83 11:56:09  | <- Extra 
              never         LT#H28VOO*     37 LT#BARC00      12 -     Lines 
Total files               1 
Total granules            3 
Elapsed time    00:00:00:44 
First line: 
-   Account is :REVIEWS, disk pack is DP#KING, current date is 07/17/86, 
    and current time is 14:51 
Second line: 
- File name is REV_AFARCHIVE_C - One asterisk indicates that during copy of 
file to tape, there has 
    been a volume change.  A blank would indicate no volume change.  - File 
organization is CON (consecutive).  - File type is F (or can be blank). - 
Descriptor flag is A; can be: 
    blank - ordinary file 
    D  - deleted 
    A  - archived (actively) 
    I  - archived (inactively) 
    SA - queued for active archiving 
    SI - queued for inactive archiving 
    FA - queued for fetch; file is inactive 
-   B  indicates bad file (or can be blank). 
-   Number of granules is 3. 
-   Number of records is 179. 
Third line: 
-   Creation date and time is 12/09/82  07:01:36 
-   Modification date/time is 12/09/82 08:12:50 
-   Last access date/time is 03/12/84  13:55:27 
Fourth line: 
-   Owner is URACCT,106USERNAME 
-   Backup date/time is 07/11/84 05:31:15 ('never' if never backed up). 
-   Archive date/time is 02/03/83 11:56:09 ('never' if never archived). 
Fifth line: 
-   Expiration date/time is never (or date/time if applicable). 
-   Backup tape serial number is LT#H28V00* (the asterisk indicates reel 
    crossing). 
-   Backup tape FSN is 37. 
-   Archive tape serial number is LT#BARCOO.  An asterisk would indicate 
    reel crossing. 
-   Archive tape FSN is 12. 
The next three lines (total files, total granules, elapsed time) are 
self-explanatory. 
Format: 
{END|[E]X[IT]|Q[UIT]} 
Description: 
The END command (and its synonyms EXIT or QUIT) causes exit from the EFT 
processor after closing EFT control files and requesting the operator to 
dismount any tapes in use by the processor. 
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
Reference Manual (HA12-00) for more information on using ADAPT dialogs. 
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
Format: 
ERROR 
Description: 
The ERROR command is used to cause EFT to reprint the last error summary. 
00001
Format: 
EST[ABLISH] ARC[HIVE] FOR DP#mpsn[, DP#psn] ... W[ITH] CT#nnnn00 [,CT#nnnn00] 
    [(topt_list)] 
Parameters: 
mpsn,psn    specify packsets that are members of the archive set.  mpsn is 
considered the master of the set. 
CT#nnnn00    specifies a 6 digit controlled tapeset number ending in two 
zeroes.  If two tapesets are specified, a duplicate set is created. 
topt_list    specifies options pertaining to storage of archived files on 
tape.  topt_list is of the form to[,to] ...  where to is any of the following: 
    BLOCK 
    CHECK 
    DENSITY 
    EXPIRE 
    IOERROR CONTINUE 
    VOLACCESS 
See TAPE_OPS for complete descriptions. 
Description: 
The ESTABLISH command creates the file :ARCHIVE.$$EFT and associates a set of 
packsets with the tapeset to be used during ARCHIVE runs. 
The file :ARCHIVE.$$EFT, created on the master packset (mpsn), contains the 
information necessary to add to the existing ARCHIVE tapeset.  A copy of the 
:ARCHIVE.$$EFT file maintained on each member packset (psn2...) points to the 
master packset (mpsn1). 
EFT assigns tape serial numbers nnnn00 through nnnn99, splitting the 100 
serial numbers into variable length subsets.  A subset is started: a) at the 
first ARCHIVE run, b) if an irrecoverable write error occurs, c) when the 
MODIFY command is used to change the density and d) when the limit of 9999 ANS 
files is reached.  A warning is issued before EFT reaches the end of the 
reserved serial numbers. 
Usage Note: 
The master of the set (mpsn) must be mounted whenever an ARCHIVE operation is 
performed for any of the member packsets. 
Example: 
*ESTABLISH ARCHIVE FOR DP#EFTY WITH CT#EFTY00(DEN=1600) 
associates the archive tapeset CT#EFTY with the packset DP#EFTY. 
00002
00004
00001
00003
Format: 
EST[ABLISH] ARC[HIVE] FOR DP#mpsn[, DP#psn] ... W[ITH] CD#nnnn00 
    [(odopt_list)] 
Parameters: 
mpsn,psn    specifies packsets that are members of the archive set.  mpsn is 
considered the master of the set. 
CD#nnnn0[0]    specifies a five or six digit controlled optical diskset number 
ending in 0 through 99. The generation of duplicate optical disksets is not 
permitted. 
odopt_list    specifies options pertaining to storage of archived files files 
on optical disk. (odopt_list) is of the form (op[,op]...) where op is any of 
the following: 
    BLOCK 
    CHECK 
    VOLACCESS 
See OPT_DISK_OPS for descriptions of these options. 
Description: 
The ESTABLISH command creates the file :ARCHIVE.$$EFT and associates a set of 
packsets with the optical diskset to be used during archiving. 
00002
00001
Format: 
FET[CH] fid1[, fid2] ... 
Parameters: 
fid1, fid2    specify CP-6 file identifiers. 
Description: 
The FETCH command requests the return to disk of inactive file(s) in the 
archive system.  The most recent copy of the file from the archive tapeset is 
obtained by FETCH.  To prevent update activity, the file is locked until it is 
returned from tape at the next RETRIEVE run, performed by the system manager. 
Usage Notes: 
1.  A user may be able to FETCH an inactive file, but be unable to access it 
    if access controls for the file exclude the user. 
    The specified fid may include a password, however, for inactively stowed 
    files it cannot be verified and is ignored. 
2.  This command may be used:  a) if the user is the creator of the file, b) 
    if the user has FMSEC active via !PRIV FMSEC or c) for stowed inactive 
    files, if the user has write access to the account. 
3.  While the file is queued for STOW or FETCH it may not be updated. 
4.  If the file management account limit is exceeded, FETCH requests are 
    ignored by the RETRIEVE process unless, however, the FETCH request was 
    made with FMSEC active. 
5.  Following the successful FETCH of an archived file, the file must be 
    UNARCHIVEd before it can be updated. 
6.  Passwords specified for files on a FETCH command cannot be verified at the 
    time they are fetched.  Thus, a user may be able to FETCH a passworded 
    file but be unable to access it if the correct password is not supplied as 
    part of the fid on a subsequently executed command. 
Example: 
!FETCH TESTFILE 
requests retrieval of the file TESTFILE; at the next RETRIEVE run, the most 
recently archived version of the file is returned to disk (over the current 
copy of the file). 
00002
00004
00001
00003
FSN
FSN
    EFT designates files on tape by file sequence number (FSN) as well as file 
    name.  A backup tapeset used in file restoration may contain multiple 
    versions of the same file; the user is responsible for specifying the 
    necessary parameters to direct EFT to the desired version of the file.  In 
    this case, the user can supply a range of tapeset FSNs by means of the EFT 
    FSN option as described under the RESTORE command. 
    The maximum number of FSNs stored in the file information table (FIT) of 
    archived files is 9999. 
    Note:  When performing restores on volume sets, the situation is sometimes 
    encountered where a file begins on one reel, and continues to the next. 
    In this case, both reels must be specified in the RESTORE command.  The 
    EFT error message 
        Volume missing or out of order for tape ... 
    usually indicates that only one reel has been specified. 
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
  ADD Command - 
      HELP ADD 
  ARCHIVE - 
      HELP ESTABLISH DESCRIPTION: 
  ARCHIVE Command - 
      HELP ARCHIVE 
  :ARCHIVE.$$EFT - 
      HELP ESTABLISH DESCRIPTION: 
      HELP STATUS FORMAT: 
  ARCOM Processor - 
      HELP ARCOM 
B 
  BACKUP Command - 
      HELP BACKUP 
  :BACKUP.$$EFT - 
      HELP STATUS FORMAT: 
C 
  CATALOG Command - 
      HELP CATALOG 
  CHECK Command - 
      HELP CHECK 
      HELP CHECK_OPTICAL 
  CLOSE Command - 
      HELP CLOSE 
  Continuation after Tape I/O Error - 
      HELP TAPE_IO_ERROR 
  Controlled Optical Disksets - 
      HELP OPTICAL_DISKSETS 
  Controlled Tapesets - 
      HELP CONTROLLED_TAPESETS 
D 
  DATE|TIME Command - 
      HELP DATE 
  DIRECTORY Command - 
      HELP DIRECTORY 
  DO Command - 
      HELP DO 
  DUAL ALL Command - 
      HELP DUAL_ALL 
  DUAL INCREMENTAL Command - 
      HELP DUAL_INCREMENTAL 
  :DUAL.$$EFT - 
      HELP STATUS FORMAT: 
E 
  EFT -   
    ADD Command - 
      HELP ADD FORMAT: 
    ARCHIVE Command - 
      HELP ARCHIVE FORMAT: 
    BACKUP Command - 
      HELP BACKUP FORMAT: 
    CATALOG Command - 
      HELP CATALOG FORMAT_2: 
    CHECK Command - 
      HELP CHECK FORMAT: 
      HELP CHECK FORMAT: 
    CLOSE Subcommand - 
      HELP CLOSE FORMAT: 
    controlled tapeset - 
      HELP CONTROLLED_TAPESETS 
    DUAL ALL Command - 
      HELP DUAL_ALL FORMAT: 
    DUAL INCREMENTAL Command - 
      HELP DUAL_INCREMENTAL FORMAT: 
    ERROR Command - 
      HELP ERROR FORMAT: 
    ESTABLISH Command - 
      HELP ESTABLISH FORMAT: 
    FETCH Command - 
      HELP FETCH FORMAT: 
    MODIFY Command - 
      HELP MODIFY FORMAT: 
    MOUNT command - 
      HELP MOUNT FORMAT: 
    OPEN Command - 
      HELP OPEN FORMAT_3_FOR_TAPE_TO_DISK: 
    PURGE Command - 
      HELP PURGE Format 
    REMOVE Command - 
      HELP REMOVE FORMAT_2_FOR_TAPE: 
      HELP REMOVE FORMAT_2_FOR_TAPE: 
    REQUALIFY Command - 
      HELP REQUALIFY FORMAT: 
    RESTORE Command - 
      HELP RESTORE FORMAT: 
    RETRIEVE Command - 
      HELP RETRIEVE FORMAT: 
    SAVE Command - 
      HELP SAVE FORMAT: 
    SCAN Command - 
      HELP SCAN FORMAT: 
    STATUS Command - 
      HELP STATUS FORMAT: 
    STOW Command - 
      HELP STOW FORMAT: 
    tapeset - 
      HELP CONTROLLED_TAPESETS 
    Transfer/Transport Subcommand - 
      HELP TRANSFER_TRANSPORT FORMAT: 
    UNARCHIVE Command - 
      HELP UNARCHIVE FORMAT: 
    UNFETCH Command - 
      HELP UNFETCH FORMAT: 
    UNSTOW Command - 
      HELP UNSTOW FORMAT: 
    VALIDATE Command - 
      HELP VALIDATE FORMAT: 
    WHERE Command - 
      HELP WHERE FORMAT: 
  EFT Commands - 
      HELP OPTICAL_DISK_COMMANDS 
  EFT Optical Diskset Options - 
      HELP OPTICAL_DISKSET_OPTIONS 
  EFT Options - 
      HELP EFT_OPTIONS 
  EFT Output Listing - 
      HELP EFT_OUTPUT_LISTING 
  EFT Search Options - 
      HELP SEARCH_OPS 
  EFT Selection List Options - 
      HELP SEL_OPS 
  EFT Source Options - 
      HELP SOURCE_OPS 
  EFT Tape Options - 
      HELP TAPE_OPS 
  EFT tapeset - 
      HELP CONTROLLED_TAPESETS 
  END Command - 
      HELP END 
  ENTER Command - 
      HELP ENTER 
  ERASE Command - 
      HELP ERASE 
  ERROR Command - 
      HELP ERROR 
  ESTABLISH Command - 
      HELP ESTABLISH 
      HELP ESTABLISH_OPTICAL 
F 
  FETCH Command - 
      HELP FETCH 
  File Sequence Number - 
      HELP FSN 
  Files Created by EFT - 
      HELP RELATED_FILES 
H 
  HELP Command - 
      HELP HELP 
I 
  Invoking EFT - 
      HELP INVOKING_EFT 
M 
  MODIFY Command - 
      HELP MODIFY 
      HELP MODIFY_OPTICAL 
  MOUNT Command - 
      HELP MOUNT 
O 
  OPEN Command - 
      HELP OPEN 
  OUTPUT Command - 
      HELP OUTPUT 
P 
  :PRIME.$$EFT - 
      HELP STATUS FORMAT: 
  PRINT Command - 
      HELP PRINT 
  Privileges for Using EFT - 
      HELP PRIVILEGES 
  PURGE Command - 
      HELP PURGE 
R 
  REBUILD Command - 
      HELP REBUILD 
  REMOVE Command - 
      HELP REMOVE 
      HELP REMOVE_OPTICAL 
  REQUALIFY Command - 
      HELP REQUALIFY 
  RESTORE Command - 
      HELP RESTORE 
  RETRIEVE Command - 
      HELP RETRIEVE 
      HELP RETRIEVE_OPTICAL 
  REWIND Command - 
      HELP REWIND 
S 
  SAVE Command - 
      HELP SAVE 
  SCAN Command - 
      HELP SCAN 
  STATUS Command - 
      HELP STATUS 
  STATUS Command (EFT) - 
      HELP STATUS FORMAT: 
  STEPCC Codes for EFT - 
      HELP STEPCC 
  STOW Command - 
      HELP STOW 
T 
  tapeset - 
      HELP CONTROLLED_TAPESETS 
  Transfer/Transport Specifications - 
      HELP TRANSFER_TRANSPORT 
U 
  UNARCHIVE Command - 
      HELP UNARCHIVE 
  UNFETCH Command - 
      HELP UNFETCH 
  UNSTOW Command - 
      HELP UNSTOW 
V 
  VALIDATE Command - 
      HELP VALIDATE 
W 
  WHERE Command - 
      HELP WHERE 
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
When invoked, EFT prompts with the * character; most EFT commands are entered 
at this level.  The OPEN command for file transfer or transport provides a 
sub-level for command entry. 
Format: 
MOD[IFY] ARC[HIVE] FOR DP#mpsn W[ITH] [CT#nnnn00] [,CT#nnnn00] [(topt_list)] 
Parameters: 
mpsn    specifies the master packset of an archive set. 
CT#nnnn00    specifies a new tapeset identifier to be used at the next ARCHIVE 
run. 
topt_list    specifies options pertaining to storage of archived files on 
tape.  (topt_list) is of the form (op[,op]...) where op is any of the 
following: 
    BLOCK 
    CHECK 
    DENSITY 
    EXPIRE 
    IOERROR CONTINUE 
    VOLACCESS 
See TAPE_OPS for complete descriptions. 
Description: 
The MODIFY command updates the :ARCHIVE file and thereby instructs EFT to 
start a new tapeset with changed attributes at the next ARCHIVE run.  If the 
tapeset is omitted, the next tape in sequence will be used with the changed 
attributes.  If tapeset is specified, the current tapeset serial number list 
will be closed and a new tapeset opened with the specified attributes.  Any 
unspecified options default to the attributes of the current tapeset. 
Usage Note: 
The master of the set (mpsn) must be mounted whenever a MODIFY ARCHIVE 
operation is performed. 
Two tapesets can be specified on the ESTABLISH command.  If two tapesets were 
specified on the ESTABLISH command, then two tapesets must be specified on the 
MODIFY command to keep the tapesets in sync. 
00002
00001
00003
Format: 
MOD[IFY] ARC[HIVE] FOR DP#mpsn W[ITH] [CD#nnnn00] [(odopt_list)] 
Parameters: 
mpsn    specifies a master packset of an archive set. 
CD#nnnn0[0]    specifies a five or six digit controlled optical diskset number 
ending in 0 through 99. 
odopt_list    specifies options pertaining to storage of archived files on 
optical disk.  (odopt_list) is of the form (op[,op]...) where op is any of the 
following: 
    BLOCK 
    CHECK 
    VOLACCESS 
See OPT_DISK_OPS for descriptions of these options. 
Description: 
The MODIFY command updates the :ARCHIVE file and thereby instructs EFT to 
start a new optical diskset with changed attributes at the next ARCHIVE run. 
The specifying of duplicate optical disksets is not permitted. 
00002
00001
Format: 
MOU[NT] tape [(option [,option]...)] 
Parameters: 
tape    is of the form LT#xxxxxx (for labeled tape) or CT#xxxxxx (for EFT 
controlled tapesets). 
option    may be one or more of the following: 
    DEN[SITY]={800|1600|6250}    specifies tape density. 
    RI[NG]    specifies that the tape is to be mounted with a write ring. 
    NOR[ING]    specifies that the tape is to be mounted without a write ring. 
    This is the default setting. 
    VOL[UME] = decimal    specifies volume number.  Used in conjunction with a 
    controlled tapeset number to indicate which of the volumes is desired. 
Description: 
MOUNT requests that the specified tape be mounted on the system tape drives. 
When MOUNT is issued, the operator is informed of the request.  No further 
commands can be issued until the requested mount has taken place.  If the 
BREAK key is struck while a MOUNT request is active, the request is 
terminated, and a cancellation message is sent to the operator. 
Examples: 
*MOUNT FT#1234 RING 
means mount labeled tape #1234 with ring. 
Related Commands: 
REMOVE, REWIND 
00002
00003
00001
00004
OPTICAL_DISKSET_OPTIONS
Format 1 for Disk to Disk: 
OPE[N] UPDATE {TRANSFER[RING] ({PRO[TECTED|UNP[ROTECTED]}) } 
              {TRANSPOR[TING]                              } 
Format 2 for Disk to Tape: 
       {CRE[ATE]} {CT#nnnn0[,CT#nnnn0  ] 
OPE[N] {EXT[END]} {CT#nnnn00[,CT#nnnn00] [(topt_list)] 
                  {LT#tsn1[#tsn2] ... 
     {TRANSFER[RING] ({PRO[TECTED]|UNP[ROTECTED]}) }} 
     {TRANSPOR[TING]                               }} 
                                                    } 
Format 3 for Tape to Disk: 
             {CT#nnnn0           }               {TRANSFER[RING]} 
OPE[N] INPUT {CT#nnnn00          } [(sopt_list)] {TRANSPOR[TING]} 
             {LT#tsn1[#tsn2] ... } 
Parameters: 
topt_list    specifies options pertaining to storage of the saved files on 
tape.  (topt_list) is of the form (op[,op]...) where op can be any of the 
following: 
    BLOCK 
    CHECK 
    DENSITY 
    EXPIRE 
    IOERROR CONTINUE 
    VOLACCESS 
See TAPE_OPS for complete descriptions. 
sopt_list    is of the form (so[, so] ... ) where so can be any of 
the following: 
    DENSITY 
    FSN 
    IOERROR CONTINUE 
    {PROTECTED|UNPROTECTED|INCREMENTAL} 
    SHARED 
    VOLUME 
SOURCE_OPS and TAPE_OPS 
for complete descriptions. 
Description: 
The OPEN command establishes the media to be used and the specific function to 
be performed at a transfer or transport operation.  The OPEN command causes 
EFT to prompt with the + character for subcommands.  The subcommands may 
consist of transfer/transport specifications, or the CLOSE command. 
The keywords UPDATE, CREATE, EXTEND, or INPUT define the media used and the 
direction of the transfer/transport operation.  UPDATE specifies that a 
disk-to-disk operation is to be performed.  CREATE and EXTEND specify that a 
disk to tape operation is to be performed, starting at the first volume of a 
tapeset (CREATE) or adding to an existing tapeset (EXTEND).  INPUT specifies a 
tape to disk operation is to be performed. 
The types of functions provided are as follows: 
o   TRANSFER - Copy accounts or files making the files on the destination 
    medium qualified for backup if the account is so authorized.  For an 
    UPDATE, CREATE, or EXTEND function, files are retained on the source if 
    PROTECTED is specified and are deleted if UNPROTECTED is specified.  (See 
    Usage Notes.) 
o   TRANSPORT - Copy accounts or files without deleting the files on the 
    source medium or altering the files on the destination medium except as 
    follows: 
        When removing BACKUP, CREATOR or STOW information from a destination 
        file's FIT as a result of the SCRUB option being specified or as a 
        result of being automatically removed when the destination account is 
        specified (see acct description). 
    Unlike TRANSFER, TRANSPORT copies files to the destination medium but does 
    not automatically qualify them for backup. 
In both cases, the copy operation includes selected files in NO BACKUP 
accounts. 
For example: 
    OPEN CREATE CT#SHIP40(DEN=1600,BLOCK=16,VOLA=ALL,EXP=10) FOR TRANSPORT 
Usage Notes: 
1.  If UNPROTECTED is specified for an update function and the DIR[ECTORIES] 
    search option is also specified: 
    o   The source account is deleted from the master account directory if it 
        exists there and the destination account is added.  However, the 
        master account directory will not be updated with the destination 
        account if the specified source account is not on the packset pointed 
        to in the master account directory. 
    o   The source account, which may contain unselected files, is not deleted 
        unless all files are transferred using the ANY[FILE] search option 
        (see SEARCH_OPTIONS), in which case the source account is deleted. 
        However, if the granule limit on the destination packset is exceeded 
        before the operation completes, the source account is not deleted. 
        Instead, only successfully transferred files are deleted from the 
        source account. 
2.  If the PAD and DIR search options are specified for an update function, 
    the packset defaults for the destination packset are replaced with the 
    source packset defaults.  If only the DIR search option is specified, the 
    packset defaults for the destination packset are preserved. 
Related Commands: 
See Transfer/Transport Specifications and CLOSE command. 
00002
00001
00004
00003
EFT_OPTIONS
EFT supports controlled optical disksets consisting of consecutive volumes 
identified by the prefix CD followed by a serial number.  Controlled optical 
diskset specification is similar to tapeset specification.  The controlled 
optical diskset specification CD#xxxxn begins with OD#xxxxn and ends with 
OD#xxxx9.  The specification CD#xxxxnn begins with OD#xxxxnn and ends with 
OD#xxxx99.  For example, CD#ABCD5 means OD#ABCD5 through OD#ABCD9. CD#ABCD01 
means OD#ABCD01 through OD#ABCD99. 
The EFT optical diskset option list (odopt_list) specifies options pertaining 
to storage of files on optical disksets.  (odopt_list) is of the form 
(op[,op]...) where op can be any of the options listed and described below. 
  Option    Description 
  BLOCK=nn 
            Specifies the maximum physical optical disk block size in pages 
            (4096 bytes each).  The maximum is 21; the minimum is 6; the 
            default is 8. 
  CHECK 
            Specifies automatic optical disk checking.  The automatic check is 
            performed after the initial command function (for example, 
            ARCHIVE) is complete.  No cleanups or deletions are performed 
            until after the check completes successfully.  CHECK checks only 
            that which was written during the previous EFT operation. 
  VOLA[CCESS]={N[ONE]|A[LL]|I[N]} 
            Indicates optical disk set access limitations. 
            NONE specifies that only the owner of the volume set (account of 
            user creating first file on the volume set) will be allowed access 
            to this volume set. 
            ALL specifies that all may read or write the volume set. 
            IN specifies that all may read the volume set, but only the owner 
            may write on it. 
  FSN (m  [- n]) 
            Specifies a file sequence number (m) within a set of EFT optical 
            disks.  If the form (m - n) is specified, only that range of files 
            is used. 
  VOL[UME]=nnn 
            Specifies on which volume the operation is to start.  For instance 
            for a controlled optical diskset CD#FGHI0 of 10 volumes, OD#FGHI0 
            through O#FGHI9, OD#FGHI7 is volume 8. 
00002
00001
00004
00003
00005
The following commands have a difference format when used to support optical 
disk archiving: 
CHECK, ESTABLISH, MODIFY, REMOVE, RETRIEVE. 
To obtain a HELP message for an individual command, type: 
HELP OPTICAL_DISK_COMMANDS command 
To view the command format and description, type: 
HELP OPTICAL_DISK_COMMAND command 
To view all the commands, type ??. 
  Command    Description 
  CHECK 
             Verifies the readability and reports the content of an EFT 
             optical diskset. 
             For more information, type:  HELP CHECK_OPTICAL 
  ESTABLISH 
             Establishes an optical diskset for archiving of packsets. 
             For more information, type:  HELP ESTABLISH_OPTICAL 
  MODIFY 
             Modifies an archived optical diskset or its attributes. 
             For more information, type:  HELP MODIFY_OPTICAL 
  REMOVE 
             Removes the specified packset from an existing group of packsets, 
             or removes an optical disk cartridge from the optical disk drive 
             and stores it in its allocated library slot. 
             For more information, type:  HELP REMOVE_OPTICAL 
  RETRIEVE 
             Retrieves all archived optical disksets for which a FETCH is 
             requested and stores them on the appropriate packset(s). 
             For more information, type:  HELP RETRIEVE_OPTICAL 
Note that the following EFT commands can also be used with optical disksets: 
    FETCH 
    STATUS 
    STOW 
    UNARCHIVE 
    UNFETCH 
    UNSTOW 
These commands require no special documentation as the syntax for their use 
remains the same as for tapesets.  Any differences in results of their use 
(e.g., STATUS output headers for optical disksets) will be apparent. 
00001
00002
00003
00004
00005
OPTICAL_DISKSET_OPTIONS
EFT_OPTIONS
OPTICAL_DISKSET_OPTIONS
Format: 
         [[OVER] LP[nn]       ] 
OUT[PUT] [[INTO] LP@[location]] [(option[,option]...[)]] 
         [[ON  ] fid          ] 
         [[TO  ] ME           ] 
Parameters: 
ON or TO    indicates to only honor the OUTPUT command if the file does not 
already exist. 
OVER    indicates to honor the OUTPUT command whether or not the file exists. 
INTO    indicates to merge the result of the OUTPUT command into the file if 
it exists, or to create a new one if it does not. 
LP    directs output to a logical device (stream) destined for a line printer 
located at the workstation defined for that logical device via the IBEX LDEV 
command.  If 'nn' is not specified, output is sent to LP01.  If specified, 
'nn' must be a decimal number (01 to 99), which designates a logical device. 
LP@    directs output to a line printer.  If 'location' is not specified, 
output is sent to a line printer at the user's default workstation.  The 
'location' option may be used to specify a workstation which may be different 
from the default workstation. 
fid    directs output to a CP-6 file.  fid is any valid CP-6 file identifier. 
ME    directs output to the terminal for a timesharing user or to a line 
printer at the user's default workstation for a batch user. 
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
The installation manager must use SUPER to authorize an account with the EFT 
processor privilege (EFT PPRIV) before the account will be allowed to perform 
most EFT operations.  EFT runs with FMSEC turned on when the account entering 
commands has EFT PPRIV. 
All EFT commands, with the exception of user archiving commands (STOW, UNSTOW, 
FETCH, UNFETCH, and UNARCHIVE), require EFT processor privilege.  All user 
archiving commands should be entered at the IBEX level and do not require EFT 
processor privilege. 
Format 1 for storing files on a specified tapeset: 
PUR[GE] DP[nn]#psn [(sopt_list)] [/(sel_list)] [OVER {CTnnnn00          } 
                                               [     {LT#tsn1[#tsn2] ...} 
    [(topt_list1)]] 
Format 2 for storing files on the archive set: 
PUR[GE] DP[nn]#psn [(sopt_list)] [/(sel_list)] [(topt_list2)] 
Parameters: 
nn    is a 2-digit, user-defined disk resource identifier. 
psn    specifies the packset to be purged. 
sopt_list    specifies criteria used to determine what files are to be purged. 
sopt_list is specified in the form (so[, so] ... ) where so is any of the 
following options: 
    EXP[IRED] 
    [NOT] [{ACC[ESSED]   }] [{BEF[ORE]| < }] {DELT[A] = n             } 
          [{BAC[KED] [UP]}] [{SIN[CE ]| >=}] 
          [{CR[EATED]    }] [{AFT[ER] | > }] {mm/dd/yy[,hh:mm[:ss.ss]]} 
          [{MO[DIFIED]   }] [{ON      | = }] 
          [{ST[OWED]     }] 
under SOURCE_OPS and SEARCH_OPS.  The default is EXPIRED. 
sel_list    specifies the files to be processed.  See SEL_OPS for format. 
topt_list1    specifies options pertaining to storage of the saved files on 
tape.  (topt_list) is of the form (op[,op]...) where option can be any of the 
following: 
    BLOCK 
    CHECK 
    DENSITY 
    EXPIRE 
    IOERROR CONTINUE 
    VOLACCESS 
topt_list2    specifies options pertaining to storage of files on an archive 
tape.  (topt_list2) is of the form (option1[,option2]....)  where option can 
be any of the following: 
    CHECK    (in Format 2) specifies that automatic tape checking will be 
    performed if purged files are being archived.  By default, tape checking 
    is performed depending on whether it was specified on the ESTABLISH 
    command.  See TAPE_OPS for a complete descriptions. 
    IOERROR CONTINUE    (in Format 2) specifies that processing should 
    continue after the occurrence of an irrecoverable tape write error.  By 
    default, continuation is performed according to the setting established 
    via the ESTABLISH command.  See TAPE_OPS for a complete descriptions. 
Description: 
The PURGE command performs various deletions of files from the packset 
specified and writes the purged files to tape.  To be purged, a file must meet 
at least one of the criteria specified as source options.  If the tapeset 
specification is omitted, purged files are stowed as inactive files on the 
appropriate archive set.  If a tapeset is specified, the purged files are 
deleted from the packset and written to the tapeset.  This tapeset can later 
be used to perform file RESTORE operations. 
00001
00003
00001
00002
END
Format: 
                      [     {CT#nnnn0           }] 
REB[UILD] DP[nn]#psn1 [FROM {CT#nnnn00          }] [(rbopt_list)] 
                      [     {LT#tsn1[#tsn2] ... }] 
                      [     {fid                }] 
    [/(sel_list)] 
Parameters: 
nn    is a 2-digit, user-defined disk resource identifier. 
psn1    specifies the packset to be rebuilt. A packset to be rebuilt should 
first be processed by VOLINIT and PIG's SCRATCH and BUILD commands. 
FROM    If the most recent :BACKUP.$$EFT file is to be read from tape (CT or 
LT specified), the file sequence number(FSN) must also be specified.  See 
rbopt_list below for a description of FSN. 
{CT#nnnn0           } 
{CT#nnnn00          } 
{LT#tsn1[#tsn2] ... }    specifies the tapeset or specific tape that contains 
the most recent :BACKUP.$$EFT file. 
fid    specifies the disk file that contains the most recent :BACKUP.$$EFT 
file. Fid is any valid CP-6 disk file identifier. 
rbopt_list    specifies options describing how the REBUILD is to be performed. 
Rbopt_list is of the form (so[,so] ... ) where so can be any of the following: 
VOL[UME]=nnn 
    Specifies which volume of the volume set is to be initially mounted for 
    the purpose of searching for the specified FSN.  By default, searching 
    will begin at the first volume. 
DEN[SITY]={800|1600|6250} [BPI] 
    Specifies density at which the tape is recorded. 
FSN=m 
    Specifies the file sequence number that contains the :BACKUP.$$EFT file 
    needed to start the REBUILD. This file sequence number is available from 
    the most recent STATUS FULL report or from the listing produced by the 
    most recent BACKUP or SAVE operation. 
DIR[ECTORIES] 
    Specifies that file directory FITs should be restored. 
NPAD 
    Specifies that the packset account directory FIT should not be restored. 
IOERROR CONTINUE {[=Y[ES]|=N[O]]} 
    Specifies whether or not processing should continue after the occurrence 
    of an irrecoverable tape read error.  See Table 6-5, EFT Tape Options, for 
    a complete description. 
sel_list    specifies the file selection criteria for the files to be rebuilt. 
These criteria apply to the entire rebuild operation.  (sel_list) is of the 
form (option1[,option2]...) where option is any of the selection options 
listed in Table 6-4, EFT Selection List Criteria. 
Description: 
The REBUILD command rebuilds files on the specified packset using multiple 
tapesets.  REBUILD can be used for the following purposes: 
o   To rebuild a packset for which no dual packset exists. In this case, both 
    BACKUP tapesets and the most recent SAVE tapeset are used. 
o   To rebuild IDS files from multiple file increments on BACKUP (and possibly 
    SAVE) tapesets. 
o   To update from BACKUP tapes a dual packset that is to replace a destroyed 
    prime packset. 
EFT reads the :BACKUP.$$EFT file to obtain the required tapes to perform the 
REBUILD. The latest version of :BACKUP must be utilized.  If the FROM clause 
is specified, EFT will look for :BACKUP.$$EFT on the specified tape, tapeset 
or disk file. If the FROM clause is not specified, EFT will look for 
:BACKUP.$$EFT on the packset being rebuilt and abort if it does not exist. 
By default, REBUILD always restores the packset account directory FIT unless 
instructed otherwise (via the NPAD option). 
A file directory FIT is restored only if it does not exist at the beginning of 
a REBUILD operation or if the DIR option is specified in which case it is 
always restored. EFT remembers which directory FITs have been restored so that 
it can continue restoring them from subsequent tapes. This information, as 
well as status information, is maintained in the :REBUILD.$$EFT file on the 
packset being rebuilt.  This information permits recovery from abort 
situations such as system crashes and tape reading difficulties, and permits 
EFT to continue the tape REBUILD operation at the point of interruption. If a 
file directory FIT is restored, the most recent copy will reside on disk at 
REBUILD completion as a result of tapes being processed in chronological 
order. 
All files or selected files are moved to disk. Since the tapes are processed 
in chronological order, the newest copy of a file will reside on disk at 
REBUILD completion. 
In rebuilding a packset, REBUILD processes the most recent SAVE tape and then 
processes subsequent BACKUP tapes from the oldest to the newest.  REBUILD 
requests mounting of tapesets as needed. The rebuilt packset resembles the 
destroyed packset in all respects except that the following update activity is 
lost: 
o   Update activity since the last BACKUP. 
o   Update activity in NO BACKUP accounts or files. 
During the rebuilding of IDS files, no updates to those files should be 
permitted. If backed up using the option IDS(FAST), the backup tapes contain 
only granules that were modified. REBUILD reconstructs the specified files 
from the most recent SAVE tapeset and multiple backup tapesets, processing the 
oldest to the newest tapes. Time stamp checking, comparing the UTS of 
corresponding tape and disk granules, is not necessary because tapes are 
processed in chronological order. 
In updating a dual packset, any changes backed up on tape since the last DUAL 
operation can be applied via REBUILD.  After REBUILD processing is complete, 
the packset resembles the destroyed packset in all respects except that update 
activity for the following is lost: 
o   Update activity since the last tape BACKUP. 
o   Update activity for NO BACKUP accounts since the last DUAL INCR. 
If the purpose of REBUILDing the dual packset is to recover from loss of the 
primary one, the rebuilt packset is typically DUALed before it is made public. 
If available granule space is exceeded, EFT scans the remainder of the tape 
looking for deleted files and deletes the matching files on disk.  EFT then 
backspaces the tape and retries to restore the remaining tape files. 
Usage Notes: 
1.  Backup of files to tape with the option (ACUP) may store only the file's 
    FIT to tape.  On a file restoration, if a file without data is created as 
    a result of restoring a FIT-only file (this occurs if data for the file 
    does not already exist on the packset), a file with data inconsistencies 
    is created.  The names of these files are maintained in a file called 
    :NODATA in the $$EFT account and may be listed using the STATUS command. 
Example: 
REBUILD DP#CHK FROM LT#H2761 (DEN=1600,FSN=150) 
Directs EFT to rebuild packset DP#CHK from the :BACKUP.$$EFT file which is 
located on tape #H2761 at file sequence number 150. 
00002
00004
00001
00003
EFT builds, updates, and/or restores specific files during save, backup, dual, 
archiving, restore, and rebuild operations.  These files, called EFT control 
files, reside on the packset for which the operation is performed. 
The following files comprise the set of EFT control files: 
    :BACKUP.$$EFT 
    :PRIME.$$EFT 
    :DUAL.$$EFT 
    :ARCHIVE.$$EFT 
    :REBUILD.$$EFT 
    :NODATA.$$EFT 
See the STATUS command for a description of these files. 
If EFT has to record information in one of its control files and the file does 
not already exist, EFT will create the file.  If the $$EFT account does not 
already exist on the packset, EFT automatically creates it before attempting 
to create the control file. 
The EFT CATALOG command creates an EFT catalog file designated by the user. 
See the CATALOG command.  Since a catalog file is not an EFT control file, EFT 
does not ensure that an account specified for a catalog file will be 
automatically created if it does not already exist. 
Format 1 for Disk: 
REM[OVE] DP#psn [FR[OM]] [ARC[HIVE]] FOR DP#mpsn 
Format 2 for Tape: 
REM[OVE] tape 
Parameters: 
psn    specifies the packset to be removed from an existing group of packsets. 
mpsn    specifies the master of the packset group. 
tape    is of the form LT#xxxxxx (for labeled tapes) or CT#xxxxxx (for EFT 
controlled tapesets). 
Description: 
Form 1 of the REMOVE command removes a packset from an existing group of 
packsets.  If a master packset is removed, the members of the packset group 
are also subsequently taken away.  EFT updates the :ARCHIVE file as additional 
packsets are removed. 
Form 2 of the REMOVE command requests that the specified tape be removed from 
the system tape drives.  (EFT does not automatically remove volumes after they 
have been used, except when making the transition to the next reel of a 
multi-volume tapeset or when a duplicate tapeset has been created.) 
Usage Notes: 
1.  The master of the set (mpsn) must be mounted whenever an ARCHIVE operation 
    is performed for any of the member packsets. 
2.  Once a packset is removed, its files can no longer be ARCHIVED.  It is 
    assumed that the packset is being returned to scratch and that the user 
    will perform the necessary FETCH operations before the system manager 
    SCRATCHes the ARCHIVE tapes. 
Related Commands: 
MOUNT 
00002
00001
00004
00003
Format 3 for Optical Diskset: 
REM[OVE] optical_diskset 
Parameters: 
psn    specifies the packset to be removed from an existing group of packsets. 
mpsn    specifies the master of the packset group. 
optical_diskset    is of the form OD#xxxxxx. 
Description: 
Form 3 of the REMOVE command requests that the specified optical disk 
cartridge be removed from the optical disk drive and stored in its allocated 
library slot.  (EFT does not automatically remove volumes after they have been 
used except when making the transition to the next optical diskset of a 
multi-volume optical diskset). 
Usage Notes: 
1.  The master of the set (mpsn) must be mounted whenever an ARCHIVE operation 
    is performed for any of the member packsets. 
2.  Once a packset is removed, its files can no longer be ARCHIVED.  It is 
    assumed that the packset is being returned to scratch and that the user 
    will perform the necessary FETCH operations before the system manager 
    SCRATCHes the ARCHIVE tapes. 
00002
00001
00003
Format: 
REQ[UALIFY] [ARC[HIVE]] DP[nn]#psn1[,DP[nn]#psn2] ... (srch_list) 
            [BACK[UP] ] 
    [/(sel_list)] 
Parameters: 
nn    is a 2-digit, user-defined disk resource identifier. 
psn1,psn2    specify the packsets to be requalified. 
srch_list    specifies the search criteria and includes all of the options 
listed under SEARCH_OPS.  The defaults are BACKED UP SINCE for BACKUP, and 
STOWED SINCE for ARCHIVE. 
sel_list    specifies a list of selection options.  (sel_list) is in the form 
(option1[,option2]...) where option is any of the selection options listed 
under SEL_OPS. 
Description: 
The REQUALIFY command permits the system manager to alter the FIT of selected 
files so that the ARCHIVE or BACKUP command can then be used to replicate 
information previously written to an archive tape or backup tape.  The 
REQUALIFY command scans the packset(s) for each file selected.  If ARCHIVE is 
specified, files selected in the specified time range are changed to appear as 
if the user has just requested STOW.  If BACKUP is specified, eligible files 
written to tapes with SAVE or BACKUP commands in the specified time range are 
changed to appear as if the user has just created the file.  If neither 
ARCHIVE or BACKUP is specified, the default is BACKUP.  Note that a file 
archived inactively cannot be requalified. 
Example: 
REQUALIFY DP#psn1,DP#psn2,DP#psn3(BAC DELTA=8) 
Select files on DP#psn1, DP#psn2 and DP#psn3 that have been SAVEd/BACKedUP in 
the last 8 hours and make them eligible for the next SAVE/BACKUP. 
REQUALIFY BACKUP DP#psn1, DP#pns2 (BAC DELTA=2) 
Select files on DP#psn1 and DP#psn2 that have been SAVEd/BACKedUP in the last 
2 hours and make them eligible for the next SAVE/BACKUP. 
REQUALIFY ARCHIVE DP#psn1 (STOW DELTA=5) 
Select files on DP#psn1 that has been actively archived in the last 5 hours 
and make them look like the user has just requested a STOW ACTIVE command on 
them. 
00002
00003
00001
Format: 
Format 1 for Tape: 
          {CT#nnnn0           } 
RES[TORE] {CT#nnnn00          } [(sopt_list)] {/(sel_list)     } 
          {LT#tsn1[#tsn2] ... }               {/[file].account1} 
    [(> mm/dd/yy,hh:mm)] [{ON|OVER} DP[nn]#psn2[.account2]] 
Format 2 for Disk: 
                                    {/[file].account} 
RES[TORE] DP[nn]#psn1 [(sopt_list)] {/(sel_list)    } 
    [{ON|OVER} DP[nn]#psn2[.account]] 
Parameters: 
{CT#nnnn0           } 
{CT#nnnn00          } 
{LT#tsn1[#tsn2] ... }    specifies the tapeset from which to restore files. 
nn    is a 2-digit, user-defined disk resource identifier. 
psn1    specifies the dual packset from which to restore files. 
sopt_list    specifies options describing how the RESTORE is to be performed. 
sopt_list is of the form (so[, so] ... ) where so can be any of the following: 
    DENSITY 
    DELETED ACCOUNTS 
    DIRECTORIES 
    FSN 
    IOERROR CONTINUE 
    PAD 
    {PROTECTED|UNPROTECTED|INCREMENTAL} 
    VOLUME 
DENSITY, FSN, IOERROR CONTINUE and VOLUME may be used for RESTORE from tape 
only. 
See TAPE_OPS, SOURCE_OPS and SEARCH_OPS for complete descriptions. 
sel_list    specifies file selection criteria for the source of the RESTORE 
operation.  Exceptions to this function with RESTORE are discussed below.  See 
SEL_OPS for format. 
psn2    specifies the destination packset. 
account1    identifies a selection account. 
account2    identifies a destination account. 
Description: 
This command allows an operator to restore specific files from backup tapes, 
save tapes, or a dual packset.  The selection criteria specify the fids of 
files to obtain from the designated tapeset or packset.  The packset and 
account to which these files are to be restored is contained within the files 
as stored on the backup tapeset, save tapeset or dual packset, or may be 
designated using the optional ON|OVER, etc.  RESTORE can return files to their 
original packset and account, or to a designated packset and account. 
CAUTION:  A backup tapeset used in file restoration may contain multiple 
versions of the same file, if the EXTEND option was used.  In this case, the 
operator is responsible for specifying the necessary parameters to direct EFT 
to the desired version of the file; otherwise RESTORE searches the tapeset 
starting from the beginning and supplies the most recent version of the file 
that it encounters.  To limit the search performed by RESTORE, the operator 
can supply either a date specification or a range of tapeset file numbers 
(i.e., FSN option). 
Usage Notes: 
1.  Backup of files to tape with the option IDS(FAST) stores only partial 
    information on tape.  If file restoration is necessary for such a file, 
    the operator may perform multiple RESTOREs in the correct sequence - 
    oldest to newest - using the INCREMENTAL option to restore the complete 
    file. 
2.  A RESTORE operation will not restore a partial file with data 
    inconsistencies if part of a restored file is on another tape volume not 
    requested by the user.  In such a case, EFT will delete the partial file, 
    and the EFT output listing will contain the file name followed by "skip 
    ***". 
3.  If the packset granule limit is exceeded during a RESTORE operation, EFT 
    processing is terminated and the step condition code is set to 5. 
4.  Backup of files to tape with the option (ACUP) may store only the file's 
    FIT to tape.  On a file restoration, if a file without data is created as 
    a result of restoring a FIT-only file (this occurs if data for the file 
    does not already exist on the packset), a file with data inconsistencies 
    is created.  The names of these files are maintained in a file called 
    :NODATA in the $$EFT account and may be listed using the STATUS command. 
00002
00001
00003
Format: 
           {CT#nnnn0           } 
RET[RIEVE] {CT#nnnn00          } [(sopt_list)] 
           {LT#tsn1[#tsn2] ... } 
    [FOR DP[nn]#psn1[,DP[nn]#psn2] ... ][{ON|OVER} [DP[nn]#psn3][.account]] 
Parameters: 
{CT#nnnn0           } 
{CT#nnnn00          } 
{LT#tsn1[#tsn2] ... }    specifies the tapeset from which to retrieve files. 
sopt_list    specifies the source option pertaining to the specified tapeset. 
sopt_list can be IOERROR CONTINUE option.  sopt_list is specified in the form 
(so[, so] ...) where so is any of the following options: 
    DUPLICATE TAPESET 
    IOERROR CONTINUE 
See TAPE_OPS for a complete description. 
nn    is a 2-digit, user-defined disk resource identifier. 
psn1, psn2 ...    specifies the packsets to be searched. 
psn3    specifies the destination packset. 
account    specifies the destination account. 
Description: 
The RETRIEVE command causes a search of the packset(s) for files to be FETCHED 
and reads the necessary archive tapesets to obtain the files.  This operation 
applies to the specified packsets, or to all packsets if no packsets are 
specified. 
Usage Note: 
The operator uses the CANT MOUNT keyin if any tape required is unavailable. 
Example: 
*RETRIEVE FOR DP#EFTY 
obtains the files in accounts for DP#EFTY that are queued for FETCH, i.e., 
files which users have requested to be retrieved from the archive tapeset. 
00002
00004
00001
00003
Format: 
RET[RIEVE] {CD#nnnn0              } 
RET[RIEVE] {CD#nnnn00             } [FOR DP[nn]#psn1[, DP[nn]#psn2] ... ] 
RET[RIEVE] {OD#odsn1[#odsn2] ...  } 
RET[RIEVE] {OD#odsn1/file.account;} 
    [{ON|OVER} [DP[nn]#psn3][.account]] 
Parameters: 
{CD#nnnn0 } {CD#nnnn00 } {OD#odsn1[#odsn2] ... } specifies the EFT optical 
diskset from which to retrieve files. 
CD#nnnn0[0]    specifies a five or six digit controlled optical diskset number 
ending in 0 through 99. 
OD#odsn    specifies an optical diskset. 
nn    is a 2-digit, user-defined disk resource identifier. 
psn1, psn2    specifies the packsets to be searched. 
file    specifies a specific file that is to be retrieved. 
account    specifies the source account when a specific file is being 
retrieved or a destination account. 
psn3    specifies the destination packset. 
Description: 
The RETRIEVE command causes a search of the packset(s) to be FETCHed and reads 
the necessary archive optical disksets to obtain the file.  This applies to 
the specified packsets, or to all packsets if no packsets are specified.  If a 
file is specified on the RETRIEVE command, only that file is retrieved.  The 
file is retrieved only if it is queued for FETCH.  In this case, there will 
not be a search for any other files to be FETCHed. 
00002
00001
Format: 
REW[IND] tape 
Parameters: 
tape    is of the form LT#xxxxxx (for labeled tape) or CT#xxxxxx (for EFT 
controlled tapesets). 
Description: 
REWIND rewinds a tape to its beginning or load point. 
Related Commands: 
MOUNT, REMOVE 
00002
00001
00003
Format: 
SA[VE] DP[nn]#psn1[,DP[nn]#psn2] ... [(sopt_list)][/(sel_list)] 
          {CT#nnnn0[,CT#nnnn0]   } 
     OVER {CT#nnnn00 [,CT#nnnn00]} [(topt_list) ] 
          {LT#tsn1[#tsn2] ...    } 
Parameters: 
nn    is a 2-digit, user-defined disk resource identifier. 
psn1,psn2    specify the packsets to be saved. 
sopt_list    specifies a list of options describing how the SAVE is to be 
performed.  sopt_list is of the form (so[, so] ... ) where so may be chosen 
from the following lists of options: 
    All options described under SOURCE_OPS, except DENSITY, FSN, and VOLUME. 
    All options described under SEARCH_OPS. 
    If no Search options are specified, the default is ANYFILE. 
sel_list    specifies criteria for the file selection when a subset of the 
files on a packset is to be saved, in the form [/(ss[, ss] ... )] See SEL_OPS 
for format. 
{CT#nnnn0  [,CT#nnnn0 ]} 
{CT#nnnn00 [,CT#nnnn00]}    specifies the controlled tapeset to receive the 
saved files.  Insert CONTROLLED_TAPESETS for additional information.  If two 
tapesets are specified, a duplicate tapeset is created. 
LT#tsn1[#tsn2] ...    specifies a labeled tapeset in which the user assumes 
complete responsibility for assignment of volume numbers (e.g., #tsn1#tsn2). 
topt_list    specifies options pertaining to storage of the saved files on 
tape.  (topt_list) is of the form (op[,op]...) where op can be any of the 
following: 
    BLOCK 
    CHECK 
    DENSITY 
    EXPIRE 
    IOERROR CONTINUE 
    VOLACCESS 
See TAPE_OPS for complete descriptions. 
Description: 
The SAVE command creates a tape copy of packset account directories, account 
directories, user files and other information to permit later RESTORE 
operations.  According to the time and selection criteria specified, the 
following is saved on tapes: 
o   For BACKUP or DEFAULT BACKUP accounts, SAVE copies the account directory 
    and user files. 
o   For NOBACKUP accounts, SAVE writes only the account directory to tape. 
For each file copied to tape, the file is closed with modification to the 
extended attributes specifying the time and date of the save, and the serial 
number of the tape to which it was copied. 
If selection criteria (sel_list) is not specified, then all files in the 
packset in eligible accounts are saved with the exception of those excluded by 
time criteria ([NOT] MODIFIED or DELTA). 
Files in a NO BACKUP account or files in a BACKUP or DEFAULT BACKUP account 
with the NO BACKUP attribute will not be saved. 
Examples: 
*SAVE DP#FXJ OVER LT#ABCD (DEN=1600,BLOCK=16) 
    Eligible files and other pertinent information from the complete FXJ 
    packset are saved. 
*SAVE DP#FXJ (MOD 01/01/81,00:00)/(A.B - E.F, H.I - K.Z) OVER CT#ABCD0 
    Eligible files and other pertinent information from packset FXJ from fids 
    in the range A.B to E.F and H.I to K.Z are saved if modified since the 
    date specified. 
    SAVE DP#psn1,; 
         DP#psn2,; 
           . 
           . 
           . 
         DP#psnx; OVER CT#TEST00 
00002
00003
00001
Format: 
SCA[N] DP[nn]#psn [(srch_list)] {/(sel_list)    } 
                                {/[file].account} 
Parameters: 
nn    is a 2-digit, user-defined disk resource identifier. 
psn    specifies a packset name. 
srch_list    specifies the search criteria.  (srch_list) is of the form 
(option1[,option2]...) where option can be any of the options listed under 
SEARCH_OPS. 
sel_list    limits the files to be scanned.  sel_list is of the form 'SKIP 
(fid_specifier)' or 'fid_specifier'.  See SEL_OPS for format. 
Description: 
The SCAN command produces formatted reports of specific classes of files.  For 
example, SCAN can list all files on a packset that are currently qualified for 
backup. 
Example: 
*SCAN DP#TSTEFT/(.acct1,.acct2,.acct3,.acct4) 
00002
00003
00001
SEARCH_OPS
The EFT search option list, (srch_list), specifies search criteria in the form 
(option1[,option2]...)  where option can be any of those listed in the 
following table: 
  Option             Meaning                                       Note 
ACT[IVE]           Files queued for STOW active or 
                   ARCHIVEd active.                                 (3) 
ANY[FILE]          Any file including deleted files. 
ARC[HIVE]          Files currently in an archive tapeset            (3) 
                   and files queued for FETCH (QF). 
BAD                Includes files marked as 'bad'.                  (2) 
BUF                Includes file qualified for backup, 
                   i.e., files for which explicit action 
                   (BACKUP command for a file in a BACKUP 
                   account, or file modification for a file 
                   in a DEFAULT BACKUP account) was taken.          (2) 
CG                 File with CG (comgroup) organization.            (3) 
CON[SEC]           File with CONSECUTIVE organization.              (3) 
DELE[TED ACCOUNTS] Deleted account names are reported.              (1) 
DELF               Includes deleted file information.            (1)(5) 
DIR[ECTORIES]      All account names, including those with no 
                   files meeting other options, are reported. 
                   Includes PIG CREATE information.                 (1) 
[NOT] EXP[IRED]    Includes (or does not include) files with 
                   expired date less than current date. 
IDS                File with IDS organization.                      (3) 
INAC[TIVE]         Files queued for STOW inactive or 
                   ARCHIVEd inactive.                            (1)(3) 
IND[EXED]          File with INDEXED organization.                  (3) 
IREL               File with IREL organization.                     (3) 
KEY[ED]            File with KEYED organization.                    (3) 
NOL[IST]           Includes file with 'NOLIST' attribute.           (2) 
PAD                Includes PIG BUILD information. 
QF                 File queued for FETCH.                        (2)(3) 
QS                 File queued for STOW.                         (2)(3) 
QU[EUED]           File queued for either STOW or FETCH.         (2)(3) 
RAN[DOM]           File with RANDOM organization.                   (3) 
REL[ATIVE]         File with RELATIVE organization.                 (3) 
SCR[UB](op[, op] ... ) 
                   Removes from destination file's FIT the 
                   information specified by these options: 
                   BACKUP    Remove time and location of 
                   last backup. 
                   CREATOR    Remove name and account of 
                   file creator. 
                   STOW    Remove time and location of 
                   last ARCHIVE and any pending STOW/FETCH 
                   requests. 
SYM[B]             File with SYMB (symbiont) organization.          (3) 
UR                 File with UR(Unit Record) organization.          (3) 
[NOT] [{ACC[ESSED]   }] [{BEF[ORE]| < }] {DELT[A] = n             } 
      [{BAC[KED] [UP]}] [{SIN[CE ]| >=}] 
      [{CR[EATED]    }] [{AFT[ER] | > }] {mm/dd/yy[,hh:mm[:ss.ss]]} 
      [{MO[DIFIED]   }] [{ON      | = }] 
      [{ST[OWED]     }] 
                   File (not) accessed, created, modified, 
                   backed up, or stowed before, after, on, 
                   or since specified date and time or 
                   within the specified number of hours (n).     (4)(5) 
                   For DELTA= hours, file (not) accessed, 
                   created, modified, backed up, or 
                   stowed in the specified number of 
                   hours prior to the time this 
                   command is parsed, <=9999 hours.                 (4) 
                   Unless the command description states another 
                   default, MODIFIED SINCE is the default. 
Usage Notes: 
The following notes describe restrictions in combining the above search 
options (srch_List). 
1.  These directory-specific options are intended to be used separately when 
    user files are not the primary target of this command. 
2.  These options are used to qualify file names.  For example, if NOLIST is 
    specified, only files with the NOLIST attribute are reported.  If several 
    of these options are specified, then any files with any of the specified 
    options are reported. 
3.  These options are file-specific and are used to restrict the set of files 
    reported.  For example, if RANDOM, QS, and INACTIVE are specified, then 
    only random files that are queued for stow inactive are reported.  If 
    ARCHIVE is used, ACTIVE or INACTIVE must be used. 
4.  DELTA=n and MODIFIED DELTA=n, which have identical meaning, must not be 
    specified in the same command. 
5.  If DELF was specified when a tape was made and DELF is specified for the 
    source packset at an INPUT function, deleted entries obey the same rules; 
    i.e., a source deleted time that is newer than a destination file results 
    in deletion of the destination file. 
00001
SEARCH_OPS
SEL_OPS
The EFT selection list (sel_list) specifies criteria for the file selection of 
a subset of files on a packset.  sel_list is in the form [/(ss[, ss] ... )] 
where ss can be any of the options shown in the following table. 
  fid_specifier 
      Select the specified files or accounts.  fid_specifier can be 
      any one of these forms: 
          filename.account[,filename[.account]] ... 
              The fid must include filename, and if fids for the 
              same account are listed contiguously, only the 
              first fid must include the account.  For example, 
                  A.B,C,E,F,G.I,K,L,M,N 
              means files A, C, E, and F are from account B and 
              files G, K, L, M, and N from account I. 
          filename.account - filename[.account] 
              This form specifies a range of fids.  The first fid 
              must include filename.account.  The second fid may 
              omit .account if all files are from the same 
              account.  For example, 
                  A.G - C 
              means all files from A.G to C.G. 
          filename.account> 
              This form specifies a range of files from the 
              specified filename.account through the end of 
              the current packset. 
  SKI[P] (fid_specifier) 
      Do not select the specified files or accounts.  fid_specifier 
      is the same as explained above. 
Usage Notes for Selection List: 
In specifying the selection list (sel_list), complex lists should be 
avoided.  However, if they are specified, the user should be aware 
of these assumptions made by EFT: 
1.  Overlapping range specifications in sel_list are considered an 
    error.  For example, EFT rejects the sel_list: 
        (.A - .R, .B - .F) 
2.  Specifying an account in sel_list precludes specifying a file in 
    the same account.  For example, EFT rejects 
        (.A - .B, .D, FILE3.A) 
    because of the ambiguity of the references to both account .A and 
    FILE3.A.  However, a list such as 
        (.A - .B, .D, SKIP(FILE3.A)) 
    is acceptable to request a save of accounts.  A through B (except 
    FILE3.A) and of account .D. 
SEL_OPS
SOURCE_OPS
The EFT source option list specifies options pertaining to (sopt_list), and is 
of the form (op[,op]...) where op can be any of the options shown in the 
following list: 
ACUP, DENSITY, CLEANUP, EA, FSN, IDS, EXPIRED, SWITCH, PROTECTED, UNPROTECTED, 
INCREMENTAL, and VOLUME. 
To obtain a HELP message for an individual option, type: 
HELP SOURCE_OPS option 
To view all the options, type: ??. 
  Option    Description 
  ACUP 
            If only the access date of a file has changed since the last save 
            operation, a BACKUP operation writes only the FIT of the file to 
            tape, and a DUAL INCREMENTAL operation updates the access date of 
            the file on the dual packset to reflect the access date of the 
            file on the primary packset. 
            If ACUP is not specified for a BACKUP or DUAL INCREMENTAL 
            operation, the entire file is written to tape or disk. 
  CLE[ANUP] 
            Specifies the removal of deleted files and accounts from the 
            included file directories.  This option is the default during 
            SAVES. 
  DEN[SITY]={800|1600|6250} [BPI] 
            Specifies tape recording density. 
  EA 
            EA (extended attributes) causes an extended listing of file 
            attributes. 
  EXP[IRED] 
            Specifies files with expiration date less than current date. 
  FSN (m  [- n]) 
            Specifies a file sequence number (m) within a set of EFT tapes. 
            If the form (m - n) is specified, only that range of files is 
            used. 
  IDS ({FAST|FULL}) 
            Specifies how to backup IDS files: 
            IDS(FAST) writes only granules with a UTS word greater than the 
            starting time (as reflected in the extended attributes) of the 
            last complete copy of the file which could be on tape or disk. 
            IDS(FULL) writes all granules. 
            The default is IDS(FULL). 
  {PRO[TECTED]|UNP[ROTECTED]|INC[REMENTAL]} 
            Specifies conditions for file restoration: 
            If PROTECTED is specified, the file is restored only if it appears 
            to the user to be deleted. 
            If UNPROTECTED is specified, the file is restored even if it 
            appears to the user that it exists. 
            If INCREMENTAL is specified, the file is restored only if the 
            destination file is older than the file specified as the source 
            (i.e., deleted files on the destination prevent older files from 
            being restored). 
            However, if the file is an IDS file which was backed up using the 
            IDS(FAST) option, restores are performed on a granule basis.  A 
            granule is restored only if the destination granule is older than 
            the source granule. 
            The default is INCREMENTAL. 
            If a contradiction arises when OVER or ON/TO is used in 
            conjunction with the PROTECTED, UNPROTECTED, or INCREMENTAL 
            option, the option takes precedence. 
  SHA[RED] 
            Specifies that EFT should open a file in shared mode (FUN=UPDATE, 
            SHARE=IN).  This keeps the file in "shared update" mode so that if 
            another user attaches to the file during the EFT operation, the 
            file will be available for shared update access when EFT is 
            finished. 
  SWI[TCH] [IF ERR[ORS]] < nn 
            Specifies that the destination packset is to become the prime and 
            the source packset is to become the dual following the copy of the 
            source to the destination if the number of bad file errors is less 
            than nn and both packsets are mounted EXCLUSIVE.  If the packsets 
            are not mounted EXCLUSIVE, the exchange will be performed only 
            after the packsets have been released and then remounted. 
  VOL[UME]=nnn 
            Specifies on which volume the operation is to start.  For 
            instance, for a controlled tapeset CT#ABCD0 of 10 volumes, 
            LT#ABCD0 through LT#ABCD9, LT#ABCD5 is volume 6.  For a labeled 
            tapeset, LT#tsn4 is volume 4. 
00001
00002
00003
00004
00005
00006
00007
00008
00008
00009
00010
00008
00011
SOURCE_OPS
SEARCH_OPS
SEARCH_OPS
SEARCH_OPS
Format: 
                                    [/:BACKUP.$$EFT ] 
STAT[US] [(F[ULL])] [OF] DP[nn]#psn [/:PRIME.$$EFT  ] 
                                    [/:DUAL.$$EFT   ] 
                                    [/:ARCHIVE.$$EFT] 
                                    [/:REBUILD.$$EFT] 
Parameters: 
nn    is a 2-digit, user-defined disk resource identifier. 
psn    specifies the packset for which status is to be reported. 
Description: 
The STATUS command displays the contents of all EFT's control files for a 
given packset or for only the control file specified.  If FULL is specified, 
the complete contents of the file(s) are displayed; otherwise only the most 
recent activity is reported.  The contents of the control files are as 
follows: 
:BACKUP.$$EFT     contains global save and backup information for a packset. 
Whenever a SAVE is performed, the :BACKUP file is reinitialized.  The 
information contained in the :BACKUP file is described below.  Each record 
displayed corresponds to one save or backup operation. 
    Run               the run number of the backup operation described by this 
                      record.  A SAVE is always run number 1.  The first 
                      backup after a SAVE is run number 2, etc. 
    Set               the tapeset number.  This number is incremented and a 
                      new tapeset is started if the last FSN for the current 
                      tapeset has reached the ANSI maximum of 9999 and a new 
                      FSN is needed. 
    VOL               indicates the volume number within a tapeset of the last 
                      tape volume in use when the save or backup completed. 
    Date              the date and time when the save or backup completed. 
    Volume            the tape serial number of the last tape volume in use 
                      when the save or backup completed. 
    FSN               the file sequence number of the last file saved or 
                      backed up during the operation. 
    Accounts Saved 
    first account -   indicates that the save or backup operation began 
    last account      in 'first account' and completed in 'last account'. 
    :BACKUP FSN       is the file sequence number (FSN) of the :BACKUP.$$EFT 
                      file saved for backup during the operation. 
:PRIME.$$EFT    resides on the prime packset and contains a record of the dual 
operations performed.  Whenever a DUAL ALL operation is executed, the :PRIME 
file is reinitialized.  The first record in the file contains the volume 
serial number (VSN) identifiers of the prime and dual packsets, and the date 
and time when the last DUAL ALL operation began.  Subsequent records contain 
the same information for DUAL INCREMENTAL operations performed since the last 
DUAL ALL. 
:DUAL.$$EFT    resides on the dual packset and contains an exact copy of the 
associated :PRIME.$$EFT file. 
:ARCHIVE.$$EFT    contains the attributes of the archive tapeset (BLOCK, 
CHECK, DENSITY, EXPIRE, IOERROR CONTINUE, VOLACCESS), the names of the master 
and member packsets contained in the archive set, and the serial numbers of 
currently available tapes in the archive tapeset and any duplicate tapeset. 
The ESTABLISH command is used to create and initialize the :ARCHIVE file. 
Subsequently, the MODIFY command may be used to alter archive tapeset 
characteristics. 
:REBUILD.$$EFT    contains rebuild information for a packset and only exists 
if a prior rebuild operation was terminated as a result of an abort, such as a 
system crash or a tape read error.  This information permits EFT to continue a 
rebuild operation at the point of interruption.  The following information is 
contained in the :REBUILD file: 
    Volume          the tape serial number of the tape volume in use when the 
                    interruption occurred. 
    VOL             the volume number within a tapeset of the tape volume in 
                    use when the interrupt occurred. 
    FSN             the file sequence number (FSN) of the last file restored. 
    Last Account    the last account restored. 
    Last File       the last file restored. 
    DENSITY         the tape density of the tape volume being restored. 
    PAD             indicates whether the packed account directory FIT was to 
                    be restored. 
    DIR             indicates whether the file directory FITS were to be 
                    restored. 
    IOERR CONT      indicates whether processing should continue after an 
                    irrecoverable tape I/O error. 
:NODATA.$$EFT   contains a list of partially restored files which contain no 
data, and is updated whenever a RESTORE or REBUILD operation is performed. 
Examples: 
*STAT DP#FXJ 
    This command reports only the most recent activity for all EFT control 
    files on FXJ. 
*STAT DP#FXJ/:PRIME.$$EFT 
    This command reports the last DUAL operation as well as the makeup of the 
    dual packset. 
*STAT DP#FXJ/:BACKUP.$$EFT 
    This command reports the last BACKUP operation. 
*STAT DP#FXJ/:ARCHIVE.$$EFT 
    This command reports the last ARCHIVE operation. 
*STAT DP#FXJ/:REBUILD.$$EFT 
    This command reports the last aborted REBUILD operation. 
*STAT DP#FXJ/:NODATA.$$EFT 
    This command lists partially restored files which contain no data. 
00002
00003
00001
EFT uses step condition codes (STEPCC) to report specific events as listed 
below. 
  STEPCC Value    Description 
     0          No error. 
     1          Minor error (e.g., data inconsistency). 
     2          Serious non-I/O error (e.g., syntax error). 
     3          Disk I/O error. 
     4          Tape I/O error, optical disk I/O error or optical 
                disk granule limit exceeded. 
     5          Disk packset not available or packset granule limit 
                exceeded. 
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
    file creator or has DELF access, or b) the account is authorized with the 
    STOW attribute and the current user has FMSEC privilege active. 
2.  While the file is queued for STOW or FETCH, it cannot be updated. 
00002
00001
00003
CONTROLLED_TAPESETS
    The tape option, IOERROR CONTINUE, specifies whether or not processing 
    should continue after an irrecoverable tape read or write error.  The 
    following headings discuss handling of irrecoverable tape I/O errors, if 
    IOERROR CONTINUE = YES is requested.  Type ?? for more information. 
Tape Read Error 
When an irrecoverable tape read error occurs, reading continues from the 
current volume depending upon whether or not data exists beyond where the 
error is encountered.  If data exists, EFT continues by skipping over the bad 
part of the tape, reading the next good block, and searching for the beginning 
of the next file.  If data does not exist, EFT rolls over to the next volume 
of the tapeset.  A partially copied file is deleted from disk.  In the case of 
a file retrieval, an unretrieved file remains in the queued-for-fetch state. 
The output listing reflects the name of the file that could not be read 
followed by an error message stating that a number of files may have been 
skipped. 
Tape Write Error 
When an irrecoverable tape write error occurs, the operator is informed that 
EFT is having difficulty writing to tape and is queried whether to abort or to 
continue writing to the next volume of the tapeset.  If the operator elects to 
abort, the message "Job aborted by operator" is written to the output listing. 
In an archiving operation, all files contained in the last block that did not 
get written to tape will be kept in queued-for-stow state.  If the operator 
elects to continue, EFT rolls over to the next volume of the tapeset. 
If data was already written to the current EFT_RESTRICT_FILE on tape, the last 
block of the EFT_RESTRICT_FILE is read and rewritten to the next volume.  This 
is performed to enable EFT to write an EFT_CVOL_FILE to an error-free portion 
of the tape.  The following error message is written to the output listing to 
reflect this activity:  "Due to the preceding error, filename.acct was 
rewritten to LT#tsn".  For archive and save operations, the FITs of the 
rewritten files are updated to reflect the new file sequence and serial 
numbers. 
If a write error occurs at the beginning of a tape, the previous tape is 
mounted (if one exists) and the EFT_CVOL_FILE is rewritten.  The operation 
continues after requesting a replacement tape. 
00001
00002
The EFT tape option list (topt_list) specifies options pertaining to storage 
of the backup files on tape.  (topt_list) is of the form 
(option1[,option2]...) where option can be any of the options shown in the 
following list: 
BLOCK, CHECK, DENSITY, DUPLICATE TAPESET, EA, EXPIRE, EXTEND, FSN, IOERROR 
CONTINUE, PROTECTED, UNPROTECTED, INCREMENTAL, RING, NORING, VOLACCESS, 
VOLUME. 
To obtain a HELP message for an individual option, type: 
HELP TAPE_OPS option 
To view all the options, type ??. 
  Option    Description 
  BLOCK=nn 
            Specifies the maximum physical tape block size in pages (4096 
            bytes each). The maximum is 21; the minimum is 6; the default is 
            8. 
  CHE[CK] {[=Y[ES]]|=N[O]} 
            Specifies, if set YES, to perform automatic tape checking.  The 
            automatic check is performed after the initial command function 
            (for example, SAVE) is complete.  No cleanups or deletions are 
            performed until after the check completes successfully.  In case 
            duplicate tapesets and automatic tape checking are both specified, 
            both tapesets specified will be checked.  CHECK checks only that 
            which was written during the previous EFT operation. 
  DEN[SITY]={800|1600|6250} [BPI] 
            Specifies tape recording density. 
  DU[PLICATE] [T[APESET]] 
            Indicates the source tape specified on the RETRIEVE command is a 
            duplicate archive tapeset.  The check to determine if the correct 
            archive tapeset has been specified for retrieving files, by 
            comparing with the STOW tape in a file's FIT, is bypassed. 
  EA 
            EA (extended attributes) causes an extended listing of file 
            attributes. 
  EXP[IRE]={ddd|NEVER} 
            Specifies the days remaining until expiration. 
  EXTEND 
            For a tape output operation (e.g., BACKUP), EXTEND causes the 
            volume set to be positioned after its last file before starting 
            output. 
  FSN (m  [- n]) 
            Specifies a file sequence number (m) within a set of EFT tapes. 
            If the form (m - n) is specified, only that range of files is 
            used. 
  IO[ERROR] C[ONTINUE] {[=Y[ES]]|=N[O]} 
            Specifies whether processing should continue after the occurrence 
            of an irrecoverable tape read or write error.  By default, when 
            IOERROR CONTINUE is not specified, the operation is terminated. 
            For additional information, see the topic TAPE_IO_ERROR. 
  VOLA[CCESS]={N[ONE]|A[LL]|I[N]} 
            Indicates labeled tape volume set access limitations. 
            NONE specifies that only the owner of the volume set (account of 
            user creating first file on the volume set) will be allowed access 
            to this volume set. 
            ALL specifies that all may read or write the volume set. 
            IN specifies that all may read the volume set, but only the owner 
            may write on it. 
            The system default is ALL. 
  VOL[UME]=nnn 
            Specifies on which volume the operation is to start.  For 
            instance, for a controlled tapeset CT#ABCD0 of 10 volumes, 
            LT#ABCD0 through LT#ABCD9, LT#ABCD5 is volume 6.  For a labeled 
            tapeset, LT#tsn4 is volume 4. 
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
DATE
TAPE_OPS
Format: 
Format 1 for UPDATE or INPUT: 
DP[nn]#psn1 [(srch_list)] [/(sel_list)] 
    {TO                } 
    {OVER              } DP[nn]#psn2[/.acct] 
    {INCR[EMENTALLY] TO} 
Format 2 for CREATE or EXTEND: 
DP[nn]#psn1 [(srch_list)] [/(sel_list)] [OVER DP[nn]#psn2] 
Parameters: 
nn    is a 2-digit, user-defined disk resource identifier. 
psn1    specifies the source of the transfer or transport operation for the 
UPDATE, CREATE, or EXTEND functions.  For the INPUT function, psn1 specifies 
that psn1 accounts or files from the tapeset specified at OPEN are the source. 
Note:  Only one source packset (psn1) can be specified per command line. 
psn2    specifies the destination packset for UPDATE and INPUT functions.  For 
CREATE, EXTEND, or INPUT psn2 requests a change of the packset of origin to 
psn2 for accounts or files as copied to the destination. 
srch_list    specifies the search and access criteria.  (srch_list) is of the 
form (option1[,option2]...) where option may be chosen from the following list 
of options: 
Any option listed under the topic SEARCH_OPS 
SHARED option, described under the topic SOURCE_OPS 
sel_list    specifies the files to be processed.  See SEL_OPS for format. 
TO    specifies that the copy is to occur only if the file does not exist on 
the destination. 
OVER    specifies that the copy is to always occur. 
INCR[EMENTALLY] TO    specifies that the copy is to occur only if the source 
file is newer. 
Note:  If DELF was specified when a tape was made and DELF is specified for 
the source packset at an INPUT function, deleted entries obey the same rules; 
i.e., a source deleted time that is newer than a destination file results in 
deletion of the destination file. 
acct    specifies the account in which files are to be written on the 
destination packset.  This option is not allowed if DIRECTORIES is also 
specified.  Use of this option automatically forces SCRUB(BACKUP, STOW).  The 
default is the account name from which the files are read. 
Description: 
The transfer and transport specifications present search, access, and 
selection criteria for the transfer or transport operation.  They specify the 
source from which accounts and files are to be copied.  For the UPDATE and 
INPUT function, they specify the destination packset and conditions for 
writing files to the destination packset. 
00002
00001
TRANSFER_TRANSPORT
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
2.  An inactively archived file must be fetched and retrieved before it can be 
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
Format: 
UNF[ETCH] fid1[, fid2] ... 
Parameters: 
fid1, fid2    specify CP-6 file identifiers. 
Description: 
This command rescinds a FETCH request, unlocking the specified files.  For any 
specified file not currently queued for FETCH, an error is reported.  UNFETCH 
can be used on a file only by the creator of the respective FETCH request or 
by persons with active FMSEC privileges. 
Usage Note: 
The specified fid may include a password, however, it cannot be verified and 
is ignored. 
00002
00001
00003
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
    STOW attribute and the current user is the file creator or has DELF 
    access, or b) the account is authorized with STOW and the current user has 
    FMSEC privilege active. 
2.  While the file is queued for STOW or FETCH, it cannot be updated. 
00002
00001
00003
Format: 
VAL[IDATE] DP[nn]#psn [(srch_list)] [/(sel_list)] 
Parameters: 
nn    is a 2-digit, user-defined disk resource identifier. 
psn    specifies the packset to be validated. 
srch_list    specifies the search criteria and includes all of the options 
listed under SEARCH_OPS except that the DELF, DELETED ACCOUNTS, INACTIVE and 
DIRECTORY options cannot be specified. 
sel_list    limits the files on the packset to be validated.  sel_list is of 
the form 'SKIP (fid_specifier)' or 'fid_specifier'.  See SEL_OPS for format. 
Description: 
This command validates that the complete packset or the specified files can be 
read in BLOCK mode.  For any file processed that has the 'BAD' bit set but can 
be read by VALIDATE without errors, the 'BAD' bit is reset, and this condition 
is reported. 
00002
00001
Format: 
WH[ERE] DP[nn]#psn {/(sel_list)    } 
                   {/[file].account} 
Parameters: 
nn    is a 2-digit, user-defined disk resource identifier. 
psn    specifies a packset name. 
sel_list    limits the files selected.  sel_list is of the form 'SKIP 
(fid_specifier)' or 'fid_specifier'. 
Description: 
The WHERE command is used to retrieve information from a catalog file.  After 
a catalog file has been specified using a CATALOG command, WHERE commands can 
be issued to determine which tapes contain specific files or ranges of files 
that have been backed up, saved, archived, or purged. 
The output format is similar to the regular output format; however, the 
date/time of the operation that caused the catalog file to be updated is given 
for each file. 
Related Commands: 
CATALOG 
00002
00001
00003
