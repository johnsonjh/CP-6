    For an overview of IDS HELP, enter: 
    HELP (IDS) OVERVIEW 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
All abnormal errors are fatal and will cause a program to abort.  Abnormal 
errors will cause an I-D-S/II SCREECH and create a dump file in the :SYSTAC 
account for possible future analysis.  The error is identified along with the 
dump file name when an abort occurs.  If the program is running with transient 
journal protection, the data base is rolled back upon detection of an abnormal 
error.  If the JOURNAL IS REQUIRED statement is present in the schema DMCL, 
the data base control system will journal the after images of updated portions 
of data base records.  The first run-time program to use a common shared 
journal will alter a system ghost which will "own" the journal.  The system 
ghost will handle all errors, volume switching and other device oriented 
problems.  For a complete description of the system ghost, see the System 
Support Manual (HA20, HA21). 
The formats of the records on the common shared journal assume conventions are 
used by all journal users.  The first four bytes of each common shared journal 
record contains the Universal Time Stamp.  Byte 5 contains a code from 1 to 20 
used by I-D-S/II and Transaction Processing.  This convention is subject to 
change if a system wide header is adopted in a future release.  Users may 
write to the common journal as long as these restrictions and assumptions are 
understood. 
    ACCEPT makes the contents of the specified currency indicators available 
    to the program and obtains the realm name that corresponds to a data base 
    key value. 
Format 1: 
dbkey<-[]DBACCEPT 'FROM [record-name] CURRENCY'                 (APL) 
                        [realm-name ] 
ACCEPT dbkey FROM [record-name  ] CURRENCY                    (COBOL) 
                  [realm-name   ] 
CALL ACCEPT (dbkey,[record-name],CURRENCY)                  (FORTRAN) 
                   [realm-name ] 
DB ACCEPT numericvariable [FROM] [record-name] CURRENCY       (BASIC) 
                                 [realm-name ] 
Format 2: 
                       [record-name] 
char<-[]DBACCEPT 'FROM [set-name   ] REALMNAME'                 (APL) 
                       [dbkey-3    ] 
                  [record-name] 
ACCEPT char  FROM [set-name   ] REALMNAME                     (COBOL) 
                  [dbkey      ] 
                   [record-name] 
CALL ACCEPT (char, [set-name   ],REALMNAME)                 (FORTRAN) 
                   [dbkey      ] 
                                [record-name] 
DB ACCEPT stringvariable [FROM] [set-name   ] REALMNAME       (BASIC) 
                                [db-key     ] 
Format 3: 
                                 {CURRENCY} 
dbkey<-[]DBACCEPT 'FROM set-name {PRIOR   }'                    (APL) 
                                 {NEXT    } 
                                 {OWNER   } 
                           {CURRENCY } 
ACCEPT dbkey FROM set-name {PRIOR    }                        (COBOL) 
                           {NEXT     } 
                           {OWNER    } 
                             {CURRENCY} 
CALL ACCEPT (dbkey,set-name, {PRIOR   }                     (FORTRAN) 
                             {NEXT    }) 
                             {OWNER   } 
                                          {CURRENCY} 
                                          {PRIOR   } 
DB ACCEPT numericvariable [FROM] set-name {NEXT    }          (BASIC) 
                                          {OWNER   } 
Syntax Rules: 
1.  In COBOL, dbkey, must be an elementary data base key item.  In APL and 
    FORTRAN, dbkey must be an integer. 
2.  char must reference a level 77 alphanumeric elementary data item in COBOL 
    or a CHARACTER item in FORTRAN. 
General Rules: 
Format 1: 
1.  If record-name or realm-name is specified, the data base key value for the 
    current record of record-name or realm-name respectively is placed in the 
    data item referenced by dbkey. 
2.  If a record-name or realm-name is not specified, the data base key value 
    for the current record of the run unit is placed in the data item 
    referenced by dbkey. 
Format 2: 
1.  The realm-name that is derived from the data base key value in the data 
    item referenced by dbkey or from the specified currency indicator is 
    placed in the data item referenced by char, according to the rules for an 
    alphanumeric elementary move. 
2.  If dbkey or a currency indicator is not specified, the name of the realm 
    that is associated with the current record of the run unit is placed in 
    the data item referenced by char, according to the rules for an 
    alphanumeric elementary move. 
Format 3: 
1.  If CURRENCY is specified, the data base key value for the current record 
    of set-name is placed in the data item referenced by dbkey. 
2.  If NEXT, PRIOR, or OWNER is specified, the data base key value for the 
    next, prior, or owner record of set-name is placed in the data item 
    referenced by dbkey.  If the next or prior record is the owner record of 
    the set type, the data base key of that (owner) record is placed in the 
    data item.  An exception condition for end of set will not occur. 
Notes: 
When a record is disconnected from a set or erased, the current indicator for 
the set is null.  Therefore, if the CURRENCY option is used with Format 3, an 
exception condition may result, indicating no current record.  However, the 
NEXT, PRIOR, or OWNER options will execute successfully and return the correct 
value. 
00002
00003
00001
The values of record items may be set and obtained by either sharing variables 
in the workspace with I-D-S/II or by the functions []DBFROM and []DBTO. 
Sharing of all database items may be requested when the database is opened or 
by using the Shared Variable system functions.  For example, if USERNAME is a 
name of an item in the database then the expression: 
        'IDS.:SYS' []SVO  'USERNAME' 
    2 
returns 2 indicating that the variable USERNAME in the active workspace may be 
referenced or assigned which really accesses the value in the UWA.  Note that 
erasing USERNAME or retracting USERNAME by the []SVR system function will 
discontinue sharing. 
This statement moves data from the User Working Area. 
Format: 
R<-[]DBFROM 'itemlist'                                           (APL) 
Syntax Rules: 
Itemlist specifies one or more items in the User Working Area formatted as 
follows: 
    item1[,item2]... 
Notes: 
This function returns the values of the specified items in the User Working 
Area.  The items in the item list must all be of the same type -- all numeric 
or all text -- or a DOMAIN ERR occurs.  Text items in the result are separated 
by carriage return characters. 
Example: 
R<-[]DBFROM 'ITEM1, ITEM2, ITEM3' 
00003
00002
00001
This statement, which interrogates the special registers in the User Working 
Area and special cells, has four formats. 
Format: 
Format 1 
This format returns the data base key value from the special register 
DIRECTREFERENCE. 
dbkey<-[]DBINFORM 'DIRECTREFERENCE'                          (APL) 
Format 2 
This format returns the names from the special registers and the names of the 
subschema and schema as well. 
                 {'DBREALM'    } 
                 {'DBDATANAME' } 
                 {'DBKEYNAME'  } 
name<-[]DBINFORM {'DBPRIVACY'  }                             (APL) 
                 {'DBRECORD'   } 
                 {'DBSET'      } 
                 {'DBSCHEMA'   } 
                 {'DBSUBSCHEMA'} 
Format 3 
This format returns an integer, which is the CP-6 Universal Time Stamp set 
when the subschema is translated. 
UTS-integer<-[]DBINFORM 'DBUTS'                              (APL) 
Format 4 
This format returns the underlying CP-6 error code or the equivalent error 
message respectively. 
char<-[]DBINFORM {'DBSYSERR'} 
                 {'DBSYSMSG'} 
Note: 
This function returns the contents of the specified data base register.  A 
DIRECTREFERENCE returns a character string of up to 32 characters. 
DIRECTREFERENCE returns an integer data base key value. 
00001
APL_SUBSCHEMA_NAME
APL_INVOCATION
This statement moves data to the User Working Area. 
Format: 
[]DBTO (itemlist;valuelist1[;valuelist2]...)                     (APL) 
Syntax Rules: 
1.  Itemlist identifies a text vector of item names or a numeric vector of the 
    names indicated in DBNAMES. 
2.  Valuelist specifies one or more values to be moved into the User Working 
    Area for each corresponding item name. 
Notes: 
A value list consists of text or numeric scalars or vectors.  If a text vector 
is supplied, separate item values may be separated by carriage return 
characters. 
00002
00001
APL_SUBSCHEMA_TYPE
    For fields, array element 2 contains usage information as follows: 
        Code      Meaning 
          0       Data item. 
          1       Data base parameter. 
          2       Location mode direct field. 
          3       Area-id field. 
          4       CALC key synonym field. 
          5       SCAN key synonym field. 
    Array element 3 contains flags that may be decoded with the expression: 
    R<-(36 2)  []DBTYPES[R;2] 
    where the values for R and their meanings are the same as for the record 
    (R) flags. 
    Array element 4 contains the record number in []DBNAMES that this field 
    belongs to. 
    Array element 5 contains a code for the data type of this field as 
    follows: 
    Code      Meaning 
      0       Text 
      1       Integer DB_KEY 
      2       Integer 
     13       Single precision floating point 
     14       Double precision floating point. 
    Array element 6 is used for text data items only.  It specifies the length 
    of the string. 
This statement informs I-D-S/II of the name of the subschema to be used.  The 
subschema contains the name of the associated schema. 
Format: 
schema-name<-[]DBSUB 
'sub-schema-name,privacy-invoking-key,SHARE'                     (APL) 
Syntax Rules: 
1.  Sub-schema-name identifies the subschema to be used. 
2.  Privacy-invoking-key is the privacy key value for the subschema PRIVACY 
    FOR INVOKING lock. 
General Rules: 
1.  This statement must be the first I-D-S/II function executed during an APL 
    session. 
2.  A )SET command may be necessary to direct I-D-S/II to the correct files. 
    (Section 4 describes use of SET commands.) 
3.  Both the schema and the subschema must be accessed in this operation. 
Notes: 
1.  Assume the following: 
    o   A subschema named SSCHFILE resides in the CP-6 file SSCHFILE_7A.BFACCT 
    o   A schema named SCHFILE resides in the CP-6 file SCHFILE.SPOAPL.PSSWD 
    o   The realm to be used in this subschema is named AREA0, and it resides 
        in CP-6 file MAGAREA.MGACCT. 
    Three )SET commands will be required to use this database: 
        )SET SSCHFILE SSCHFILE_7A.BFACCT 
        )SET SCHFILE SCHFILE.SPOAPL.PSSWD 
        )SET AREA0 MAGAREA.MGACCT 
2.  The following is a list of error diagnostics that can occur when the DBSUB 
    system function is executed.  Each error diagnostic is followed by an 
    explanation of the error condition that produces the message. 
        201 IDS LIBRARY NOT AVAILABLE 
        The alternate shared library called IDS either does not exist or 
        another alternate library is currently associated.  This error may be 
        sidetracked as error number 201. 
        202 INVALID SUBSCHEMA 
        The CP-6 file identified as the subschema is not an I-D-S/II subschema 
        file.  This error may be sidetracked as error number 202. 
        203 FILE TBL FULL 
        The maximum number of files that an APL user may open are currently 
        open.  Close some files.  This error may be sidetracked as error 
        number 203. 
        204 NOT APL SUBSCHEMA 
        The specified CP-6 file appears to be a valid subschema; however, it 
        can not be used by APL.  This error may be sidetracked as error number 
        204. 
        205 SUBSCHEMA NAME ERR 
        Either the subschema name and privacy key is invalid or the subschema 
        name in the CP-6 file does not match the name supplied.  This error 
        may be sidetracked as error number 205. 
        206 SUBSCHEMA ACCESS ERR 
        Access to the subschema has been denied because either the file does 
        not exist, it has a password, or the privacy locks do not match.  This 
        error may be sidetracked as error number 206. 
Example: 
R<-[]DBSUB 'SSCHFILE,SECRET' 
00004
00002
00003
00001
    Array element 4 contains the index in []DBNAMES of the record related to 
    this data base parameter. 
Examples: 
R<-[]DBNAMES 
00001
    For records, array element 2 contains the location mode as follows: 
        Code      Location Mode 
          0       DIRECT 
          1       CALC 
          2       VIA SET 
          3       SEQUENTIAL 
          4       INDEXED. 
    Array element 3 contains flags decoded as: 
        R<-(36 2)  []DBTYPES[R;2] 
    where the value for R can be 
        Value      Meaning 
        R[1]       Name is in SUBSCHEMA. 
        R[2]       Name understood by IDS. 
        R[3]       STORE is allowed. 
        R[4]       MODIFY is allowed. 
        R[5]       DELETE is allowed. 
        R[6]       ERASE is allowed. 
        R[7]       Variable length. 
        R[8]       In multiple areas. 
        R[9]       Has alternate keys. 
        R[10]      An elementary item. 
        R[11]      Item is signed. 
        R[12]      Item is scaled. 
    For sets, array element 2 indicates the mode as follows: 
        Code    Mode 
          0     Chain 
          1     Record array 
    Array element 4 indicates the index in []DBNAMES of the record that owns 
    this set. 
    Array element 5 indicates the type of set as follows: 
        Code   Set Type 
          0    User 
          1    CALC 
          2    Primary key 
          3    Secondary key. 
    Array element 6 indicates how this set is ordered, as follows: 
        Code   Order 
          0    FIRST 
          1    LAST 
          2    NEXT 
          3    PRIOR 
          4    SORTED BY KEY. 
  Statement          Function 
R<-[]DBFROM        Returns the values of the specified items in 
                   the User Working Area. 
R<-[]DBINFORM      Returns the contents of the specified data base 
                   register in the User Working Area. 
R<-[]DBNAMES       Lists area, set, record and item names and keyword 
                   values. 
R<-[]DBSUB         Specifies the name of the subschema. 
R<-[]DBTO          Moves values to the User Working Area. 
R<-[]DBTYPES       Describes the attributes of areas, sets, records, 
                   items and keyword values. 
See also: 
HELP APL_DBFROM 
HELP APL_DBINFORM 
HELP APL_DBNAMES 
HELP APL_DBSUB 
HELP APL_DBTO 
HELP APL_DBTYPES 
This niladic system function returns the names of all of the areas, sets, 
records, items and I-D-S/II keywords available through the current subschema. 
(A niladic function is one which has no argument on the right.) 
Format: 
array-nxm<-[]DBNAMES                                             (APL) 
Notes: 
The shape of the result is n by m, where n is the number of names and m is the 
length of the longest name. 
Example: 
R<-[]DBNAMES 
00002
00001
The result of using this niladic system function is to return an n by 6 array 
indicating the attributes of each corresponding name in DBNAMES. 
Format: 
array-nx6<-[]DBTYPES                                             (APL) 
Notes: 
Each row in the array contains the following information for one name in 
DBNAMES: 
    Array 
    Element     Contents 
       1        A code that defines the type of object as follows: 
                  Code         Object Type 
                    1          Realm 
                    2          Record 
                    3          Field 
                    4          Set 
                    5          Parameter 
                    6          (Unused) 
                    7          I-D-S/II keyword. 
       2        Usage or mode information. 
       3        Type-specific flags. 
       4        The index in DBNAMES of the object that owns this object. 
       5        Sub-type information. 
       6        Length of the object's order. 
    See also: 
    HELP (IDS) APL_RECORD 
    HELP (IDS) APL_FIELD 
    HELP (IDS) APL_SET 
    HELP (IDS) APL_PARAMETER 
00001
ASL_DATA_SEGS
The Data Base Control System is physically located in a CP-6 work space 
identified as the Alternate Shared Library (ASL).  The ASL is accessed by Data 
Manipulation Statements in the application program.  The ASL is a shared work 
space and contains only procedure and constants.  The data for I-D-S/II is 
unique for each user associated with the ASL. 
The first user whose execution invokes the subschema causes the schema subset 
to be extracted from the subschema file and put in a shared data segment.  All 
subsequent subschema invocations of the same subschema by other users will 
share the schema subset via the shared data segment.  The last user to release 
the data base context will also release the shared data segment containing the 
schema subset.  Sharing the schema subset can result in a significant savings 
in memory usage. 
The buffers and context for I-D-S/II are obtained dynamically from the ASL 
data segment in each user's work space.  The ASL data segment can contain up 
to 128 pages of 1024 words each.  The ASL data segment is not in the user's 
domain even though it is in the user's work space.  This is an important 
security feature of the I-D-S/II system on CP-6, which protects all of the 
buffers and data base context from the user. 
The ASL data segment is used to store context, key record buffers, INTEGRATED 
file page pool and INDEXED record buffers.  This storage is charged to the 
user and counts toward the maximum memory limit. 
The number of buffers which can be assigned to the page pool may be extended 
or limited by a CALL to IDSBUFFERS.  A minimum of six page buffers are 
required.  The default is 20 buffers, if space is available. 
This statement moves data from the User Working Area. 
Format: 
[line no.] DB FROM dbvar,basicvar                              (BASIC) 
Example: 
DB FROM ITEM1, BASVAR1 
00001
BASIC_SUBSCHEMA_NAME
This statement moves data to the User Working Area. 
Format: 
[line no.] DB TO exp,dbvar                                     (BASIC) 
Note: 
This statement moves the result of the evaluated expression to the specified 
data base item. 
00001
BASIC_SUBSCHEMA_TYPE
2.  Field Type Information 
    For fields, array element 2 contains usage information as follows: 
        Code    Meaning 
          0     Data item. 
          1     Data base parameter. 
          2     Location mode direct field. 
          3     Area-id field. 
          4     CALC key synonym field. 
          5     SCAN key synonym field. 
    Array element 3 contains flags that may be decoded with the expression: 
        MOD(A(x,y),z) 
    where the values for R and their meanings are the same as for the record 
    (R) flags. 
    Array element 4 contains the record number in DBNAMES$ that this field 
    belongs to. 
    Array element 5 contains a code for the data type of this field as 
    follows: 
        Code     Meaning 
          0      Text 
         13      Single precision floating point 
         14      Double precision floating point. 
    Array element 6 is used for text data items only.  It specifies the length 
    of the string. 
This statement informs I-D-S/II of the name of the subschema to be used.  It 
must be the first I-D-S/II function encountered in a BASIC session.  The 
statement will take effect immediately upon compilation. 
The subschema contains the name of the associated schema. 
Format: 
[line no.] DB SUB sub-schema-name[,privacy lock]               (BASIC) 
Syntax Rules: 
1.  Sub-schema-name identifies the subschema to be used. 
2.  Privacy-invoking-key is the privacy key value for the subschema PRIVACY 
    FOR INVOKING lock. 
General Rules: 
1.  This statement must be the first I-D-S/II function executed during a BASIC 
    session. 
2.  An IBEX "SET fid" command may be necessary to direct I-D-S/II to the 
    correct files.  (Section 4 of the I-D-S/II Programmer Reference Manual 
    (CE35) describes use of SET commands.) 
3.  Both the schema and the subschema must be accessed in this operation. 
Notes: 
1.  Assume the following: 
    o   A subschema named SSCHFILE resides in the CP-6 file SSCHFILE_7A.BFACCT 
    o   A schema name SCHFILE resides in the CP-6 file SCHFILE.SPOBAS.PSSWD 
    o   The realm to be used in this subschema is named AREA0, and it resides 
        in CP-6 file MAGAREA.MGACCT. 
2.  Three IBEX "SET fid" commands will be required to use this database: 
         >IBEX "SET SSCHFILE SSCHFILE_7A.BFACCT" 
         >IBEX "SET SSCHFILE SSCHFILE.SPOBAS.PSSWD" 
         >IBEX "SET AREA0 MAGAREA.MGACCT" 
Example: 
DB SUB SSCHFILE, SECRET 
00004
00002
00003
00001
BASIC_INVOCATION
4.  Parameter type information 
    Array element 4 contains the index in DBNAMES$ of the record related to 
    this data base parameter. 
