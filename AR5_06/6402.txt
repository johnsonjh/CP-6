Portions of the File Information Table (FIT) can be viewed by calling the 
M$OPEN monitor service specifying FPARAM.  Library services discussed next 
give access to the FIT data returned in the FPARAM buffer. 
FIT data is organized by sections each of which is associated with a code. 
The FIT contents varies for each file type.  The FIT for one file type may 
include 02 and 03 data; whereas the FIT for another file type may include 03 
and 04 data.  Macros which define each data section are discussed in this 
section and are identified by code number. 
After file opening, the user calls one of the library services provided to 
obtain access to the desired data section within the FPARAM buffer.  By 
invoking a macro for the appropriate data section (e.g., %CODE03; ), the user 
can access the data using the defined names (e.g., CODE03.DESC.QS) for that 
particular section of the FIT. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1992 
  ************************************************************** 
CODE01 contains items which are always in the FIT, but are not included in the 
FPARAM buffer. 
CODE02 contains items which are in the FIT and FPARAM buffer for KEYED and 
INDEXED files. 
    GDA = VALUE-DEC(0-n) Contains the file relative disk address of the last 
    unfilled data blocking granule. 
    KEYL = VALUE-DEC(1-255)  See M$OPEN. 
    KEYX = VALUE-DEC(0-32K)  See M$OPEN. 
    LRDL0 = VALUE-DEC(1-511)  See M$OPEN. 
    LSLIDE = VALUE-DEC(1-511)  See M$OPEN. 
    SLIDE = VALUE-DEC(0-511) Contains the number of level 0 Master Index 
    granules in the file if level 1 does not exist.  Otherwise, SLIDE contains 
    the number of level 0 Master Index granules which have been added since 
    the last time the upper level index was rebuilt. 
    SPARE = VALUE-DEC(0-511)  See M$OPEN. 
    TDA = VALUE-DEC(0-n) Contains the file relative disk address of the first 
    index granule at the top of the multi-level index structure.  If no such 
    structure exists, TDA contains zero. 
    TDALVL = VALUE-DEC(0-511) Contains the level number of the top level of a 
    multi-level key structure, i.e., the level of TDA. 
00001
00002
00003
00004
00005
00006
00007
00008
00009
CODE03 contains items which are always in the FIT and the FPARAM buffer. 
    COMP = {YES|NO}  See M$OPEN. 
    DESC.ACTIVE = VALUE-BIT(1).  See M$DCB. 
    DESC.ARCHIVE = VALUE-BIT(1).  See M$DCB. 
    DESC.BAD = VALUE-BIT(1)  See M$DCB. 
    DESC.BUF = VALUE-BIT(1)  See M$DCB. 
    DESC.BUPM = VALUE-BIT(1)  See M$DCB. 
    DESC.DELF = VALUE-BIT(1)  See M$DCB. 
    DESC.FETCH = VALUE-BIT(1).  See M$DCB. 
    DESC.NBUF = VALUE-BIT(1)  See M$DCB. 
    DESC.NOLIST = VALUE-BIT(1)  See M$DCB. 
    DESC.ODSTOW = VALUE-BIT(1)  See M$DCB. 
    DESC.QS = VALUE-BIT(1).  See M$DCB. 
    DESC.TERMINATE = VALUE-BIT(1).  See M$DCB. 
    DESC.TPB = VALUE-BIT(1).  See M$DCB. 
    EXPIRE = VALUE-DEC(<0-16K)  See M$OPEN. 
    GHSTACS = VALUE-DEC(0-15)  See M$OPEN. 
    LDA = VALUE-DEC(0-n) Contains the file relative disk address of the last 
    level 0 granule. 
    NGAVAL = VALUE-DEC(1-n)  Contains the number of unused granules available. 
    NRECS = VALUE-DEC(0-n) Contains the current number of records or total 
    number of records if the file is RELATIVE. 
    NSTAMP = Irreversibly scrambled name for RMA purposes. 
    ORG = OPTION  See M$OPEN. 
    RCSZ = VALUE-DEC(0-511) Contains a value one less than the number of pages 
    (1024 words) required to contain the largest record in the file. 
    RECL = VALUE-DEC(1-32K)  See M$OPEN. 
    TYPE = VALUE-CHAR(2)  See M$OPEN. 
    UGRANS = VALUE-DEC(1-n) Contains the current number of granules occupied. 
    UGRANS does not include NGAVAL. 
    XTNSIZE = VALUE-DEC(1-32K)  See M$OPEN. 
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
CODE04 contains dates which are required by or supplied by the monitor. This 
entry is not made for STAR files.  Each DATE/TIME field is represented as a 
UTS, which can be converted to other forms via the M$TIME service.  Only 
CREATION, MODIFY, and ACCESS are moved to FPARAM unless the user has FMSEC 
privilege. 
    ACCESS.TIME = VALUE-DEC(0-n) Contains the UTS date/time of the last 
    non-TEST open unless CODE14.ACCESS.NOACUP is set for the account. 
    CREATION.TIME = VALUE-DEC(0-n) Contains the UTS date/time of file or 
    directory creation. 
    CREATOR.ACCT = VALUE-CHAR(8) Contains the account of the creator of the 
    file.  This field is used for accounting purposes and is not returned in 
    in the FPARAM buffer. 
    CREATOR.NAME = VALUE-CHAR(12) Contains the name of the creator of the 
    file.  This field is used for accounting purposes and is not returned in 
    the FPARAM buffer. 
    GAC.N = VALUE-DEC(0-n) Contains the storage integral in floating point 
    form, i.e., the number of granules occupied by the file multiplied by the 
    number of .01 second intervals since the last granule accounting function 
    was performed for the packset.  See the System Support Reference Manual 
    for further information on PIG. 
    GAC.TIME = VALUE-DEC(0-n) Contains the UTS date/time of the last update to 
    GAC.N. 
    MODIFY.TIME = VALUE-DEC(0-n) Contains the UTS date/time of the last file 
    update or file directory modification. 
    SVMODIFY.TIME = VALUE-DEC(0-n) Contains the value of MODIFY at the time 
    the file is opened for updating.  At that time, MODIFY is changed to 
    reflect the date/time at the open.  At file closing if the file was not 
    modified, MODIFY is reset to SVMODIFY so that it appears that the file was 
    not opened for updating. 