Example: 
MAT A=DBTYPES 
1.  Record Type Information 
    For records, array element 2 contains the location mode as follows: 
        Code    Location Mode 
          0     DIRECT 
          1     CALC 
          2     VIA SET 
          3     SEQUENTIAL 
          4     INDEXED. 
    Array element three contains a set of flags for record or field types. 
    The bits are packed into a floating point number.  In order to access the 
    first bit, the user would type: 
        MOD(A(2,3),2) 
    In order to access the second bit the user would type: 
        MOD(A(2,3)/2,2) 
    and so on. 
    The meaning of these flags is as follows: 
        First          Name is in subschema 
        Second         Name understood by IDS 
        Third          STORE is allowed 
        Fourth         MODIFY is allowed 
        Fifth          DELETE is allowed 
        Sixth          ERASE is allowed 
        Seventh        Variable length 
        Eighth         In multiple realms 
        Ninth          Has alternate keys 
        Tenth          An elementary item 
        Eleventh       Item is signed 
        Twelfth        Item is scaled 
3.  Set Type Information 
    For sets, array element 2 indicates the mode as follows: 
        Code    Mode 
          0     Chain 
          1     Record array 
          2     Pointer array 
    Array element 4 indicates the index in DBNAMES$ of the record that owns 
    this set. 
    Array element 5 indicates the type of set as follows: 
        Code     Set Type 
          0      User 
          1      CALC 
          2      Primary key 
          3      Secondary key. 
    Array element 6 indicates how this set is ordered, as follows: 
        Code   Order 
          0    FIRST 
          1    LAST 
          2    NEXT 
          3    PRIOR 
          4    SORTED BY KEY 
  Statement            Function 
DB FROM              Returns the values of the specified items in the 
                     User Working Area. 
DBSTATUS             Returns the contents of the specified data base 
DBREALM$             register in the User Working Area. 
DBSET$ 
DBRECORD$ 
DBPRIVACY$ 
DBDATANAME$ 
DBKEYNAME$ 
DIRECTREFERENCE 
DBNAMES$             Lists area, set, record and item names and 
                     keyword values. 
DB SUB               Specifies the name of the subschema. 
DB TO                Moves values to the User Working Area. 
DBTYPES              Describes the attributes of areas, sets, records, 
                     items and keyword values. 
For specific information, enter: 
HELP (IDS) Statement-name 
See HELP (IDS) TOPICS for correct entry 
This niladic system function returns the names of all of the areas, sets, 
records, items and I-D-S/II keywords available through the current subschema. 
(A niladic function is one which has no argument on the right.) 
Format: 
[line no.] MAT aname = DBNAMES$                                (BASIC) 
Note: 
The result will be a string vector.  The size of aname will be dynamically 
determined by the number of names returned. 
Example: 
MAT B$=DBNAMES$ 
00002
00001
The result of using this niladic system function is to return an n by 6 array 
indicating the attributes of each corresponding name in DBNAMES$.  The size of 
aname will be dynamically modified if necessary. 
Format: 
[line no.] MAT aname = DBTYPES                                 (BASIC) 
Notes: 
Each row in the array contains the following information for one name in 
DBNAMES$. 
    Array 
    Element     Object Type 
       1.       A code that defines the type of object as follows: 
                    Code      Object Type 
                      0       REALM 
                      1       SET 
                      2       RECORD 
                      3       FIELD 
                      4       Unused 
                      5       PARAMETER 
                      6       LOCK 
                      7       I-D-S/II Keyword 
                      8       KEY 
       2.       Usage or mode information. 
       3.       Type-specified flags. 
       4.       The index in DBNAMES$ of the object that owns 
                this object. 
       5.       Sub-type information. 
       6.       Length of the object's order. 
    See also\ 
    HELP (IDS) BASIC_RECORD 
    HELP (IDS) BASIC_FIELD 
    HELP (IDS) BASIC_SET 
    HELP (IDS) BASIC_PARAMETER 
00001
During the invocation of the subschema, the Data Base Control System attempts 
to bind the program to the data extracted from the subschema.  Binding results 
in the modification of the Reference Vector Area defined within the 
application program.  APL and COBOL programs do not contain this structure at 
the source level.  In FORTRAN, this structure is defined in the INCLUDE file. 
All of the values defined in the Reference Vector Area must match the invoked 
subschema for binding to be completed.  The execution time resolution permits 
changes to occur in the schema definition without requiring either 
recompilation or relinking. 
In addition to binding, there are three consistency checks to confirm the 
program, subschema and schema are consistent.  One consistency check ensures 
that the names in the schema file match the names in the subschema file. 
These names also are the DCB names used to access the schema and subschema 
files.  Another consistency check ensures that subschema translation date 
(between the program and the subschema) is correct.  A third consistency check 
compares the subschema validation date against the validation date in the 
schema for that subschema. 
System exception codes xx7yyyy are generated in DB-STATUS to reflect problems 
in binding or consistency.  Therefore, any errors in the binding process may 
be detected by testing DB-STATUS as the first executable step after subschema 
invocation in any user program.  In a COBOL program, the first activity should 
be to test DB-STATUS.These errors include a missing subschema, a subschema 
which does not match the schema, and inadequate memory allocation. 
Because FORTRAN and COBOL programs are compiled and then run, binding or 
consistency errors can occur that will reflect differences in the subschema 
between compilation time and run time.  APL users do not compile or link.  APL 
does have binding but there should never be a binding or consistency error 
since there is only one reference to the subschema and that is at run time. 
The GENERATE RVA option of the DBACS VALIDATE directive is provided for 
FORTRAN users who wish to avoid the overhead incurred at run-time when an 
initialized Reference Vector Area (RVA) is built each time a user invokes the 
data base.  When the option is present, an initialized RVA is built during the 
validation process and is written to a shared data segment file.  The DCB and 
default file name for the shared data segment file is subschema-name$. 
To use the initialized RVA in the shared data segment file, the user must 
compile the FORTRAN program with the CDS option specifying that the common 
area for the RVA be placed in DS8 as follows : 
   !FORTRAN si OVER ,NO (DBM,CDS(rva-name=8)) 
where rva-name is the name of the common Reference Vector Area as shown in the 
FORTRAN include file generated during the validation process.  At runtime the 
DCB and default file name for the shared data segment file is subschema-name$. 
Specifies the maximum number of usable page buffers. 
Format: 
n-received<-[]DBBUFFERS n-desired                               (APL) 
CALL "IDSBUFFERS" USING n-desired, n-received                 (COBOL) 
CALL BUFFERS (n-desired,n-received)                         (FORTRAN) 
DB BUFFERS exp,numeric-variable                               (BASIC) 
Notes: 
1.  If this subroutine is not called, the Data Base Control System will 
    attempt to get 6 buffers. 
2.  The first parameter, n-desired, must be a binary number.  It is the number 
    of buffers desired. 
3.  The second parameter, n-received, is a binary number.  It is the number of 
    buffers actually obtained. 
4.  The number of buffers can dramatically affect performance in some programs 
    and have little impact on other programs. 
5.  Acquiring too many buffers may exceed the system limit of 128 for the 
    number of dynamic data segment pages an ASL can have. 
00001
This subroutine makes possible the optimized loading of a CALC location mode 
record by returning the dbkey of the calc header for which the record is 
destined.  The record can be moved into a SORT input record buffer which 
contains the page numbers.  The SORT can return the records in dbkey order and 
the records can be stored as in the data base part of the SORT output 
procedure. 
Format: 
calc-hdr-dbkey<-[]DBCALC 'record-name'                          (APL) 
CALL "IDSCALC" USING record-name,calc-hdr-dbkey               (COBOL) 
CALL CALC (record-name,calc-hdr-dbkey)                      (FORTRAN) 
DB CALC numeric-variable record-name                          (BASIC) 
Notes: 
1.  CALC records can be stored randomly resulting in at least one I/O per 
    record.  This subroutine is used to store CALC records after sorting by 
    destination calc header data base key.  The calc header data base key is 
    the dbkey of a control record which identifies the page and calc bracket 
    to which the record has been hashed. 
2.  SORT is not available in APL.  The DBCALC function is useful for the 
    interactive user to find the physical location of CALCed records in a data 
    base. 
00001
Specifies data base checkpointing. 
Format: 
dbstatus<-[]DBCHECK check-num                                   (APL) 
CALL "IDSCHECK" USING check-num,db-status                     (COBOL) 
CALL CHECK (check-num,db-status)                            (FORTRAN) 
DB CHECK integer                                              (BASIC) 
Notes: 
1.  The parameter check-num is a one word binary number that is used to 
    identify a checkpoint on the common journal.  A long program may have many 
    checkpoints which may be distinguished using the checkpoint number. 
2.  The db-status is the label of a data item which must contain at least 
    seven characters.  The DB-STATUS cell may be used here. 
3.  If BACKUP was specified in the schema DMCL, this subroutine will force all 
    modified buffers to be written, release all enqueues and release the 
    deadlock journal (transient journal). 
4.  If there is no concurrent access controls and BACKUP is not specified in 
    the schema DMCL, the modified buffers are written. 
5.  All READY and FINISH statements are implicit checkpoints and a CALL to 
    CHECK is not required. 
6.  (BASIC only) The execution of every DB READY, DB FINISH, and DB CHECK 
    establishes a check point for roll back. Under an error condition of a 
    deadlock in the data base, BASIC will resume execution after the most 
    recent executed READY, FINISH or CHECK statement. 
7.  When deadlock is detected, the Data Base Control System will roll all 
    updates out of the data base and transfer control to the first statement 
    after the last checkpoint.  The last checkpoint is the last CALL to CHECK 
    or the last READY or FINISH.  The DB-STATUS cell will be set to 1901100 to 
    indicate that a roll back has occurred. 
8.  The compiler for the programming language does not know that control may 
    reach the statement following the CHECK call by a path other than the 
    normal return.  This may result in unexpected operation of the program if 
    the code optimizer makes assumptions about program flow, and its effect on 
    local variables.  In the following example, the GOTO statement is an 
    important part of the program because it informs the compiler of the true 
    program flow (though it is never executed). 
         FLAG=0 
         CALL CHECK 
     10  IF FLAG=1 ... 
         . 
         . 
         . 
         FLAG=1 
         CALL ROLL 
         GOTO 10 
00001
In COBOL, the source program compilation references the I-D-S/II validated 
subschema, which is named in the SUB-SCHEMA SECTION of the COBOL program.  The 
data base structures that are required at run time are all defined by the 
subschema.  The COBOL object units are then linked.  The common shared library 
and the I-D-S/II Alternate Shared Library are linked automatically. 
In FORTRAN, the source program compilation uses INCLUDE to fetch a file of 
data base labelled common data.  The INCLUDE file is generated by the 
VALIDATOR directive of the DBACS processor.  To maintain the integrity of the 
data base interface, the user is not allowed to change this file in any way. 
It is suggested that the DBM option be specified on all FORTRAN compilations 
to suppress warning error messages which result from mixing data types in 
labeled common.  The FORTRAN object units must then be explicitly linked using 
the ALT=IDS option on the (IBEX) LINK command. 
COBOL_COMPILE
The subschema entry specifies the subschema description to be obtained from 
the subschema file during compilation. 
Format: 
Column 
1        8 
         DATA DIVISION. 
         SUB-SCHEMA SECTION. 
         DB  subschema-name WITHIN schema-name [;PRIVACY KEY IS "literal"]. 
Syntax Rules: 
1.  The literal can be from 1 to 12 characters in length and must be bound by 
    quotation marks. 
2.  The PRIVACY KEY clause must be specified if the subschema referenced by 
    subschema-name is defined to have an invocation privacy lock associated 
    with it. 
3.  The SUB-SCHEMA SECTION must be the first section in the DATA DIVISION. 
4.  The name of the DCB assigned to the subschema fid is the same as the 
    subschema name defined in the SUB-SCHEMA SECTION. 
5.  The subschema file must be supplied by the user.  The file must have write 
    permission so that the successful compilation will be noted in the 
    subschema file directory. 
General Rules: 
1.  The subschema referenced by subschema-name, which has been translated and 
    validated against the schema file referenced by schema-name, is made 
    available to the program for compilation, subject to the following rule. 
2.  The value of the literal is matched to the value of the invocation privacy 
    lock associated with the subschema.  If the value of the literal is equal 
    to the value of the invocation privacy lock, the subschema is made 
    available to the program.  If the values are not equal, the subschema is 
    not made available, all references to data items in it are invalid, and 
    all uses of Data Manipulation Language statements are invalid. 
Example: 
The control stream and initial divisions of a COBOL program that accesses a 
subschema follows. 
    Column 
    1       8 
    !SET SUB-1 subschema-fid 
    !COBOL (IDS) 
            IDENTIFICATION DIVISION. 
            PROGRAM-ID. PROG22. 
                . 
                . 
                . 
            DATA DIVISION. 
            SUB-SCHEMA SECTION. 
            DB SUB-1 WITHIN SCHEMA-1; PRIVACY KEY IS "ABC". 
            FILE SECTION. 
                . 
                . 
                . 
In this example: 
1.  The COBOL compiler is called.  The compiler invoking command includes the 
    IDS option, which causes a listing of the subschema source used by the 
    compilation to be included in listing output. 
2.  The referenced subschema name (SUB-1) is obtained from the file. 
    Successful validation is verified as is the schema name.  The subschema 
    was given a PRIVACY LOCK FOR INVOKING IS "ABC" clause when it was 
    initially translated.  In order to unlock the subschema and properly 
    invoke it, the required privacy key value ABC must be supplied here.  If 
    the proper key is not specified, the subschema is not made available for 
    the compilation.  If the proper key is specified, the subschema is made 
    available and, because the IDS option has been specified on the COBOL 
    command, the subschema is listed. 
00003
00002
00001
COBOL_SUBSCHEMA
Some data base applications require concurrent access for many retrieval and 
update users in a controlled fashion.  Other applications require management 
of many retrieval users and only one update user.  Still other applications 
require exclusive data base access.  The I-D-S/II Data Base Control System 
applies concurrent access controls to all I-D-S/II users uniformly whether 
they are on-line, batch, or transaction processing users.  This is possible 
since there is one common Data Base Control System in the Alternate Shared 
Library and I-D-S/II must be used to manage the files (because of the CP-6 
access control vehicle). 
I-D-S/II supports the following five categories of file sharing.  Each 
category contains members.  The members of a category can share with the other 
members in the same category. 
1.  Multiple Protected Readers       IDSSHARE 
    Multiple Unprotected Readers     IDSSHAREANY 
    Multiple Protected Writers       IDSSHARE 
2.  Multiple Protected Readers       IDSSHARE 
    Multiple Unprotected Readers     IDSSHAREANY 
    Single Protected Writer          IDSSHAREIN 
3.  Multiple Protected Readers       IDSSHAREIN 
    No Writer 
4.  Multiple Unprotected Readers     IDSSHAREANY 
    Single Unprotected Writer        IDSSHAREANY 
5.  Single Writer                    IDSNOSHARE 
Each user may specify the type of sharing possible for each data base area by 
using one of the four subroutines: 
    CALL "IDSSHARE" 
    CALL "IDSSHAREIN" 
    CALL "IDSNOSHARE" 
    CALL "IDSSHAREANY" 
The IDSSHARE subroutine specifies that data base areas may be shared either 
for update or retrieval. 
The IDSSHAREIN subroutine specifies that only other retrieval users may share 
the data base areas. 
The IDSNOSHARE subroutine specifies that one user has exclusive use of the 
data base areas. 
The IDSSHAREANY subroutine specifies that the user does not want concurrent 
access controls and is prepared to handle possible error conditions. 
A more complete discussion of these subroutines and data base lockout is 
included in Section 5. 
Concurrent access is required for all IDSSHARE users, and for IDSSHAREIN users 
with update programs.  Concurrent access implies the use of the CP-6 
enqueue/dequeue facility, and the use of *I transient journals.  The 
enqueue/dequeue facility guarantees that two users will not update the same 
page at the same time.  The transient journal is unique for each user and is 
maintained at the item level to roll back a user in the case of deadlock.  The 
transient journal is also used by RECOVERY to roll users back to the last 
clean point after a system crash. 
Deadlock means that users are waiting for each other to release enqueued 
resources.  There is a possibility of deadlock whenever two or more programs 
are concurrently accessing the same area if at least one of them is updating 
the area.  For example, Program A reads page 1 causing it to be locked with 
shared status.  Program B then also reads page 1 locking it with shared status 
(many programs may lock a page with shared status without interfering with 
each other).  Program A then attempts to update page 1, resulting in a request 
to promote the lock status to exclusive.  This promotion is delayed waiting 
for Program B to remove the shared lock on page 1.  If, instead of removing 
the shared lock on page 1, Program B also attempts to promote to exclusive 
lock status to update page 1, it will be delayed, waiting for Program A to 
remove its shared lock.  The two programs are in deadlock and neither can 
proceed. 
The user that detects deadlock has his data base updates rolled back, receives 
a deadlock error code and has program control transferred to the statement 
following the last READY, FINISH, or CHECK.  Note that a data base and not a 
program roll back occurs.  A test for roll back is appropriate after each 
READY, FINISH or CHECK. 
The maximum number of enqueues and dequeues allowed is limited to the number 
of enqueue elements (MAXENQ) defined by site specific parameters.  This means 
that the number of queue elements allowed by I-D-S/II and the CP-6 system are 
the same.  However, the user should limit the queue elements to a reasonable 
number. 
The IDSCHECK and IDSROLL subroutines are described in Section 5. 
All system errors that result in status codes starting with a 7 usually have 
underlying CP-6 error codes.  Therefore, if DB-STATUS contains a non-zero 
status, IDSSYSERR may be checked.  If this cell is non-zero, it will contain a 
CP-6 error code.  IDSSYSERR is defined in the common shared library and in the 
I-D-S/II interface for FORTRAN. 
CONNECT causes a record stored in the data base to become a member of a named 
set in which the record has been declared to be an AUTOMATIC OPTIONAL, MANUAL 
MANDATORY, or MANUAL OPTIONAL member.  The current run unit is the object of 
the statement. 
Format: 
dbstatus<-[]DBCONNECT '[record-name] [TO] setname'              (APL) 
CONNECT [record-name] TO set-name                             (COBOL) 
CALL CONNECT ([record-name,] set-name)                      (FORTRAN) 
DB CONNECT [record-name] [TO] set-name                        (BASIC) 
Syntax Rules: 
1.  The record-name parameter is not required.  If specified, record-name must 
    be the name of the current record of the run unit. 
2.  The current record of the run unit must be defined to be an AUTOMATIC 
    OPTIONAL, MANUAL MANDATORY, or MANUAL OPTIONAL member of the set specified 
    in the CONNECT statement. 
General Rules: 
1.  Execution of the CONNECT statement causes the current record of the run 
    unit to become a member of the specified set provided that it is not 
    currently a member of the set type. 
2.  The set occurrence to which the current record of the run unit is 
    connected is governed by the set selection criteria.  The record is 
    connected to the set occurrence in accordance with the set ordering 
    criteria of the set type. 
3.  The realms in which the current record of the run unit is stored and in 
    which the record of the affected set are stored must be in update usage 
    mode. 
4.  The current record of the run unit becomes the current record of the set 
    type into which the record has been connected.  Other currency indicators 
    are not affected. 
Notes: 
1.  The schema Data Description Language translator requires the set selection 
    criteria to be by APPLICATION.  In addition, no THEN THRU clauses are 
    allowed.  This means that CONNECT effectively connects the current record 
    of the run unit to the set occurrence identified by the currency indicator 
    for the set type specified. 