00001
00002
00003
00004
00005
00006
00007
00008
CODE05 contains the backup date/time and reel or packset number.  This entry 
is not made for STAR files. 
    BACKUP.EFT.CROSS = VALUE-BIT(1) Is set when the file spans more than one 
    tape volume. 
    BACKUP.EFT.FSN = VALUE-DEC(0-n) Contains the tape file sequence number 
    containing the "BACKED UP" copy of the file. 
    BACKUP.REEL = VALUE-CHAR(6) Contains the reel number or packset name of 
    the backup medium, left-justified. 
    BACKUP.TIME = VALUE-DEC(0-n) Contains the UTS date/time at which file 
    backup occurred. 
00001
00002
00003
00004
CODE06 contains the STOWed UTS date/time and reel number.  This entry is not 
made for STAR files.  For STOWed inactive files, this is the only entry in the 
FPARAM buffer. 
    STOW.EFT.CROSS = VALUE-BIT(1) Is set when the file spans more than one 
    tape volume. 
    STOW.EFT.FSN = VALUE-DEC(1-9999) Contains the File Sequence Number of the 
    file on the archive volume set which contains this file. 
    STOW.EFT.INACTIVE = VALUE-BIT(1) Is set when the file is stowed inactive. 
    STOW.ODFSN = VALUE-DEC(1-262143) Contains the File Sequence Number of the 
    file on the archive volume set which contains this file.  This is only 
    used for files stowed on optical disk. 
    STOW.REEL = VALUE-CHAR(6) Contains the reel number of the STOW tape, 
    left-justified. 
00001
00002
00003
00004
00005
CODE07 contains the scrambled password.  This entry is not made for STAR 
files. 
    PASS = VALUE-CHAR(8)  Contains the irreversibly scrambled password. 