2.  The values of sort and duplicate control fields used when connecting the 
    record are those in the record on the data base.  The values in the User 
    Working Area are not used during the execution of the CONNECT statement. 
    A MODIFY should be executed before the CONNECT to change the control keys 
    for the set. 
3.  If an error or exception occurs during the execution of a CONNECT 
    statement, the data base is restored to its state prior to execution of 
    the statement.  In addition, no currency indicators are affected by an 
    unsuccessful statement. 
Examples: 
Consider the following data base relationships: 
                  ----------- 
                 | DIVISION- |-------- 
                 |  RECORD   |        | 
                  -----------         | 
                      |               | 
                      |               | 
                      v               | 
               -------------          | 
              | ORGANIZATION |        |   STAFF-TO 
              |    -UNIT     |        | 
               --------------         | 
                      |               | 
                      |               | 
                      |               | 
                      |               | 
                      | WORKS-FOR     | 
                      |               | 
                      |               | 
                      |               | 
                      |               v 
                      |        ---------- 
                      |       | EMPLOYEE |(MANUAL 
                       ------>|          | Member) 
                               ---------- 
The EMPLOYEE record is a MANUAL member of the STAFF-TO set.  First the proper 
owner record is located: 
    MOVE "nnnnnn" TO DIVISION-NUMBER. 
    FIND ANY DIVISION-RECORD. 
The correct DIVISION-RECORD record is not the current record of the STAFF-TO 
set.  Next the EMPLOYEE record is made the current record of the run unit. 
    MOVE "mmmmmmm" TO EMPLOYEE-NUMBER. 
    FIND ANY EMPLOYEE. 
Assuming that EMPLOYEE is not currently a member of the STAFF-TO set, the 
currency indicator for the STAFF-TO set will not be updated.  Finally, the 
current EMPLOYEE record is made a member of the optional STAFF-TO set, as 
follows: 
    CONNECT EMPLOYEE TO STAFF-TO. 
00004
00002
00003
00001
Passes an encryption seed used to decode area files. 
Format: 
[]DBCRPT (seed)                                                 (APL) 
CALL "IDSCRPT" USING seed                                     (COBOL) 
CALL CRPT (seed)                                            (FORTRAN) 
DB CRPT integer-exp                                           (BASIC) 
General Rules: 
1.  The encryption seed cannot be passed with a SET command and must be 
    specified before the file READY. 
2.  The seed parameter is a one word binary item containing the encryption 
    seed. 
3.  Encryption is specified by the data base administrator for each data base 
    area. 
00001
  APL                 COBOL               FORTRAN            BASIC 
DBSTATUS           DB-STATUS           DBSTATUS           DBSTATUS 
DBREALM            DB-REALM-NAME       DBREALM            DBREALM$ 
DBSET              DB-SET-NAME         DBSET              DBSET$ 
DBRECORD           DB-RECORD-NAME      DBRECORD           DBRECORD$ 
DBPRIVACY          DB-PRIVACY-KEY      DBPRIVACY          DBPRIVACY$ 
DIRECTREFERENCE    DIRECT-REFERENCE    DIRECTREFERENCE    DIRECTREFERENCE 
DBDATANAME         DB-DATA-NAME        DBDATANAME         DBNAME$ 
DBKEYNAME          DB-KEY-NAME         DBKEYNAME          DBKEYNAME$ 
BUFFERS
CALC
CHECK
CONNECT
CRPT
DISCONNECT
ERASE
FIND_CALC
FIND_CURRENT
FIND_DIRECT
FIND_DUPLICATE
FIND_KEY
FIND_MATCH
FIND_OWNER
FIND_POSITION
FINISH
GET
IDSKEEP
MODIFY
USE_FOR_PRIVACY
READY
FIND
ROLL
RPTSTATS
STATSOFF
STATSON
STORE
TRACEOFF
TRACEON
BUFFERS
CALC
CHECK
CONNECT
CRPT
DISCONNECT
ERASE
FIND_CALC
FIND_CURRENT
FIND_DIRECT
FIND_DUPLICATE
FIND_KEY
FIND_MATCH
FIND_OWNER
FIND_POSITION
FINISH
GET
IDSKEEP
This function returns the sets or records that the supplied record or set may 
be a member of and other attributes of membership. 
Format: 
[line no.] MAT aname=DBMEMBERINFO$(strexp)                    (BASIC) 
General Rules: 
strexp    is either the name of a set or record. 
aname    is dynamically dimensioned to N by 3. 
Notes: 
1.  The first column indicates the sets or records that the supplied record or 
    set may be a member of. 
2.  The second column contains "MANUAL' or "AUTOMATIC" to tell what the 
    membership is. 
3.  The third column contains "OPTIONAL" or "MANDATORY" to tell another 
    membership attribute. 
00001
00002
MODIFY
    This function returns a string which is the name of the record which owns 
    the set and the names of sets that this record may own. 
Format: 
DBOWNERINFO$(strexp1) 
[line no.] MAT aname=DBOWNERINFO$(strexp2)                    (BASIC) 
General Rules: 
strexp1    must be a set name.  The result returned is a string which is the 
name of the record owning this set. 
strexp2    must be a record name.  The results returned are strings which are 
the names of the sets that this record may own. 
aname    is dynamically dimensioned. 
See also HELP (IDS) DB_MEMBER 
HELP (IDS) INQUIRY 
00001
USE_FOR_PRIVACY
READY
FIND
ROLL
RPTSTATS
STATSOFF
STATSON
STORE
TRACEON
DISCONNECT logically removes a record from a specified set if the record is an 
AUTOMATIC OPTIONAL or MANUAL OPTIONAL member of the set.  The current record 
of the run unit is the object of the statement. 
Format: 
dbstatus<-[]DBDISCONNECT '[record-name] [FROM] set-name'        (APL) 
DISCONNECT [record-name] FROM set-name                        (COBOL) 
CALL DISCONNECT ([record-name,] set-name)                   (FORTRAN) 
DB DISCONNECT [record-name] [FROM] set-name                   (BASIC) 
Syntax Rules: 
1.  Record-name is not required.  If specified, record-name must be the name 
    of the current record of the run unit. 
2.  The current record of the run unit must be defined to be an AUTOMATIC 
    OPTIONAL or MANUAL OPTIONAL member of the set specified in the DISCONNECT 
    statement. 
General Rules: 
1.  Execution of the DISCONNECT statement causes the current record of the run 
    unit to be removed from membership in the specified set provided that it 
    is currently a member of the set type. 
2.  The realm in which the current record of the run unit is stored and in 
    which the records of the affected set are stored must be in update usage 
    mode. 
3.  If the current record of the run unit is the current record of the set 
    specified, the currency indicator for the set is updated to identify the 
    position between the two records where the disconnect record was.  If the 
    current record of the run unit is not the current record of the set 
    specified, the currency indicator is not affected.  Other currency 
    indicators are not affected. 
Notes: 
1.  The current record of the specified set may become unavailable, as 
    described in General Rule 3.  However, the NEXT, PRIOR, and OWNER records 
    are available.  This means that the currency indicator is valid for all 
    subsequent data manipulation statements requiring a current record of a 
    set except FIND CURRENT WITHIN set-name.  For example, the following 
    sequence is valid: 
         DISCONNECT FROM set-name. 
         FIND NEXT WITHIN set-name. 
2.  If an error or exception occurs during the execution of a DISCONNECT 
    statement, the data base is restored to the state it was before the 
    statement was executed.  In addition, no currency indicators are affected 
    by an unsuccessful statement. 
00002
00003
00001
  Statement      Description 
ACCEPT         Obtains the data base key or realm names held within the 
               Data Base Control System currency indicators. 
CONNECT        Inserts a new record occurrence into a set in which the 
               record has been defined to be a MANUAL or an OPTIONAL 
               member. 
DISCONNECT     Removes a record from a set in which it resides as an 
               OPTIONAL member. 
ERASE          Logically removes a record from the data base.  Removes all 
               subordinate member records, if any. 
FIND           Locates any record in the data base subject to a variety of 
               record selection expression options. 
FINISH         Makes a realm unavailable to further access. 
GET            Obtains the contents of a current record and transforms any 
               specified data items into the format needed by the program. 
MODIFY         Alters the contents of data items in the data base and/or 
               the set relationships of a record. 
READY          Makes the contents of a realm available for processing. 
SET            Moves data base key items within the program (COBOL only). 
STORE          Adds a new record occurrence to the data base. 
USE            Defines to the Data Base Control System any DB-EXCEPTION or 
               DB-PRIVACY procedures to be automatically invoked when 
               needed. 
USAGE IS       Defines a data item as a data base key in the file 
               description entries or in the Working Storage Section of the 
               Data Division (COBOL only). 
For specific information, enter HELP (IDS) statement_name 
MEMBER
    ERASE removes one or more records from the data base.  The current record 
    of the run unit is the object of the statement.  Physical deletion is 
    assumed for all data base areas. 
Format: 
dbstatus<-[]DBERASE '[record-name] [ALL MEMBERS]'               (APL) 
ERASE [record-name] [ALL MEMBERS]                             (COBOL) 
CALL ERASER ([record-name,][ALL])                           (FORTRAN) 
DB ERASE [record-name] [ALL MEMBERS]                          (BASIC) 
Syntax Rules: 
1.  Record-name is not required.  If specified, record-name must be the name 
    of the current record of the run unit. 
General Rules: 
1.  Execution of the ERASE statement causes one or more records to be removed 
    from the data base. 
2.  The realm in which the current record of the run unit is stored and in 
    which the records of the affected sets are stored must be in update usage 
    mode. 
3.  If ALL is not specified and the current record of the run unit is not the 
    owner of a set that currently has members, the record is removed from the 
    data base.  It is also disconnected from any other sets it is currently a 
    member of and the record key entries are removed for all of the record 
    keys defined in the record. 
4.  If ALL is not specified and the current record of the run unit is the 
    owner of a set that currently has members, an exception condition results. 
5.  If ALL is specified, and the current record of the run unit is the owner 
    of a set that currently has members, all of these members records are also 
    removed from the data base.  Any record so removed is treated as an object 
    record of the ERASE statement.  The process is repeated until all records 
    have been removed from the data base that are hierarchically related to 
    the current record of the run unit.  If any object record is currently the 
    member of another set, the record is disconnected from that set. 
6.  If ALL is specified, and the current record of the run unit is not the 
    owner of a set that currently has members, execution proceeds as if ALL 
    had not been specified. 
7.  Currency indicators are affected as follows: 
    a.  The indicator for current record of the run unit is set to null. 
    b.  If any record removed from the data base is the current record of its 
        record-name, the currency indicator for the record-name is set to 
        null. 
    c.  If any record removed from the data base is the current record of a 
        set type that it is the owner of, the currency indicator for the set 
        type is set to null. 
    d.  If any record removed from the data base is the current record of a 
        set type that it is a member of, the currency indicator for the set 
        type is updated to identify the position between the two records where 
        the remove record had been. 
    e.  If an entire set occurrence is removed from the data base as a result 
        of an ERASE ALL statement and the current record of the set type was 
        one of the records removed, the currency indicator for the set type is 
        set to null. 
    f.  If any record removed from the data base is the current record of its 
        realm, the currency indicator for the realm is updated to identify the 
        position between the two data base keys where the removed record 
        occurred. 
    g.  If any record from the data base is the current record of a record key 
        type, the currency indicator for the key type is updated to identify 
        the position between the two records where the removed record 
        occurred. 
Notes: 
1.  As specified in General Rules 3 and 5, each object record is disconnected 
    from any sets it is currently a member of.  This means no special 
    consideration need be made for OPTIONAL MANUAL sets.  If an object record 
    is currently a member of an OPTIONAL MANUAL set, it will be disconnected 
    before the record is removed from the data base.  If an object record is 
    not currently a member of an OPTIONAL MANUAL set, no error will result and 
    the record will be removed from the data base. 
2.  The current record of a set may become unavailable as described in General 
    Rule 7d; however, the next, prior, and owner records are available.  This 
    means the currency indicator is valid for subsequent data manipulation 
    statements requiring a current record of a set except FIND CURRENT WITHIN 
    set-name.  For example, the following sequence is valid: 
        ERASE B. 
        FIND NEXT WITHIN A-B. 
    where the B record is a member of the A-B set. 
3.  The current record of a realm may become unavailable as described in 
    General Rule 7f; however, the next and prior records are available.  this 
    means the currency indicator is valid for subsequent data manipulation 
    statements requiring a current record of a realm except FIND CURRENT 
    WITHIN realm-name. 
4.  If an error or exception is encountered during the execution of an ERASE 
    statement, the data base may not be restored to its original state.  The 
    data base will be in a consistent state in that each object record will 
    either be removed or will still be a member of all sets that it was before 
    the ERASE was executed.  No damaged sets or records will be a member of 
    some sets and not a member of other sets.  In addition, the currency 
    indicators may not be restored to what they were before the ERASE was 
    executed.  If it is important to recover completely, the CHECKPOINT and 
    ROLLBACK facilities should be used. 
00002
00003
00001
ERASE
Each data base application program must have access to the schema, subschema 
and some or all of the data base areas and key files.  File access is 
controlled by the file management system through a list of accounts with 
specified privileges.  Each account granted access may be granted access in 
the account authorization.  In addition, each file has access controls 
including the specification of accounts and the specification of the use of 
access control vehicles, such as IDS, APL, COBOL, FORTRAN, and IDP.  Thus, a 
data base can be authorized to ALL accounts without list authorization and, if 
IDS is specified as an access vehicle with general access, no one can list the 
file or access it without using the Data Base Control System. 
The originator (creator or owner) of the file has unrestricted access to it 
and may change the access permissions using PCL.  The Peripheral Conversion 
Language (PCL) processor is described in the CP-6 Programmer Reference Manual 
(CE40).  originator should make files available to the accounts using the data 
base.  Data base areas can be created specifying a list of accounts which will 
have access to the initialized data base (using the DBUTIL ACCESS list 
clause). 
The schema, the subschema, and all of the needed data base areas must be 
assigned to the program.  Files are known to the program by logical names used 
in the schema or subschema Data Description Language.  In CP-6, these logical 
names are used as Data Control Block (DCB) names.  The DCBs are assigned to 
CP-6 file identifiers by (IBEX) SET commands or by using the IDSSET 
subroutine.  A file identifier is a string naming the file, account, password 
and other items of file identification (such as the private pack serial 
number).  The format of the SET command is: 
    !SET dcb fid[,optionlist] 
Examples: 
    !SET STUSCHEMA XYZW.SOMEACCT.SUPERPAS    Sets schema to file XYZW. 
    !SET RET-SUB LMNOP.SOMEACCT.SUPERPAS     Sets subschema to file LMNOP. 
    !SET AREA-1 FILE1.SOMEACCT.SUPERPAS      Sets a realm to file FILE1. 
    !SET AREA-2 FILE2.SOMEACCT.SUPERPAS      Sets a realm to file FILE2. 
See the CP-6 Programmer Reference Manual (CE40) for a detailed explanation of 
the SET command. 
In addition to using SET commands, DCBs contained in the run unit may be used 
to perform the association of logical to physical names.  These DCBs can be 
either compiled directly into the program or can be acquired dynamically.  If 
a DCB exists with the proper name, the values in the DCB will be used as the 
defaults for the open of the file.  If an IBEX SET or IDSSET is done on the 
same name, the values specified override those specified in the program's DCB. 
No matter how the association is done, the DCB names are the names of the 
schema, subschema, and realms, as defined in the subschema used by the 
application program. 
A convenient set of defaults may be used, if desired.  If the user does not 
specify a file name when the schema, subschema or the realm are created, the 
file identifier will be the same as the logical names defined in subschema 
Data Description Language.  (At run time, the Data Base Control System 
defaults the file names to the logical names used in the program). 
Furthermore, the account of the schema and the realms are assumed to be those 
assigned to the subschema.  Therefore, a simplified set of file assignments is 
possible depending on installation needs. 
Separating the logical name of the file from the physical name of the file 
permits creation of test data bases and template data bases in the same 
account with different names.  Alternate key files are sometimes associated 
with INTEGRATED areas.  The alternate key files never require SET commands. 
Alternate key files are located by appending a ':' character to the area file 
name in the same account. 
00001
    FIND establishes a specific record occurrence in the data base as the 
    object of subsequent statement. 
Format: 
            {|{REALM       }|} 
[]DBRETAIN '{|{SETS        }|}'                                 (APL) 
            {|{setname-list}|} 
            {|{RECORD      }|} 
[]DBFIND 'record-selection-expression'                          (APL) 
FIND record-selection-expression 
        [                         {|REALM         |}] 
        [                         {|{SETS        }|}] 
        [, RETAINING CURRENCY FOR {|{setname-list}|}]         (COBOL) 
        [                         {|RECORD        |}] 
                       {|REALM        |} 
CALL RETAIN (set-list) {|{SETS       }|})                   (FORTRAN) 
                       {|setname-list}|} 
                       {|RECORD       |} 
CALL FIND (record-selection-arguments)                       (FORTRAN) 
          {|REALM       |} 
DB RETAIN {|SETS        |}                                    (BASIC) 
          {|setname-list|} 
          {|RECORD      |} 
Syntax Rules: 
1.  Setname-list consists of one or more set-names separated by commas or 
    blanks except that in FORTRAN commas must be used. 
General Rules: 
1.  Execution of the FIND statement causes the record referenced by the 
    record-selection-expression to become the current record of the run unit. 
    The realm name for the record found is placed in the special register 
    DB-REALM-NAME and the name of the record found is place in DB-RECORD-NAME. 
2.  Execution of a FIND statement causes the record referenced by a 
    record-selection-expression to become the current record of a record key 
    type if the record was accessed through that particular key type (i.e., 
    FIND record-name USING key-name). 
Notes: 
1.  The execution of a FIND statement does not make the selected record 
    contents available to the program; it merely identifies the record for use 
    in subsequent statements.  To obtain the contents of data items within the 
    record, a GET statement must be issued. 
2.  If an exception condition is encountered, no currency indicators are 
    changed.  However, the special register DB-REALM-NAME, DB-SET-NAME, 
    DB-KEY-NAME, DB-DATA-NAME, and DB-RECORD-NAME are updated. 
3.  The currency indicator for an OPTIONAL MANUAL set will not be updated if 
    the record found is not a member of the set.  The currency indicator will 
    be updated if the record found is a member of the set. 
    The following rules which refer to the RETAINING clause of COBOL also 
    apply to the []DBRETAIN statement in APL and the CALL RETAIN statement in 
    FORTRAN. 
3.  If the RETAINING phrase is not specified, the record referenced by the 
    record-selection-expression becomes the current record of the realm, the 
    current record of its record type, and the current record of all sets in 
    which it is a tenant. 
4.  If the RETAINING phrase with the optional word REALM is specified, no 
    realm currency indicators are changed. 
5.  If the RETAINING phrase with the optional word SETS is specified, no set 
    type currency indicators are changed. 
6.  If the RETAINING clause with the optional word RECORD is specified, no 
    record type currency indicators are changed. 
7.  If the RETAINING clause with the optional setname-list is specified, the 
    set currency indicators for the named sets are not changed. 
    See also: 
    HELP (IDS) FIND_DIRECT 
    HELP (IDS) FIND_CALC 
    HELP (IDS) FIND_DUPLICATE 
    HELP (IDS) FIND_POSITION 
    HELP (IDS) FIND_CURRENT 
    HELP (IDS) FIND_OWNER 
    HELP (IDS) FIND_MATCH 
    HELP (IDS) FIND_KEY 