00001
The macro FITALTKEYS contains alternate index information for indexed files. 
The code for this entry is 8. 
    ALTBLD = VALUE-BIT(1).  Set if alternate indices must be built or rebuilt. 
    K = ARRAY(0:511) One entry per index currently defined. Entry number zero 
    (of the array K) is the primary index of the file (corresponding to INDX=1 
    on data manipulation Monitor Services). Entry number n is the nth 
    alternate index and corresponds to INDX=n+1. 
    K.DUPKEY = VALUE-BIT(1) Set if any duplicate keys were found in this index 
    the last time it was built or rebuilt. 
    K.FDA = VALUE-DEC  Disk address of beginning of this index. 
    K.KEYL = VALUE-DEC(0-255)  Length of key for this index. 
    K.KEYX = VALUE-DEC(0-65000).  Byte index in record to start of this 
    index's key. 
    K.LDA = VALUE-DEC  Disk address of end of this index. 
    K.TDA = VALUE-DEC Disk address of top of upper level index structure for 
    this index. 
    K.TDALVL = VALUE-DEC(1-4).  Level number of the granule pointed to by TDA. 
    K.UNIQUE = VALUE-BIT(1)  Set if keys in this index are to be unique. 
    MINWRSIZE = VALUE-DEC(1-4095) The minimum record size that can be written. 
    Calculated by finding the largest value for KEYX+KEYL for all indices. 
    NUMENTS = VALUE-DEC(1-21)  Number of indices currently defined. 
    NUMWRDS = VALUE-DEC(1-511) Number of words in this structure. 
    UNIQUEBLD = VALUE-BIT(1) Indicates whether or not indexes marked as UNIQUE 
    need to be rebuilt. 
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
CODE09 describes one entry of an account access control list.  CODE09 is 
repeated (UNALIGNED) as many times as required.  This information, if present, 
is moved to FPARAM buffer. 
    ACCT = VALUE-CHAR(8) Contains the account to which the CODE09.FFLG bits 
    apply. 
    FFLG.AU = VALUE-BIT(1)  See M$DCB. 
    FFLG.AURD = VALUE-BIT(1)  See M$DCB. 
    FFLG.CREATE = VALUE-BIT(1)  See M$DCB. 
    FFLG.DELF = VALUE-BIT(1)  See M$DCB. 
    FFLG.DELR = VALUE-BIT(1)  See M$DCB. 
    FFLG.EXEC = VALUE-BIT(1)  See M$DCB. 
    FFLG.NOLIST = VALUE-BIT(1) If set, in a file, the file's existence cannot 
    be determined.  If set in a directory, files appear not to exist and 
    access cannot be gained via specific file access control.  If CODE09.FFLG 
    for a directory contains all zeros or if only CODE09.FFLG.CREATE is set, 
    the default access to the files is NOLIST, but this can be overridden by 
    specific access control. 
    FFLG.READ = VALUE-BIT(1)  See M$DCB. 
    FFLG.REATTR = VALUE-BIT(1)  See M$DCB. 
    FFLG.TCTL = VALUE-BIT(1)  See M$DCB. 
    FFLG.UPD = VALUE-BIT(1)  See M$DCB. 
    FFLG.WNEW = VALUE-BIT(1)  See M$DCB. 
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
CODE10 describes one entry of the vehicle access control list.  The format is 
repeated as necessary.  Only the space required is used. 
    ACSVEH Contains the access vehicle (processor) name in TEXTC format. The 
    vehicle is assumed to be in the system account, the same account as the 
    file being accessed, or the specified account, depending on the format of 
    the vehicle name. 'Name' implies the system account, 'name.' implies the 
    account of the file, and 'name.account' specifies the account explicitly. 
    FFLG.AU = VALUE-BIT(1)  See M$DCB. 
    FFLG.AURD = VALUE-BIT(1)  See M$DCB. 
    FFLG.DELF = VALUE-BIT(1)  See M$DCB. 
    FFLG.DELR = VALUE-BIT(1)  See M$DCB. 
    FFLG.EXEC = VALUE-BIT(1)  See M$DCB. 
    FFLG.NOLIST = VALUE-BIT(1)  See M$DCB. 
    FFLG.READ = VALUE-BIT(1)  See M$DCB. 
    FFLG.REATTR = VALUE-BIT(1)  See M$DCB. 
    FFLG.TCTL = VALUE-BIT(1)  See M$DCB. 
    FFLG.UPD = VALUE-BIT(1)  See M$DCB. 
    FFLG.WNEW = VALUE-BIT(1)  See M$DCB. 
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
CODE11 contains information specified by UATTR on M$OPEN or M$CLOSE. No 
structure is provided as it is not used by the CP-6 system. 
CODE12 contains information specified by INSTATTR on M$OPEN or M$CLOSE. No 
structure is provided as it is not used by the CP-6 system. 
CODE13 contains information specified by PROCATTR on M$OPEN or M$CLOSE. No 
structure is provided as it is not used by the CP-6 system. 
CODE14 contains the account and file directory information. 
    ACCESS.BUPF = VALUE-BIT(1) If set, specifies that file backup is 
    permitted. 
    ACCESS.BUPM = VALUE-BIT(1)  Contains the default for BUPM. 
    ACCESS.GACSHELF = VALUE-BIT(1) Applies to the account directory only. If 
    set, shelf-time is to be accounted separately from on-line time, which 
    means that a GAC run is required every time the packset is mounted. 
    ACCESS.LIST = VALUE-BIT(1) If set, a CODE09 access control list exists for 
    the directory 
    ACCESS.MERGEAC = VALUE-BIT(1) If set, file access control (CODE09) appears 
    to be concatenated on the end of the account access control (also CODE09), 
    instead of replacing it. 
    ACCESS.NEWFD = VALUE-BIT(1) Applies to the account directory only. If set, 
    new file directories may be created automatically. 
    ACCESS.NOACUP = VALUE-BIT(1) If set, the access date is not to be 
    maintained. 
    ACCESS.NOSTOW = VALUE-BIT(1) If set, files in the account may not be 
    stowed. 
    ACCESS.NPUR = VALUE-BIT(1)  If set, files are not to be purged. 
    ACCESS.OWNERF = VALUE-BIT(1)  If set, users in the account own its files. 
    ACCESS.WCDATA = VALUE-BIT(1) If set, specifies that non-directory writes 
    for the account are to be done with checkwrite operations. 
    ACCESS.WRCMP = VALUE-BIT(1) If set, specifies that directory writes for 
    the account are to be done with checkwrite operations. 
    CGMEM = VALUE-DEC(0-511) Contains the maximum memory (measured in 
    %CGMEMSIZK increments) permitted to comgroups in this account at any given 
    time. 
    CGRANS = VALUE-DEC(0-n) Applies to file directories only. CGRANS specifies 
    the current number of granules in this account. 
    DFLTALL = VALUE-BIT(18) Contains default access control flags for files. 
    The DFLTALL flags can be overridden by a CODE09 entry in the directory or 
    by a specific file's access control. See CODE09.FFLG for the format and 
    meaning of the DFLTALL flags. 
    MGRANS = VALUE-DEC(0-n) Contains the maximum granules occupied by files 
    within an account.  MGRANS is specified in the account directory for use 
    when a new file directory is created.  MGRANS is specified in a file 
    directory as the granule authorization for the account. 
    OWNER Contains an array of the account/ name of user(s) authorized to 
    modify account/set attributes.  This information is not returned in the 
    FPARAM buffer.  The array is of size (0:MAX).  The default for MAX is 
    zero, and may be changed by specifying MAX=value on the macro invocation 
    line. 
    OWNER.ACCT = VALUE-CHAR(8) Contains the account of an owner. 
    OWNER.NAME = VALUE-CHAR(12) Contains the name of an owner. 
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
CODE15 contains Comgroup file information. 
    CGORG = OPTION (see ORG in M$DCB). 
    QISS = {YES|NO}.  See QISS in M$DCB. 
00001
00002
This information is in the FIT and FPARAM buffer, and is moved to a memory 
area pointed to by F$DCB.FORM$ when a DCB is open to the file. 
    ATTR = VALUE-BIT(18)  See M$OPEN. 
    BANNER_CHARGES = VALUE-BIT(1) if BANNER_CHARGES is '1'B then the number of 
    pages in BANNER_REPEATS should be added to the number of pages accounted 
    for in this file.  If BANNER_CHARGES is '0'B, then no charge is made. 
    BANNER_REPEATS = VALUE-DEC(1-511) This field is kept for accounting 
    purposes only.  It contains the number of repeats for the banner to print 
    at the start of output. 
    COMODE = VALUE-BIT(1)  Set if concurrent output mode. 
    CONTFORM = VALUE-BIT(1) Set if the form describes continuous line-printer 
    paper (Limbo and Firstline zero) 
    COPIES = VALUE-DEC(1-511) Contains the number of times output is to be 
    sent to the destination device. 
    DDEV = VALUE-BIT(9)  See M$DCB. 
    DEV = VALUE-CHAR(2)  Contains the destination device type. 
    DVFC = VALUE-CHAR(1)  Contains the default printer VFC character. 
    FORM = VALUE-CHAR(6) Contains the name of the form to be mounted on the 
    device. 
    GOOD = VALUE-BIT(1)  Is an internal flag for form verification. 
    LINENO = VALUE-DEC(0-n) Contains the current line number in a printer 
    file. 
    LINES = VALUE-DEC(1-32K)  Contains the number of lines in a printer page. 
    NBANNER_RECS = VALUE-UBIN(18) Contains the number of records in the banner 
    of a symbiont file.  This is used to eliminate symbiont files which only 
    have banner information in them after recovery from a crash. 
    NOTCOL1 = VALUE-BIT(1) Set if the current printer line has been printed 
    on. 
    NSFORM = VALUE-BIT(1) Set if FORM is not the installation's standard form 
    for device type DEV at workstation WSN. 
    OLDSEQ.SEQCOL = VALUE-DEC(1-255) Contains the SEQCOL value from the last 
    Set Sequencing record written to the file.  This must be appended to the 
    next Set Sequencing record so that punch symbiont files can be efficiently 
    backspaced. 
    OLDSEQ.SEQID = VALUE-CHAR(4) Contains the SEQID from the last Set 
    Sequencing record written to the file.  This must be appended to the next 
    Sequencing record so that punch symbiont files can be efficiently 
    backspaced. 
    OLDTABS = ARRAY(0:31) Contains the tab settings from the last Set Tabs 
    record written to the file.  This information must be appended to the next 
    Set Tabs record so that symbiont files can be efficiently backspaced. 
    PAGEBASE = VALUE-DEC(0-n) Contains a number to be subtracted from PAGENO 
    to produce printer page numbering. 
    PAGENO = VALUE-DEC(0-n)  Contains the number of printer pages in the file. 
    RECNO = VALUE-DEC(0-n)  Contains the number of punch records in the file. 
    STEPPAGENO = VALUE-DEC(0-n) Contains the last PAGENO tallied for 
    accounting purposes. 
    STEPRECNO = VALUE-DEC(0-n) Contains the last RECNO tallied for accounting 
    purposes. 
    VFCIM.LINE = ARRAY(0:31) Contains an array of line numbers (1-511). 
    Entries 1 through 15 are the line numbers of the first occurrences of 
    channels 1 through 15 in the VFC image.  Entries 16 through 31 are for 
    not-first occurrences, linked through VFCIM.NEXT. 
    VFCIM.NEXT = ARRAY(0:31) Contains an array of indexes into VFCIM. A 
    non-zero entry means that there is another occurrence of the channel at 
    line number VFCIM.LINE (this value). 
    WIDTH = VALUE-DEC(1-511)  Contains the output width of the device. 
    WSN = VALUE-CHAR(8)  Contains the destination workstation. 
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
CODE17 contains information specified by FPRG on M$OPEN.  The VLP_FPRG macro 
is used to generate the CODE17 structure.  This information is found in the 
FIT and the FPARAM buffer and is moved into the read-only segment during open. 
It may be located at an offset of F$DCB.FPRGX from B$ROSEG$. 
This information is in the FIT and FPARAM buffer.  It may be in Keyed, 
Indexed, Consecutive, Relative, and IREL files.  It represents the physical 
order of fields in a record, including a data type and length for each field 
specified. Its structure is identical to VLP_RECFIELD. 
    DECFIELD - The array used for decimal fields in a record.  Length values 
    are in bytes for data types: 
    UDNS, UDLS, UDTS, UDLO, UDTO, and UDFLT.  Length values are in nibbles for 
    data types:  PDTA, PDTE, PDNS, PDLA, PDLE, PDFLT, DATE, and TIME. 
    DECFIELD.LEN = VALUE-DEC(1-63) The length of the field. 
    DECFIELD.SCALE = VALUE-DEC(-32 - 31) The scale factor for decimal fields. 
    DECFIELD.TYPE = VALUE-DEC(0-63) specifies the data type of the field.  Use 
    data type definitions found in the %VREBL_DATATYPES macro in the 
    B$OBJECT_C include file. 
    FIELD - The array used for non-decimal fields in a record. Length values 
    are in bytes for data types:  NO, SFLT, DFLT, CHAR, TEXTC, and TEXTH. The 
    length value for data type LIST determines the number of elements in the 
    list (array).  The length for data type VLIST contains the index into 
    CODE18.FIELD or CODE18.DECFIELD of the count field which determines the 
    number of elements in the variable length list.  Length values are in bits 
    for data types: SBIN, UBIN, and UTS. 
    FIELD.LEN = VALUE-DEC(1-4095) The length of the field. 
    FIELD.TYPE = VALUE-DEC(0-63) specifies the data type of the field.  Use 
    data type definitions found in the %VREBL_DATATYPES macro in the 
    B$OBJECT_C include file. 
    NFIELDS = VALUE-DEC(0-511) specifies the number of elements in the 
    CODE18.FIELD or CODE18.DECFIELD array. 
    VLPID = VALUE-DEC(511) specifies the identifier which differentiates a 
    VLP_RECFIELD from other VLPs which may be specified in the same vector 
    location on an M$OPEN or M$CLOSE. Although this value is only useful in a 
    VLP_RECFIELD, it is carried in the CODE18 as well. 
00001
00002
00003
00004
00005
00006
00007
00008
00009
This information is in the FIT and FPARAM buffer.  It applies to IREL files 
only.  It contains user supplied information about the keys and is identical 
to VLP_IRKEYS. 
    FIELDN = VALUE-DEC(0-511) Specifies the field number (index into a CODE18 
    or VLP_RECFIELD field array) for this key fragment. 
    KEYEND = VALUE-BIT(1) Specifies the end of a new key definition. 
    NKEYS = VALUE-DEC(0-n)  Contains the number of keys defined in the file. 
    UNIQUE = VALUE-BIT(1) Specifies that this key must be unique.  UNIQUE is 
    only meaningful for the first field of a key. 
00001
00002
00003
00004
This information is in the FIT only.  It applies to IREL files only.  CODE20 
contains information necessary for file management, but not the user. 
    ALTBLD = VALUE-BIT(1) Indicates whether the alternate keys need to be 
    rebuilt. 
    CDA = VALUE-DEC(0-n) Contains the file relative disk address of the first 
    index granule for this index. 
    CONTIGUOUS = VALUE-BIT(1) Indicates that this key is entirely composed of 
    fields that are contiguous within the data record, allowing them to be 
    compared as a unit, rather than field-by-field. 
    DEGENERATE = VALUE-BIT(1) Indicates that this index is entirely composed 
    of fields whose data types allow them to be compared using a normal ASCII 
    compare, rather than needing special effort. 
    LDA = VALUE-DEC(0-n) Contains the file relative disk address of the last 
    index granule for this index. 
    NKEYS = VALUE-DEC(0-n)  Contains the number of keys defined. 
    TDA = VALUE-DEC(0-n) Contains the file relative disk address of the first 
    index granule at the top of the multi-level structure.  If no such 
    structure exists, TDA contains zero. 
    TDALVL = VALUE-DEC(0-511) The top level number for the upper level 
    structure. 
    UNIQUEBLD = VALUE-BIT(1) Indicates whether or not the unique indexes need 
    to be rebuilt. 