00002
00003
00001
This format is used for LOCATION MODE IS CALC records. 
[]DBFIND '{ANY      } record-name                               (APL) 
          {DUPLICATE} 
FIND {ANY      } record-name                                  (COBOL) 
     {DUPLICATE} 
CALL FIND {ANY      } ,record-name)                         (FORTRAN) 
          {DUPLICATE} 
DB FIND {ANY      } record-name                               (BASIC) 
        {DUPLICATE} 
General Rules: 
1.  The record referenced by record-name must have a calculation location 
    mode. 
2.  A realm is selected, if there is a choice.  The schema supplied area 
    identification parameter or procedure is used. 
3.  If the ANY phrase is specified, the calculation key values for the record 
    named by record-name are used to calculate the data base key value for the 
    identified record.  The values must be moved in to control fields before 
    the FIND statement is issued.  If more than one record of the named record 
    type contains calculation key values equal to those in the record area, 
    the record identified is the one whose data base key is the lowest. 
4.  If the DUPLICATE phrase is specified, then the record type of the current 
    record of the run unit must be the record type of the record referenced by 
    record-name.  If it is not, the exception condition 03300 is returned. 
    The calculation key values of the record identified are equal to the 
    calculation key in the current record of the run unit.  The Data Base 
    Control System searches for the identified record beginning with the 
    current record of the run unit and proceeds in sequence by ascending data 
    base key values.  The first record found after the current record of the 
    run unit, with the proper calculation key values, is the record 
    identified. 
5.  If a record with the proper calculation key values is not found the 
    exception condition "no record found to satisfy record selection 
    expression" (02400) is returned and currency indicators are left. 
00001
This format is used to find the current record of a realm or set or key. 
                                                  {realm-name} 
dbstatus<-[]DBFIND 'CURRENT [record-name] [WITHIN {set-name  }]' (APL) 
                                                  {key-name  } 
                            [        {realm-name}] 
FIND CURRENT [record-name]; [WITHIN  {set-name  }]             (COBOL) 
                            [        {key-name  }] 
                                [ {realm-name}] 