00001
00002
00003
00004
00005
00006
00007
00008
00009
This information is in the FIT and FPARAM buffer.  It may be in Keyed, 
Indexed, Consecutive, Relative, and IREL files.  It represents the logical 
order of fields in a record.  This information is never used by file 
management and is solely for the convenience of various processors and/or the 
user.  Its structure is identical to VLP_IRREC. 
    FIELDN - An array of field indexes.  Each element contains an index into 
    the corresponding CODE18.FIELD or CODE18.DECFIELD array.  Hence, element 
    values range from 0-511. 
    NFIELDS = VALUE-DEC(0-511) Specifies the number of elements in the 
    CODE21.FIELDN array.  This value may be less than or equal to 
    CODE18.NFIELDS. 
    VLPID = VALUE-DEC(511) specifies the identifier which differentiates a 
    VLP_IRREC from other VLPs which may be specified in the same vector 
    location on an M$OPEN or M$CLOSE. Although this value is only useful in a 
    VLP_IRREC, it is carried in the CODE21 as well. 
00001
00002
00003
CODE08
The FPARAM buffer includes a header preceding the data section(s).  The 
structure of the header, which may be of interest to some users, can be 
generated by invoking the FM$FIT macro. 
FM$FIT defines an array CODES which contains an entry for each FIT data 
section.  The array is of size (0:N).  The default value of N is 30, which may 
be changed by specifying N=value on the macro invocation line.  The array 
CODES contains: 
    CODE = VALUE-DEC(1-31) Contains the data section number. CODE(0) contains 
    the number of entries in the CODES array. 
    ITEMX = VALUE-DEC(1-1020) Contains the word index of the start of the data 
    section relative to the beginning of the FIT header. 
    NAW = VALUE-DEC(0-1023) Contains the number of available words in the data 
    section.  NAW is always equal to NDW in FPARAM.  In IFPARAM, it may be set 
    to reserve space in the FIT.  NAW(0) is the total number of words occupied 
    by the FIT. 
    NDW = VALUE-DEC(0-1023) Contains the number of significant words in the 
    data section.  NDW(0) in FPARAM is the total number of words occupied by 
    the FPARAM information. 
00001
00002
00003
00004
A 
  Access Control Lists - 
      HELP CODE09 
  Access Vehicle Control List - 
      HELP CODE10 
  ACCESS.BUPF -   
    CODE14 - 
      HELP CODE14 ACCESS.BUPF 
  ACCESS.BUPM -   
    CODE14 - 
      HELP CODE14 ACCESS.BUPM 
  ACCESS.GACSHELF -   
    CODE14 - 
      HELP CODE14 ACCESS.GACSHELF 
  ACCESS.LIST -   
    CODE14 - 
      HELP CODE14 ACCESS.LIST 
  ACCESS.MERGEAC -   
    CODE14 - 
      HELP CODE14 ACCESS.MERGEAC 
  ACCESS.NEWFD -   
    CODE14 - 
      HELP CODE14 ACCESS.NEWFD 
  ACCESS.NOACUP -   
    CODE14 - 
      HELP CODE14 ACCESS.NOACUP 
  ACCESS.NOSTOW -   
    CODE14 - 
      HELP CODE14 ACCESS.NOSTOW 
  ACCESS.NPUR -   
    CODE14 - 
      HELP CODE14 ACCESS.NPUR 
  ACCESS.OWNERF -   
    CODE14 - 
      HELP CODE14 ACCESS.OWNERF 
  ACCESS.TIME -   
    CODE04 - 
      HELP CODE04 ACCESS.TIME 
  ACCESS.WCDATA -   
    CODE14 - 
      HELP CODE14 ACCESS.WCDATA 
  ACCESS.WRCMP -   
    CODE14 - 
      HELP CODE14 ACCESS.WRCMP 
  Account and File Directory Information - 
      HELP CODE14 
  ACCT -   
    CODE09 - 
      HELP CODE09 ACCT 
  ACSVEH -   
    CODE10 - 
      HELP CODE10 ACSVEH 
  ALTBLD -   
    CODE08 - 
      HELP CODE08 ALTBLD 
    CODE20 - 
      HELP CODE20 ALTBLD 
  Always in FPARAM - 
      HELP CODE03 
  ATTR -   
    CODE16 - 
      HELP CODE16 ATTR 
B 
  Backup Date and Reel - 
      HELP CODE05 
  BACKUP.EFT.CROSS -   
    CODE05 - 
      HELP CODE05 BACKUP.EFT.CROSS 
  BACKUP.EFT.FSN -   
    CODE05 - 
      HELP CODE05 BACKUP.EFT.FSN 
  BACKUP.REEL -   
    CODE05 - 
      HELP CODE05 BACKUP.REEL 
  BACKUP.TIME -   
    CODE05 - 
      HELP CODE05 BACKUP.TIME 
  BANNER_CHARGES -   
    CODE16 - 
      HELP CODE16 BANNER_CHARGES 
  BANNER_REPEATS -   
    CODE16 - 
      HELP CODE16 BANNER_REPEATS 
C 
  CDA -   
    CODE20 - 
      HELP CODE20 CDA 
  CGMEM -   
    CODE14 - 
      HELP CODE14 CGMEM 
  CGORG -   
    CODE15 - 
      HELP CODE15 CGORG 
  CGRANS -   
    CODE14 - 
      HELP CODE14 CGRANS 
  CODE -   
    FM$FIT - 
      HELP FM$FIT CODE 
  CODE01 - 
      HELP CODE01 
  CODE01 - Not in FPARAM - 
      HELP CODE01 
  CODE02 - 
      HELP CODE02 TDALVL 
  CODE02 - Keyed Files - 
      HELP CODE02 
  CODE03 - 
      HELP CODE03 XTNSIZE 
  CODE03 - Always in FPARAM - 
      HELP CODE03 
  CODE04 - 
      HELP CODE04 SVMODIFY.TIME 
  CODE04 - Dates - 
      HELP CODE04 
  CODE05 - 
      HELP CODE05 BACKUP.TIME 
  CODE05 - Backup Date and Reel - 
      HELP CODE05 
  CODE06 - 
      HELP CODE06 STOW.REEL 
  CODE06 - Stow Date and Reel - 
      HELP CODE06 
  CODE07 - 
      HELP CODE07 PASS 
  CODE07 - Password - 
      HELP CODE07 
  CODE08 - FITALTKEYS - 
      HELP CODE08 
  CODE09 - 
      HELP CODE09 FFLG.WNEW 
  CODE09 - Access Control Lists - 
      HELP CODE09 
  CODE10 - 
      HELP CODE10 FFLG.WNEW 
  CODE10 - Access Vehicle Control List - 
      HELP CODE10 
  CODE11 - UATTR Information - 
      HELP CODE11 
  CODE12 - INSTATTR Information - 
      HELP CODE12 
  CODE13 - PROCATTR Information - 
      HELP CODE13 
  CODE14 - 
      HELP CODE14 OWNER.NAME 
  CODE14 - Account and File Directory Information - 
      HELP CODE14 
  CODE15 - 
      HELP CODE15 QISS 
  CODE15 - COMGROUP File Information - 
      HELP CODE15 
  CODE16 - 
      HELP CODE16 WSN 
  CODE16 - Device Attributes - 
      HELP CODE16 
  CODE17 - FPRG Information - 
      HELP CODE17 
  CODE18 - 
      HELP CODE18 VLPID 
  CODE18 - Physical Field Organization of a Record - 
      HELP CODE18 
  CODE19 - 
      HELP CODE19 UNIQUE 
  CODE19 - IREL Keys, Part 1 - 
      HELP CODE19 
  CODE20 - 
      HELP CODE20 UNIQUEBLD 
  CODE20 - IREL Keys, Part 2 - 
      HELP CODE20 
  CODE21 - 
      HELP CODE21 VLPID 
  CODE21 - Logical Field Organization of a Record - 
      HELP CODE21 
  COMGROUP File Information - 
      HELP CODE15 
  COMODE -   
    CODE16 - 
      HELP CODE16 COMODE 
  COMP -   
    CODE03 - 
      HELP CODE03 COMP 
  CONTFORM -   
    CODE16 - 
      HELP CODE16 CONTFORM 
  CONTIGUOUS -   
    CODE20 - 
      HELP CODE20 CONTIGUOUS 
  COPIES -   
    CODE16 - 
      HELP CODE16 COPIES 
  CREATION.TIME -   
    CODE04 - 
      HELP CODE04 CREATION.TIME 
  CREATOR.ACCT -   
    CODE04 - 
      HELP CODE04 CREATOR.ACCT 
  CREATOR.NAME -   
    CODE04 - 
      HELP CODE04 CREATOR.NAME 
D 
  Dates - 
      HELP CODE04 
  DDEV -   
    CODE16 - 
      HELP CODE16 DDEV 
  DECFIELD -   
    CODE18 - 
      HELP CODE18 DECFIELD 
  DECFIELD.LEN -   
    CODE18 - 
      HELP CODE18 DECFIELD.LEN 
  DECFIELD.SCALE -   
    CODE18 - 
      HELP CODE18 DECFIELD.SCALE 
  DECFIELD.TYPE -   
    CODE18 - 
      HELP CODE18 DECFIELD.TYPE 
  DEGENERATE -   
    CODE20 - 
      HELP CODE20 DEGENERATE 
  DESC.ACTIVE -   
    CODE03 - 
      HELP CODE03 DESC.ACTIVE 
  DESC.ARCHIVE -   
    CODE03 - 
      HELP CODE03 DESC.ARCHIVE 
  DESC.BAD -   
    CODE03 - 
      HELP CODE03 DESC.BAD 
  DESC.BUF -   
    CODE03 - 
      HELP CODE03 DESC.BUF 
  DESC.BUPM -   
    CODE03 - 
      HELP CODE03 DESC.BUPM 
  DESC.DELF -   
    CODE03 - 
      HELP CODE03 DESC.DELF 
  DESC.FETCH -   
    CODE03 - 
      HELP CODE03 DESC.FETCH 
  DESC.NBUF -   
    CODE03 - 
      HELP CODE03 DESC.NBUF 
  DESC.NOLIST -   
    CODE03 - 
      HELP CODE03 DESC.NOLIST 
  DESC.ODSTOW -   
    CODE03 - 
      HELP CODE03 DESC.ODSTOW 
  DESC.QS -   
    CODE03 - 
      HELP CODE03 DESC.QS 
  DESC.TERMINATE -   
    CODE03 - 
      HELP CODE03 DESC.TERMINATE 
  DESC.TPB -   
    CODE03 - 
      HELP CODE03 DESC.TPB 
  DEV -   
    CODE16 - 
      HELP CODE16 DEV 
  Device Attributes - 
      HELP CODE16 
  DFLTALL -   
    CODE14 - 
      HELP CODE14 DFLTALL 
  DVFC -   
    CODE16 - 
      HELP CODE16 DVFC 
E 
  EXPIRE -   
    CODE03 - 
      HELP CODE03 EXPIRE 