CALL FIND (CURRENT[,record-name][,{set-name  }])             (FORTRAN) 
                                [ {key-name  }] 
                              [       {realm-name} 
DB FIND CURRENT [record-name] [WITHIN {set-name  }            (BASIC) 
                              [       {key-name  } 
General Rules: 
1.  If set-name is specified, the record identified is the current record of 
    the set type. 
2.  If realm-name is specified, the record identified is the current record of 
    the realm-name. 
3.  If record-name and set-name are specified, record-name must be the current 
    record of the set type indicated. 
4.  If record-name and realm-name are specified, record-name must be the 
    current record of the realm referenced by realm-name. 
5.  If record-name is specified and the WITHIN clause is omitted, the record 
    identified is the current record of the record type indicated. 
6.  If neither realm-name, set-name, key-name, nor record-name are specified, 
    the record identified by the statement is the current record of the run 
    unit. 
7.  If key-name is specified, the record identified is the current record of 
    the record key type. 
8.  If record-name and key-name are specified, record-name must be the current 
    record of the record key type specified. 
00001
dbstatus<-[]DBFIND '[record-name] DBKEY IS dbkey'               (APL) 
FIND [record-name]; DB-KEY IS dbkey                           (COBOL) 
CALL FIND ([record-name],DBKEY,dbkey)                       (FORTRAN) 
DB FIND [record-name] DBKEY [IS] {dbkey           }           (BASIC) 
                                 {numeric-variable} 
General Rules: 
1.  dbkey must be defined as a data base key item. 
2.  The record identified is the record whose data base key value is equal to 
    the value of the data item referenced by dbkey. 
3.  Record-name is not required.  If specified, the record found must be of 
    the record type specified by record-name. 
4.  In COBOL, a program value must be MOVEed to DIRECT-REFERENCE and then 
    dbkey must be SET to DIRECT REFERENCE. 
00001
This format is used to find a duplicate of current record of set using values. 
dbstatus<-[]DBFIND 'DUPLICATE WITHIN set-name USING identifier-list'  (APL) 
FIND DUPLICATE WITHIN set-name USING identifier-list                (COBOL) 
CALL FIND (DUPLICATE,set-name,identifier-list)                    (FORTRAN) 
DB FIND DUPLICATE [WITHIN] set-name [USING] identifier              (BASIC) 
General Rules: 
1.  Each identifier specified in identifier-list must be defined in the record 
    description entry of the subschema for the current record of the set type 
    referenced by set-name. 
2.  Identifiers in identifier list are separated by commas or blanks except 
    that in FORTRAN they must be separated by commas. 
3.  The record identified: 
    a.  Is a member of the set occurrence identified by the currency indicator 
        for set-name. 
    b.  Has a record type equal to the current record of the set type 
        referenced. 
    c.  Has the contents of the data item referenced by the identifiers equal 
        to those in the current record of the set type referenced. 
4.  The Data Base Control System begins its search at the next record in the 
    order defined by the set ordering criteria of the set type reference. 
5.  The Data Base Control System proceeds in its search in the order defined 
    by the set ordering criteria of the set type referenced. 
Notes: 
1.  The values of the identifiers used in the search are those in the record 
    on the data base.  The values in the User Working Area are not used during 
    the execution of the FIND DUPLICATE statement. 
2.  If the owner record type is encountered before a duplicate record is 
    found, an "end of set" (02100) exception condition results.  If the 
    duplicate record exists between the first and the current record of the 
    set, it will not be found. 
00001
00002
This format is used to find records through their alternate keys.  It is also 
used to locate INDEXED records using their primary keys. 
                    {{FIRST      }              } 
dbstatus<-[]DBFIND '{{NEXT       } [record-name]} USING key-name'(APL) 
                    {record-name                } 
     {{FIRST}              } 
FIND {{NEXT } [record-name]} USING key-name                    (COBOL) 
     { record-name         } 
           {{FIRST}               } 
CALL FIND ({{NEXT } [,record-name]},USING,key-name)          (FORTRAN) 
           {record-name           } 
        {{FIRST}              } 
DB FIND {{NEXT } [record-name]} USING key-name                 (BASIC) 
        {record-name          } 
General Rules: 
1.  Key-name must be defined in a key-description-entry in the subschema. 
2.  Record-name must be defined in the subschema and must be a record type 
    whose record key is identified by key-name. 
3.  The schema-supplied area identification parameter or procedure is used 
    when the FIRST and NEXT options are not specified to select a realm if 
    there is a choice. 
4.  Key-name identifies a record key for accessing a record type defined in 
    the subschema. 
5.  A given key-name can be referenced with more than one record type defined 
    in the subschema, allowing multiple record types to be accessed via the 
    same record key. 
6.  A record can have more than one record key by which the record may be 
    accessed.  Each record key is identified by a key-name that is specified 
    in a key-description-entry in the subschema. 
7.  Records are maintained in ascending order of sequence by record key 
    content for each key-name specified for record types in the subschema. 
8.  If record-name is specified, only the record type referenced by 
    record-name is considered in evaluating the record selection expression. 
9.  If record-name is not specified, all record types defined in the subschema 
    whose record key is identified by key-name are considered in evaluating 
    the record-selection-expression. 
10. Upon successful completion of the record-selection-expression, the record 
    found is established as the current record of the specified record key. 
    Current of record for all other record keys is left unchanged. 
11. If the FIRST or NEXT options are not specified, the value of the data item 
    in the record area for record-name, which constitutes the record key 
    referred to by key-name, is used to identify the record to be selected. 
    If a record of the named record type with the specified key values is not 
    found, and: 
    a.  There are no records of the named record type whose key value is 
        greater than the specified key value, the exception condition END OF 
        REALM HAS BEEN REACHED (02100) is returned.  Currency indicators are 
        left unchanged. 
    b.  A record of the named record type whose key value is greater than the 
        specified key value is found, the exception condition RECORD RETURNED 
        WHOSE KEY VALUE IS GREATER THAN THE SPECIFIED KEY VALUE (02401) is 
        returned.  Current of key-name, current of realm, current of run and 
        current of record-name are set to the occurrence of record-name whose 
        key value is next higher than the specified key value. 
12. If the FIRST option is specified, the record selected is the record whose 
    record key value is lowest within the logical ordering of records 
    specified for key-name. 
13. If the NEXT option is specified, the record selected is the record whose 
    record key value is next higher relative to the current record key of 
    record types referred to by key-name. 
14. If the FIRST or NEXT options are specified and a record occurrence of the 
    record type specified by the record selection expression is not found, the 
    exception condition END OF REALM HAS BEEN REACHED (02100) is returned. 
    Currency indicators are left unchanged. 
15. The FIRST or NEXT option can only be specified after the current of key 
    has been established.  The current of key may be established by FIND 
    record-name. 
16. Currency indicators for record keys are not affected by any other 
    allowable format of the FIND statement. 
00001
This format is used to find a record within a set with matching program 
values. 
dbstatus<-[]DBFIND 'record-name WITHIN set-name [CURRENT] 
[USING identifier-list]'                                                 (APL) 
FIND record-name; WITHIN set-name [CURRENT] [USING identifier-list]    (COBOL) 
CALL FIND (record-name,WITHIN set-name[,CURRENT][,identifier-list])  (FORTRAN) 
DB FIND record-name [WITHIN] set-name CURRENT [USING] identifier-list  (BASIC) 
General Rules: 
1.  Identifier-list items are separated by commas or blanks except that in 
    FORTRAN they must be separated by commas. 
2.  Identifier-list items must be defined in the record description entry of 
    the subschema of the record type referenced by record-name. 
3.  Record-name must be defined in the schema Data Description Language as a 
    member of the set type referenced by set-name. 
4.  The record identified has a type equal to that of the record referenced by 
    record-name. 
5.  If the CURRENT phrase is specified, the record identified is a member of 
    the set in which the current record of the set type referenced by set-name 
    is a tenant. 
6.  If the CURRENT phrase is not specified, the Data Base Control System 
    proceeds in its search as follows: 
    a.  The correct set occurrence is selected according to the set selection 
        rules specified in the schema Data Description Language. 
        (1)  The entry point record is selected by one of three methods: by 
             APPLICATION (currency indicator for set type); CALC_KEY 
             (randomize specified control fields); or DATA_BASE_KEY (data base 
             key of record supplied by program). 
        (2)  Each intervening set is searched based on the keys defined in the 
             schema Data Description Language.  Each set searched corresponds 
             to a THEN THRU clause in the set entry of the schema Data 
             Description Language. 
        (3)  The last set searched identifies the set occurrence in which the 
             identified record is a member.  If there are no THEN THRU clauses 
             in the schema Data Description Language, the entry point record 
             identifies the set occurrence in which the identified record is a 
             member. 
    b.  The set occurrence identified by the set selection criteria, as 
        described above, is searched to locate the record in which the 
        contents of the items in identifier-list are equal to the contents of 
        those data items in the User Working Area.  Only records of the type 
        referenced by record-name are considered in this search.  Other record 
        types are ignored. 
7.  If the USING phrase is specified, the record identified has the contents 
    of the data item referenced by the items in identifier-list equal to these 
    data items in the User Working Area. 
8.  If the USING phrase is not specified, the record identifier is the first 
    member of set-name according to the set ordering criteria for that set. 
Notes: 
1.  If the entry point record as described in Rule 6a(1) is identified by CALC 
    key and the record can reside in more than one realm, realm selection will 
    be invoked.  The schema-supplied area identification parameter or 
    procedure is used.  The CALC keys for this record must be initialized 
    before executing the FIND statement. 
2.  If the entry point record as described in Rule 6a(1) is identified by 
    APPLICATION, the current record of the set type specified in the schema 
    Data Description Language must be established before executing the FIND 
    statement.  This set type is the one referenced by the first THRU phrase 
    of the SELECTION clause of the SET subentry in the schema Data Description 
    Language.  The record identified may be either owner or member of the set 
    type. 
3.  If the entry point as described in Rule 6a(1) is identified by 
    DATA_BASE_KEY, the data base parameter specified in the schema Data 
    Description Language must be set to the correct value before executing the 
    FIND statement.  The record identified must be the owner of the set. 
4.  The set selection keys (if any) as described in Rule 6a(2) must be set to 
    the correct values before executing the FIND statement. 
5.  If a set occurrence is not found which satisfies the set selection 
    criteria as described in Rule 6a, the exception condition SET SELECTION 
    NOT SATISFIED (02300) is returned.  This can occur during any of the steps 
    described in Rule 6a.  The special register DB-SET-NAME will identify 
    which step failed. 
6.  If the correct set occurrence is found, but a record cannot be found that 
    satisfies the record selection expression as described in Rule 6b, the 
    exception condition RECORD SELECTION EXPRESSION NOT SATISFIED (02400) is 
    returned. 
7.  The search of the set occurrence as described by Rule 6b will search the 
    entire set occurrence.  This is of significance when the set selection 
    rules specify the entry point record by APPLICATION and there are no THEN 
    THRU phrases specified in the schema Data Description Language.  In this 
    case, the search will proceed from the current record of the set type, 
    past subsequent member records, past the owner of the set, and past the 
    records between the owner and the current record of the set.  Only when 
    all of the records of the identified set occurrence have been searched in 
    this manner will an exception condition be returned. 
00001
00002
This format is used to find the owner of the current of set. 
dbstatus<-[]DBFIND 'OWNER WITHIN set-name'                       (APL) 
FIND OWNER; WITHIN set-name                                    (COBOL) 
CALL FIND (OWNER, set-name)                                  (FORTRAN) 
DB FIND OWNER [WITHIN} set-name                                (BASIC) 
General Rules: 
1.  The set type referenced by set-name must not be a singular set. 
2.  The record type defined in the schema Data Description Language as the 
    owner of the set type referenced by set-name must be defined in the 
    subschema. 
3.  In some complex network structures it is advisable to use the optional 
    RETAINING CURRENCY FOR... clause to insure that other set currencies are 
    not altered by the execution of the FIND.  When the owner record is found, 
    it is made the current record of all set types in which it is a tenant. 
    Consider the following network structure for an organization chart 
    application: 
                        ------------------- 
                       | ORGANIZATION-UNIT | 
                        ------------------- 
                            |         | 
                            |         | 
                            |         | 
                SUPERIOR    |         |    SUBORDINATE 
                            |         | 
                            |         | 
                            v         v 
                          -------------- 
                         | RELATIONSHIP | 
                          -------------- 
    When traversing the SUPERIOR set to locate all other ORGANIZATION-UNITS 
    which are subordinate to the current ORGANIZATION-UNIT record, the FIND 
    OWNER WITHIN SUBORDINATE statement issued after each RELATIONSHIP record 
    has been found.  The new ORGANIZATION-UNIT record will reset the current 
    of set type indicator for the SUPERIOR set, thereby terminating the 
    initial retrieval.  If instead, the statement is written: 
        FIND OWNER WITHIN SUBORDINATE; 
        RETAINING CURRENCY FOR SETS 
    the current record of SUPERIOR set type remains unchanged, when the new 
    owner ORGANIZATION-UNIT is found, allowing the next RELATIONSHIP record to 
    be found. 
4.  The record identified is the owner of the set occurrence identified by the 
    currency indicator for set-name. 
00001
This format is used to find the relative or absolute position of records 
within the realm or within a set. 
                    {NEXT   } 
                    {PRIOR  } 
                    {FIRST  } 
dbstatus<-[]DBFIND '{LAST   } [record-name] WITHIN  {set-name  }'  (APL) 
                    {integer}                       {realm-name} 
     { NEXT      } 
     { PRIOR     } 
     { FIRST     } 
FIND { LAST      } [record-name]; WITHIN {set-name  }            (COBOL) 
     { integer   }                       {realm-name} 
     { identifier} 
            { NEXT       } 
            { PRIOR      } 
            { FIRST      } 
CALL FIND ( { LAST       } [,record-name],{set-name  } )       (FORTRAN) 
            { integer    }                {realm-name} 
            { identifier } 
        {NEXT      } 
        {PRIOR     } 
DB FIND {FIRST     } [record-name] [WITHIN] {set-name  }         (BASIC) 
        {LAST      }                        {realm-name} 
        {integer   } 
        {identifier} 
General Rules: 
1.  Integer may be signed.  This allows a relative forward or backward 
    reference. 
2.  The data item referenced by identifier must be a signed elementary integer 
    (i.e., an APL integer, COBOL USAGE COMP-6, or FORTRAN INTEGER). 
3.  Record-name, if specified, must be defined in the subschema. 
4.  If a record-name is not specified, all record types defined in the 
    subschema are considered in evaluating the record selection expression. 
    Any records defined in the schema but not in the subschema are ignored. 
5.  If record-name is specified, only the record type of the referenced record 
    is considered in evaluation of the record selection expression.  All other 
    record types are ignored. 
6.  If the NEXT phrase and a realm-name are specified, the record identified 
    is the one whose data base key value is the next higher, relative to the 
    data base key value of the current record of the realm referenced by the 
    realm-name. 
7.  If the PRIOR phrase and a realm-name are specified, the record identified 
    is the one whose data base key value is the next lower, relative to the 
    data base key value of the current record of the realm referenced by the 
    realm-name. 
8.  If the FIRST phrase and a realm-name are specified, the record identified 
    is the one whose data base key value is the lowest, relative to all 
    records stored in the realm referenced by the realm-name.  This is the 
    first record stored in the realm. 
9.  IF the LAST phrase and a realm-name are specified, the record identified 
    is the one whose data base key value is the highest, relative to all 
    records stored in the realm referenced by the realm-name. 
10. If integer or identifier is specified, and a realm-name is specified, the 
    record identified is the one whose ordinal position in the realm is equal 
    to the value of integer or the contents of the data items referenced by 
    identifier.  If the value of integer or the contents of the data item 
    referenced by identifier is positive, the ordinal position is relative to 
    the record whose data base key value is the lowest in the realm referenced 
    by realm-name.  If negative, the ordinal position is relative to the 
    record whose data base key value is the highest in the realm referenced by 
    realm-name. 
11. If the NEXT phrase and set-name are specified, the record identified is 
    the next record in the set, relative to the current record of the set type 
    referenced by set-name according to the set ordering criteria for that set 
    type. 
12. If the PRIOR phrase and set-name are specified, the record identified is 
    the prior record in the set, relative to the current record of the set 
    type referenced by set-name according to the set ordering criteria for 
    that set type. 
13. If the FIRST phrase and set-name are specified, the record identifier is 
    the first member of the set in which the current record of the set type 
    referenced by set-name is a member, according to the set ordering criteria 
    for that set type. 
14. If the LAST phrase and set-name are specified, the record identified is 
    the last member of the set in which the current record of the set type 
    referenced by set-name is a member, according to the set ordering criteria 
    for that set type. 
15. If integer or identifier is specified, and set-name is specified, the 
    record identifier is the one whose ordinal position is the set in which 
    the current record of the set referenced by set-name is a member.  The 
    ordinal position is equal to the value of integer or the contents of the 
    data item referenced by identifier.  If the value of integer or the 
    contents of the data item referenced by identifier is positive, the 
    ordinal position is relative to the first member of the set, according to 
    the set ordering criteria of that set type.  If negative, the ordinal 
    position is relative to the last member of the set, according to the set 
    ordering criteria of that set type. 
00001
    FINISH terminates the availability of one or more realms to the program. 
    A FINISH with no argument list will release buffers and contents in the 
    Alternate Shared Library.  The explicit FINISH of named realms will keep 
    the buffers and contents. 
Format: 
dbstatus<-[]DBFINISH '[realm-list]'                             (APL) 
FINISH [realm-list]                                           (COBOL) 
CALL FINISH [(realm-list)]                                  (FORTRAN) 
DB FINISH [realm-name]                                        (BASIC) 
General Rules: 
1.  Execution of the FINISH statement terminates the availability of the 
    affected realm. 
2.  If realm-list is specified, the ready mode of the specified realms is 
    terminated. 
3.  If realm-list is not specified, the ready mode of all realms is 
    terminated. 
4.  At the completion of the execution of a FINISH statement, all currency 
    indicators that identify records stored in the affected realm are made 
    null. 
5.  All records in the realms subject to privacy lock controls are left in 
    their locked or unlocked state established by the previous READY.  A 
    subsequent READY statement does not invoke the privacy procedures again. 
6.  All affected realms must be in ready mode at the beginning of execution of 
    a FINISH statement. 
7.  A FINISH with no realm-list will release all the context used by the Data 
    Base Control System in the ASL. 
8.  (BASIC only) The execution of every DB READY, DB FINISH, and DB CHECK 
    establishes a check point for roll back. Under an error condition of a 
    deadlock in the data base, BASIC will resume execution after the most 
    recent executed READY, FINISH or CHECK statement. 
9.  When deadlock is detected, the Data Base Control System will roll all 
    updates out of the data base and transfer control to the first statement 
    after the last checkpoint.  The last checkpoint is the last CALL to CHECK 
    or the last READY or FINISH.  The DB-STATUS cell will be set to 1901100 to 
    indicate that a roll back has occurred. 
10. The compiler for the programming language does not know that control may 
    reach the statement following the FINISH call by a path other than the 
    normal return.  This may result in unexpected operation of the program if 
    the code optimizer makes assumptions about program flow, and its effect on 
    local variables.  In the following example, the GOTO statement is an 
    important part of the program because it informs the compiler of the true 
    program flow (though it is never executed). 
         FLAG=0 
         CALL FINISH 
     10  IF FLAG=1 ... 
         . 
         . 
         . 
         FLAG=1 
         CALL ROLL 
         GOTO 10 
00001
COBOL_COMPILE
    The subschema is explicitly invoked through the following CALL statement: 
    CALL INVOKE (Ixxxx,Uxxxx,Rxxxx)                                  (FORTRAN) 
Syntax Rules: 
1.  Ixxxx specifies the information area defined in the INCLUDE file. 
2.  Uxxxx identifies the user work area.  In a FORTRAN program, the User 
    Working Area is defined by the INCLUDE file. 
3.  Rxxxx specifies the reference vector area defined in the INCLUDE file. 
4.  xxxx are the first four characters of the subschema name. 
General Rules: 
1.  Execution of this call causes the Data Base Control System to load the 
    schema subset, to check consistency and to check validity.  This CALL 
    statement must be the first data-base related CALL statement in the 
    program.  This invocation defines important data structures the Data Base 
    Control System will reference in all subsequent data base CALLs. 
2.  The user should not modify the IA or the RVA control structures in any way 
    during program execution. 
3.  The INCLUDE file must not have been modified in any way before 
    compilation. 
4.  RECORD and SET names are not variables and may only be used in DML calls 
    and not in I/O statements, calls to procedures, etc. 
Using INCLUDE File Identifiers 
Care must be taken when dealing with identifiers defined in the INCLUDE file. 
Only elementary data item names (fields) can be used in statements that assign 
values to variables, or use the values of variables.  Thus they are the only 
names that are legal in READ, WRITE, assignment, COMPUTED GOTOs, non-DML calls 
etc. 
The other identifiers (records, sets and areas) defined in the INCLUDE file 
are only to be used in IDS DML calls (those beginning CALL IDSxxxx).  Thus 
RECORD, SET and AREA names can only be used in these calls and nowhere else. 
00002
00003
00001
FORTRAN_INVOCATION
COBOL_COMPILE
    GET makes a part or all of the fields in a data base record available to 
    the program through the User Working Area defined in the subschema.  The 
    object of the statement is the current record of the run unit. 
Format: 
dbstatus<-[]DBGET '[identifier-list]'                           (APL) 
GET [identifier-list]                                         (COBOL) 
CALL GET [(identifier-list)]                                (FORTRAN) 
DB GET [identifier-list]                                      (BASIC) 
Syntax Rules: 
1.  If the first identifier in the list is not a record name, the 
    identifier-list items must be defined in the Record Description entry of 
    the subschema for the current record of the run unit and must correspond 
    to a data-base-identifier in the schema. 
2.  If the first identifier in the list is the record-name of the current 
    record, then no other identifiers are allowed.  All fields in the record 
    are moved to the User Working Area. 
3.  The items in identifier list may be separated by blanks or commas except 
    that in FORTRAN they must be separated by commas. 
General Rules: 
1.  Execution of a GET statement causes the Data Base Control System to place 
    all or part of the current record of the run unit in its associated record 
    area in the User Working Area. 
2.  If identifier-list is not specified, the entire contents of the current 
    record are moved to the User Working Area.  All other fields for the 
    record will be changed. 
3.  Only those data items listed will be moved to the record area for the 
    current record in the User Working Area.  All other fields for the record 
    will be unchanged. 
4.  All transformation specified by the validation of the subschema against 
    the schema description of the data base is performed for all data items 
    moved. 
5.  All records that contain data items required by the execution of a GET 
    statement must be stored in realms that are in ready mode. 
Notes: 
Execution of a GET statement will proceed until a decode operation has been 
attempted for all the fields specified.  An exception code will then be 
returned if invalid data was encountered in any of the fields.  This will 
occur when significant digits are truncated, for example. 
00002
00003
00001
The schema represents data items at the elementary level only; that is, group 
structures are not permitted.  However, the subschema and the application 
program language allow a variety of group data descriptions.  Any group data 
names which are not defined in the schema cannot be referred to by data 
manipulation statements.  The system default rules provide three ways to 
combine elementary data items from the schema into group items in the 
subschema: 
1.  A schema item can be divided into elementary items in the subschema view. 
    For example, in the schema a field is described as: 
        02 ITEM_1  TYPE IS CHARACTER 20. 
    In the subschema a group item is constructed from it as follows: 
        02 ITEM_1. 
          03 FIRST-TEN           PIC X(10). 
          03 SECOND-TEN. 
             04 FIRST-FIVE       PIC X(5). 
             04 SECOND-FIVE      PIC X(5). 
    The data characteristic of the elementary items must be consistent with 
    the characteristics of the schema item; that is, DISPLAY or packed decimal 
    (with no sign) string items must map to corresponding string items. 
2.  A number of schema data items in the same record can be grouped together 
    in the subschema to create a new group item.  For example, in the schema 
    the fields are: 
        02 SALESMAN_CODE    TYPE CHAR 10. 
        02 BRANCH_CODE      TYPE CHAR 2. 
    In the subschema, a new group item is created that combines both fields: 
        02 COMPOSITE-CODE 
          03 SALESMAN-CODE   PIC 9(10). 
          03 BRANCH-CODE     PIC 99. 
    The data-name COMPOSITE-CODE cannot be referred to by data manipulation 
    statements. 
HELP_OVERVIEW
A 
  Abnormal Errors - 
      HELP ABNORMAL_ERRORS 
  ACCEPT - 
      HELP ACCEPT 
  Accessing Data in the Database - 
      HELP APL_DATA_ACCESS 
  ASL Data Segments and Buffer Management - 
      HELP ASL_DATA_SEGS 
B 
  Binding and Consistency - 
      HELP BINDING_AND_CONSISTENCY 
  BUFFERS Subroutine - 
      HELP BUFFERS 
C 
  CALC Subroutine - 
      HELP CALC 
  CALL INVOKE Statement - 
      HELP FORTRAN_INVOCATION 
  CHECK Subroutine - 
      HELP CHECK 
  Compiling and Linking COBOL and FORTRAN Programs - 
      HELP COBOL_COMPILE 
  Concurrent Access Control - 
      HELP CONCURRENT_ACCESS_CONTROL 
  CONNECT - 
      HELP CONNECT 
  CRPT Subroutine - 
      HELP CRPT 
D 
  Data Base Key Comparison (COBOL only) - 
      HELP KEY_COMPARISON 
  DBMEMBERINFO$ - 
      HELP DB_MEMBER 
  DBOWNERINFO$ - 
      HELP DB_OWNER 
  DISCONNECT - 
      HELP DISCONNECT 
E 
  ERASE - 
      HELP ERASE 
F 
  File Access - 
      HELP FILE_ACCESS 
  File Assignments - 
      HELP FILE_ASSIGNMENTS 
  FIND - 
      HELP FIND 
  FINISH - 
      HELP FINISH 
G 
  GET - 
      HELP GET 
  Group Data Items - 
      HELP GROUP_DATA_ITEMS 
I 
  IDSKEEP Subroutine (For CURRENCIES ONLY) - 
      HELP IDSKEEP 
  IDSNOSHARE Subroutine - 
      HELP IDSNOSHARE 
  IDSREDUCEQ Subroutine (For IDSSHARE users) - 
      HELP IDSREDUCEQ 
  IDSSET Subroutine - 
      HELP IDSSET 
  IDSSHARE Subroutine (Protected) - 
      HELP IDSSHARE 
  IDSSHAREANY Subroutine (Unprotected) - 
      HELP IDSSHAREANY 
  IDSSHARECUR Subroutine - 
      HELP IDSSHARECUR 
  IDSSHAREIN Subroutine - 
      HELP IDSSHAREIN 
  IDSSHAREINCUR Subroutine - 
      HELP IDSSHAREINCUR 
  IDSSYSERROR Subroutine - 
      HELP IDSSYSERROR 
  Inquiry Functions (BASIC only) - 
      HELP INQUIRY_FUNCTIONS 
  Invoking the Subschema - 
      HELP INVOKING_THE_SUBSCHEMA 
L 
  Looking at Data Base Special Registers - 
      HELP APL_DBINFORM 
M 
  Member Condition (EMPTY) - 
      HELP MEMBER 
  MODIFY - 
      HELP MODIFY 
  Moving Data from the Data Base - 
      HELP APL_DBFROM 
      HELP BASIC_DBFROM 
  Moving Data to the Data Base - 
      HELP APL_DBTO 
      HELP BASIC_DBTO 
R 
  READY - 
      HELP READY 
  Recovery - 
      HELP RECOVERY 
  ROLL Subroutine - 
      HELP ROLL 
  RPTSTATS Subroutine - 
      HELP RPTSTATS 
S 
  SET - 
      HELP SET 
  STATSOFF Subroutine - 
      HELP STATSOFF 
  STATSON Subroutine - 
      HELP STATSON 
  STORE - 
      HELP STORE 
  Subschema Invocation - 
      HELP APL_INVOCATION 
      HELP BASIC_INVOCATION 
  Subschema Name Information - 
      HELP APL_SUBSCHEMA_NAME 
      HELP BASIC_SUBSCHEMA_NAME 
  Subschema Name Type Information - 
      HELP APL_SUBSCHEMA_TYPE 
      HELP BASIC_SUBSCHEMA_TYPE 
T 
  Tenancy Condition (OWNER/MEMBER/TENANT) - 
      HELP TENANCY 
  TRACEOFF Subroutine - 
      HELP TRACEOFF 
  TRACEON Subroutine - 
      HELP TRACEON 
U 
  UOPT0 SET option - 
      HELP IDSSHAREANY NOTES: 
  UOPT1 SET option - 
      HELP IDSSHARECUR NOTES: 
      HELP IDSSHAREINCUR NOTES: 
  USAGE IS (COBOL only) - 
      HELP USAGE_IS 
  USE (for Privacy) - 
      HELP USE_FOR_PRIVACY 
  USE FOR EXCEPTION Condition - 
      HELP USE_FOR_EXCEPTION 
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
    For general information, enter: 
    HELP (IDS) NOTATION_CONVENTIONS 
    HELP (IDS) PROCESSOR 
    HELP (IDS) DATABASE_REGISTERS 
    HELP For APL only information, enter: 
    HELP (IDS) APL_STATEMENTS 
    HELP (IDS) APL_INVOCATION 
    HELP (IDS) APL_SUBSCHEMA_NAME 
    For COBOL only information, enter: 
    HELP (IDS) COBOL_SUBSCHEMA 
    HELP (IDS) KEY_COMPARISON 
    HELP (IDS) USAGE_IS 
    HELP (IDS) IDSSYSERROR 
    For FORTRAN only information, enter: 
    HELP (IDS) FORTRAN_INVOCATION 
    For BASIC only information, enter: 
    HELP (IDS) BASIC_STATEMENTS 
    HELP (IDS) BASIC_INVOCATION 
    HELP (IDS) BASIC_SUBSCHEMA_NAME 
    HELP (IDS) DB_OWNER 
    HELP (IDS) DB_MEMBER 
    For tenancy information, enter: 
    HELP (IDS) TENANCY 
    HELP (IDS) MEMBER 
    For DML statement information, enter: 
    HELP (IDS) DML_STATEMENTS 
    For subroutine information, enter: 
    HELP (IDS) SUBROUTINES 
    For a complete list of topics, enter: 
    HELP (IDS) TOPICS 
HELP_INDEX
BUFFERS
CALC
CHECK
The IDSKEEP subroutine flags the current record of run so that it will be 
protected even though it may be a currency until the checkpoint.  This 
subroutine allows the user to increase the level of protection to meet 
individual needs. 
Format: 
dbstatus<-[]DBKEEP                                               (APL) 
CALL "IDSKEEP" USING db-status                                 (COBOL) 
CALL KEEP                                                    (FORTRAN) 
[line no] DB KEEP                                              (BASIC) 
General Rules: 
1.  IDSKEEP applies only to the current record of run. 
2.  Records identified by IDSKEEP will remain enqueued as shared until the 
    next checkpoint. 
3.  The db-status is the error status which is a seven character error code. 
    DB-STATUS may be used here as an alternative to a program variable. 
Note: 
The IDSKEEP subroutine allows users to augment the enqueued page list.  This 
subroutine will keep the current of run on the enqueue list even though it is 
no longer a currency.  This subroutine applies only to the currencies only 
concurrent access control schema when IDSSHARECUR was applied to the READY. 
00001
00002
00003
An IDSNOSHARE updater may gain exclusive use of the data base using this mode. 
An IDSNOSHARE reader will be treated as IDSSHAREIN. 
Format: 
CALL "IDSNOSHARE"                                             (COBOL) 
Notes: 
1.  An IDSNOSHARE updater may be locked out from file access by any other user 
    already having the file in READY. 
2.  An IDSNOSHARE updater locks out all other users from file access. 
3.  IDSNOSHARE retrievers can run concurrently without protection with no 
    updaters allowed.  IDSNOSHARE applies primarily to updaters. 
4.  IDSNOSHARE retrievers lock out all other updaters. 
5.  Concurrent access controls are not required for IDSNOSHARE users. 
6.  This subroutine applies only to the next READY statement. 
7.  The set command that may be used instead of the IDSNOSHARE subroutine CALL 
    is: 
        !SET dcb-name fid,SHARE=NONE 
00001
The IDSREDUCEQ subroutine gives IDSSHARE users the ability to dequeue some 
shared pages without having to do a checkpoint.  All pages which do not 
contain currencies and are not modified are dequeues.  This subroutine does 
not help in walking a sorted set or in scanning an area but it does help to 
keep down the number of enqueues without having to do checkpoints. 
Format: 
dbstatus<-[]DBREDUCEQ                                            (APL) 
CALL "IDSREDUCEQ" USING db-status                              (COBOL) 
CALL REDUCEQ                                                 (FORTRAN) 
[line-no.] DB REDUCEQ                                          (BASIC) 
General Rules: 
1.  IDSREDUCEQ is intended only for use with IDSSHARE for the purpose of 
    reducing the number of shared enqueues. 
2.  The db-status field for COBOL must be a seven character field and may be 
    DB-STATUS.  A non-zero status is returned when there is no current of run 
    to enqueue. 
Note: 
When using IDSSHARE on the READY, every page that is read is first enqueued as 
shared.  Thus, the number of shared enqueues grows with every new page that is 
accessed.  The execution of IDSREDUCEQ will dequeue any shared page that does 
not contain a currency and that is not in the buffer pool. 
This call helps a user keep below the 256 enqueue limit imposed by the system. 
This subroutine has no effect upon those pages enqueued as noshare due to 
updates. 
00001
00002
ROLL
RPTSTATS
This subroutine allows the user to issue SET commands for data base areas from 
within a program.  (The schema and subschema may not be SET using this 
subroutine.) 
Format: 
)SET dcb-name fid                                               (APL) 
CALL "IDSSET" USING string-name,error-word                    (COBOL) 
CALL SET (string-name,error-word)                           (FORTRAN) 
Notes: 
String-name must be the name of a data item that contains a text string 'SET 
dcb-name file-identifier'.  The first four characters must be SET b where b is 
blank.  The dcb-name and file-identifier must be separated by blanks and 
terminated by a blank.  The text string is passed to the CP-6 system via the 
M$YC system service.  Error-word is used to return the error, if any, to the 
user and must be defined as computational.  The error if non-zero will be a 
CP-6 system service error. 
00001
IDSSHARE allows other IDSSHARE readers, other IDSSHAREANY readers and other 
IDSSHARE updaters in a data base concurrently (multiple readers updaters). 
Format: 
CALL "IDSSHARE"                                               (COBOL) 
Notes: 
1.  IDSSHARE readers may share files with each other and with many IDSSHAREIN 
    readers (multiple readers and no updaters); or with a single IDSSHAREIN 
    update user (multiple readers and one updater), or with IDSSHAREANY 
    readers. 
2.  IDSHARE users can be locked out from file access by an IDSNOSHARE user. 
    IDSSHARE update users can be locked out from file access by an IDSSHAREIN 
    or by a single IDSSHAREANY updater. 
3.  Concurrent access controls are applied and a deadlock journal is created 
    for users with one or more areas opened with IDSSHARE. 
4.  This subroutine applies only to the next READY statement. 
5.  The SET command that may be used instead of the IDSSHARE subroutine CALL 
    is: 
        dcb-name fid,SHARE=ALL 
00001
IDSSHAREANY is a mode of sharing which does not receive any concurrent access 
controls. 
Format: 
CALL "IDSSHAREANY"                                            (COBOL) 
Notes: 
1.  IDSSHAREANY readers do not receive access control protection and may share 
    a data base with other retrievers and updaters. 
2.  An IDSSHAREANY updater must be the only updater and will share only with 
    the other IDSSHAREANY retrievers.  IDSSHAREANY is designed to avoid the 
    overhead inherent in ENQ/DEQ.  It does this by allowing only a single 
    updater, and multiple readers.  The updater and readers must have made a 
    specific request for this mode of operation since it has some side affects 
    on the consistency of the data the user sees.  I-D-S/II does not allow 
    multiple updaters in this case because without using ENQ/DEQ there is no 
    way to insure that the combination of updates issued by multiple updaters 
    is valid. 
3.  IDSSHAREANY users may be locked out from file access by an IDSNOSHARE 
    updater.  IDSSHAREANY updaters may be locked out from file access by 
    another IDSSHAREANY updater or by another IDSSHARE reader. 
4.  Concurrent access controls are not used with this access mode.  Programs 
    are not protected from updaters and exception conditions must be 
    anticipated.  There is no risk to the data base - only to the program. 
5.  This subroutine applies only to the next READY statement. 
6.  The SET command that may be used instead of the IDSSHAREANY subroutine 
    CALL is as follows: 
        !SET dcb-name fid,SHARE=ALL,UOPTO=YES (For retrieval.) 
        !SET dcb-name fid,SHARE=IN,UOPTO=YES (For update.) 
00001
       IDSSHARECUR users are treated the same as IDSSHARE users except that 
       only those pages which contain currencies are kept as enqueued as 
       shared.  Updated pages are treated the same as IDSSHARE.  Generally the 
       total number of enqueues is lower, and the level of protection is lower 
       and the probability of deadlock is lower and the cost of the enqueue 
       administration is higher. 
Format: 
Call "IDSSHARECUR"                                                 (COBOL) 
Notes: 
1.  IDSSHARECUR readers may share files with each other and with IDSSHARE 
    readers and with other IDSSHAREIN readers (multiple readers and not 
    updaters); or with a single IDSHAREIN update user (multiple readers and 
    one updater), or with IDSSHAREANY readers. 
2.  IDSSHARECUR users can be locked out from file access by an IDSNOSHARE 
    user.  IDSSHARECUR update users can be locked out from file access by an 
    IDSSHAREIN or by a single INSSHAREANY updater. 
3.  Concurrent access controls are applied and a deadlock journal is created 
    for users with one or more areas opened with IDSSHARECUR. 
4.  This subroutine applies only to the next READY statement. 
5.  The SET command that may be used instead of the IDSSHARECUR subroutine 
    CALL is: 
        !SET dcb-name fid,SHARE=ALL,UOPT1=YES 
6.  The implementation of currency only mode ensures that the total number of 
    pages enqueued at any given time for a currency only area during a DML 
    operation can be no more than the number of buffers allocated plus the 
    number of currency pages and the number of modified pages that are not in 
    memory.  Also, at the end of every DML statement, all non-modified pages 
    enqueued but containing no currencies will be dequeued whether they are in 
    memory or not. 
00001
IDSSHAREIN input users may share files with each other and with IDSSHARE input 
users (multiple readers and no updaters). 
Format: 
CALL "IDSSHAREIN" (Protected update, Unprotected retrieval)   (COBOL) 
General Notes: 
1.  IDSSHAREIN users may be locked out from file access by a single IDSNOSHARE 
    user or by a single IDSSHARE update user. 
2.  Concurrent access controls are required for an IDSSHAREIN update user. 
3.  Concurrent access controls are not required for IDSSHAREIN input users 
    since no concurrent updaters are allowed. 
4.  This subroutine applies only to the next READY statement. 
5.  The SET command that may be used instead of the IDSSHAREIN subroutine CALL 
    is: 
        !SET dcb-name fid,SHARE=IN 
00001
IDSSHAREINCUR input users may share files with each other and with IDSSHAREIN 
readers and with IDSSHARE readers (multiple readers and no updaters). 
IDSSHARECUR offers "currencies only" concurrent access control protection with 
less enqueues than IDSSHARE and with reduced protection.  Data that is re-read 
is subject to change between reads unless the data is in a record that is a 
currency.  IDSKEEP can be used to extend currencies only protection to include 
records that must be protected. 
Format: 
Call "IDSSHAREINCUR"                                              (COBOL) 
Notes: 
1.  IDSSHAREINCUR users may be locked out from file access by a single 
    IDSNOSHARE user or by a single IDSSHARE update user or by a single 
    IDSSHARECUR user. 
2.  Concurrent access controls are required for an IDSSHAREINCUR user. 
3.  This subroutine applies only to the next READY statement. 
4.  The SET command that may be used instead of the IDSSHAREINCUR subroutine 
    CALL is: 
        !SET dcb-name fid,SHARE=IN,UOPT1=YES 
For APL BASIC and FORTRAN, the SHARECUR and SHAREINCUR OPTIONS are available 
on the READY statement as an alternative to SHARE, SHAREIN, and NOSHARE. 
00001
STATSOFF
From time to time an application may receive a DB-STATUS code with a 7 as the 
first digit after the statement code.  These error codes may have underlying 
CP-6 system error codes which are needed for complete information.  This 
subroutine returns the underlying CP-6 system error code to the application 
program for analysis and optionally prints the error messages using the system 
error message file. 
Format: 
CALL "IDSSYSERROR" USING flag,ids-error                             (COBOL) 
Notes: 
1.  flag is a binary COMP-6 variable which is set to 1 to indicate that error 
    message printing is desired.  The flag is set to 0 to indicate no error 
    message printing is desired. 
2.  ids-error is a binary COMP-6 variable which is used to return the CP-6 
    system error which was returned to the COBOL interface on the last 
    I-D-S/II Data Manipulation Language statement. 
3.  When a DB-STATUS code of xx7yyyy is returned, the 7 means there was a 
    system error which may or may not be recoverable.  An analysis of the 
    underlying system error is sometimes more useful than the DB-STATUS error 
    alone.  This subroutine returns the error and optionally prints the error 
    message depending upon the flags. 
    APL makes the system available through a different mechanism.  FORTRAN can 
    directly reference the symbol IDSSYSERR and analyze the error without this 
    subroutine. 
00001
TRACEOFF
TRACEON
    The following four functions are inquiry functions: 
    DBEMPTY(strexp) 
    DBOWNER(srtexp) 
    DBMEMBER(strexp) 
    DBTENANT(strexp) 
strexp must represent a setname.  These functions will return a 0 or 1, 
depending on the status of the current record.  For example, if the current 
record is a member of setname, then DBMEMBER will return a 1. 
In APL, all I-D-S/II interface processing is accomplished as a run time 
activity. The subschema specification must be the first I-D-S/II function to 
be performed.  The subschema is specified through the DBSUB function, which 
reads the subschema, builds name tables, builds data structures for internal 
use, and includes a value for the privacy lock.  The privacy lock is the lock 
for invoking which must match the lock stored in the subschema file (specified 
in the APL subschema DDL). 
In COBOL programs, code that is automatically generated at the entry of each 
COBOL module causes the Data Base Control System in the Alternate Shared 
Library to read the subschema.  Since no user statement is needed for this 
invocation, it may be a normal practice to test DB-STATUS for errors which may 
have been encountered during the invocation.  The DB-STATUS test for 
invocation, binding, consistency, file accessed correctly and memory 
availability is located as the first executable code in a COBOL program. 
In a FORTRAN program, the program must CALL INVOKE, a subroutine which causes 
the Data Base Control System to access the validator subschema file and the 
schema file.  This is a run time activity for FORTRAN. 
    CALL INVOKE (Ixxxx,Uxxxx,Rxxxx) 
where 
Ixxxx    is the Information Area defined in the INCLUDE file. 
Uxxxx    is the User Work Area defined in the INCLUDE file. 
Rxxxx    is the Reference Vector Area defined in the INCLUDE file. 
IDSKEEP
Relation tests can be made between two data base key items to determine 
whether the two items contain equal values.  The result of the comparison of a 
data base key item with any data item that is not a data base key item is 
undefined.  The result of a comparison of two data base key items that is not 
a comparison to determine equality or inequality is undefined. 
A relation test between a data base key item and a literal may be made only if 
the literal is the figurative constant NULL and if the comparison is to 
determine equality or inequality. 
Format: 
identifier-1 IS [NOT] EQUAL TO  {identifier-2}                (COBOL) 
                                {NULL        } 
General Rules: 
1.  Identifier-1 and identifier-2 must both be described with usage DB-KEY. 
2.  NULL is a figurative constant representing an empty or null value of a 
    data base key data item. 
Examples: 
The following COBOL example illustrates data base key comparison. 
    First, a value of a data base key is saved as follows: 
        ACCEPT SAVE-DBK FROM CURRENCY. 
    Later, a record is located based on realm currency. 
        FIND NEXT WITHIN REALM-1. 
    Then, the data base key of the found record is compared with the saved 
    value of the previous data base key as follows: 
        ACCEPT TEMP-DBK FROM CURRENCY. 
        IF TEMP-DBK IS EQUAL TO SAVE-DBK GO TO FOUND-IT ELSE ... 
    NOTE:  SAVE-DBK and TEMP-DBK must both be declared as data base key items. 
00002
00001
The member condition determines whether or not a specified set has any 
members. 
Format: 
R<-[]DBIF 'set-name EMPTY'                                      (APL) 
IF set-name IS [NOT] EMPTY statement                          (COBOL) 
CALL IFEMPTY (set-name,logical-result)                      (FORTRAN) 
IF (logical-result-expression) statement                    (FORTRAN) 
See Set Conditions (BASIC only) 
General Rules: 
1.  The object set is identified by the current record of the set type 
    referenced by set-name.  If the object set has no member, the result of 
    the test is true.  If the object set has members, the result of the test 
    is false. 
2.  NOT can be specified in COBOL.  If it is, the result of the test is 
    reversed.  The condition is true if the set occurrence has member records 
    connected to it. 
Example (COBOL) 
    IF MYSET IS NOT EMPTY FIND FIRST WITHIN MYSET. 
retrieves the first member record from the current set but only if the set 
type has members. 
00003
00002
00001
MODIFY alters the contents of one or more data items in a record and/or 
changes the set membership of the record.  The object of the statement is the 
current record of the run unit. 
Format 1: 
                                                                      (APL) 
dbstatus<-[]DBMODIFY '[record-name][{ONLY     } {ALL         } MEMBERSHIP]' 
                                   [{INCLUDING} {setname-list}           ] 
                                                                    (COBOL) 
[MODIFY] [record-name] [{INCLUDING} {ALL         } MEMBERSHIP] 
                       [{ONLY     } {setname-list}           ] 
CALL MODIFY ([record-name,][{INCLUDING},{ALL         }]           (FORTRAN) 
                           [{ONLY     } {setname-list}] 
                                                                    (BASIC) 
DB MODIFY [record-name] [{INCLUDING} {ALL         } [MEMBERSHIP] 
                        [{ONLY     } {setname-list}            ] 
Format 2: 
                                                                      (APL) 
dbstatus[]DBMODIFY 'identifier-list [INCLUDING {ALL         } MEMBERSHIP]' 
                                    [          {setname-list}           ] 
                                                                    (COBOL) 
MODIFY identifier-list [          { ALL        } [MEMBERSHIP]] 
                       [INCLUDING {setname-list}             ] 
CALL MODIFY (identifier-list[,INCLUDING{,ALL          }]          (FORTRAN) 
                            [          {setname-list  }] 
                                                                    (BASIC) 
DB MODIFY identifier-list [INCLUDING {ALL         } [MEMBERSHIP] 
                          [          {setname-list} [          ] 
Syntax Rules: 
1.  Record-name, if specified, must be the name of the current record of the 
    run unit. 
2.  The items in identifier-list must reference data items contained within 
    the current record of the run unit. 
3.  The current record of the run unit must be defined in the schema Data 
    Description Language as a member of the set types referenced by the items 
    in setname-list. 
4.  The items in item-list may be separated by commas or blanks, except that 
    in FORTRAN they must be separated by commas. 
General Rules: 
1.  Execution of a MODIFY statement causes the Data Base Control System to 
    replace, in the current record of the run unit, the contents of specified 
    data items.  The contents of these data items on the data base are 
    replaced with the contents of the corresponding items in the User Working 
    Area.  The data items to be updated are specified as follows: 
    a.  Format 1 with an ONLY phrase specifies that no data items are to be 
        updated. 
    b.  Format 1 without an ONLY phrase specifies that all data items in the 
        current record of the run unit are to be updated. 
    c.  Format 2 specifies that the items in identifier-list are to be 
        updated. 
2.  Execution of a MODIFY statement causes the Data Base Control System to 
    change the set membership of the current record of the run unit for 
    specified set types.  The set types for which membership is changed is 
    specified as follows: 
    a.  If no INCLUDING or ONLY phrase is present, no set membership is 
        changed. 
    b.  If ALL is specified in an INCLUDING or ONLY phrase, the record's 
        membership is changed in every set in which it is a member. 
    c.  If setname-list is specified in an INCLUDING or ONLY phrase, the 
        record's membership is changed in the specified set. 
    For each set type specified as above, the set membership is changed as 
    follows: 
    a.  The current record of the run unit is removed from membership in the 
        set occurrence to which it belongs. 
    b.  A new set occurrence is selected according to the set selection 
        criteria specified in the schema Data Description Language. 
    c.  The current record of the run unit is inserted in the set occurrence 
        selected above.  This is done according to the set ordering criteria 
        specified in the schema Data Description Language. 
3.  The realm in which the current record of the run unit is stored will not 
    be changed by the execution of a MODIFY statement.  Realm selection is not 
    invoked for the current record of the run unit. 
4.  The current record of the run unit becomes the current record of its 
    realm, the current record of its record type, and the current record of 
    all sets in which it is a tenant.  The special registers DB-REALM-NAME, 
    DB-SET-NAME, DB-RECORD-NAME, DB-KEY-NAME, DB-DATA-NAME, are not changed by 
    the successful execution of a MODIFY statement. 
5.  The realm in which the current record of the run unit is stored must be in 
    update usage mode.  Records of sets in which membership is affected by the 
    execution of the MODIFY statement must be stored in realms that are in 
    update usage mode. 
6.  Records of sets referenced by the set selection criteria of the specified 
    sets must be stored in realms that are in ready mode. 
7.  If a data item to be replaced as specified in General Rule 1 is a control 
    field for a set in which the current record of the run unit is a member, 
    the set-name (or ALL) must be specified in an INCLUDING phrase.  A control 
    field is a sort key or a duplicate control field. 
8.  If the current record of the run unit is defined as an OPTIONAL MANUAL 
    member of one of the set types referenced in setname-list, it must be 
    currently a member of the set. 
9.  The value of an INDEXED location record key cannot be changed by the 
    execution of a MODIFY statement.  It is possible to use Format 1 of the 
    MODIFY verb with a record that has a location mode of INDEXED.  However, 
    the value of the location key must not change.  If the value changes, the 
    exception condition INVALID DATA BASE KEY CHANGE REQUIRED (80210) is 
    returned. 
10. The current record of the run unit becomes the current record of all 
    record key types whose values in the record are changed as a result of the 
    execution of the MODIFY statement. 
Notes: 
1.  When ALL is specified, the meaning is all fields of a record or all sets 
    that are defined in the subschema. 
2.  OPTIONAL MANUAL set membership can be changed with a MODIFY statement.  If 
    the current record of the run unit is currently a member of the set, it is 
    treated exactly as a MANDATORY AUTOMATIC set and is subject to General 
    Rule 7.  If the current record of the run unit is not currently a member 
    of the set, the control can be changed as if they are not control fields. 
    A MODIFY statement cannot be used to obtain the effect of a CONNECT 
    statement.  If the record is a member of a set before the MODIFY 
    statement, it will be a member afterwards.  If the record is not a member 
    of a set before the MODIFY statement, it will not be a member afterwards. 
3.  No set membership will be changed by a MODIFY statement unless there is an 
    INCLUDING or ONLY phrase.  This means that in order to change a data item 
    specified as a sort key, the set type that it is a sort key for must be 
    specified in an INCLUDING phrase.  This in turn implies that the set 
    selection criteria, as specified in the schema Data Description Language, 
    must be established before execution of the MODIFY statement. 
4.  If one of several control fields is to be changed, the one specified will 
    be obtained from the User Working Area.  Other fields required to execute 
    the function will be obtained from the current record of the run unit on 
    the data base.  This means any combination of data items in a record can 
    be changed. 
5.  If modification of a varying-length field causes the length of a field to 
    change, the records on the page will expand or contract.  If the records 
    expand and there is insufficient space available on the page, the 
    exception condition INVALID DATA BASE KEY CHANGE REQUIRED is returned. 
Examples: 
                 | 
                 | 
                 |                    RECORD A 
           ---   |                      LOCATION MODE CALC A_1 
          | A |<-                    RECORD B 
           ---                          LOCATION MODE CALC B_1 
            |                         SET A_B 
            |                           SORTED ON B_2 
            | A_B   |                     SET SELECTION IS THRU A_B 
            v       |                       OWNER IDENTIFIED BY 
           ---      |                           CALC_KEY 
          | B |<---- 
           --- 
    1.  Modify sort key in record B. 
               MOVE key-1 TO A-1. 
               FIND ANY A. 
               MOVE key-2 TO B-1. 
               FIND ANY B. 
               MOVE new-sort-key TO B-2. 
               MODIFY B-2 INCLUDING A-B. 
    2.  Modify non-control field in record A. 
               MOVE key-1 TO A-1. 
               FIND ANY A. 
               MOVE new-data TO A-3. 
               MODIFY A-3. 
    3.  Put a B record under a new A record without changing any field in the 
        B record. 
               MOVE key-1 TO B-1. 
               FIND ANY B. 
               MOVE new-owner-key TO A-1. 
               MODIFY B ONLY A-B. 
    4.  Put a B record under a new A record and change the sort key in the B 
        record. 
               MOVE key-1 TO B-1. 
               FIND ANY B. 
               MOVE new-owner-key TO A-1. 
               MOVE new-sort-key TO B-2. 
               MODIFY B-2 INCLUDING A-B. 
                      | 
                      |                     RECORD C 
               ---    |                       LOCATION MODE CALC C_1 
              | C |<--                      RECORD D 
               ---                            LOCATION MODE CALC D_1 
                |   C_D                     SET C_D 
                |    |                         SET SELECTION IS THRU C_D 
                v    |                            OWNER IDENTIFIED BY 
               ---   |                            APPLICATION 
              | D |<- 
               --- 
    5.  Put a D record under a new C record. 
               MOVE new-owner-key TO C-1. 
               FIND ANY C. 
               MOVE key-1 TO D-1. 
               FIND ANY D RETAINING CURRENCY C-D. 
               MODIFY D ONLY C-D. 
00004
00002
00003
00001
IDSNOSHARE
    Notation Conventions are: 
    WORDS, BRACKETS, BRACES, BARS, PUNCTUATION 
    SPECIAL_CHARACTERS, FORMATS and SYNTAX_RULES 
    For specific information, enter: 
    HELP (IDS) NOTATION convention_name 
    or enter ?? for complete list 
  Notation     Description 
  Words 
               All underlined uppercase words are called keywords and are 
               required when the functions of which they are a part are used. 
               Uppercase words which are not underlined are optional and may 
               be included in the source program at the discretion of the 
               user.  Uppercase words, whether underlined or not, must be 
               spelled correctly. 
               In formats, lowercase words are generic terms used to represent 
               words, literals, character strings, or a complete syntactical 
               entry supplied by the user.  If such generic terms are repeated 
               within a format, a number or letter appendage to the term 
               serves to identify that occurrence of the term for subsequent 
               explanation or discussion. 
  Brackets, Braces, and Bars 
               When a portion of a format is enclosed in brackets [], that 
               portion may be included or omitted at the user's choice. 
               Braces {}, enclosing a portion of a format indicate that one of 
               the options contained within the braces must be selected.  In 
               both cases, the possible choices are stacked vertically in the 
               format.  Stacked choices are delimited by vertical bars (e.g., 
               {||} to indicate that more than one choice can be selected. 
               When brackets or braces enclose a portion of a format but only 
               one possibility is shown, the function of the brackets or 
               braces is to delimit the portion of the format to which a 
               following ellipsis applies (see next paragraph).  If an option 
               within braces contains only reserved words that are not 
               keywords, then the option is a default option (implicitly 
               selected unless one of the reserved words is explicitly 
               indicated). 
  Punctuation 
               The punctuation characters comma and semicolon are shown in 
               some formats.  In COBOL source programs, these two punctuation 
               characters are optional.  They may be included or omitted and 
               are interchangeable.  (Either one may be used when one of them 
               is shown in the format.)  Neither character may appear 
               immediately preceding the first clause of an entry or 
               paragraph.  If desired, a comma or semicolon may be used 
               between statements in the Procedure Division of a COBOL 
               program.  In FORTRAN, commas are required where shown. 
               Paragraphs within the Identification Division and Procedures 
               Division, and the entries within the Environment and Data 
               Division, must be terminated by the separator period. 
  Special Characters 
               When the characters '+', '_', '<' '>', '=', "(", ")", "<-", and 
               "[]" appear in formats, they are required when such formats are 
               used, even though they are not underlined.  The special APL 
               characters <- (left arrow), and [] (quad) may be entered from a 
               non-APL terminal as $IS and $Q, respectively. 
  Formats 
               A format is the specific arrangement of the elements of a 
               clause or a statement.  A clause or a statement consists of 
               elements which are the uppercase words, lowercase words, 
               level-numbers, brackets, braces, connectives, and special 
               characters depicted in the appropriate sections of this manual. 
               In this manual, a format is shown adjacent to information which 
               defines the clause or statement.  If more than one specific 
               arrangement is permitted, a general format is presented where 
               appropriate by specific numbered formats.  Clauses must be 
               written in the sequence given in the format.  (If used, clauses 
               that are optional must appear in the sequence shown).  In 
               certain cases, stated explicitly in the rules associated with a 
               given format, clauses may appear in sequence other than those 
               shown.  Applications, requirements, or restrictions are shown 
               as rules. 
  Syntax Rules 
               A syntax rule defines or clarifies the order in which words or 
               elements are arranged to form larger elements such as phrases, 
               clauses, or statements.  Syntax rules also impose restrictions 
               on individual words or elements. 
               Syntax rules are used to define or clarify the exact manner in 
               which the statements must be written; that is, the order of the 
               elements of the statement and the restrictions on what each 
               element may represent. 
00002
00002
00002
00005
00003
00004
00006
00001
HELP_OVERVIEW
TENANCY
USE_FOR_PRIVACY
I-D-S/II is a network data base management system which allows concurrent 
access of a data base by many independent users. 
The data management system has three components: 
o   The Data Base Administrator Control System (DBACS).  DBACS is an 
    administrative processor used to define the logical and physical structure 
    of the data base. 
o   The DBUTIL utility processor.  This processor's functions include loading, 
    dumping, and printing the data base; rebuilding keys; and checking and 
    repairing set pointers. 
o   The Data Base Control System (DBCS).  The Data Base Control System is the 
    data base manager.  All data base retrievals and stores and modifications 
    are executed via application programs which use the services of the Data 
    Base Control System.  Application program interfaces are provided for APL, 
    COBOL and FORTRAN. 
    See also: 
    HELP (IDS) OVERVIEW 
    READY prepares one or more realms for processing.  Several types of 
    sharing are possible through the use of the IDSSHARE, IDSSHAREIN, 
    IDSNOSHARE, and IDSSHAREANY supplementary subroutines described in Section 
    5. 
Format: 
                                                                    (APL) 
                                               {UPDATE   } [{SHAREALL}] 
dbstatus<-[]DBREADY '[realmname-list][USAGE IS]{RETRIEVAL} [{SHAREIN }]' 
                                               {LOAD     } [{SHAREANY}] 
                                                           [{NOSHARE }] 
                       [                { UPDATE    } ] 
READY [realmname-list] [; USAGE-MODE IS { RETRIEVAL } ]           (COBOL) 
                       [                { LOAD      } ] 
                             {UPDATE   } [{SHARE    }] 
CALL READY ([realmname-list],{RETRIEVAL} [{SHAREIN  }])         (FORTRAN) 
                             {LOAD     } [{SHAREANY }] 
                                         [{NOSHARE  }] 
                                  [SHARECUR  ] 
                                  [SHAREINCUR] 
                      {UPDATE   } [SHARE     ] 
DB READY [realm-list] {RETRIEVAL} [SHAREIN   ]                    (BASIC) 
                      {LOAD     } [NOSHARE   ] 
                                  [SHAREANY  ] 
                                  [SHARECUR  ] 
                                  [SHAREINCUR] 
Syntax Rules: 
1.  If any item in realmname-list is defined as a temporary realm, the 
    USAGE-MODE cannot be specified as RETRIEVAL. 
2.  The items in realmname-list are separated by commas or blanks except that 
    in FORTRAN they must be separated by commas. 
General Rules: 
1.  Execution of any READY statement affects entire realms, regardless of the 
    specific format of the statement. 
2.  At the beginning of the execution of a READY statement, no realm affected 
    by that READY statement may be in ready mode. 
3.  If realmname-list is specified, each realm referenced is prepared for 
    access and placed in ready mode. 
4.  If realmname-list is not specified, all realms in that portion of the data 
    base described by the subschema are prepared for access and placed in 
    ready mode. 
5.  The UPDATE phrase permits both access to, and modification of, the 
    contents of the affected realm. 
6.  The RETRIEVAL phrase permits access to the contents of the affected 
    realms. 
7.  If defaults have not been used, file identifiers must have been assigned 
    for the data base files being readied by using an (IBEX) SET command or by 
    using a CALL "IDSSET" using text-string from within the program. 
8.  Any temporary realms made ready are initialized each time the READY 
    statement is issued for the realm.  At the termination of a run unit, the 
    contents of all temporary realms are unavailable. 
9.  Execution of the first READY statement of a run unit causes all privacy 
    procedures to be executed.  Subsequent READY statements do not invoke the 
    privacy procedures.  The resources remain locked or unlocked from the 
    first READY statement executed. 
10. If the USAGE-MODE phrase is omitted, execution of the READY statement 
    occurs as though USAGE-MODE IS RETRIEVAL has been specified. 
11. If USAGE-MODE is LOAD, no alternate keys will be stored for records in an 
    INTEGRATED realm.  The alternate keys for an INTEGRATED area must be built 
    through a key file using DBUTIL and the REBUILD KEY directive.  This is 
    primarily a matter of efficiency.  It is better to extract the keys from 
    the data base; do a co-resident SORT, and build the key file in order 
    rather than randomly construct a key file using the file system.  If 
    duplicates are not allowed, the records are stored and error diagnostics 
    are issued upon the FINISH (of an INDEXED area) or by DBUTIL (for an 
    INTEGRATED area). 
12. If USAGE-MODE is LOAD for an INDEXED realm, the index structure is built 
    at the FINISH. 
13. (BASIC only) The execution of every DB READY, DB FINISH, and DB CHECK 
    establishes a check point for roll back. Under an error condition of a 
    deadlock in the data base, BASIC will resume execution after the most 
    recent executed READY, FINISH or CHECK statement. 
14. When deadlock is detected, the Data Base Control System will roll all 
    updates out of the data base and transfer control to the first statement 
    after the last checkpoint.  The last checkpoint is the last CALL to CHECK 
    or the last READY or FINISH.  The DB-STATUS cell will be set to 1901100 to 
    indicate that a roll back has occurred. 
15. The compiler for the programming language does not know that control may 
    reach the statement following the READY call by a path other than the 
    normal return.  This may result in unexpected operation of the program if 
    the code optimizer makes assumptions about program flow, and its effect on 
    local variables.  In the following example, the GOTO statement is an 
    important part of the program because it informs the compiler of the true 
    program flow (though it is never executed). 
         FLAG=0 
         CALL READY 
     10  IF FLAG=1 ... 
         . 
         . 
         . 
         FLAG=1 
         CALL ROLL 
         GOTO 10 
00002
00001
System failures and recovery are important considerations in many data base 
applications.  The degree of protection is specified by the data base 
administrator in the definition of the schema for the data base.  Protection 
involves the use of a journal of after-image skeletons, which minimizes the 
size of the journal file.  DBUTIL is used to roll the after-image skeletons 
starting with a data base load of a previous data base dump.  All users who 
update the data base must use the same common journal. 
If recovery is possible, shared data bases are protected in the CP-6 system, 
which saves the transient journal for each user. At restart, each shared data 
base user with an *I file is rolled back to the last clean point in the 
program.  If recovery is complete, the data base is at a clean point, and no 
broken chains or incomplete shared logical operations remain.  There is one 
restriction to automatic roll back at recovery.  That restriction is that the 
Data Base Control System ASL must be specified in the TIGR deck in order to be 
SYSMAKed prior to recovery (see the CP-6 System Support Manual (HA21)). 
An individual program should position IDSCHECK subroutine CALLs to ensure that 
clean points are conveniently and appropriately placed.  The individual 
program is, however, dependent upon successful journal roll forward or upon 
successful recovery and roll back.  Frequent dumps of the data base establish 
global clean points which can be used as fall back points if roll forward and 
recovery are not possible. 
The validity of data base, set points can be checked quickly by using the 
(DBUTIL) CHECK directive.  The CHECK is also an option on a DUMP directive to 
provide regular assurances that the data base set pointers are correct. 
Inventory pages and alternate keys can be rebuilt for INTEGRATED realm in case 
of doubt. 
IDSREDUCEQ
FIND
    Rolls back the deadlock journal to the last clean point. 
Format: 
dbstatus<-[] DBROLL  ''                                         (APL) 
CALL "IDSROLL" USING db-status                                (COBOL) 
CALL ROLL (db-status)                                       (FORTRAN) 
DB ROLL                                                       (BASIC) 
Notes: 
1.  The last checkpoint is the last CALL to CHECK or the last READY or FINISH. 
2.  A ROLL can be used to test the program for restartability at the 
    checkpoint or to ROLL the data base back for some user defined reason. 
3.  The error number 1901100, meaning "rollback has been performed" is 
    returned after a rollback to the last READY or FINISH or CHECK statement. 
00001
Prints statistics accumulated through the STATSON and STATSOFF subroutines. 
Format: 
[]DBRPTSTATS                                                    (APL) 
CALL "IDSRPTSTATS"                                            (COBOL) 
CALL RPTSTATS                                               (FORTRAN) 
DB RPTSTATS                                                   (BASIC) 
Notes: 
1.  All of the statistics gathered since the statistics mechanism was turned 
    on are printed when this subroutine is called. 
2.  The statistics tables are cleared after the report is printed to prepare 
    for another measurement period. 
3.  The statistics are output via the STATS DCB, the same DCB used for global 
    statistics.  The default STATS setting is to the NO device. 
00001
    SET moves the contents of one data base key item to one or more data base 
    key items.  COBOL requires a special operator for this purpose. 
Format: 
SET identifier-list TO {identifier-n}                             (COBOL) 
                       {NULL        } 
Syntax Rules: 
1.  All identifiers must reference data base key items. 
2.  NULL represents an empty or null value of a data base key data item. 
General Rules: 
The contents of the data base key item referenced by identifier-n are moved to 
the data base key items referenced by identifier-1, identifier-2,... .  No 
conversion takes place.  SET is a COBOL operator only which is used to move 
data base keys. 
00002
00001
IDSSHARE
IDSSHAREANY
IDSSHARECUR
IDSSHAREIN
IDSSHAREINCUR
Turns off the I-D-S/II statistics gathering mechanism. 
Format: 
[]DBSTATSOFF                                                    (APL) 
CALL "IDSSTATSOFF"                                            (COBOL) 
CALL IDSSTATSOFF                                            (FORTRAN) 
DB STATSOFF                                                   (BASIC) 
Notes: 
1.  The statistics gathering thus far are kept in a table.  Subsequent 
    IDSSTATSON calls will allow statistics to be accumulated in table. 
2.  A report of the accumulated statistics is available through the 
    IDSREPSTATS subroutine. 
00001
Turns on the I-D-S/II statistics gathering mechanism for all subsequent data 
base operations. 
Format: 
[]DBSTATSON                                                     (APL) 
CALL "IDSSTATSON"                                             (COBOL) 
CALL STATSON                                                (FORTRAN) 
DB STATON                                                     (BASIC) 
Notes: 
1.  The STATS DCB must be SET to obtain statistical reports via IDSRPTSTATS as 
    well as end of job data base statistics. 
2.  The STATS DCB is set to the special device NO by default.  (Refer to of 
    the CP-6 Programmer Reference Manual (CE40). 
00001
STORE causes a record to be stored in the data base.  This statement 
establishes the current record of the run unit. 
Format: 
            {|REALM         |} 
[]DBRETAIN '{|{SETS        }|}'                                      (APL) 
            {|{setname-list}|} 
            {|RECORD        |} 
dbstatus<-[]DBSTORE 'record-name'                                    (APL) 
                 [                         {|REALM         |}    ] 
STORE record-name[; RETAINING CURRENCY FOR {|{SETS        }|} ...] (COBOL) 
                 [                         {|{setname-list}|}    ] 
                 [                         {|RECORD        |}    ] 
             {|REALM         |} 
CALL RETAIN ({|{SETS        }|})                                 (FORTRAN) 
             {|{setname-list}|} 
             {|RECORD        |} 
CALL STORE (record-name)                                         (FORTRAN) 
DB STORE record-name                                               (BASIC) 
General Rules: 
1.  The record referenced by record-name becomes a member of each set type in 
    which it has been declared to be an automatic member.  The sets to which 
    the record is connected are governed by the set selection criteria.  The 
    record is connected to each set in accordance with the set ordering 
    criteria of each set type. 
2.  The record referenced by record-name is established as the owner of an 
    empty set for each set type in which it is defined as an owner. 
3.  The fields of the record referenced by record-name are moved to the record 
    in the data base.  These moves are made in accordance with the encode 
    specifications in the schema and subschema. 
4.  Execution of a STORE statement causes the record referenced by record-name 
    to become the current record of the run unit.  The realm-name and 
    record-name of the record are placed in the special registers 
    DB-REALM-NAME and DB-RECORD-NAME respectively. 
5.  If the RETAINING phrase is not specified, the record referenced by 
    record-name becomes the current record of its realm-name, the current 
    record of its record-name, the current record of all set types in which it 
    has been declared to be a tenant (owner or member), and the current of all 
    record key types that are defined for the record. 
6.  IF the RETAINING phrase with the optional word REALM is specified, no 
    realm currency indicators are changed. 
7.  If the RETAINING phrase with the optional word SETS is specified, no set 
    type currency indicators are changed. 
8.  If the retaining phrase with the optional word RECORD is specified, no 
    record type currency indicators are changed. 
9.  If the RETAINING phrase and setname-list is specified, the currency 
    indicators of the specified are not changed. 
10. The record referenced by record-name remains available to the program in 
    its associated record area. 
11. Entries are made in the key file for all alternate record keys that are 
    defined for the record unless the area is readied with a USAGE MODE of 
    LOAD. 
00001
  Purpose             Name           Language   Description 
Concurrent Access   IDSSHARE       COBOL      Allows concurrent read 
Specification                                 and update. 
                    IDSSHAREANY    COBOL      Provides no concurrent 
                                              control. 
                    IDSSHAREIN     COBOL      Allows concurrent read 
                                              only. 
                    IDSNOSHARE     COBOL      Allows no concurrent 
                                              access. 
Currencies Only     IDSSHARECUR    COBOL      Allows currencies 
Sharing                                       only read and update. 
                    IDSSHAREINCUR  COBOL      Allows currencies only 
                                              read only. 
                    []DBKEEP       APL        Flags the current record of 
                                              run for protection. 
                    IDSKEEP        COBOL 
                    KEEP           FORTRAN 
                    DBKEEP         BASIC 
For IDSSHARE        []DBREDUCEQ    APL        Enables IDSSHARE users 
users                                         to dequeue some shared 
                                              pages without having to 
                                              do a checkpoint. 
                    IDSREDUCEQ     COBOL 
                    REDUCEQ        FORTRAN 
                    DBREDUCEQ      BASIC 
DCB Assignment      )SET           APL        Executes (IBEX) SET 
                    IDSSET         COBOL      commands from within 
                    SET            FORTRAN    a program. 
DBCS Trace          []DBTRACEON    APL        Enables I-D-S/II trace 
                    IDSTRACEON     COBOL      mechanisms. 
                    TRACEON        FORTRAN 
                    DB TRACEON     BASIC 
                    []DBTRACEOFF   APL        Disable I-D-S/II trace 
                    IDSTRACEOFF    COBOL      mechanisms. 
                    TRACEOFF       FORTRAN 
                    DB TRACEOFF    BASIC 
Statistical         []DBSTATSON    APL        Turns the I-D-S/II 
Gathering           IDSSTATSON     COBOL      statistical gathering 
                    STATSON        FORTRAN    mechanism on and off. 
                    DB STATSON     BASIC 
                    []DBSTATSOFF   APL        Turns the I-D-S/II 
                    IDSSTATSOFF    COBOL      statistical gathering 
                    STATSOFF       FORTRAN    mechanism off. 
                    DB STATSOFF    BASIC 
                    []DBRPTSTATS   APL        Produces statistical 
                    IDSRPTSTATS    COBOL      reports. 
                    RPTSTATS       FORTRAN 
                    DB RPTSTATS    BASIC 
Encryption Seed     []DBCRPT       APL        Supplies an encryption 
Specification       IDSCRPT        COBOL      seed. 
                    CRPT           FORTRAN 
                    DB CRPT        BASIC 
CALCing Record      []DBCALC       APL        Optimize loading of CALC 
                    IDSCALC        COBOL      location mode records. 
                    CALC           FORTRAN 
                    DB CALC        BASIC 
Buffer Control      []DBBUFFERS    APL        Specify the maximum 
                    IDSBUFFERS     COBOL      numbers of usable buffers. 
                    BUFFERS        FORTRAN 
                    DB BUFFERS     BASIC 
Data Base Check     []DBCHECK      APL        Defines a clean point 
Checkpointing       IDSCHECK       COBOL      where all updates are 
                    CHECK          FORTRAN    committed, all entries 
                    DB CHECK       BASIC      realeased from the system 
                                              enqueue/dequeue tables 
                                              and the user's deadlock 
                                              journal is released. 
Data Base           []DBROLL       APL        Rolls back the deadlock 
Roll Back           IDSROLL        COBOL      journal to the last clean 
                    ROLL           FORTRAN    point. 
                    DB ROLL        BASIC 
For specific information, enter: 
HELP (IDS) subroutine-name 
Use the functional portion of the subroutine 
name.  For example: 
HELP (IDS) STATSON 
For IDSSET use the full name 
HELP (IDS) IDSSET 
The tenancy condition determines whether or not the current record of the run 
unit is either a member or an owner in a specified set or in any sets.  The 
format for specifying a tenancy condition follows. 
Format: 
                      {MEMBER} 
R<-[]DBIF '[set-name] {OWNER } '                                (APL) 
                      {TENANT} 
                    {MEMBER} 
IF [NOT] [set-name] {OWNER } statement                        (COBOL) 
                    {TENANT} 
     {IFMEMBER} 
CALL {IFOWNER } ([set-name],logical-result)                  (FORTRAN) 
     {IFTENANT} 
IF (logical-result-expression) statement                     (FORTRAN) 
See HELP (IDS) DB_OWNER for BASIC 
General Rules: 
1.  If set-name is specified, only the set type referenced is considered in 
    determining the truth value of the condition.  If set-name is not 
    specified, all set types are considered in determining the truth value of 
    the condition.  The structure is tested to determine if the current record 
    is a member, owner, or either of any set in the subschema. 
2.  If the OWNER phrase is specified, the result of the test is true if the 
    current record of the run unit is the owner of the referenced set type. 
3.  If the MEMBER phrase is specified, the result of the test is true if the 
    current record of the run unit is a member of the referenced set.  If the 
    current record is an OPTIONAL MANUAL member, the record must be tested to 
    see if it has been connected to that set. 
4.  If the TENANT phrase is specified, the result of the test is true if the 
    current record of the run unit is either a member or an owner of the 
    referenced set.  If the current record has an OPTIONAL MANUAL member, the 
    record must be tested to see if it has been connected to that set. 
5.  NOT can be specified in COBOL.  If it is, the result of the test is 
    reversed.  The condition is true if the current record is not an OWNER, 
    MEMBER, or TENANT of the named set. 
6.  APL, FORTRAN, and BASIC return 1 if the assertion is true and 0 if it is 
    false. 
    See also HELP (IDS) MEMBER 
    See also HELP (IDS) DB_MEMBER for BASIC 
Example: 
    IF MYSET MEMBER FIND OWNER WITHIN MYSET.                      (COBOL) 
retrieves the owner record of a set when the current record of the run unit is 
a member of the set. 
00002
00001
TENANCY
This subroutine turns data base trace mechanisms off one at a time or all at 
once. 
Format: 
[]DBTRACEOFF [(integer)]                                        (APL) 
CALL "IDSTRACEOFF" [USING integer]                            (COBOL) 
CALL TRACEOFF [(integer)]                                   (FORTRAN) 
DB TRACEOFF [integer]                                         (BASIC) 
Notes: 
1.  Integer is a binary word that describes which trace mechanism to turn off 
    as follows: 
        Argument                  Description 
        0 or no argument          Trace all of the functions (1 through 4). 
        1                         Trace I-D-S/II entries. 
        2                         Trace I-D-S/II page I/O. 
        3                         Trace I-D-S/II stores/modifies/erase. 
        4                         Trace I-D-S/II record accesses. 
2.  Trace options may be specified one at a time with successive CALLs or all 
    at once in a single CALL. 
00001
This subroutine turns data base trace mechanisms on one at a time or all at 
once. 
Format: 
[]DBTRACEON [(integer)]                                         (APL) 
CALL "IDSTRACEON" [USING integer]                             (COBOL) 
CALL TRACEON [(integer)]                                    (FORTRAN) 
DB TRACEOFF [integer]                                         (BASIC) 
Notes: 
1.  Integer is a binary word that describes which trace mechanism to turn on 
    as follows: 
        Argument              Description 
        0 or no argument      Trace all of the functions (1 through 4). 
        1                     Trace I-D-S/II entries. 
        2                     Trace I-D-S/II page I/O. 
        3                     Trace I-D-S/II stores/modifies/erases. 
        4                     Trace I-D-S/II record accesses. 
2.  Trace options may be specified one at a time with successive CALLs or all 
    at once in a single CALL. 
3.  Trace output is listed via the TRACE DCB and defaults to the LO device. 
4.  The trace option controls the volume of output to focus on the trace 
    mechanism that is of interest.  Trace output is of great value for either 
    on-line or batch testing. 
00001
    This statement is used in the file description entries or in the Working 
    Storage Section of the Data Division to define a data item as a data base 
    key. 
Format: 
[USAGE IS] DB-KEY                                             (COBOL) 
General Rules: 
1.  DB-KEY is an unsigned 36-bit binary integer, aligned on a word boundary. 
2.  A data item described with usage DB-KEY cannot have any of the following 
    clauses associated with it: 
        BLANK WHEN ZERO 
        JUSTIFIED 
        PICTURE 
        SYNCHRONIZED 
        VALUE 
3.  A data item described with usage DB-KEY cannot be a conditional variable. 
00001
    USE FOR EXCEPTION CONDITION specifies procedures to be executed when the 
    execution of a data base statement results in a non-zero data base 
    exception condition. 
    Appropriate values are placed in the special registers DB-STATUS, 
    DB-REAL-NAME, DB-SET-NAME, DB-KEY-NAME, and DB-RECORD-NAME by the Data 
    Base Control System prior to the execution of a data base exception 
    section. 
Format: 
exception-condition-list  []DBUSE function-list                 (APL) 
USE FOR DB-EXCEPTION [ON {OTHER        }]                     (COBOL) 
                     [   {literal-list }] 
CALL USEPROC (subroutine-name,exception-condition-list)     (FORTRAN) 
APL Rules 
1.  To attach more than one exception condition to a single APL procedure, 
    supply a list on the left argument and a single procedure on the right 
    argument. 
2.  To attach n exception conditions to n APL procedures, supply a list of 
    exception conditions on the left and a corresponding list of APL 
    procedures on the right. 
3.  To delete USE procedures, supply an exception condition list on the left 
    and an empty vector on the right. 
4.  To list all exception conditions which have USE procedures, issue the 
    following statement: 
    []DBUSE 2 0 
5.  To list the name of a procedure attached to an exception condition, issue 
    the following statement: 
    []DBUSE exception-code 
6.  To list all USE procedures, issue the following statement: 
    []DBUSE []DBUSE 2 0 
7.  There is an implementation limit of 75 USE procedures. 
8.  The USE procedure table is deleted by )CLEAR and )LOAD and must be 
    reinitialized by execution of []DBUSE statements each time it is deleted. 
COBOL Rules 
1.  A USE statement, when presented, must immediately follow a section header 
    in the Declaratives Section of the Procedure Division and must be followed 
    by a separator period.  The remainder of the section must consist of one 
    or more procedural paragraphs that define the procedures to be used. 
2.  The USE statement itself is never executed; rather, it defines the 
    criteria for the execution of the USE procedures. 
3.  Within a USE procedure, there must be no reference to any non-declarative 
    procedure. 
4.  Within a non-declarative procedure there must be no reference to 
    procedure-names that appear in a Declaratives Section. 
5.  Each literal must be a nonnumeric literal and should represent a valid 
    data base status indicator. 
6.  There can be multiple occurrences of the USE FOR DB-EXCEPTION statement 
    within a program only if the ON phrase is specified in each.  The literals 
    in each USE statement must be unique; multiple USE statements must not 
    cause the simultaneous request for execution of more than one USE 
    declarative.  The OTHER phrase may be specified only once in a program. 
7.  If a USE FOR DB-EXCEPTION statement is specified without the optional ON 
    phrase, it must be the only occurrence of the USE FOR DB-EXCEPTION 
    statement in the program. 
8.  Statements appearing within a given data base exception section may 
    reference procedure-names defined within a different USE procedure only 
    with a PERFORM statement. 
9.  If no ON phrase is specified, or if the ON OTHER phrase is the only phrase 
    specified in the program, the data base exception section is executed 
    whenever the execution of a statement results in a data base exception 
    condition.  At the end of the execution of the data base exception 
    section, control is returned to the statement following the statement that 
    causes the exception. 
COBOL Examples 
1.  In the absence of any USE FOR DB-EXCEPTION statement, the program must 
    test the contents of DB-STATUS for a nonzero value after each Data 
    Manipulation Language function.  Successfully completed functions return a 
    zero status code, while unsuccessful functions return a value according to 
    the action taken and the exception experienced.  A typical sequence of 
    statements is: 
        MOVE "value" TO CALC-CONTROL-ITEM. 
        FIND ANY CALC-REC RECORD. 
        IF DB-STATUS IS EQUAL TO "0502400" GO TO MISSING-RECORD 
        ELSE IF DB-STATUS IS NOT EQUAL TO ZERO GO TO OTHER-ERROR. 
2.  A single USE FOR DB-EXCEPTION statement can be used to process all 
    exception conditions.  This procedure must distinguish between normal 
    exceptions, such as END OF SET or NO RECORD FOUND TO SATISFY RECORD 
    SELECTION, and those exceptions that are errors.  All data items in the 
    Data Division of the program and all the data base special registers are 
    available to the procedure.  Many of the data base special registers are 
    updated for error conditions.  Status flags can be moved depending on the 
    type of exception and the identity of records, sets, or realm involved. 
    For example: 
        Col. 
        1       8     12 
                77    STATUS-FLAG       PIC 9 COMP. 
                      88 END-OF-PATH                VALUE 1. 
                      88 MISSING-REC                VALUE 2. 
                      88 BAD-ERROR                  VALUE 3. 
                PROCEDURE DIVISION. 
                DECLARATIVES. 
                ERROR-PROCESSING SECTION. 
                     USE FOR DB-EXCEPTION. 
                ERROR-PROCESSING-PARAGRAPH. 
                     IF DB-STATUS IS EQUAL TO "0502100" GO TO SET-END-FLAG. 
                     IF DB-STATUS IS EQUAL TO "0502400" GO TO SET-MISSING REC. 
                     MOVE 3 TO STATUS-FLAG. 
                     GO TO BAD-BAD. 
                SET-END-FLAG. 
                     MOVE 1 TO STATUS-FLAG. 
                     GO TO EXIT-EXIT. 
                SET-MISSING-REC. 
                     MOVE 2 TO STATUS-FLAG. 
                     GO TO EXIT-EXIT. 
                     . 
                     . 
                     . 
                EXIT-EXIT. 
                BAD-BAD. 
                END DECLARATIVES. 
                     . 
                     . 
                     . 
                     FIND NEXT WANTED-RECORD WITHIN THIS-SET. 
                     IF END-OF-PATH GO TO DONE-WITH-IT. 
                     . 
                     . 
                     . 
    In this example, each data base exception causes the USE FOR DB-EXCEPTION 
    section to be invoked.  This procedure only checks the status code for 
    certain values and sets condition indicators for reference by the program. 
    The program must subsequently test for acceptable or error conditions. 
    The USE procedure itself can detected an error status and cause the 
    program to abort or terminate abnormally. 
3.  Multiple USE statements can be used to trap specific exceptions as 
    follows: 
        Col. 
        1        8     12 
                 PROCEDURE DIVISION. 
                 DECLARATIVES. 
                 FIRST-LAST-TEST SECTION. 
                      USE FOR DB-EXCEPTION ON "0502100". 
                 SET-INDICATOR-FLAG. 
                      MOVE 1 TO STATUS-FLAG. 
                 SECOND-ERROR-TEST SECTION. 
                      USE FOR DB-EXCEPTION ON "0502400". 
                 SET-FLAG-TO 2. 
                      MOVE 2 TO STATUS-FLAG. 
                 OTHER-ERRORS-TEST SECTION. 
                      USE FOR DB-EXCEPTION ON OTHER. 
                 SET-FLAG-TO-3. 
                      MOVE 3 TO STATUS-FLAG. 
                 END DECLARATIVES. 
    In this variation, three separate USE procedures are invoked for specific 
    data bases exceptions.  The condition values as established by the proper 
    USE procedure will be available to the program.  In this case, all the 
    testing of the specific status code values is performed by the Data Base 
    Control System, which only invokes the proper procedure for each type of 
    exception. 
FORTRAN Rules 
Subroutines may be attached to one or more exception conditions. 
Subroutine names must be declared EXTERNAL in the FORTRAN source program. 
00001
00003
00002
00004
USE for privacy specifies procedures (for COBOL and FORTRAN) and specifies 
privacy keys (for APL and BASIC).  The first data base READY checks all 
privacy keys.  In COBOL and FORTRAN, checking requires the execution of the 
privacy procedures.  In APL and BASIC, the values are checked directly.  COBOL 
establishes USE procedures at compile time.  FORTRAN, APL, and BASIC must 
establish privacy via the PRIVACY and []DBPRIVACY procedures respectively at 
run time before the first READY. 
In each language, USE for privacy has three formats:  one for records, one for 
sets and one for items. 
Format 1 (Record Privacy): 
                    {|CONNECT   |} 
                    {|DISCONNECT|} 
                    {|FIND      |} 
                    {|ERASE     |} 
[]DBPRIVACY 'RECORD {|GET       |} privacy-key [record-list]'           (APL) 
                    {|MODIFY    |} 
                    {|STORE     |} 
                [   {|CONNECT   |}] 
                [   {|DISCONNECT|}] 
                [   {|FIND      |}] 
USE FOR PRIVACY [ON {|ERASE     |}] FOR {RECORDS    }                 (COBOL) 
                [   {|GET       |}]     {record-list} 
                [   {|MODIFY    |}] 
                [   {|STORE     |}] 
                     {|,CONNECT   |} 
                     {|,DISCONNECT|}                                (FORTRAN) 
                     {|,FIND      |} 
CALL PRIVACY (RECORD {|,ERASE     |} ,privacy-subroutine-name[,record-list]) 
                     {|,GET       |} 
                     {|,MODIFY    |} 
                     {|,STORE     |} 
                  {|CONNECT   |} 
                  {|DISCONNECT|} 
                  {|FIND      |} 
DB PRIVACY RECORD {|ERASE     |} privacy-key [record-list]            (BASIC) 
                  {|GET       |} 
                  {|MODIFY    |} 
                  {|STORE     |} 
Format 2 (Set Privacy): 
                 {|CONNECT   |} 
[]DBPRIVACY 'SET {|DISCONNECT|} privacy-key [set-list]'                 (APL) 
                 {|FIND      |} 
                   {|CONNECT   |} {SETS     } 
USE FOR PRIVACY ON {|DISCONNECT|} {set-list }                         (COBOL) 
                   {|FIND      |} 
                                                                    (FORTRAN) 
                   {|,CONNECT   |} 
CALL PRIVACY (SET  {|,DISCONNECT|} ,privacy-subroutine-name [,set-list]) 
                   {|,FIND      |} 
               {|CONNECT   |} 
DB PRIVACY SET {|DISCONNECT|} privacy-key [set-list]                  (BASIC) 
               {|FIND      |} 
Format 3 (Item Privacy): 
[]DBPRIVACY 'ITEM {|MODIFY|} privacy-key,item-list'                     (APL) 
                  {|GET   |} 
USE FOR PRIVACY ON {|MODIFY|} FOR item-list                           (COBOL) 
                   {|GET   |} 
CALL PRIVACY (ITEM {|,MODIFY|},privacy-subroutine-name,item-list)   (FORTRAN) 
                   {|,GET   |} 
DB PRIVACY ITEM {|MODIFY|} privacy-key item-list                      (BASIC) 
                {|GET   |} 
COBOL Notes: 
1.  Any USE statement, when present, must immediately follow a section header 
    in the Declaratives Section of the Procedure Division and must be followed 
    by a separator period.  The remainder of the section must consist of one 
    or more procedural paragraphs that define the procedures to be used. 
2.  The USE statement itself is never executed; rather, it defines the 
    criteria for the execution of the USE procedures. 
3.  Within a USE procedure, there must be no reference to any non-declarative 
    procedure. 
4.  Within a non-declarative procedure there must be no reference to 
    procedure-names that appear in a Declaratives section. 
5.  If a USE for privacy statement is used, at least one of the optional FOR 
    phrases must be specified. 
6.  Statements appearing within a given privacy section may reference 
    procedure-names within a different USE procedure only with a COBOL PERFORM 
    statement (COBOL only). 
7.  The execution of any given privacy procedure is caused by the execution of 
    the first READY statement of the run unit. 
8.  The value contained in the special register DB-PRIVACY-KEY at the 
    completion of the execution of the privacy procedure is the privacy key 
    associated with the realms or record types with which that privacy 
    procedure is associated. 
9.  If the COBOL ON phrase is not specified with any given FOR phrase, the 
    privacy key produced by that privacy procedure applies to all phrases that 
    could have been specified in that omitted phrase.  The record(s) or set(s) 
    to which this privacy clause applies are not permitted to have additional 
    privacy procedures which apply to a specified function. 
    One or more or all options must be applied for APL or FORTRAN. 
10. The record-list or set-list is optional in APL and FORTRAN with the 
    implication that all records or all sets are to be used.  For COBOL, if 
    the "FOR RECORDS" or "FOR SETS" phrase is used rather than specifying an 
    individual record or set, the privacy key produced by that privacy 
    procedure applies to all records or set for which privacy for the 
    specified function or functions has not yet been assigned in previously 
    declared privacy procedures.  Thus, the order in which the procedures 
    appear may be critical. 
    For example, if the following lock values are assigned: 
        "XYZ" for the lock on storing MEMBER-RECORD 
        "ALL" for the lock on storing all other records in the data base. 
        The privacy section set up in the following COBOL program will satisfy 
        the privacy keys: 
        PROCEDURE DIVISION. 
        DECLARATIVES. 
        FIRST-PRIV SECTION. 
             USE FOR PRIVACY ON STORE FOR MEMBER-RECORD. 
        FIRST-MOVE. 
             MOVE KEY1 TO DB-PRIVACY-KEY. 
        SECOND-PRIV SECTION. 
             USE FOR PRIVACY ON STORE FOR RECORDS. 
        SECOND-MOVE. 
             MOVE KEY2 TO DB-PRIVACY KEY. 
The values "XYZ" and "ALL" must be moved to working storage items KEY1 and 
KEY2 before the execution of the first ready. 
However, if the sections are reversed, the privacy key value "ALL" is applied 
to the store for all records including the MEMBER-RECORD record.  The clause 
USE FOR PRIVACY ON STORE FOR MEMBER-RECORD is flagged as a duplicate 
assignment during compilation and is ignored.  And it is possible to store the 
MEMBER-RECORD record during execution since the privacy lock was not properly 
satisfied. 
COBOL Example: 
In a particular data base, the data base administrator has established 
controls on who may store a particular record, connect that record into a 
MANUAL set, and access items within the owner record.  The program has access 
to the privacy key values for each of the privacy locks.  The values are: 
    Value                     Lock 
    AAAAAA                    To store MEMBER-RECORD. 
    12345                     To connect that record. 
    0000                      To connect anything into the set MANUAL-SET. 
    J                         To GET function for OWNER-RECORD. 
The privacy procedures are invoked only when the first realm is made ready. 
Since the realm is being changed by these STORE and CONNECT functions, the 
files must have WRITE permission for the execution of the run unit.  The 
Declaratives Section is: 
    PROCEDURE DIVISION. 
    DECLARATIVES. 
    FIRST-PRIVY SECTION. 
         USE FOR PRIVACY ON GET FOR OWNER-RECORD. 
    FIRST-MOVE. 
         MOVE KEY3 TO DB-PRIVACY KEY. 
    SECOND-PRIVY SECTION. 
         USE FOR PRIVACY ON STORE FOR MEMBER-RECORD. 
    SECOND MOVE. 
         MOVE KEY4 TO DB-PRIVACY-KEY. 
    THIRD-PRIVY SECTION. 
         USE FOR PRIVACY ON CONNECT FOR MEMBER-RECORD. 
    THIRD MOVE. 
         MOVE KEY5 TO DB-PRIVACY KEY. 
    FOURTH-PRIVY SECTION. 
         USE FOR PRIVACY ON CONNECT FOR MANUAL-SET. 
    FOURTH-MOVE. 
         MOVE KEY6 TO DB-PRIVACY KEY. 
    END DECLARATIVES. 
The proper values must be moved to KEY3,...,KEY6 before the execution 
execution of the first READY. 
When the first realm is made ready, all the privacy procedures are invoked in 
turn, each supplying a single privacy key value.  Those resources receiving a 
correct key value are unlocked and remain unlocked until the run unit 
terminates.  During the execution of the program, the special register 
DB-PRIVACY-KEY is only referenced once for each locked resource. 
If any of the locks applied to the above resources are assigned a value of 
null, then the corresponding USE FOR PRIVACY procedure is not invoked since 
the lock with a null value for the key is considered to be satisfied. 
FORTRAN Note: 
The privacy-subroutine-name must be declared EXTERNAL if the subroutine is an 
external one. 
00002
00001
00003