F 
  FFLG.AU -   
    CODE09 - 
      HELP CODE09 FFLG.AU 
    CODE10 - 
      HELP CODE10 FFLG.AU 
  FFLG.AURD -   
    CODE09 - 
      HELP CODE09 FFLG.AURD 
    CODE10 - 
      HELP CODE10 FFLG.AURD 
  FFLG.CREATE -   
    CODE09 - 
      HELP CODE09 FFLG.CREATE 
  FFLG.DELF -   
    CODE09 - 
      HELP CODE09 FFLG.DELF 
    CODE10 - 
      HELP CODE10 FFLG.DELF 
  FFLG.DELR -   
    CODE09 - 
      HELP CODE09 FFLG.DELR 
    CODE10 - 
      HELP CODE10 FFLG.DELR 
  FFLG.EXEC -   
    CODE09 - 
      HELP CODE09 FFLG.EXEC 
    CODE10 - 
      HELP CODE10 FFLG.EXEC 
  FFLG.NOLIST -   
    CODE09 - 
      HELP CODE09 FFLG.NOLIST 
    CODE10 - 
      HELP CODE10 FFLG.NOLIST 
  FFLG.READ -   
    CODE09 - 
      HELP CODE09 FFLG.READ 
    CODE10 - 
      HELP CODE10 FFLG.READ 
  FFLG.REATTR -   
    CODE09 - 
      HELP CODE09 FFLG.REATTR 
    CODE10 - 
      HELP CODE10 FFLG.REATTR 
  FFLG.TCTL -   
    CODE09 - 
      HELP CODE09 FFLG.TCTL 
    CODE10 - 
      HELP CODE10 FFLG.TCTL 
  FFLG.UPD -   
    CODE09 - 
      HELP CODE09 FFLG.UPD 
    CODE10 - 
      HELP CODE10 FFLG.UPD 
  FFLG.WNEW -   
    CODE09 - 
      HELP CODE09 FFLG.WNEW 
    CODE10 - 
      HELP CODE10 FFLG.WNEW 
  FIELD -   
    CODE18 - 
      HELP CODE18 FIELD 
  FIELD.LEN -   
    CODE18 - 
      HELP CODE18 FIELD.LEN 
  FIELD.TYPE -   
    CODE18 - 
      HELP CODE18 FIELD.TYPE 
  FIELDN -   
    CODE19 - 
      HELP CODE19 FIELDN 
    CODE21 - 
      HELP CODE21 FIELDN 
  FITALTKEYS - 
      HELP CODE08 
      HELP CODE08 UNIQUEBLD 
  FM$FIT - 
      HELP FM$FIT 
      HELP FM$FIT NDW 
  FORM -   
    CODE16 - 
      HELP CODE16 FORM 
  FPRG Information - 
      HELP CODE17 
G 
  GAC.N -   
    CODE04 - 
      HELP CODE04 GAC.N 
  GAC.TIME -   
    CODE04 - 
      HELP CODE04 GAC.TIME 
  GDA -   
    CODE02 - 
      HELP CODE02 GDA 
  Get FIT Data or FIT Index - 
      HELP XSF$LOCCODx 
  GHSTACS -   
    CODE03 - 
      HELP CODE03 GHSTACS 
  GOOD -   
    CODE16 - 
      HELP CODE16 GOOD 
I 
  INSTATTR Information - 
      HELP CODE12 
  IREL Keys, Part 1 - 
      HELP CODE19 
  IREL Keys, Part 2 - 
      HELP CODE20 
  ITEMX -   
    FM$FIT - 
      HELP FM$FIT ITEMX 
K 
  K -   
    CODE08 - 
      HELP CODE08 K 
  K.DUPKEY -   
    CODE08 - 
      HELP CODE08 K.DUPKEY 
  K.FDA -   
    CODE08 - 
      HELP CODE08 K.FDA 
  K.KEYL -   
    CODE08 - 
      HELP CODE08 K.KEYL 
  K.KEYX -   
    CODE08 - 
      HELP CODE08 K.KEYX 
  K.LDA -   
    CODE08 - 
      HELP CODE08 K.LDA 
  K.TDA -   
    CODE08 - 
      HELP CODE08 K.TDA 
  K.TDALVL -   
    CODE08 - 
      HELP CODE08 K.TDALVL 
  K.UNIQUE -   
    CODE08 - 
      HELP CODE08 K.UNIQUE 
  Keyed Files - 
      HELP CODE02 
  KEYEND -   
    CODE19 - 
      HELP CODE19 KEYEND 
  KEYL -   
    CODE02 - 
      HELP CODE02 KEYL 
  KEYX -   
    CODE02 - 
      HELP CODE02 KEYX 
L 
  LDA -   
    CODE03 - 
      HELP CODE03 LDA 
    CODE20 - 
      HELP CODE20 LDA 
  LINENO -   
    CODE16 - 
      HELP CODE16 LINENO 
  LINES -   
    CODE16 - 
      HELP CODE16 LINES 
  Logical Field Organization of a Record - 
      HELP CODE21 
  LRDL0 -   
    CODE02 - 
      HELP CODE02 LRDL0 
  LSLIDE -   
    CODE02 - 
      HELP CODE02 LSLIDE 
M 
  MGRANS -   
    CODE14 - 
      HELP CODE14 MGRANS 
  MINWRSIZE -   
    CODE08 - 
      HELP CODE08 MINWRSIZE 
  MODIFY.TIME -   
    CODE04 - 
      HELP CODE04 MODIFY.TIME 
N 
  NAW -   
    FM$FIT - 
      HELP FM$FIT NAW 
  NBANNER_RECS -   
    CODE16 - 
      HELP CODE16 NBANNER_RECS 
  NDW -   
    FM$FIT - 
      HELP FM$FIT NDW 
  NFIELDS -   
    CODE18 - 
      HELP CODE18 NFIELDS 
    CODE21 - 
      HELP CODE21 NFIELDS 
  NGAVAL -   
    CODE03 - 
      HELP CODE03 NGAVAL 
  NKEYS -   
    CODE19 - 
      HELP CODE19 NKEYS 
    CODE20 - 
      HELP CODE20 NKEYS 
  Not in FPARAM - 
      HELP CODE01 
  NOTCOL1 -   
    CODE16 - 
      HELP CODE16 NOTCOL1 
  NRECS -   
    CODE03 - 
      HELP CODE03 NRECS 
  NSFORM -   
    CODE16 - 
      HELP CODE16 NSFORM 
  NSTAMP -   
    CODE03 - 
      HELP CODE03 NSTAMP 
  NUMENTS -   
    CODE08 - 
      HELP CODE08 NUMENTS 
  NUMWRDS -   
    CODE08 - 
      HELP CODE08 NUMWRDS 
O 
  OLDSEQ.SEQCOL -   
    CODE16 - 
      HELP CODE16 OLDSEQ.SEQCOL 
  OLDSEQ.SEQID -   
    CODE16 - 
      HELP CODE16 OLDSEQ.SEQID 
  OLDTABS -   
    CODE16 - 
      HELP CODE16 OLDTABS 
  Optical Disk -   
    CODE03.DESC.ODSTOW - 
      HELP CODE03 DESC.ODSTOW 
    CODE06.STOW.ODFSN - 
      HELP CODE06 STOW.ODFSN 
    CODE20.CONTIGUOUS - 
      HELP CODE20 DEGENERATE 
    CODE20.DEGENERATE - 
      HELP CODE20 CONTIGUOUS 
  ORG -   
    CODE03 - 
      HELP CODE03 ORG 
  OWNER -   
    CODE14 - 
      HELP CODE14 OWNER 
  OWNER.ACCT -   
    CODE14 - 
      HELP CODE14 OWNER.ACCT 
  OWNER.NAME -   
    CODE14 - 
      HELP CODE14 OWNER.NAME 
P 
  PAGEBASE -   
    CODE16 - 
      HELP CODE16 PAGEBASE 
  PAGENO -   
    CODE16 - 
      HELP CODE16 PAGENO 
  PASS -   
    CODE07 - 
      HELP CODE07 PASS 
  Password - 
      HELP CODE07 
  Physical Field Organization of a Record - 
      HELP CODE18 
  PROCATTR Information - 
      HELP CODE13 
Q 
  QISS -   
    CODE15 - 
      HELP CODE15 QISS 
R 
  RCSZ -   
    CODE03 - 
      HELP CODE03 RCSZ 
  RECL -   
    CODE03 - 
      HELP CODE03 RECL 
  RECNO -   
    CODE16 - 
      HELP CODE16 RECNO 
S 
  SLIDE -   
    CODE02 - 
      HELP CODE02 SLIDE 
  SPARE -   
    CODE02 - 
      HELP CODE02 SPARE 
  STEPPAGENO -   
    CODE16 - 
      HELP CODE16 STEPPAGENO 
  STEPRECNO -   
    CODE16 - 
      HELP CODE16 STEPRECNO 
  Stow Date and Reel - 
      HELP CODE06 
  STOW.EFT.CROSS -   
    CODE06 - 
      HELP CODE06 STOW.EFT.CROSS 
  STOW.EFT.FSN -   
    CODE06 - 
      HELP CODE06 STOW.EFT.FSN 
  STOW.EFT.INACTIVE -   
    CODE06 - 
      HELP CODE06 STOW.EFT.INACTIVE 
  STOW.ODFSN -   
    CODE06 - 
      HELP CODE06 STOW.ODFSN 
  STOW.REEL -   
    CODE06 - 
      HELP CODE06 STOW.REEL 
  SVMODIFY.TIME -   
    CODE04 - 
      HELP CODE04 SVMODIFY.TIME 
T 
  TDA -   
    CODE02 - 
      HELP CODE02 TDA 
    CODE20 - 
      HELP CODE20 TDA 
  TDALVL -   
    CODE02 - 
      HELP CODE02 TDALVL 
    CODE20 - 
      HELP CODE20 TDALVL 
  TYPE -   
    CODE03 - 
      HELP CODE03 TYPE 
U 
  UATTR Information - 
      HELP CODE11 
  UGRANS -   
    CODE03 - 
      HELP CODE03 UGRANS 
  UNIQUE -   
    CODE19 - 
      HELP CODE19 UNIQUE 
  UNIQUEBLD -   
    CODE08 - 
      HELP CODE08 UNIQUEBLD 
    CODE20 - 
      HELP CODE20 UNIQUEBLD 
V 
  VFCIM.LINE -   
    CODE16 - 
      HELP CODE16 VFCIM.LINE 
  VFCIM.NEXT -   
    CODE16 - 
      HELP CODE16 VFCIM.NEXT 
  VLPID -   
    CODE18 - 
      HELP CODE18 VLPID 
    CODE21 - 
      HELP CODE21 VLPID 
W 
  WIDTH -   
    CODE16 - 
      HELP CODE16 WIDTH 
  WSN -   
    CODE16 - 
      HELP CODE16 WSN 
X 
  XSF$LOCCODx - Get FIT Data or FIT Index - 
      HELP XSF$LOCCODx 
  XTNSIZE -   
    CODE03 - 
      HELP CODE03 XTNSIZE 
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
HELP_INDEX
Several services are provided to access data in the FIT and FIT header.  These 
services have the form: 
CALL XSF$LOCCODx (FIT$,CODE) ALTRET (label); 
where 
XSF$LOCCODx is the service name. The various names and the function of each 
service are described in the table below. 
FIT$ Is a pointer to the beginning of the FPARAM buffer. For the contents of 
FIT$ on return from the service, see the table below. 
CODE Contains the code of a FIT data section, right-justified in one word. For 
the contents of CODE on return from the service, see the table below. 
Service               Result 
------------------------------------------------------------------- 
XSF$LOCCODE           FIT$ points to the FIT data section specified by CODE 
                      CODE contains the index of the data section entry in FIT 
                           header 
XSF$LOCCODX           FIT$ is unchanged 
                      CODE contains the index of the data section entry in the 
                           FIT header 
XSF$LOCCODT           FIT$ points to the data section specified by CODE if 
                           there is significant data in the section (i.e., if 
                           FM$FIT.CODES.NDW is not zero) 
                      CODE is unchanged. 
XSF$LOCCODP           FIT$ points to the data section specified by CODE 
                      CODE is unchanged. 
The alternate return is taken if the data section requested by CODE is not 
contained in the FPARAM buffer.  The alternate return is also taken for 
XSF$LOCCODT if the requested data section contains no significant data. 
