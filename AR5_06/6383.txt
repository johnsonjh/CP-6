The ARES processor is invoked by entering "ARES" at the system level prompt
(!).  The example below creates a database (model) named BUSINESS containing a
table named EMP. The table is made up of several columns which will contain
information about employees.
 
     !ARES
     ARES D01 Here
     :
 
ARES responds with a salutation.  The ARES salutation includes the current
software version of the ARES processor.  The colon prompt (:)  indicates that
ARES is prepared to receive commands.  Any command(s) recognized by ARES may
now be entered.
 
     :
     : CREATE MODEL BUSINESS
     :
     : CREATE TABLE EMP;
 
     +        (NAME CHAR(20),;
     +         EMP_NO INTEGER,;
     +         SALARY DECIMAL(8,2),;
     +         MAN_NO INTEGER,;
     +         DEPT_NAME CHAR(10),;
     +         GROUP_SIZE INTEGER);
     +     KEY IS PRIMARY(EMP_KEY=EMP_NO)
     :
 
A semicolon (;) at the end of a line is used to indicate command continuation.
If a command is continued from one line to another by ending it with a
semicolon, the colon prompt is replaced by a plus (+) character.  The plus
character continues to prompt each line until the command continuation is
terminated by a line that does not end in semicolon.
 
     :
     : " This comment or remark will not be processed, but
     : " documents what is taking place or marks a certain
     : " place in a file of ARES commands.
     :
 
Comment or remark lines may be included in ARES command files by using a
double quote (") to indicate the beginning and an optional double quote to
indicate the end of the remark or comment.
 
     : COMMIT
       The model BUSINESS has been created.
     : END
 
The ARES session is terminated by typing END.
 
This online HELP facility is intended primarily for quick and easy reference
to command syntax information.
For more information about ARES concepts and examples of usage, please refer
to the ARES manuals.
For manual ordering information see:
HELP (ARES) RELATED_MANUALS
ARES Reference Manual - HA02-03A
*************************************************************************
*
* Copyright (c) Bull HN Information Systems Inc., 1990, 1992
*
*************************************************************************
Syntax:
ABORT
Description:
The affect of an ABORT command is dependent on the mode at the time it is
issued.  If it is issued in create, alter, or drop mode, its effect is to
cancel all DDL commands issued since the mode has been entered (the last
CREATE, ALTER or DROP MODEL command).  The effect is as if the original
CREATE, ALTER or DROP MODEL command and all intervening DDL commands had never
been issued.
 
If it is issued within a transaction in invoke mode, it attempts to back out
of any updates made by DML commands since the last BEGIN or CHECKPOINT command
(whichever is later) and ends the current transaction.  Any options specified
on the BEGIN command that started the transaction will no longer be in effect
after the ABORT command is issued.
Rules:
 
 1. In invoke mode, the ABORT command can only be issued if a transaction is
    active (as defined by a previously issued BEGIN command).  If no such
    transaction is active, an error will be reported.
 2. In invoke mode, a valid ABORT also causes the following actions to be
    taken:
 
   o   If the transient journal is active (as defined under BEGIN_COMMAND) it
       is used to back out of any updates that were made since the last BEGIN
       or CHECKPOINT command.
   o   All records in the transient journal are erased.
   o   All record locks and table locks are released.
   o   If the common journal is active a ROLL BACK record is written.
   o   The transaction is ended.
See also:
BEGIN, CHECKPOINT, COMMIT, ROLL_BACK
00001
00002
00003
ABORT
ARES contains its own access control implementation that is controlled by the
GRANT and REVOKE commands.  These commands have the ability to give users
various privileges within the ARES model.  In no way will any GRANT or REVOKE
command affect the file management access controls on the files created by
ARES.
 
The access controls defined on the files created by ARES are shown  below.
These controls give ARES complete access to any file created by ARES, but does
not affect the use of passwords.  ARES then enforces the access defined by the
creator of the database.  Although ARES itself can always access the file, it
will only do so if the user running ARES has been authorized by the model
creator.
 
Trying to modify access controls of the physical files will usually not have
the desired effect and should therefore be avoided.  ARES expects to have full
access to the files it owns, and does not look at the file access controls to
determine the result of operations.  ARES looks only at the lists defined by
GRANT or REVOKE.
 
A special case exists if the ARES database resides in an account that is
defined with the MERGE attribute.  In this case, if an account is also
specified in the account access controls with anything less than WRITE access,
ARES will not have the proper access to the files comprising the database when
run from that account.  This can be corrected by specifying EXEC for that
account, i.e., "READEXEC=ABC?".  If EXEC is not specified, ARES will indicate
that there is insufficient access to the files.
 
Should the user find it necessary to modify the access controls on the files,
ARES preserves them in future operations.  If new files are created, the user
is responsible for modifying the access controls to conform with the user's
requirements.
 
Org TY  Gran  NGAV     Rec   Last modified   Name
Irl Ia     2     0      10 19:47 MAY 27 '86  EXAMPLES-EMP
  ALL<A>=nolist,exec   ARES?<P>=read,delr,wnew,upd,delf,reattr
Irl Ia     2     0       4 19:46 MAY 27 '86  EXAMPLES-LOCATION
  ALL<A>=nolist,exec   ARES?<P>=read,delr,wnew,upd,delf,reattr
Irl Ia     2     0       5 19:46 MAY 27 '86  EXAMPLES-SALARY_RANGE
  ALL<A>=nolist,exec   ARES?<P>=read,delr,wnew,upd,delf,reattr
Irl Ia     2     0       7 19:46 MAY 27 '86  EXAMPLES-SALES
  ALL<A>=nolist,exec   ARES?<P>=read,delr,wnew,upd,delf,reattr
Key 1a     1     0       7 19:46 MAY 27 '86  EXAMPLES_MOD
  ALL<A>=nolist,exec   ARES?<P>=read,delr,wnew,upd,delf,reattr
Ran 1a     3     0       3 19:46 MAY 27 '86  EXAMPLES_RTD
  ALL<A>=nolist,exec   ARES?<P>=read,delr,wnew,upd,delf,reattr
 ..    6 files,     12 granules listed     36 records listed
ACCESS_CONTROLS
UPDATE commands vary in complexity.  Setting certain fields to constants is
straight-forward.  The following example shows how a user could give everyone
in the same department a raise by issuing one UPDATE command.
 
 : UPDATE ALL EMP SET SALARY=SALARY+SALARY/10
   .. 10 records UPDATEed.
 
As a more complex example, a column named GROUP_SIZE is added to the table.
The user then wishes to have this column contain the number of employees in
the group belonging to each manager.  This requires adding one to the
manager's GROUP_SIZE column for each employee listed under that manager.  This
is shown in the example below.
 
 : UPDATE MAN;
 + FROM EMP,EMP MAN;
 + SET GROUP_SIZE=MAN.GROUP_SIZE+1;
 + WHERE MAN.EMP_NO=EMP.MAN_NO
   .. 9 records UPDATEed.
 :
 : SELECT * FROM EMP
   .. 10 records SELECTed.
 NAME   EMP_NO SALARY MAN_NO DEPT_NAME GROUP_SIZE
 ------ ------ ------ ------ --------- ----------
 SMITH    7369  19800   7654 SHOE               0
 ALLEN    7499  27500   7844 TOY                0
 WARD     7521   9900   7844 TOY                0
 JONES    7566  28600   7902 LOAN               0
 MARTIN   7654  24200   7902 SHOE               3
 
 BLAKE    7698  26400   7654 SHOE               0
 CLARK    7782  17160   7654 SHOE               0
 SCOTT    7788  26125   7844 TOY                0
 TURNER   7844  19800   7902 TOY                3
 FORD     7902  28050      0 PRESIDENT          3
 
Setting values in one table equal to values in another table is slightly more
complicated.  In this case, the SET command contains references to other
tables on the right side of the assignment.  Using the example shown below,
the user matches the current salary to the range and then applies the
increase.  As shown in this example, values found in one table can be assigned
to another with any legal algebraic expression.
 
 : SELECT * FROM SALARY_RANGE
   .. 5 records SELECTed.
   LOW  HIGH PERCENT_RAISE
 ----- ----- -------------
     0  9999            .1
 10000 14999           .14
 15000 19999           .16
 20000 29999           .12
 30000 99999            .8
 
 : UPDATE EMP;
 + FROM EMP,SALARY_RANGE;
 + SET SALARY=SALARY+SALARY*SALARY_RANGE.PERCENT_RAISE;
 + WHERE EMP.SALARY IS BETWEEN SALARY_RANGE.LOW AND SALARY_RANGE.HIGH
   .. 16 records UPDATEed.
Syntax:
{column-id           }
{function-expression } [algebraic-operator [unary-operator]
{                    }     algebraic-expression]
{constant            }
Parameters:
 
algebraic-operator  any of the following:  +, -, *, /.
 
column-id  unique identifier for a column.  See the specific command for
    further detail.
 
constant  as described under CONSTANTS
 
function-expression  as described under FUNCTION_EXPRESSIONS.
 
unary-operator  either + or -.
Description:
An algebraic-expression is a combination of constants, column-ids, algebraic-
operators, function-expressions, and parentheses.  Note that the column-ids in
an algebraic-expression need not belong to the same table.  The symbols for
the algebraic-operators are summarized in the following table with the
precedence of the operator indicated by the magnitude of the associated
number.
 
                     Operator    Meaning        Precedence
                    --------------------------------------
                          +      Unary Plus         7
 
                          -      Unary Minus        7
 
                          *      Multiplication     6
 
                          /      Division           6
 
                          +      Addition           5
 
                          -      Subtraction        5
 
Thus, within the same level of parentheses, operators with higher precedence
numbers are evaluated first.  If this is not desired, parentheses can be
placed around an algebraic-expression to force it to be evaluated in the
correct order.
 
The following are examples of valid algebraic-expressions (blanks are not
significant):
 
    PNAME
    P * 203 / QTY
    3.14 * (INFO.RADIUS1 + INFO.RADIUS2)
 
algebraic-expressions can be used wherever column-ids can be used.  Cases
where only simple column-ids are valid are specifically pointed out in the
commands where required.
00002
00001
GRANT_ALL
The ALTER commands are used to alter the elements of an ARES database.  Both
permanent and temporary elements can be altered.
 
For additional information see:
HELP (ARES) TOPICS ALTER?
 
           Command        Description
 
           ABORT          Cancel the alteration of a model
 
           ALTER BULKFILE Alter a description of a non-ARES file
 
           ALTER COLUMN   Alter a column description
 
           ALTER FUNCTION Alter a user function
 
           ALTER JOURNAL  Change database journaling options
 
           ALTER TABLE    Alter a table
 
           COMMIT         Complete the alteration of a model
 
           DROP BULKFILE  Remove a description of a non-ARES file
 
           DROP FUNCTION  Remove a user function
 
           DROP JOURNAL   Remove database journaling options
 
           DROP TABLE     Remove a table
 
           RENAME COLUMN  Change the name of a column to a new name
Syntax:
ALTER BULKFILE bulkfile-name [COMMENT = literal1]
 
    [alter-column [, alter-column . . .]]
ALTER_COLUMN:
 
                   [BEFORE [COLUMN] {column-name2  }]
                   [                {column-number1}]
ADD {column-name1} [datatype                        ] [,...]
    {      *     } [COMMENT = literal2              ]
 
DELETE column-name3
 
MOVE {column-name4  } [BEFORE [COLUMN] {column-name5  }]
     {column-number2} [                {column-number3}]
Parameters:
 
bulkfile-name  the name of an existing bulkfile in the database.
 
column-name1  an ARES column name.
 
column-name2,3,4,5  name of column which exists in the bulkfile.
 
column-number1,2,3  positional number of a column within the bulkfile.
 
datatype  ARES representation of a data type.
 
literal1,2  text string enclosed in single quotes with a length of 0 to
    255.
Description:
The ALTER BULKFILE command is used to add or delete column descriptions
contained in a bulkfile definition.
Rules:
 
 1. The data type description is optional on each non-filler column, if that
    column name exists in another bulkfile in the model.  If the data type is
    specified, any other bulkfile column with the same name must be the same
    data type.
 2. All occurrences of a bulkfile column in the database must have the same
    COMMENT field.  If it is specified for a column which already exists, it
    will be ignored.
 3. The MOVE clause can be used to change the logical and physical order of
    columns in a bulkfile description.  Use caution when using the MOVE
    clause, since changing the order of the columns will invalidate the use of
    any existing bulkfiles created with the old description.
 4. The BEFORE option may be used when adding or moving a column to place the
    column at a specific position in the bulkfile.  If BEFORE is not
    specified, the column will be added at or moved to the end of the
    bulkfile.
 5. A zero length quoted string (") on a COMMENT will delete the existing
    COMMENT.
 6. To alter permanent bulkfiles, you must be in alter mode.
 7. Altering a bulkfile description may invalidate stored queries which use
    the bulkfile.
 8. The maximum record length allowed by ARES in a bulkfile description is
    65535 bytes.
See also:
CREATE_BULKFILE, DISPLAY_BULKFILE, DROP_BULKFILE, LIST_BULKFILE
00001
00003
00002
00004
00005
ALTER_BULKFILE
Syntax:
ALTER COLUMN [(] column-def [,column-def...] [)]
COLUMN_DEF:
column-name [datatype] [COMMENT=literal1] [HEADING=literal2]
Parameters:
 
column-name  name of column which exists in the table.
 
datatype  ARES representation of a data type.
 
literal1,2  text string enclosed in single quotes with a length of 0 to
    255.
Description:
The ALTER COLUMN command is used to modify the description of a database
column in all tables in which the column exists.
Rules:
 
 1. The column-name parameter must specify the name of a column which exists
    in at least one table in the model.
 2. The datatype parameter is optional.  If specified, the data type of the
    column will be modified in all tables in which the column exists.
 3. The COMMENT and HEADING fields may also be modified for the column.  If
    not specified, their values will be kept.  A zero length quoted string (")
    on a COMMENT or HEADING will delete the existing COMMENT or HEADING.
 4. ARES automatically converts the data in the table to match the new table
    description.  This will be done when the COMMIT command is entered for
    alter mode, or immediately if the alteration is made to a temporary table.
    Two things are important to note because of this:
 
   o   The alteration may take a while.  ARES must read and convert all of the
       data in any modified table to match its new description.
   o   If a column is altered which is a member of the primary key, records
       will be lost from the table if the new description does not cause the
       old data to still be unique in the primary key.
 5. To alter columns that are part of permanent tables, you must be in alter
    mode.
See also:
DISPLAY_COLUMN, RENAME_COLUMN
00001
00003
00002
00004
00005
ALTER_COLUMN
Syntax:
ALTER FUNCTION function-name1 (parameter-list) [: datatype1]
 
    [COMMENT = literal]
 
    [DEFINE function-var1 datatype2 [, function-var2 datatype3 . . .]]
    [[INIT assignment-statement [, assignment-statement . . .]]
         [FOR] [EACH] ROW function-statement]
 
    [block-statement]
FUNCTION_STATEMENT:
{if-statement|while-statement|assignment-statement|block-statement}
IF_STATEMENT:
IF constraint-expression1 THEN function-statement
    [ELSE function-statement]
WHILE_STATEMENT:
WHILE constraint-expression2 DO function-statement
ASSIGNMENT_STATEMENT:
{function-name2|function-var3} := algebraic-expression
BLOCK_STATEMENT:
BEGIN function-statement [, function-statement . . .] END
Parameters:
 
algebraic-expression  as described under ALGEBRAIC_EXPRESSIONS.
 
constraint-expression  as described under CONSTRAINT_EXPRESSIONS.
 
datatype1,2,3  ARES representation of a data type.
 
function-name1,2  ARES identifier naming the function.
 
function-var1,2,3  ARES identifier naming a local function variable.
 
literal  text string enclosed in single quotes with a length of 1 to 255.
 
parameter-list  list of ARES identifiers used as parameters to the
    function.  These parameters are matched with the list of arguments
    passed to the function when it is called.
Description:
The ALTER FUNCTION command is used to redefine functions created using the
CREATE FUNCTION command.
Rules:
 
 1. The only identifiers legal in algebraic expressions and constraint
    expressions used in the function are:  parameters, function variables, and
    the function name.
 2. Subqueries are not allowed in the constraint expressions used in the
    function.
 3. Function expressions are not allowed in the function being defined.
 4. The data type of the function is defined by datatype1.  If it is not
    specified, the data type of the function is determined by the data type of
    the parameter with the highest precedence.
 5. To alter permanent functions, you must be in alter mode.
 6. Altering a function may invalidate stored queries which use the function.
See also:
CREATE_FUNCTION, DROP_FUNCTION, DISPLAY_FUNCTION, LIST_FUNCTION
00004
00005
00007
00001
00002
00006
00008
00009
00003
ALTER_FUNCTION
Syntax:
ALTER JOURNAL { TRANSIENT      } [,...]
              { COMMON [=] fid }
Parameters:
 
fid  a valid CP-6 file identifier.
Description:
The ALTER JOURNAL command is used to alter a journal for the database.  There
are two types of journals: transient and common.  The transient journal
contains images of records before they were updated and is used to back out of
updates.  The common journal contains images of records after they were
updated and is used to roll a database forward from a backup copy.
Rules:
 
 1. The ALTER JOURNAL command can only be issued in create or alter mode.
 2. Specifying TRANSIENT indicates that a transient journal should be active
    when updates are made to the database whether within a transaction or not.
    This protects the user from partially completed updates in the case of
    soft crashes.  No fid is specified since the transient journal is kept in
    a temporary system file.
 3. Specifying COMMON indicates that a common journal should be created.  All
    updates made to the database will be logged in the common journal.  The
    fid for the common journal must specify a valid CP-6 file in an account
    the creator has write access to, and the file must not yet exist.  The
    file will be created with access controls that allow ARES to write to the
    file on behalf of users that do not have write access to the account the
    journal was created in.
 
 4. If a common journal was already defined when the ALTER JOURNAL command is
    issued, journaling is switched to the file identified by the fid specified
    in this command.  The file identified by the old fid is left unaffected.
See also:
BEGIN, CREATE_JOURNAL, DROP
00002
00001
00003
00004
ALTER_JOURNAL
This mode is used to alter an existing model and is entered by issuing the
ALTER MODEL command.  Once in this mode, new tables and elements can be added
to the model by issuing model creation commands.  In addition, existing
elements of the model can be altered or dropped by using the alter model
commands.
 
The commands which are used to modify the database description are similar to
those which are used to create the initial model.  The difference is that only
those parts of the database description that are changing need to be declared.
 
The alteration commands are checked for errors, but are not processed until
all the model alteration commands are entered.  The model alteration is
completed by entering a COMMIT command, or halted by issuing the ABORT
command.  These commands are summarized under the ALTER topic.
 
For additional information see:
HELP (ARES) TOPICS ALTER?
Syntax:
ALTER MODEL fid
Parameters:
 
fid  a file name which identifies the model to be altered.
Description:
The ALTER MODEL command is used to enter the alter mode for model alteration
commands.  The ALTER MODEL command implicitly begins a transaction which must
be completed with a COMMIT command when all alterations have been completed.
Rules:
 
 1. The fid must specify an existing model.
 2. Anyone who has CREATOR permission to the model and WRITE permission to the
    directory where the model resides may enter this command.
 3. If the model was created with a password, that password must be specified
    in the fid or the command is aborted.
 4. The command waits until exclusive use of the model is available.
See also:
ABORT, ALTER_MODE, COMMIT
00002
00001
00003
00004
ALTER_MODEL
A number of changes to the structure of a model make the common journal file
obsolete:
 
   Adding new columns to a table.
   Deleting existing columns from a table.
   Changing the data types of columns in a table.
The following changes to a model do not make the common journal file
obsolete:
 
   Creating new tables.
   Deleting existing tables.
   Changing the secondary key structure of a table.
 
When altering a model, ARES prints warning messages if any requested changes
would invalidate the common journal.  The user can then decide whether to
commit these changes or not.  If the user does commit the changes, it is
recommended that a new backup copy of the database be made, and a new common
journal be started.  These procedures are discussed under BACKUP_COPIES.
 
If the user decides to abort the changes, no further action is required since
the model is not changed and is therefore still in agreement with the common
journal.
 
When rolling a journal forward that contains records for a deleted table, the
records are simply skipped.  When rolling a journal forward that contains
records for a newly created table, the records are applied in the normal
manner.  The roll forward operation never changes the description of any
tables in the model.
ALTER_MODE
Syntax:
ALTER TABLE table-name [COMMENT = literal1]
 
    [alter-column [, alter-column . . .]]
 
        [KEY alter-key [, alter-key . . .]]
ALTER_COLUMN:
[BEFORE [COLUMN] {column-name2  }]
                 [                {column-number1}]
ADD column-name1 [datatype                        ] [,...]
                 [INIT = literal2                 ]
                 [COMMENT = literal3              ]
                 [HEADING = literal4              ]
 
DELETE column-name3
 
MOVE {column-name4  } [BEFORE [COLUMN] {column-name5  }]
     {column-number2} [                {column-number3}]
ALTER_KEY:
{ADD   }
{MODIFY} (key-name1 = column-name6[ ,column-name7 . . .])
 
{DELETE} key-name2
Parameters:
 
column-name1  an ARES column name.
 
column-name2,3,4,5,6,7  name of column which exists in the table.
 
column-number1,2,3  positional number of a column within the table.
 
datatype  ARES representation of a data type.
 
key-name1,2  ARES identifier specifying the name of each key (primary or
    secondary).
 
literal1,3,4  text string enclosed in single quotes with a length of 0 to
    255.
 
literal2  an ARES constant.
 
table-name  the name of an existing table in the database.
Description:
The ALTER TABLE command is used to add, delete, modify, or move descriptions
contained in a table definition.  The new or modified descriptions can be for
columns (either adding, deleting, or moving existing column definitions), or
for keys (either adding, deleting, or modifying key definitions).
Rules:
 
 1. The table-name and column-name(s) in the column list of the KEY
    specification must reference names of a previously created table and
    columns.
 2. The data type description is optional on each column, if that column name
    exists in another table in the model.  If the data type is specified, any
    other table column with the same name must be the same data type.
 3. All occurrences of a column in the database must have the same COMMENT and
    HEADING fields.  If they are specified for a column which already exists,
    they will be ignored.  To change these fields once they have been entered,
    the ALTER COLUMN command must be used.
 4. If the INIT clause is specified on an ADD column, the constant specified
    will be stored in that column in all records of the altered table.  If the
    INIT clause is not specified, a single blank will be stored in character
    or character varying columns, zero will be stored in numeric or TIMESPAN
    columns, and Jan.  1, 1 AD will be stored in DATE columns.
 5. The MOVE clause can be used to change the logical order of columns in a
    table.  The logical order determines the order in which columns are
    displayed when a SELECT * command is issued.
 6. The BEFORE option can be used when adding or moving a column to place the
    column at a specific position in the table.  If BEFORE is not specified,
    the column will be added at or moved to the end of the table.
 7. A zero length quoted string (") on a COMMENT or HEADING in alter mode will
    delete the existing COMMENT or HEADING.
 8. To alter permanent tables, you must be in alter mode.
 9. To modify the description of a column, the ALTER COLUMN command must be
    used.
10. Altering a table description may invalidate stored queries which reference
    the table.
11. The size of any individual key defined for a table cannot exceed 511
    bytes.  The total size for all fields contained in any key of the table
    cannot exceed 4000 bytes.  (This is a restriction on the types of keys
    that can be defined, and in no way restricts the number of records that
    can be stored in a table.)
12. The maximum record length allowed by ARES in a table description is 65535
    bytes.
See also:
CREATE_TABLE, DISPLAY_TABLE, DROP_TABLE, LIST_TABLE
00001
00002
00004
00003
00005
00006
ALTER_TABLE
The ARES Application Program Interface is designed as a call level interface
to the ARES database manager.  This means that the user codes calls into an
application program in a defined format, then links that program with the
object unit library of interface routines.  The call interface is available to
application programs written in any language which generates standard CP-6
calling sequences.
 
For a list of CALL commands used to interface ARES with another program
language, type:
HELP (ARES) TOPICS API?
 
For the syntax and description of a single command, type:
HELP (ARES) command
Format:
CALL ARES_ABORT
Description:
The ARES_ABORT call is used to abort the current transaction.  It functions
 
the same, and is governed by the same rules as the ABORT command.  In
addition, the following rule applies:
Rules:
 
 1. The abort process releases all currently started queries.
00001
00002
Format:
CALL ARES_BEGIN ([begin-command])
Parameters:
 
begin-command  a character argument containing a valid BEGIN command.  A
    valid BEGIN command may not contain the keyword 'BEGIN' or 'Begin'.
Description:
The ARES_BEGIN call is used to define the beginning of a transaction.  It
functions the same, and is governed by the same rules, as the BEGIN command.
In addition, the following rules apply:
Rules:
 
 1. Before a call to ARES_BEGIN is issued, all queries that have been started
    must be released.  If any are not, an error will be generated.
 2. If a rollback occurs (or is issued by calling ARES_ROLLBACK), control will
    automatically be returned to the statement following the call to
    ARES_BEGIN with a special error code set.  If a call to ARES_CHECKPOINT
    has been issued within the same transaction, control will be returned to
    the statement following the last such call.
 3. The compiler for the programming language does not know that control may
    reach the statement following the ARES_BEGIN call by a path other than the
    normal return.  This may result in unexpected operation of the program if
    the code optimizer makes assumptions about program flow, and its effect on
    local variables.  In the following example, the GOTO statement is an
    important part of the program because it informs the compiler of the true
    program flow (though it is never executed).
 
        FLAG=0
        CALL ARES_BEGIN
    10  IF FLAG=1 ...
        .
        .
        .
        FLAG=1
        CALL ARES_ROLLBACK
        GOTO 10
00002
00001
00003
Format:
CALL ARES_CHECKPOINT
Description:
The ARES_CHECKPOINT call informs ARES to checkpoint the current transaction.
It functions the same, and is governed by the same rules, as the CHECKPOINT
command.  In addition, the following rules apply:
Rules:
 
 1. If a rollback occurs, control is returned to the statement following the
    most recent call to ARES_CHECKPOINT from within the current transaction
    with a special error code set.
 2. Those record locks which do not correspond to the current record position
    for any started query are released.
 3. The compiler for the programming language does not know that control may
    reach the statement following the ARES_CHECKPOINT call by a path other
    than the normal return.  This may result in unexpected operation of the
    program if the code optimizer makes assumptions about program flow, and
    its effect on local variables.  In the following example, the GOTO
    statement is an important part of the program because it informs the
    compiler of the true program flow (though it is never executed).
 
        FLAG=0
        CALL ARES_CHECKPOINT
    10  IF FLAG=1 ...
        .
        .
        .
        FLAG=1
        CALL ARES_ROLLBACK
        GOTO 10
00001
00002
Format:
CALL ARES_COMMIT
Description:
The ARES_COMMIT call informs ARES to successfully end the current transaction.
It functions the same, and is governed by the same rules, as the COMMIT
command.  In addition, the following rule applies:
Rules:
 
 1. The commit process releases all currently started queries.
00001
00002
Format:
CALL ARES_DELETE (query-number)
Parameters:
 
query-number  a one-word integer variable containing the query number
    returned to the user by the ARES_START call for the query.
Description:
The ARES_DELETE call allows the user's program to delete the result received
from the last ARES_FETCH call on a query.
Rules:
 
 1. The query-number passed to ARES_DELETE must be the query number which was
    returned to the program by the ARES_START call for the query from which
    the user fetched the result being deleted.
 2. Only the current result, the last result fetched from the query, may be
    deleted.
 3. The query must be started with MODE set to UPDATE or ARES_DELETE will not
    be allowed.
00002
00001
00003
Format:
CALL ARES_DESCRIBE (variable, datatype)
Parameters:
 
datatype  a character argument containing an ARES data type description.
 
variable  a variable in the program.
Description:
The ARES_DESCRIBE call allows the user to specify to the interface the data
types of variables which will be passed on subsequent interface calls.
Rules:
 
 1. If the application language being used does not generate standard CP-6
    argument descriptors, an ARES_DESCRIBE call must be issued for every
    program variable which is passed to the interface.  In addition, literals
    are not allowed as arguments to the interface calls.  This call is not
    necessary if the application language being used generates standard CP-6
    argument descriptors.
 2. The interface remembers the address of each variable described.  If the
    variable's address changes (if it is pointer qualified and a new pointer
    is used or if the variable is local and the routine has returned and been
    reentered) it must be described again.  It is not recommended to describe
    this type of variable or individual elements of an array because the
    interface requires memory to store each of the descriptions.  It is much
    better in most cases to describe a global temporary variable to the
    interface and move the value from there to the desired location.
 3. The datatype must be a text string containing a legal specification of an
    ARES data type terminated by a semicolon.  Data type and conversion
    information can be found under DATATYPE_CORRESPONDENCE
 4. ARES remembers the datatype information specified and uses it to do data
    conversion in subsequent interface calls.
00002
00001
00003
Format:
CALL ARES_DISPLAY (command-text)
Parameters:
 
command-text  the text literal, enclosed in single quotes, containing
    either an ARES DISPLAY or LIST command.
Description:
The ARES_DISPLAY call returns the text generated by ARES for the DISPLAY or
LIST command, passed as a parameter, to a file.
Rules:
 
 1. The SYNTAX and ON/OVER/INTO fid options of the DISPLAY command are
    allowed.
 2. The ON/OVER/INTO fid option of the LIST command is allowed.
 3. If the command uses the ON/OVER/INTO fid option, the result is returned in
    the specified file.  Otherwise, the result is returned in a file called
    "***ARES_DISPLAY".
 4. All types of the ARES LIST command may be used.  The current lists are of
    TABLES, BULKFILES, COLUMNS, FUNCTIONS, DML, DML OWNER, and PRIVS.
 5. Most types of the ARES DISPLAY command may be used.  The acceptable
    displays are of STATS, PRIVS, JOURNALS, TABLES, COLUMNS, BULKFILES,
    FUNCTIONS, DML, and MODEL.
00002
00001
00003
Format:
CALL ARES_END
Description:
The ARES_END call specifies to the interface that use of the ARES databases in
this program is done.  The interface releases any memory it has acquired and
disassociates the database manager.
Rules:
 
 1. Once the ARES_END call has been issued in a program, the interface is
    reset to its initial state.
 2. An ARES_END call is not necessary in an application program.  It is used
    to lower the memory requirements of a program which has completed its
    database processing and needs additional memory to continue processing.
00001
00002
Format:
CALL ARES_ERRMSG ([buffer1 [, buffer2]])
Parameters:
 
buffer1  a character buffer where ARES error message text is stored, if
    needed.
 
buffer2  a character buffer where CP-6 error message text is stored, if
    needed.
Description:
The ARES_ERRMSG call allows the user to report the text of the current ARES
error.
Rules:
 
 1. The ARES_ERRMSG call reports the last ARES or CP-6 error which the
    interface encountered.  It does not generate a valid result if called when
    no error has occurred.
 2. If either buffer1 or buffer2 is present, the text will be written into
    either/both of the buffers.  If not present, both the ARES error message
    text and the CP-6 error message text will be written through M$LO/M$DO.
 3. The ARES_ERRMSG call uses the M$ERRMSG monitor service call to fill in the
    buffers supplied by the user (if any) and to print out the actual error
    messages.  Because this monitor service is used, the buffer must be a
    multiple of 120 bytes.  ARES will never return an error message that is
    longer that 600 bytes.  Therefore, 600 bytes may be safely used as the
    size for the first error message buffer; 600 bytes is also a reasonable
    size for the second buffer, where the CP-6 error messages are returned.
    In the case of a few very long CP-6 error messages, it is possible that
    some text may be truncated.  If this appears to be happening, the error
    buffer can be increased 120 bytes at a time until the full error text
    fits.
    To determine how many lines were actually filled, the buffer can be
    examined in 120 byte chunks.  The first 120 bytes that is found to be all
    blank indicates the end of the message (there will be no blank lines in
    the middle of a message).  Some errors result in only an ARES message or
    only a CP-6 message being returned.  In these cases, the other buffer will
    be left completely blank.
00002
00001
00003
Description:
The ARES_ERROR routine is supplied by the user, not by the interface.  It is
an optional user routine which is called when an error condition occurs.
Rules:
 
 1. ARES_ERROR is optional.  It is called only if supplied in the link for the
    user program.  If supplied, its primary entry point must be called
    "ARES_ERROR". If the program is overlaid, the ARES_ERROR routine must be
    in the root node.
 2. The interface sets the global error code variable before calling the error
    routine.
 3. If the routine is supplied, the interface calls it whenever an error
    condition occurs.  The user routine is optional, but if control is
    returned to the interface via any form of return, the interface will do a
    normal return to the original interface call.
 4. When implementing an ARES_ERROR routine, an attempt to call ARES_END or
    ARES_ROLLBACK within the routine results in a loop with the following
    repeating message:
          *** The attempted call of program: ARES_ERROR
              is unsuccessful because it is a recursive call.
          A ROLLBACK has been performed.
    Using an ARES_ERROR routine without auto causes ARES to make invalid
    recursive calls.  Using an ARES_ERROR with auto without setting up the
    ARES_ERROR routine to handle it, causes an infinite loop of each call from
    ARES_ERROR to again invoke ARES_ERROR.
    To issue a rollback on certain errors, make sure ARES_ERROR is not called
    again after the error that says a rollback has been performed.
 5. COBOL-74 does not allow an underscore (_) in subroutine names.  ARES_ERROR
    must be written in some other language.  This can either do error
    processing or call a COBOL-74 routine of some other name.
00001
Format:
CALL ARES_EXEC (dml-name [, argument-list])
 
CALL ARES_EXECTEXT (dml-text [, argument-list])
Parameters:
 
argument-list  an optional list of values to substitute for parameters in
    the query.
 
dml-name  a character argument containing the name of the DML statement to
    be executed.
 
dml-text  a character argument containing the text of an ARES DML
    statement.
Description:
The ARES_EXEC call requests that the interface execute a DML statement which
was previously stored in the database.  The ARES_EXECTEXT call requests that
the interface parse the text passed to it and pass the result on to the
database manager for execution.
Rules:
 
 1. dml-name must be the name of a DML statement which was previously stored
    in the database via an interactive ARES STORE command.
 2. dml-text must be the full text of a legal ARES DML statement.  It may be
    passed either as a literal or in a program variable.
 3. A DML command being passed as text may be parameterized by utilizing the
    syntax #n, where n is an integer, to hold a place in the DML statement for
    the n'th parameter.  Legal values for n are:   1-39, inclusive.  The first
    n used should be one (1) and then numbered consecutively.  Parameters may
    only be specified in the query where a constant is legal.  Table names,
    column names or other database items may not be parameterized.
 4. Parameters in the DML statement are satisfied from the argument list
    positionally.  If a stored DML is being started, the order is the same as
    that used on the STORE command.  If the command is being passed in text,
    the order is that of the n's used to hold places for the parameters.  An
    argument must be passed for each parameter in the query.
 
 5. Automatic data type conversion is performed on the arguments by the
    interface.  The program may pass constants or program variables of any
    supported type as arguments as long as the contents are appropriate for
    the operations being performed.  If the application language generates
    standard CP-6 argument descriptors, this process is completely automatic.
    If not, the ARES_DESCRIBE call must be issued to inform the interface of
    the data types of the arguments.
 6. The DML statement is completely executed by the ARES_EXEC or ARES_EXECTEXT
    call before control is returned to the program.
 7. If the caller supplied any or all of the optional fields (operations,
    skipped, existed, or overwrite) on the call to ARES_INIT, these fields
    will be filled in on return from these calls.
 8. If the command is a SELECT statement, the data is made available with the
    ARES_REPORT call.
00002
00001
00003
API_ARES_EXEC
Format:
CALL ARES_FETCH (query-number, result-item-list)
Parameters:
 
query-number  a one-word integer variable containing the query number
    returned to the user by the ARES_START call for the query.
 
result-item-list  a list of user-program variables into which the
    interface is to store the results of the fetch.
Description:
The ARES_FETCH call returns the result of the next query to the user program.
Rules:
 
 1. The query-number passed to ARES_FETCH must be the query number which was
    returned to the program by the ARES_START call for the query from which
    the user wishes to fetch the result.
 2. The result-item-list must correspond, one-for-one, with the item list
    returned by the query.  Extra result-item arguments are ignored.  No nil
    arguments are allowed.
 3. Automatic data type conversion is performed on the result-items by the
    interface.  The program may pass program variables of any supported type
    to receive results.  If the application language generates standard CP-6
    argument descriptors, this process is completely automatic.  If not, the
    ARES_DESCRIBE call must be issued to inform the interface of the data
    types of the result-list variables.
 4. When the end of the query is reached, the query number is automatically
    released.
00002
00001
00003
Format:
CALL ARES_FETCHR (query-number, api-rec[, api-rec-desc])
Parameters:
 
api-rec  a user-program variable into which ARES returns the result record
    of the fetch.  This variable must be a character buffer which is at
    least one word long and starts on a word boundary.
 
api-rec-desc  a user-program variable into which ARES returns the
    description of the physical definition of the fields in the record.
    This variable must be a character buffer which is at least one word
    long and starts on a word boundary.
 
query-number  a one-word integer variable containing the query number
    returned to the user by the ARES_START call for the query.
Description:
The ARES_FETCHR call returns to the user program the next result from a query
in record form.  If the optional api-rec-desc parameter is specified, the API
record description associated with the query-number is also returned.
Rules:
 
 1. The query-number passed to ARES_FETCHR must be the query number which was
    returned to the program by the ARES_START call of the query for which the
    user wishes to fetch the record.
 2. The api-rec parameter must be large enough to hold the result record
    returned by ARES. If it is not, a special error code is set and the
    required size of the result record is returned in the first word of
    api-rec.
 3. If the api-rec-desc parameter is specified it must be large enough to hold
    the API record description returned by ARES. If not, a special error code
    is set and the required size of the description is returned in the first
    word of api-rec-desc.
 4. If a size error occurs on api-rec or api-rec-desc no record will be
    fetched.
 5. When the end of the query is reached, the query number is automatically
    released.
00002
00001
00003
Format:
 
CALL ARES_FINDFIELD (api-rec, api-rec-desc, field-num, offset-to-field,
         length-of-field)
Parameters:
 
api-rec  a user-program variable which contains the result record obtained
    by a call to ARES_FETCHR. This variable must be a character buffer
    which is at least one word long.
 
api-rec-desc  a user-program variable which contains the description of
    the physical definition of the fields in api-rec.  This variable must
    be a character buffer which is at least one word long.
 
field-num  a one-word integer which contains the number of the field the
    user wishes to find in api-rec.
 
length-of-field  a one-word integer returned by ARES which specifies the
    length of the field which begins at the offset in offset-to-field.
 
offset-to-field  a one-word integer returned by ARES which contains the
    offset from the beginning of api-rec to the field specified in
    field-num.
Description:
The ARES_FINDFIELD call returns to the user program an offset to the specified
field in api-rec as well as the length of the field.
Rules:
 
 1. The length returned in length-of-field reflects the length in bytes, bits,
    or nibbles depending on the data type of the field.  The units associated
    with each data type are shown in the "Length" column of  under topic
    API_REC_DESC_RULES.
 2. The offset-to-field is in bytes if the data type length of the field is in
    bytes and in bits if the length is in bits or nibbles.  The data is not
    guaranteed to be doubleword aligned for FORTRAN so the user should not
    plan to use it where it is.
 3. If the field to be found is of type CHARACTER VARYING, the offset returned
    in offset-to-field is to the beginning of the text string.
 4. The field-num specified must be within the legal range for the number of
    fields described in api-rec-desc, or one (1) greater than this number.
 5. If field-num is one (1) greater than the number of fields in the api-rec,
    the offset-to-field will contain the byte offset to the byte immediately
    following the data in the api-rec buffer, or in other words, the length of
    the data in the api-rec buffer.  The length-of-field will be zero in this
    case.
00002
00001
00003
Format:
CALL ARES_GETDESC (query-number, api-rec-desc[, conversion-type])
Parameters:
 
api-rec-desc  a user-program variable into which ARES returns the
    description of the physical definition of the fields in the record.
    This variable must be a character buffer which is at least one word
    long and starts on a word boundary.
 
conversion-type  a keyword which indicates a specific type of data
    conversion.
 
query-number  a one-word integer variable containing the query number
    returned to the user by the ARES_START call for the query.
Description:
The ARES_GETDESC call returns to the user program the description of the API
record associated with the query-number.
Rules:
 
 1. The query-number passed to ARES_GETDESC must be the query number which was
    returned to the program by the ARES_START call of the query for which the
    user wishes to get the API record description.
 2. If api-rec-desc is not large enough to hold the API record description
    returned by ARES, a special error code is set and the required size of the
    description is returned to the user program in the first word of
    api-rec-desc.
 3. The API record description in api-rec-desc describes the result of a
    record returned from ARES on a call to ARES_FETCHR or passed to ARES on a
    call to ARES_UPDATER. It in no way affects the description of program
    variables that may be specified in an ARES_FETCH or ARES_UPDATE call.
 4. The API record is composed of fields which are packed together according
    to COBOL alignment rules; every field is byte aligned.
 5. The user may want ARES to modify the api-rec-desc which would normally be
    returned, to contain only the types requested by the conversion-type
    parameter.  The keywords allowed for conversion-type are:   CHAR, FORTRAN,
    and COBOL. The keywords can be abbreviated to a minimum of three letters.
    If CHAR is specified, all fields in api-rec-desc are described as
    character.  If FORTRAN is specified, all fields in api-rec-desc are
    described as legal FORTRAN data types.  If COBOL is specified, all fields
    in api-rec-desc are described as legal COBOL data types.  The ARES data
    types and the corresponding FORTRAN and COBOL data types are described in
    the following table.
 
  ARES Data Type          FORTRAN Data Type         COBOL Data Type
------------------------------------------------------------------------------
------------------------------------------------------------------------------
  CHARACTER(n)            CHARACTER*n               DISPLAY X(n)
  CHARACTER(n) VARYING    CHARACTER*n               DISPLAY X(n)
 
  INTEGER(0 to 18)        INTEGER*2                 COMP-6
 
  INTEGER(19 to 36)       INTEGER                   COMP-6
 
  REAL                    REAL                      COMP-11
 
  DOUBLE PRECISION        DOUBLE PRECISION          COMP-12
 
  DECIMAL(n,m) PACKED     DOUBLE PRECISION          COMP-4 9(n-m).9(m)
 
  DECIMAL(n,m) UNPACKED   DOUBLE PRECISION          DISPLAY 9(n-m).9(m)
 
  DECIMAL(n,m) FLOAT      DOUBLE PRECISION          COMP-12
 
  DATE,TIMESPAN           CHARACTER*format-max      DISPLAY X(format-max)
00002
00001
00003
Format:
CALL ARES_GETFIELD (api-rec, api-rec-desc, field-num, dest-for-field)
Parameters:
 
api-rec  a user-program variable which contains the result record obtained
    by a call to ARES_FETCHR. This variable must be a character buffer
    which is at least one word long.
 
api-rec-desc  a user-program variable which contains the description of
    the physical definition of the fields in api-rec.  This variable must
    be a character buffer which is at least one word long.
 
dest-for-field  a user-program variable into which ARES returns the
    contents of the field specified by field-num.
 
field-num  a one-word integer which contains the number of the field the
    user wishes to get out of api-rec.
Description:
The ARES_GETFIELD call returns to the user program the contents of the field
in api-rec which is specified by field-num.  The data is returned in
dest-for-field.
Rules:
 
 1. The field-num specified must be within the legal range for the number of
    fields described in api-rec-desc and is one-based.
 2. The data types of dest-for-field and the field in api-rec-desc specified
    by field-num must match exactly except for the following cases:
 
   o   CHARACTER or CHARACTER VARYING to CHARACTER or CHARACTER VARYING of any
       size.
   o   INTEGER to INTEGER of any size.
   o   REAL or DOUBLE PRECISION to REAL or DOUBLE PRECISION of any size.
   o   DECIMAL to DECIMAL of any size (packed or unpacked).
    ARES_DESCRIBE may be used to describe dest-for-field as something other
    than what the programming language supports.
00002
00001
00003
Format:
 
CALL ARES_GETSIZE (query-number, number-of-fields, minrec-size[, maxrec-size])
Parameters:
 
maxrec-size  a one-word integer variable into which ARES returns the
    maximum size of the result record for the query.
 
minrec-size  a one-word integer variable into which ARES returns the
    minimum size of the result record for the query.
 
number-of-fields  a one-word integer variable into which ARES returns the
    number of fields in the result record for the query.
 
query-number  a one-word integer variable containing the query number
    returned to the user by the ARES_START call for the query.
Description:
The ARES_GETSIZE call returns to the user program the number of fields in the
result record as well as the minimum, and possibly the maximum, size of the
resulting record.
Rules:
 
 1. The query-number passed to ARES_GETSIZE must be the query number which was
    returned to the program by the ARES_START call of the query for which the
    user wishes to get the sizes.
 2. The size of the api-rec-desc can be calculated using the formula:
       4*(1+(3*number-of-fields)) = size of api-rec-desc in bytes.
 3. The minrec-size reflects the size of the result record as if all CHARACTER
    VARYING fields have lengths of zero.
 4. The maxrec-size reflects the size of the result record as if all CHARACTER
    VARYING fields use the maximum lengths.
 5. If there are no CHARACTER VARYING fields in the result record, minrec-size
    and maxrec-size are equal.
 6. A word of warning is offered here.  A lot of situations create CHARACTER
    VARYING fields which are not obvious to the user.  For example, several
    string functions (i.e., CONCAT, etc.)  return CHARACTER VARYING fields.
00002
00001
00003
Format:
CALL ARES_INIT (error [, [CP6error], [operations],
    [overwrite], [existed], [skipped], [argument-number]])
Parameters:
 
argument-number  a global variable into which the interface is to store
    the number of the argument when a data conversion error occurs.  The
    number will be the position within the argument-list or update-list on
    the call.
 
CP6error  a global variable into which the interface is to store the CP-6
    error code of any error which occurs.
 
error  a global variable into which the interface is to store the ARES
    error code of any error which occurs.
 
existed  a global variable into which the interface is to store the number
    of records that already existed (INSERT and LOAD only).
 
operations  a global variable into which the interface is to store the
    number of records operated on by this DML.
 
overwrite  a global variable into which the interface is to store the
    number of records overwritten (INSERT and LOAD only).
 
skipped  a global variable into which the interface is to store the number
    of records skipped (LOAD only).
Description:
The ARES_INIT call is used to initialize the interface and to provide
variables where error codes and other information may be stored.  All but the
first field (error) is optional; however, null values must be used as
placeholders for any items omitted when following items are supplied.
 
If the database manager is not currently associated, it will be associated by
this call (see API_LINKING_INFORMATION for more information).
Rules:
 
 1. All parameters must be one-word, integer global variables which will not
    change address during the execution of the program.
    Examples of normal definitions of the error variable are:   COMMON for
    FORTRAN, a working storage variable in the main program for COBOL, or
    STATIC for PL-6.  The interface remembers the address of this variable and
    always stores an error code number into it before returning to the user's
    program.  A value of zero in this variable after a call to an interface
    routine means that the call executed successfully.  A value other than
    zero means that an error occurred.  A full description of error conditions
    may be found under the topic API_ERROR_CONDITIONS.
 2. The only routines that the user may call before ARES_INIT are
    ARES_DESCRIBE and ARES_SETNIL. If an error occurs in one of these routines
    and an error code has never been passed to ARES_INIT, the error message is
    reported to the user.  Any attempt to call any other routine before a
    successful call to ARES_INIT results in an error message.
 3. The ARES error code variable, error, contains the error message number of
    any ARES_ERROR which occurred (see API_ERROR_CONDITIONS).
 4. The CP-6 error code variable, CP6error, will contain the entire C-6 error
    code, including FCG, MID, MON, etc.  Interpretation may not be possible
    from some languages (like COBOL) that do not support bit data types.  A
    user-written PL-6 subroutine may be required to interpret these codes.
 5. If more than one error occurs on any single call, only the first error is
    returned to the user.
 6. The operations, overwrite, existed, and skipped parameters are used to
    store various statistics about execution of a DML statement.  These values
    are only valid after the return from a call to either ARES_EXEC or
    ARES_EXECTEXT; refer to these calls for more information.
00002
00001
00003
Format:
CALL ARES_INVOKE (model [, password])
Parameters:
 
model  a character argument containing the model fid.
 
password  a character argument containing the password for the model.
Description:
The ARES_INVOKE call specifies to the interface which database the user wishes
to access.  During this call, access controls are checked to verify that the
user has access to the database, the database is "opened" by the database
manager, and the interface is initialized.
Rules:
 
 1. The model parameter may be a full CP-6 fid including DP#packset, account,
    and password.  If a password is specified in the model, the password
    argument on the call is ignored.
 2. The password argument is optional.  It specifies a password for use in
    opening the database.
 3. Multiple ARES_INVOKE calls may be issued during the execution of a single
    program.  Issuing a new ARES_INVOKE call terminates all open queries,
    closes the currently open database, and proceeds just as if it were the
    first ARES_INVOKE call.
 4. If the model is currently being altered, ARES waits until the invoke can
    be accomplished.
00002
00001
00003
Format:
CALL ARES_KEEP (query-number)
Parameters:
 
query-number  a one-word integer variable containing the query number
    returned to the user by the ARES_START call identifying the query.
Description:
The ARES_KEEP call allows the user to keep record locks active on records that
have not been updated.
Rules:
 
 1. The query-number passed to ARES_KEEP must be the query number which was
    returned to the program by the ARES_START call for the query for which the
    user wishes to keep the record locks.
 2. ARES_KEEP can only be called from within a transaction.
 3. At least one table in the query must have been specified in the current
    ARES_BEGIN with options that cause record locks to be issued.
 4. Any records belonging to tables in the query for which record locks are
    being issued that represent the current position of the query will be
    marked such that the record locks will not be released.
00002
00001
00003
Format:
CALL ARES_NAMELIST (list-type, result-buf [, table-name])
Parameters:
 
list-type  the keyword associated with the desired type of LIST.
 
result-buf  a user-program variable of type character into which ARES
    returns the result list.  This variable must be at least one word
    long.
 
table-name  the name of the table or bulkfile for which columns will be
    listed when list-type is COLUMNS and the columns of a particular table
    are desired.
Description:
The ARES_NAMELIST call returns to the user program the list of names resulting
from the LIST command.  The names are returned in the specified character
buffer and are separated by commas.
Rules:
 
 1. The result-buf must be large enough to hold the list returned by ARES. If
    it is not, a special error code is set and the required size of the result
    list is returned in the first word of result-buf.
 2. The keywords allowed for list-type are:   TABLES, BULKFILES, COLUMNS,
    FUNCTIONS, and DML. All of these work exactly like the LIST commands
    issued from interactive ARES with three exceptions:   LIST DML OWNER and
    LIST PRIVS are not allowed, and LIST COLUMNS in a particular table is only
    used by ARES_NAMELIST and not by interactive ARES. The keywords can be
    abbreviated to a minimum of three letters.
 3. Use of COLUMNS as the list-type parameter along with the use of table-name
    results in a list of all the columns in the specified table or bulkfile.
    If the table-name parameter is not used when COLUMNS is specified, the
    result is a list of all the column names in the database.
 4. Only the list of names is returned.  Any comments associated with the
    names will not be returned.  If the user wishes to get this extra
    information, a call to ARES_DISPLAY must be used.
00002
00001
00003
Format:
CALL ARES_PUTDESC (query-number, api-rec-desc)
Parameters:
 
api-rec-desc  a user-program variable which contains the user's
    description of the physical definition of the fields in the record.
    This variable must be a character buffer which is at least one word
    long.
 
query-number  a one-word integer variable containing the query number
    returned to the user by the ARES_START call for the query.
Description:
The ARES_PUTDESC call passes to ARES the user's description of the API record
which is associated with the query-number.
Rules:
 
 1. The query-number passed to ARES_PUTDESC must be the query number which was
    returned to the program by the ARES_START call of the query for which the
    user wishes to describe records.
 2. ARES verifies the user's API record description in api-rec-desc.  An error
    will be returned to the user if it is invalid and the old description will
    remain associated with the query number.
 3. It is not necessary for the user to make the api-rec-desc lengths
    associated with protected fields (see ARES_UPDATER_CALL, Rule 9) negative
    before calling ARES_PUTFIELD as ARES updates the api-rec-desc parameter to
    indicate such fields before returning to the application program.  It is
    necessary, however, for the user to be aware that the signs of these
    lengths may change during this call.
 4. The lengths of fields with data types containing non-variable lengths will
    be changed to the value shown  under API_REC_DESC_RULES, if any other
    value is specified during the call to ARES_PUTDESC.
 5. If a change is to be made to the description, it should be done just
    before an API record is fetched or the results cannot be guaranteed.
 6. ARES remembers the new description put in api-rec-desc for a query and
    uses it to create the result records accordingly.
00002
00001
00003
Format:
CALL ARES_PUTFIELD (api-rec, api-rec-desc, field-num, source-of-field)
Parameters:
 
api-rec  a user-program variable described by api-rec-desc in which ARES
    replaces the data of the field specified by field-num with the
    contents of source-of-field.  This variable must be a character buffer
    which is at least one word long.
 
api-rec-desc  a user-program variable which contains the description of
    the physical definition of the fields in api-rec.  This variable must
    be a character buffer which is at least one word long.
field-num  a one-word integer which contains the number of the field the
    user wishes to replace in api-rec.
 
source-of-field  a user-program variable which contains the data to be put
    into api-rec.
Description:
The ARES_PUTFIELD call returns to the user program the api-rec which contains
the new data from source-of-field which was put in the specified field.
Rules:
 
 1. The field-num specified must be within the legal range for the number of
    fields described in api-rec-desc and is one-based.
 2. The data types of source-of-field and the field in api-rec-desc specified
    by field-num must match exactly except for the following cases:
 
   o   CHARACTER or CHARACTER VARYING to CHARACTER or CHARACTER VARYING of any
       size.
   o   INTEGER to INTEGER of any size.
   o   REAL or DOUBLE PRECISION to REAL or DOUBLE PRECISION of any size.
   o   DECIMAL to DECIMAL of any size (packed or unpacked).
    ARES_DESCRIBE may be used to describe source-of-field as something other
    than what the programming language supports.
 3. The api-rec parameter must be large enough to hold the updated API record
    returned by ARES. If it is not, a special error code is set and the
    required size of the updated record is returned in the first word of
    api-rec.
00002
00001
00003
Format:
CALL ARES_RELEASE (query-number)
Parameters:
 
query-number  a one-word integer variable containing the query number
    returned to the user by the ARES_START call identifying the query.
Description:
The ARES_RELEASE call allows the user to close a currently open query.
Rules:
 
 1. If the started query associated with the query-number specified in the
    call is open, it is closed and released for use in other queries.  If it
    is closed or not allocated, the call is ignored.
 2. The ARES_RELEASE call is not necessary if the user fetches all of the
    results from a query because the interface automatically releases the
    query-number when there are no more results to return.
00002
00001
00003
Format:
CALL ARES_REPORT (report-options)
 
CALL ARES_XREPORT (report-options)
Parameters:
 
report-options  a character argument containing a valid report command to
    the ARGENT report writer product.
Description:
These calls transfer control to ARGENT for the generation of a report.
Rules:
 
 1. The calls pass the report-options to ARGENT and do not return control to
    the user program until the entire report has been generated.
 2. The calls do not function if the ARGENT product is not available on the
    user's system.
 3. If the data for the report is from a SELECT command which has just been
    processed by one of the ARES_EXEC calls, ARES_REPORT should be used.  If
    the data is from another source, ARES_XREPORT should be used.  In
    addition, the fid information necessary to find the data must be present
    in the report-options parameter or in the report workspace.
 4. A using-clause must be specified as one of the report-options, and the
    using-clause must reference a previously defined ARGENT workspace.
00002
00001
00003
API_ARES_SET_OVERWRITE
Format:
CALL ARES_ROLLBACK
Description:
The ARES_ROLLBACK call informs ARES to roll back the latest set of updates
using the transient journal.  It functions the same, and is governed by the
same rules as the ROLL command with the BACK option.  In addition, the
following rules apply:
Rules:
 
 1. When a call to ARES_ROLLBACK is issued, control is transferred to the
    statement following the most recent call to ARES_CHECKPOINT or ARES_BEGIN
    that was issued within the current transaction with a special error code
    set.
 2. The rollback process releases all currently started queries.
00001
00002
Format:
CALL ARES_SETNIL (nil-loc)
Parameters:
 
nil-loc  a program variable.
Description:
The ARES_SETNIL call allows the user of the interface to specify an address to
be recognized as NIL by the interface.
Rules:
 
 1. nil-loc must be a program variable whose address does not change during
    the execution of the program.  The interface does not use this variable
    but remembers its address and recognizes it, if passed on a subsequent
    interface call, as a NIL parameter.
 2. This call is not necessary if the application language being used supports
    NIL parameters.
00002
00001
00003
Format:
CALL ARES_SET_BEGIN [({REQUIRED|OPTIONAL})]
Description:
The ARES_SET_BEGIN routine allows the programmer to prevent DML commands from
inadvertently locking the whole model by issuing them outside of a
transaction.
Rules:
 
 1. If REQUIRED is specified, any DML command issued outside of a transaction
    will result in an error.
 2. If OPTIONAL is specified, a DML command can be issued in or out of a
    transaction.
 3. The default is OPTIONAL, if no routine is called.
 4. If no parameter is specified, REQUIRED is assumed.
00001
00002
Format:
CALL ARES_SET_DATE (date-format)
Parameters:
 
date-format  a character string containing a date format or the keywords
    MODEL or DEFAULT.
Description:
The ARES_SET_DATE routine gives ARES a format specification for DATE data.
The input of DATE data through the date constant or DATE function will be
affected as will all formatting of selected results (when converted to a
character datatype).
Rules:
 
 1. If the date-format argument is omitted or passed as NIL, or the keyword
    DEFAULT is specified, the date format will be set to the system default.
 2. If the keyword MODEL is specified, the date format will be set to the
    model default if one exists, or to the system default if one does not.
00002
00001
00003
Format:
CALL ARES_SET_OVERWRITE
 
CALL ARES_RESET_OVERWRITE
Description:
The ARES_SET_OVERWRITE routine sets the OVERWRITE flag in ARES. The
ARES_RESET_OVERWRITE routine resets the OVERWRITE flag in ARES.
Rules:
 
 1. If set, the OVERWRITE flag allows INSERT, LOAD, and DUMP commands to
    overwrite existing records with the same primary key.  The If reset,
    overwriting is not allowed.  The user must also have UPDATE privilege to
    the table in which the overwrite takes place.
 2. The default for OVERWRITE is OFF.
See also:
DUMP, INSERT, LOAD
00001
00002
00003
Format:
CALL ARES_SET_TIME (time-format)
Parameters:
 
time-format  a character string containing a timespan format, or the
    keywords MODEL or DEFAULT.
Description:
The ARES_SET_TIME routine gives ARES a format specification for TIMESPAN data.
(This is not to be confused with the time portion of a DATE data type.)  The
input of TIMESPAN data through the timespan constant or TIME function will be
affected as will all formatting of selected results (when converted to a
character datatype).
Rules:
 
 1. If the time-format argument is omitted or passed as NIL, or the keyword
    DEFAULT is specified, the timespan format will be set to the system
    default.
 2. If the keyword MODEL is specified, the time format will be set to the
    model default if one exists, or to the system default if one does not
    exist.
00002
00001
00003
Format:
CALL ARES_START (dml-name, query-number, mode [, argument-list])
 
CALL ARES_STARTEXT (dml-text, query-number, mode [, argument-list])
Parameters:
 
argument-list  a list of values to substitute for parameters in the query.
 
dml-name  a character argument containing the name of the stored query to
    be started.
 
dml-text  a character argument containing the text of an ARES SELECT
    statement.
 
mode  a character argument containing the mode of execution of the query.
    The value for mode may be either INPUT or UPDATE (see Rules below).
 
query-number  a one-word integer variable into which the interface may
    store the query number it has allocated.
Description:
The ARES_START call requests that the interface start a query (SELECT
statement) which was previously stored in the database.  The ARES_STARTEXT
call requests that the interface parse the text passed to it and pass the
result on to the database manager for execution.
Rules:
 
 1. dml-name must be the name of a query (SELECT statement) which was
    previously stored in the database via an interactive ARES STORE command.
 2. dml-text must be the full text of a legal ARES SELECT command.  It may be
    passed either as a literal or in a program variable.
 3. A SELECT command being passed as text may be parameterized by utilizing
    the syntax #n, where n is an integer, to hold a place in the query for the
    n'th parameter.  Legal values for n are:   1-39, inclusive.  The first n
    used should be one (1) and then numbered consecutively.  Parameters may
    only be specified where constants are legal.  Table names, column names or
    other database items may not be parameterized.
 4. The query-number argument should be a one-word, integer variable in the
    user's program into which the interface may store the query number it has
    allocated.  The user must return this query number on all subsequent calls
    to the interface which operate upon the query.
 5. The mode parameter specifies the mode in which the user intends to use
    this query.  Currently defined values for mode are:
 
   o   IN/PUT    the results are only going to be fetched.
   o   UP/DATE    the results may be updated or deleted by the program.
    The mode argument is passed to the program in text.
 6. If mode is UPDATE, the following restrictions apply to the query being
    started:
 
   o   select-list may only contain columns or a table.
   o   select-list may only contain columns from a single table.
   o   UNION, INTERSECT, and MINUS are prohibited.
   o   ORDER BY, GROUP BY, and DISTINCT are prohibited.
 7. Parameters in the query are satisfied from the argument-list positionally.
    If a stored query is being started, the order is the same as that used on
    the STORE command.  If the query is being passed in text, the order is
    that of its n'th place in the parameterization.  An argument must be
    passed for each parameter in the query.
 8. Automatic data type conversion is performed on the arguments by the
    interface.  The program may pass constants or program variables of any
    supported type as arguments as long as the contents are appropriate for
    the operations being performed.  If the application language generates
    standard CP-6 argument descriptors, this process is completely automatic.
 
    If not, the ARES_DESCRIBE call must be issued to inform the interface of
    the data types of the arguments.
 9. When the first ARES_START or ARES_STARTEXT call is issued, if the user is
    not within a transaction, all tables in the model are locked.  The command
    waits until all tables are locked (see SHARING_TABLES).
00002
00001
00003
API_ARES_START
Format:
CALL ARES_UPDATE (query-number, update-list)
Parameters:
 
query-number  a one-word integer variable containing the query number
    returned to the user by the ARES_START call for the query.
 
update-list  a list of values which are to update the values received from
    the ARES_FETCH call.
Description:
The ARES_UPDATE call allows the user's program to change values in the last
result received from an ARES_FETCH call on the query.
Rules:
 
 1. The query-number passed to ARES_UPDATE must be the query number which was
    returned to the program by the ARES_START call for the query from which
    the user fetched the result being updated.
 2. Only the current result (i.e., the last result fetched from the query) may
    be updated.
 3. The update-list must correspond, one-for-one, with the item list returned
    by the query.  If the update list is shorter than the list returned by the
    query, the missing arguments are treated as NIL arguments.
 4. The update-list may contain NIL arguments.  The interface recognizes these
    and does not attempt to update the item represented positionally by the
    NIL argument.  If the application language does not support NIL arguments,
    the ARES_SETNIL call may be used to supply an address for the interface to
    recognize as NIL.
 5. Automatic data type conversion is performed on the update-list items by
    the interface.  The program may pass constants or program variables of any
    supported type as update-list items as long as the contents are
    appropriate for the operations being performed.  If the application
    language generates standard CP-6 argument descriptors, this process is
    completely automatic.  If not, the ARES_DESCRIBE call must be issued to
    inform the interface of the data types of the arguments.
 6. The interface does not allow the program to update items which are part of
    the primary key of the table being updated.
 7. The query must be started with mode set to UPDATE or ARES_UPDATE will not
    be allowed.
00002
00001
00003
Format:
CALL ARES_UPDATER (query-number, api-rec[, update-list])
Parameters:
 
api-rec  a user-program variable which contains the updated version of the
    record received from the ARES_FETCHR call.  This variable must be a
    character buffer which is at least one word long and starts on a word
    boundary.
 
query-number  a one-word integer variable containing the query number
    returned to the user by the ARES_START call for the query.
 
update-list  a list of the field numbers which are updated with the values
    in api-rec.  A character buffer representing a list of one-word
    entries should be used to pass the field numbers to ARES. If
    specified, this variable must be at least one word long.
Description:
The ARES_UPDATER call allows the user's program to change values in the last
result record received from an ARES_FETCHR call on the query.
Rules:
 
 1. The query-number passed to ARES_UPDATER must be the query number which was
    returned to the program by the ARES_START call of the query for which the
    user wishes to update the result record.
 2. The last call to ARES_FETCHR must have been successful before a call to
    ARES_UPDATER is allowed.
 3. Only the current result record (i.e., the last result record fetched from
    the query) may be updated.
 4. The api-rec must correspond to the API record description used when the
    record was fetched.
 5. The first word of update-list tells how many entries are in the list.
 6. The field numbers are one-based as are all ARES field (column) numbers
    from the user's view.
 7. Only the fields which are specified by number in the update-list are
    updated.  If no field numbers are specified, all fields in the record,
    with the exception of primary key fields, are updated.
 8. If update-list is used and the field number of a primary key field is
    specified, an error is returned since primary keys cannot be updated.
 9. Only fields referring directly to database column names may be updated.
    Fields which are the result of functions, constants, arithmetic equations,
    etc., are considered to be protected fields (as are fields which are part
    of a primary key).  Primary key fields and other protected fields will
    have negative lengths in the api-rec-desc associated with the query.  The
    absolute value of this length is the actual length of the field (see
    API_REC_DESC_RULES).
10. The query must be started with mode set to UPDATE or ARES_UPDATER will not
    be allowed.
00002
00001
00003
API_ARES_REPORT
Since the part of ARES which the API talks to is an Alternate Shared Library
(ASL), break control must be handled in a special way.  If the user hits the
BREAK key while the ASL is in control, it receives the break event.  In
general, the ASL will remember this break event and delay the posting of this
event on the application program until the current ASL operation is complete.
Once the application is given the break event, there is no way to return to
the point-of-interrupt within the ASL. To the application program, it will
appear as if the current call to an ARES_?  routine had just been completed
when the BREAK key was hit.
 
When ARES is waiting to lock or open files, this behavior fails because ARES
keeps retrying the locks or opens at regular intervals until they are
successful.  This may delay the posting of the break for too long (especially
since the user is probably using the BREAK key to shorten the waiting period).
ARES must therefore process the break immediately.
 
Since processing the break in such a manner will prevent ARES from continuing
directly where it left off, it must inform the user that the interrupted call
must be reissued by the application program.  To indicate this, a special
error code will be returned (see API_ERROR_CODES).
COBOL users need to code the call to the interface routine as a call to an
external routine written in another language.
 
     CALL "ARES_RELEASE" USING QUERY-NUMBER.
API_COBOL
API_COBOL
The following chart shows the correspondence between the ARES data types and
the data types of FORTRAN, COBOL, and PL-6.  Note that for PL-6, the entry
points to the ARES Application Program Interface routines must be declared
with the CONV(0) clause in order for data type descriptors to be generated.
 
COBOL-85 and FORTRAN automatically generate the proper data type descriptors
for calling the Application Program Interface, and in general users of these
languages do not need to worry about data type conversions.  COBOL-74 does not
generate any data type descriptors, and users will have to use the
ARES_DESCRIBE call for each data item passed to ARES through the Application
Program Interface.  ARES will accept either ASCII or EBCDIC signs on decimal
numbers, but will return only ASCII signs.
 
It is not necessary to have the data type of items in a table match the data
type that will be used by a program to manipulate that data; ARES will
automatically do any conversion necessary.
 
The ARES Application Program Interface supports all data types shown in the
following table.  Any data types not mentioned in this table are not supported
by the ARES Application Program Interface, and should not be used.
 
  PL-6 data type                       ARES data type
------------------------------------------------------------------------------
  CHAR(n)                              CHAR (n)
 
  SBIN(n)                              INTEGER (n) SIGNED
 
  UBIN(n)                              INTEGER (n) UNSIGNED
 
  literal string                       CHAR (n)
 
  numeric literal                      INTEGER (36) SIGNED
------------------------------------------------------------------------------
  (n indicates the size of the item)
 
  FORTRAN data type                    ARES data type
------------------------------------------------------------------------------
------------------------------------------------------------------------------
  INTEGER                              INTEGER (36) SIGNED
  INTEGER*2                            INTEGER (18) SIGNED
 
  REAL                                 REAL
 
  DOUBLE PRECISION                     DOUBLE PRECISION
 
  CHARACTER*n                          CHARACTER (n)
 
  literal string of length n           CHARACTER (n)
 
  numeric literal without decimal pointINTEGER (36) SIGNED
 
  numeric literal with decimal point   REAL
------------------------------------------------------------------------------
  (n indicates the size of the item)
 
  COBOL Syntax                         ARES data type
------------------------------------------------------------------------------
------------------------------------------------------------------------------
  COMP (no sign in picture)            DECIMAL (s,f) PACKED
  COMP (leading sign clause)           DECIMAL (s,f) PACKED SIGNED LEADING
 
  COMP-3 (no sign in picture)          DECIMAL (s,f) PACKED UNSIGNED
 
  COMP-3 (leading sign clause)         DECIMAL (s,f) PACKED SIGNED LEADING
 
  COMP-3                               DECIMAL (s,f) PACKED SIGNED TRAILING
 
  COMP-4 (no sign in picture)          DECIMAL (s,f) PACKED
 
  COMP-4 (leading sign clause)         DECIMAL (s,f) PACKED SIGNED LEADING
 
  COMP-5 (no sign in picture)          DECIMAL (s,f) PACKED
 
  COMP-5 (leading sign clause)         DECIMAL (s,f) PACKED SIGNED LEADING
 
  COMP-6                               INTEGER
 
  COMP-7                               INTEGER
 
  COMP-8 (no sign in picture)          DECIMAL (s,f) PACKED UNSIGNED
 
  COMP-8                               DECIMAL (s,f) PACKED SIGNED LEADING
 
  COMP-11                              REAL
 
  COMP-12                              DOUBLE PRECISION
 
  DISPLAY (alphanumeric)               CHARACTER (n)
 
  DISPLAY (numeric no sign)            DECIMAL (s,f) UNPACKED UNSIGNED
 
  DISPLAY (lead sign separate)         DECIMAL (s,f) UNPACKED SIGNED LEADING
 
  DISPLAY (trail sign separate)        DECIMAL (s,f) UNPACKED SIGNED
                                       TRAILING
 
  DISPLAY (leading sign)               DECIMAL (s,f) UNPACKED OVERPUNCHED
                                       LEADING
 
  DISPLAY (trailing sign)              DECIMAL (s,f) UNPACKED OVERPUNCHED
                                       TRAILING
------------------------------------------------------------------------------
  (n indicates the size of the item)
 
  (s indicates the total number of digits for a decimal number)
 
  (f indicates the scale factor for a decimal number)
------------------------------------------------------------------------------
Before data can be transferred in record mode between the user program and
ARES by way of either an ARES_FETCHR or an ARES_UPDATER call, the description
of the physical definition of the fields in the API record must be determined.
The variable api-rec-desc refers to this API record description.
 
The API record description is determined by ARES during a call to ARES_START
or ARES_STARTEXT (see API_ARES_START) for a given query.  This default record
description is stored internally for use by a given query until a call to
ARES_PUTDESC is made to change it.  The description may be retrieved by the
user by either issuing a call to ARES_GETDESC or a call to ARES_FETCHR which
specifies the api-rec-desc parameter.  The user may request that the data
types of the fields in api-rec-desc be converted to all character fields, to
appropriate FORTRAN data types, or to appropriate COBOL data types by using
the conversion-type parameter on the call to ARES_GETDESC. The user is
responsible for allocating the memory into which the description is returned
from ARES. If not enough memory is allocated, a special error code is set to
indicate that the api-rec-desc parameter is not large enough (see
API_ERROR_CODES). The required size is then returned in the first word of the
api-rec-desc parameter.
 
The user may wish to change the contents of the api-rec-desc returned by a
call to ARES_GETDESC or ARES_FETCHR, or create a description from scratch.  In
order to associate this new api-rec-desc with a given query number, a call to
ARES_PUTDESC must be issued.  Once this is done, records associated with this
query number will be processed according to the new description.  ARES checks
the user's description for legal data types and sizes, and returns an
appropriate error code, if necessary.  The user must be careful not to change
the API record description while still processing the current API record, as
ARES will not detect this as an error.  If a change is to be made to the
description, it is recommended that it be done just before a record is fetched
or the result cannot be guaranteed.
 
The amount of memory to be allocated by the user can be determined in a couple
of ways.  The user can either make a guess about the maximum size of the API
record description or call ARES_GETSIZE. The purpose of ARES_GETSIZE is to
return the number of fields in the result record as well as the minimum, and
possibly the maximum, size of the resulting record.  The parameter for the
maximum record size is optional and will equal the minimum record size if no
CHARACTER VARYING fields are in the record.  The size of the API record
description may be easily calculated since the number of fields in the record
is known (see API_ARES_GETSIZE, Rule 2).
The following table lists a portion of the error codes that may be returned by
the Application Program Interface.  The remaining error codes are not relevant
to program control and are therefore not documented here.  (Bracketed items,
i.e., [ ], indicate variable information filled by ARES for that particular
session.)
 
  Error / Explanation
 
  1     The end of the query [for query number n] has been reached.
 
  This error message means that there are no more results for the query number
  used on a call to ARES_FETCH.
------------------------------------------------------------------------------
  2     Break hit while waiting to access the model.
 
  This error message means that the interactive user hit the BREAK key while
  ARES was waiting for another user to finish altering the model.  Since the
  operation could not be completed before returning the break event to the
  API, the special error code is returned.
------------------------------------------------------------------------------
  3     Break hit while waiting to access a table.
 
  This message means the interactive user hit the BREAK key while ARES was
  waiting to open or lock the necessary tables.  Since the operation could not
  be completed before returning the break event to the API, the special error
  code is returned.
------------------------------------------------------------------------------
  4     Error processing argument number [argument-number].
 
  This message means that a data conversion error occurred while handling the
  specified argument in the call.  The operation was not done.  The argument
  number may be found in the argument-number specified on the ARES_INIT call.
  The argument-number will represent the position within the argument-list or
  update-list on the call.
------------------------------------------------------------------------------
  5     Some records were not processed during the current operation.  Either
  bulkfile records were skipped or attempts to overwrite existing records were
  ignored.
 
  This message means that one or both of the variables specified for skipped
  or existed on the ARES_INIT call have values other than zero.
------------------------------------------------------------------------------
  6     A rollback has been performed.
 
  This error indicates that the latest updates to the model have been rolled
  back.  This may be due to either an explicit call to ARES_ROLLBACK, or to an
  automatic rollback due to a deadlock condition.
------------------------------------------------------------------------------
  7     You attempted to issue a DML command-name outside of a transaction and
  have previously specified to not allow them.
 
  This error indicates that you have called ARES_SET_BEGIN with the REQUIRED
  option and have subsequently called ARES_START when a transaction is not
  active.
------------------------------------------------------------------------------
  8     Nothing to {COMMIT|ABORT|ROLLBACK|CHECKPOINT}.
 
  This error means that you called ARES_COMMIT, ARES_ABORT, ARES_ROLLBACK,
  ARES_CHECKPOINT when no transaction was active.
------------------------------------------------------------------------------
  9     The data to be returned in the api-rec parameter on the call to
  command-name exceeds the length of the buffer passed.  The first word of
  your buffer now contains the actual size needed.
 
  This error indicates that a larger buffer needs to be allocated to contain
  the data record being returned in the api-rec parameter during a call to
  ARES_FETCHER or ARES_PUTFIELD. The operation was not done.
------------------------------------------------------------------------------
  10    The field descriptions to be returned in the api-rec-desc parameter on
  the call to command-name exceed the length of the buffer passed.  The first
  word of your buffer now contains the actual size needed.
 
  This error indicates that a larger buffer needs to be allocated to contain
  the data record description being returned in the api-rec-desc parameter
  during a call to ARES_FETCHER or ARES_GETDESC. The operation was not done.
------------------------------------------------------------------------------
  11    The result list to be returned in the result-buf parameter on the call
  to NAMELIST exceeds the length of the buffer passed.  The first word of your
  buffer now contains the actual size needed.
 
  This error indicates that a larger buffer needs to be allocated to contain
  the list of database names being returned to the result-buf parameter during
  a call to ARES_NAMELIST. The list of names was not returned.
API_ERROR_CODES
The original ARES Application Program Interface (API) was designed and
implemented to be a tool for programmers who wished to implement ARES database
applications using SQL-compliant queries with known result lists.  Another
class of users exists who wish to build programs which dynamically develop
queries (which are also SQL-compliant) and manipulate their results.  The
extension routines described in this section are a supplement to the original
API capabilities rather than a replacement.  A system programmer may use the
original API calls as well as the extended API calls to build an application.
 
A number of additional capabilities are required in order to allow this type
of ARES use from a programming language.  Textual information about the
database description must be available in order for the user to dynamically
build queries which use table, column, function, or stored DML names.  A
description of the physical layout of the columns in a record is necessary for
the user program to communicate with ARES when fetching a record, manipulating
the record contents, or updating a record.  Since dynamically-built queries
are unknown to the programmer, the number of results returned by such a query
is also unknown.  This means that the results must be returned to the program
in record format rather than returned on a one-parameter/one-result basis, as
is the case for the original API routines.  Due to this fact, routines to
handle record results are necessary for fetching and updating records.
Several routines are also needed to manipulate data in specified fields of a
fetched record in preparation for updating the record in the database.
Several routines are available for the purpose of fetching, manipulating, and
updating record results.  This section describes the general use of these
routines as well as the details of each one.
 
The user may wish to fetch a record from the database by using a call to
ARES_FETCHR. ARES will return the record to the user in the api-rec parameter.
Since the physical description of the fields in api-rec is contained in the
api-rec-desc parameter, manipulation of the individual fields in api-rec is
possible.  Three ARES routines are provided for this field manipulation.  The
offset to a specified field as well as the length of the field is found and
returned to the user by calling ARES_FINDFIELD. The contents of a specified
field may be extracted from api-rec and placed in a user variable by calling
ARES_GETFIELD. The contents of a user variable may be put into a specified
field of api-rec by calling ARES_PUTFIELD. The user could use these routines
to find, get, and change the data in api-rec in preparation for a call to
ARES_UPDATER which will update the record in the database.
 
The ARES_FETCHR call returns the next result from a query to the user in
record form.  The user is responsible for allocating memory into which ARES
returns the fetched API record.  The user may estimate the amount of memory
required or may call ARES_GETSIZE (described in the previous subsection) which
returns the minimum and optionally the maximum size a record for this query
may be.  If not enough memory is allocated, ARES_FETCHR sets a special error
code (see API_ERROR_CODES) and returns the required size in the first word of
the api-rec parameter.  The api-rec-desc parameter is optional for the
ARES_FETCHR call.  If specified, ARES returns the API record description
associated with the query-number to the user program.  If an error occurs
during the ARES_FETCHR call, such as an insufficient size for one of the
parameters, no record will actually be fetched.  The insufficient size may be
adjusted by the user who then re-calls ARES_FETCHR which attempts to return
the current record again.  The user is allowed to intermix record fetches
(ARES_FETCHR) with field fetches (ARES_FETCH) if so desired.
 
The ARES_FINDFIELD call returns to the user the offset to a specified field in
api-rec as well as the length of the field.  The specified field number must
be within the legal range for the number of fields described in api-rec-desc.
If the field type is CHARACTER VARYING, the offset returned is to the
beginning of the text string portion of the TEXTC or TEXTH structure.  In all
other cases, the offset is to the beginning of the field.  The length of a
CHARACTER field is in bytes, while bits are used for INTEGER fields, and so on
(see the Rules under ARES_FINDFIELD_CALL for more details).
The ARES_GETFIELD call returns to the user the contents of a specified field
in api-rec.  The data returned is placed in a user-program variable.  If the
data type of the field retrieved from api-rec does not match the data type of
the user variable into which the data will be placed, the user must either
convert the data or use ARES_PUTDESC to change api-rec-desc so the data
returned in api-rec will be of the desired data type.
 
The ARES_PUTFIELD call returns to the user the api-rec which contains the new
data from a user-program variable which was put in a specified field.  The
comments about data type conversion and legal field numbers discussed above
for ARES_GETFIELD also hold true for ARES_PUTFIELD. The only variation is that
the user program variable in ARES_PUTFIELD is the source of the data, and in
ARES_GETFIELD it is the data destination.
 
A call to ARES_UPDATER allows the user program to make updates to a record
fetched by an ARES_FETCHR call.  The entire record, with the desired updates,
is passed as a parameter on the ARES_UPDATER call.  In order for ARES to know
which fields to update, a buffer containing a list of the numbers
corresponding to these fields may also be passed as a parameter.  If no update
list is passed all fields in the record will be updated, with the exception of
primary key fields and other protected fields.
FORTRAN users need only code the call to the interface routine as they would
any other call.
 
     CALL ARES_RELEASE(Q)
 1. A maximum of 100 queries may be active at one time in a single program.
 2. The maximum number of items allowed in a result-item-list or argument-list
    is 39.  This maximum may be less if the language being used has
    restrictions on the number of arguments which may be specified on a CALL
    statement.
When linking an API program, a diagnostic for two or three unsatisfied
secondary references will occur.  This is to be expected.  An unresolved
secondary entry reference is reported if the optional routine ARES_ERROR is
not supplied.  Two additional unresolved secondary references will always be
reported:  one for ZJE$ASLENTRY and one for ZJ_STATUS. None of these above
unresolved secondary references are to be considered error conditions.  The
run unit will still be created with a severity level of zero.
 
If ARES_ASL.:SYS is specified as an object unit, a warning diagnostic is
issued indicating that ARES_ASL.:SYS is in fact a run unit file and only
 
definitions will be used from it.  This is a diagnostic message, not an error
condition.
Users of the Application Program Interface must specify the following LINK
options:
 
    DCBSLOTS=100, UNSAT (:LIB_ARES.:SYS, :LIB_SYSTEM.:SYS),
    ALTSHARELIB=ARES_ASL.
 
The above options cause the ARES Alternate Shared Library (ARES_ASL) to always
be associated with the run unit.  There are cases in which this is not
desirable; having ARES_ASL associated reduces the amount of memory available
to the user for other tasks (the memory is charged against the user's resource
unit).  Thus, if the task being performed has a high memory requirement, it
may be desirable to put off associating ARES_ASL until the memory can be
freed.
 
In order to accomplish this, do not specify ALTSHARELIB=ARES_ASL, but instead
include ARES_ASL.:SYS when linking the program as if it was an object unit.
This satisfies the external references without causing automatic association
of ARES_ASL. When the ARES_INIT call is actually issued, the association is
performed.
Depending on the programmer's use, the database description can be returned to
the user program in a couple of ways.  If the programmer only wants to display
the information, the text result is returned in a file which the user program
can then read and write to the user.  On the other hand, if the programmer
intends to use various pieces of the text (i.e., individual table or column
names) in the program, the result is returned directly in memory.
 
Almost all of the ARES LIST and DISPLAY commands are allowed from the
application program if the result is to be returned in a file.  The actual
text of either a LIST or DISPLAY command is passed to ARES by using the
ARES_DISPLAY command.  Displays of STATS, PRIVS, JOURNALS, TABLES, COLUMNS,
BULKFILES, FUNCTIONS, DML, and MODEL are allowed as well as lists of TABLES,
BULKFILES, COLUMNS, FUNCTIONS, DML, DML OWNER, and PRIVS. The text returned is
the exact output produced when these commands are issued in interactive ARES.
ARES_NAMELIST is used when the programmer wishes to have the result returned
in memory.  The list-type parameter it used to indicate the type of list
desired.  Legal list commands are TABLES, BULKFILES, COLUMNS, FUNCTIONS, and
DML as well as the columns in a table or bulkfile.  The programmer is
responsible for allocating the memory into which ARES returns the result.  If
not enough memory is allocated in the program to accommodate the result, a
special error code is set (see API_REC_DESC_RULES). The required size of the
result is then returned to the program in the first word of the result-buf
parameter.  If no error occurs, the result list is returned in result-buf with
the list names separated by commas.
One (1) data segment is allocated by the interface and will be held until an
ARES_END call is issued.
From PL-6, each routine should be DCL'd as an entry point with the appropriate
number of parameters.  CONV(0) should be specified on the calls so that the
data type descriptors are passed to the application program interface; ALTRET
should not be specified.
 
     DCL ARES_RELEASE ENTRY(1) CONV(0);
 
For the routines that can have a variable number of parameters (such as
ARES_EXEC), the maximum number of parameters that will be used should be
specified on the DCL statement.
The actual call to the routine should be coded as a standard PL-6 call:
 
     CALL ARES_RELEASE(QUERY_NUMBER);
The variable api-rec-desc refers to a word-oriented structure.  The first word
reflects the number of entries in the structure, followed by a three word,
data type entry for each field in the API record.  Both decimal and non-
decimal data types may be specified.  Conventions for specifying decimal and
non-decimal data are as follows:
 
o   Decimal data types require specification of data type, length, and scale.
    Type is defined as an unsigned integer while length and scale are signed
    integers.
 
   -   Decimal data types are as follows:  PDLA, PDTA, PDLE, PDTE, PDNS,
       PDFLT, UDNS, UDLO, UDTO, UDLS, UDTS, UDFLT, DATE, and TIME.
   -   Lengths are in nibbles for packed decimal and in bytes for unpacked
       decimal.  A negative number indicates a protected field (see
       ARES_UPDATER_CALL, Rule 9) and the absolute value is the actual length
       of the field.
   -   The scale factor indicates the position of the decimal point for scaled
       decimal numbers.  A value of zero places the decimal point to the right
       of the least significant digit.  Positive values move the decimal point
       to the left, while negative values move it to the right.
o   Non-decimal data types require specification of data type and length.
    Type is defined as an unsigned integer, while length is a signed integer.
    Note that an extra word follows the two words used for non-decimal data
    types in order to use the same amount of space (three words) as a decimal
    data type uses.  This way the user can easily access various entries in
    the api-rec-desc without spacing through all preceding entries.
 
   -   Non-decimal data types include the following:   CHAR, TEXTC, TEXTH,
       SBIN, UBIN, UTS, SFLT, and DFLT.
   -   Lengths are in bits for SBIN, UBIN, and UTS data types.  Lengths are in
       bytes for CHAR, TEXTC, TEXTH, SFLT, and DFLT data types.  Lengths for
       TEXTC and TEXTH data types are not known until a record is actually
       read or written and are therefore ignored at initialization.  A
       negative number indicates a protected field (see ARES_UPDATER_CALL,
       Rule 9) and the absolute value is the actual length of the field.
    Legal data types and their requirements are described in the following
    table.  Note that lengths which do not specify ranges are not variable and
    the numbers shown in the table are returned to the user by a call to
    ARES_GETDESC or ARES_FETCHR. These same fields are also changed to these
    values during a call to the ARES_PUTDESC, if any other values are
    specified.  Also note that the scale factors which do not specify ranges
    are returned as zero values to the user by a call to ARES_GETDESC or
    ARES_FETCHR and are unchanged by a call to ARES_PUTDESC.
 
            ----------------------------------------------------------
 
              Data
              TypeMnemonic UnitsLength Scale  Description
            ----------------------------------------------------------
            ----------------------------------------------------------
              0            -    -      -      Type not specified
            ----------------------------------------------------------
              Non-Decimal Data Types
            ----------------------------------------------------------
              1   SBIN     bits 1 - 36 N/A    Binary fixed point
                                              single
                                              (INTEGER,COMP-6)
              3   SFLT     bytes4      N/A    Binary (hex exp) float
                                              single (REAL, COMP-11)
 
              4   DFLT     bytes8      N/A    Binary (hex exp) float
                                              double (DOUBLE
                                              PRECISION, COMP-12)
 
              21  CHAR     bytes1 -
                                4095   N/A    Character string
                                              (CHARACTER, DISPLAY)
              22  TEXTC    bytes1 - 511N/A    Varying character
                                              string, 9-bit size
 
              24  UBIN     bits 1 - 36 N/A    Unsigned binary fixed
                                              point single
 
              55  UTS      bits 36     N/A    Universal time stamp,
                                              UBIN value
 
              56  TEXTH    bytes512 -
                                262143 N/A    Varying character
                                              string, 18-bit size
            ----------------------------------------------------------
            ----------------------------------------------------------
              Decimal Data Types
            ----------------------------------------------------------
              9   PDLA     nibbles
                                2-63   -32 -
                                       +31    Packed decimal fixed,
                                              lead ASCII sign
                                              (COMP-4)
              10  PDFLT    nibbles
                                4 - 63 N/A    Packed decimal float
              25  PDTA     nibbles
                                2 - 63 -32 -
                                       +31    Packed decimal fixed,
                                              trail ASCII sign
                                              (COMP, COMP-4)
              40  PDNS     nibbles
                                1 - 63 -32 -
                                       +31    Packed decimal fixed,
                                              no sign (COMP, COMP-3,
                                              COMP-4)
              41  UDNS     bytes1 - 63 -32 -
                                       +31    Unpacked decimal
                                              fixed, no sign
              42  UDLS     bytes2 - 63 -32 -
                                       +31    Unpacked decimal
                                              fixed, lead sign
              43  UDTS     bytes2 - 63 -32 -
                                       +31    Unpacked decimal
                                              fixed, trail sign
              44  UDLO     bytes1 - 63 -32 -
                                       +31    Unpacked decimal
                                              fixed, lead
                                              overpunched sign
            ----------------------------------------------------------
              45  UDTO     bytes1 - 63 -32 -
                                       +31    Unpacked decimal
                                              fixed, trail
                                              overpunched sign
            ----------------------------------------------------------
              50  UDFLT    bytes3 - 63 N/A    Unpacked decimal float
            ----------------------------------------------------------
              54  DATE     nibbles
                                15     0      Date, packed decimal
                                              fixed lead ASCII sign
                                              value
            ----------------------------------------------------------
              57  TIME     nibbles
                                15     0      Time in 1/100 seconds,
                                              packed decimal fixed
                                              lead ASCII sign value
The ARES database manager itself is an Alternate Shared Library (ASL). This
provides security for the database by protecting the database manager from
user program errors and unauthorized access.  It also makes the amount of code
which actually exists in the interface routines quite small, cutting down link
time and user memory requirements.
 
Two mechanisms are provided for execution of DML commands.  First, a command
which has previously been stored in the ARES database may be started in a way
similar to the way it would be started from the interactive ARES. This allows
canned commands to be stored in the database and maintained there by ARES,
then executed by either a program or an interactive user.  Second, a command
may be submitted to the interface in text form.  This allows the user to build
or input parts of the command, then execute it.  The text is parsed by the
interface and the resulting command is passed on to the database manager.
Two modes are available for the execution of ARES DML commands:  immediate
mode and query mode.  All ARES DML commands (SELECT, UPDATE, INSERT, DELETE,
LOAD, and DUMP) may be executed in immediate mode.  In immediate mode a
command is completely executed, whether it affects one record or many, before
control is returned to the program.
 
SELECT commands may also be executed in query mode.  In query mode, the
command is prepared for execution so that one result may be returned to the
program at a time.  The result is a collection of zero or more rows, each of
which is a set of elements, corresponding one for one, with the list of
elements in the SELECT list.  One call is required to the interface to return
each result row to the user's program.  In addition, the user is allowed to
update elements in that result and return it to the interface, which causes
the actual row in the database to be updated.
 
It is often necessary to execute immediate mode DML commands in conjunction
with query mode commands.  One such case where this is useful is when an
application program needs to update fields which are part of a primary key.
ARES does not allow direct updating of primary key fields.  Therefore, it is
necessary to delete the old record and reinsert the updated data via a new
record.  It is possible to delete records through the query mode ARES_DELETE
command but the table cannot be reopened for update to do the necessary insert
using immediate mode commands while the table is being updated by the query.
 
When a table is open for an update mode query, only changes that are under the
control of the query are allowed (that is, via ARES_UPDATE and ARES_DELETE
calls).  To insert a new record, it is necessary to issue an immediate command
(via ARES_EXEC or ARES_EXECTEXT) that is not part of the query.  As the
example below shows, this can be done, but only in an input mode query.  That
way, the only updaters are the immediate commands, so the user does not run
into the problem of trying to update a table that is already being updated.
In an input mode query, calls to ARES_UPDATE and ARES_DELETE are not allowed,
but these are easily replaced with equivalent calls to ARES_EXEC or
ARES_EXECTEXT.
 
The following example shows how to update fields which are part of a primary
key by using query mode commands to fetch the records and then immediate
commands to delete the old record and insert the new record.
 
    CALL ARES_BEGIN ('MODE=UPDATE, SHARE=NONE, TABLE')
    CALL ARES_STARTEXT ('SELECT FLD1,FLD2,FLD3 FROM TABLE', Q, 'INPUT')
LOOP:
        CALL ARES_FETCH (Q, F1, F2, F3)
        IF END-OF-FILE THEN GOTO END_LOOP
        CALL ARES_EXECTEXT ('DELETE TABLE WHERE FLD1=#1',F1)
                       .
                       .
                       .
           Make updates to F1, F2, F3, if desired.
                       .
                       .
                       .
        CALL ARES_EXECTEXT ('INSERT INTO TABLE VALUES(#1,#2,#3)',F1,F2,F3)
        GOTO LOOP
END_LOOP:
    CALL ARES_RELEASE (Q)
    CALL ARES_COMMIT
API
API_ARES_ABORT
API_ARES_BEGIN
API_ARES_CHECKPOINT
COMMANDS
API_ARES_COMMIT
API_ARES_DELETE
API_ARES_DESCRIBE
API_ARES_DISPLAY
API_ARES_END
API_ARES_ERRMSG
API_ARES_ERROR
API_ARES_EXEC
API_ARES_EXEC
API_ARES_FETCHR
API_ARES_FETCH
API_ARES_FINDFIELD
API_ARES_GETDESC
API_ARES_GETFIELD
API_ARES_GETSIZE
API_ARES_INIT
API_ARES_INVOKE
API_ARES_KEEP
API_ARES_NAMELIST
API_ARES_PUTDESC
API_ARES_PUTFIELD
API_ARES_RELEASE
API_ARES_REPORT
API_ARES_ROLLBACK
API_ARES_SETNIL
API_ARES_SET_BEGIN
API_ARES_SET_DATE
API_ARES_SET_OVERWRITE
API_ARES_SET_TIME
API_ARES_START
API_ARES_START
API_ARES_UPDATER
API_ARES_UPDATE
API_ARES_REPORT
SET_AUTOPRINT
ROLL_BACK
When it is time to make a new backup copy of the database, the general
procedures below should be followed:
 
o   To insure that the database is not being updated while the operation is
    taking place, issue a LOCK command in ARES.
o   Wait until all current users of the database are finished.
o   Back up the physical database.
o   Start a new common journal.
o   Use the UNLOCK command to allow users to access the database.
 
Note that the LOCK command does not prevent users with CREATOR privileges from
accessing the database.
 
There are a number of ways to back up a database.  The DUMP command in ARES
can be used to make backup copies of the data in tables.  PCL or EFT can be
used to back up physical files used to represent tables (see
MODEL_STORAGE_ALLOCATION, TEMPORARY_STORAGE_ALLOCATION, and ACCESS_CONTROLS
for a discussion of table to file-name mapping).  for a discussion of table to
file-name mapping).  When using PCL or EFT, only back up and restore files
used to represent tables; restoring other files could result in the loss of
changes to the model.  If a table in a model using common journaling is
altered, ARES ignores after images recorded for that table before the time the
alter occurred.  Thus, when the user alters a table, a new backup copy of the
table should be made.
 
To start a new copy of the common journal, use the RENAME command in JAYS (see
the CP-6 System Support Reference (A-P) (HA20)).  The RENAME command renames
the common journal, and replaces the original name with an empty file.  The
renamed common journal can then be saved or deleted, according to the needs of
the database owner.
 
Never delete the journal file.  In case this does happen, ARES attempts to
recreate the journal when the next user tries to write to it.  It is possible
that the next user does not normally have write access to the account in which
the journal is kept.  If so, an error is issued stating that the journal file
cannot be created.  The model creator should then use the ALTER JOURNAL
command to restore a physical journal file.  When ARES creates the journal
file, it places access controls on it that allow ARES to write records to the
common journal on behalf of all ARES users.
Syntax:
      [ currencies-option                           ]
      [ mode-option                                 ]
BEGIN [ share-option                                ] [,...]
      [ table-name [ ( { mode-option  } [,...] ) ]  ]
      [            [   { share-option }          ]  ]
CURRENCIES_OPTION:
CURRENCIES[[=]{ON|OFF}]
MODE_OPTION:
MODE [=] {INPUT|LOAD|UPDATE}
SHARE_OPTION:
SHARE [=] {ALL|ANY|INPUT|NONE}
Parameters:
 
table-name  an ARES identifier specifying a table name.
Description:
The BEGIN command is used to define the beginning of a transaction.
Transactions are terminated by using the ABORT and COMMIT commands, and are
affected by CHECKPOINT and ROLL BACK commands.  The BEGIN command allows
specification of certain parameters that control the tables being accessed,
the type of access to those tables, and the willingness of the user to share
the tables with other simultaneous users during the transaction.  These in
turn determine the activation of the transient journal, and the need to issue
record locks for concurrent access control.
 
Two users can share a table if each user's MODE for the table is compatible
with the other user's SHARE for the same table.  Thus, a user who specifies a
SHARE of IN may share a table with another user who specifies a MODE of IN,
but may not share a table with another user who specifies a MODE of UPDATE. A
special SHARE mode called ANY allows more efficient access to shared tables by
eliminating the need to issue record locks.  Another special option called
CURRENCIES allows the user to reduce the number of outstanding record locks at
any given time.
 
To guarantee sharing of tables between users, special locks are issued on each
of the tables.  These table locks remain in effect for the length of the
transaction.
Rules:
 
 1. If at least one table-name clause is specified, only those tables listed
    are affected by the BEGIN command.  If no table-name clause is specified,
    all tables in the model that the user has privilege to access are affected
    by the BEGIN command.
 2. If a mode-option or share-option clause is specified outside of the table-
    name clause, they are treated as default specifications for any tables
    specified in the BEGIN command that do not explicitly state a mode-option
    or share-option.
 3. If a table-name clause is specified with a mode-option or share-option
    clause, the specified options apply only to that table.  If a table-name
    clause is specified without either a mode-option or share-option clause,
    the appropriate default specifications are used.
 4. Within the transaction, permanent tables can only be used if they are
    covered by the BEGIN command and if the type of access is compatible with
    the mode applicable to that table.  Temporary tables can be accessed and
    updated within a transaction whether or not they are covered in the BEGIN
    command and regardless of the mode-option specified.
 
 5. If MODE=IN[PUT] is specified for a permanent table, DML commands that
    reference the table are only allowed to retrieve information from it.  No
    updating of data in the permanent table is allowed.  MODE=IN does not
    restrict the access to a temporary table.  DML commands can both retrieve
    and update information in the table.
    Note:   While most command and options may only be abbreviated to three
    (3) characters, INPUT may be abbreviated to only two (2) characters, i.e.,
    IN.
 6. If MODE=UPDATE is specified for either a permanent or temporary table, DML
    commands that reference the table can both retrieve and update information
    in the table.
 7. If MODE=LOAD is specified for either a permanent or temporary table, DML
    commands that reference the table can both retrieve and update information
    in the table.  MODE=LOAD rebuilds secondary keys when the table is closed,
    instead of updating them each time a record is inserted.  This mode is
    used for efficiently loading large amounts of data into permanent or
    temporary tables.  (See MODE Option in Section 6 for further details.)
 8. For each table, if MODE is IN, the default for SHARE is IN. If MODE is
    UPDATE, the default for SHARE is NONE. If MODE is LOAD, SHARE is forced to
    NONE.
 9. If SHARE=ALL is specified for a permanent table, the table can be shared
    with users who specify MODE=IN or MODE=UPDATE for the same table.
    Specifying SHARE=ALL for a permanent table causes record locks to be
    issued while accessing the records in the table.
10. If SHARE=ANY is specified for a permanent table, the action taken is
    dependent on the mode.  If MODE=IN the table can be shared with users who
    specify MODE=IN or MODE=UPDATE for the same table.  If MODE=UPDATE the
    table can only be shared with users who specify MODE=IN and SHARE=ANY for
    the same table.  Thus, MODE=UPDATE, SHARE=ANY guarantees that only one
    user can be updating the table.  Specifying SHARE=ANY for a permanent
    table prevents record locks from being issued while accessing the records
    in the table.
11. If SHARE=IN is specified for a permanent table, the table can only be
    shared with users who specify MODE=IN for the table.
12. If SHARE=NONE is specified for a permanent table, the table cannot be
    shared with any other user.
13. Temporary tables are never shared since they are guaranteed to be unique
    for each user.
14. CURRENCIES=ON can only be specified for tables on which record locks are
    being issued.  If specified, records that have not been updated are
    unlocked as soon as they are no longer the current record.  This results
    in a much smaller set of active record locks at any given time.
15. If CURRENCIES=OFF is specified, records remain locked whether they are the
    current record or not.
16. For each table, if MODE=IN and SHARE=ALL or MODE=UPDATE and SHARE=IN or
    MODE=UPDATE and SHARE=ALL, the default for CURRENCIES is ON. In all other
    cases, the currencies-option may not be specified.
17. If one table has a MODE of LOAD, no other table can have a MODE of UPDATE
    or a SHARE of ALL.
18. The transient journal is activated if at least one table whose MODE is
    UPDATE has a SHARE of IN or ALL, or if at least one table has a MODE of
    UPDATE and a CREATE JOURNAL TRANSIENT command has been issued against the
    model.  Updates to a temporary table are not reflected in the transient
    journal unless it was specifically mentioned in the BEGIN command and has
    a MODE of UPDATE.
19. Record locks are issued against a table if its MODE is IN and its SHARE is
    ALL, or if its MODE is UPDATE and its SHARE is either IN or ALL. Record
    locks are never issued against tables whose SHARE is ANY or NONE.
20. The options specified on a BEGIN command and the table locks issued to
    guarantee the proper table sharing stay in effect until a COMMIT or ABORT
    command is issued.
21. The command waits until all table locks have been issued.
22. DDL commands cannot be issued within a transaction started by a BEGIN
    command.
See also:
ABORT, CHECKPOINT, COMMIT, ROLL_BACK
00001
00005
00002
00004
00006
00007
00003
BEGIN
API_BREAK_CONTROL
Following are the ARES built-in functions:
ABS_FUNCTION
AVG_FUNCTION
COUNT_FUNCTION
MAX_FUNCTION
MIN_FUNCTION
SQRT_FUNCTION
STDEV_FUNCTION
SUM_FUNCTION
UAVG_FUNCTION
 
For more information about built-in functions see:
!HELP BUILTIN_FUNCTIONS function-name
ABS_FUNCTION      CREATE FUNCTION ABS( P ) ;
BEGIN ;
    IF P < 0 ;
    THEN ;
        ABS := - P;
    ELSE ;
        ABS := P;
    END
AVG_FUNCTION      CREATE FUNCTION AVG(PARAM) : DEC(60) FLOAT ;
DEF ;
    SUM DEC(60) FLOAT, ;
    COUNT DOUBLE PRECISION, ;
    C INTEGER ;
INIT ;
    SUM := 0, ;
    COUNT := 0 ;
FOR EACH ROW ;
    BEGIN ;
        SUM := SUM + PARAM, ;
        COUNT := COUNT + 1 ;
        END ;
BEGIN ;
    C := COUNT, ;
    AVG := SUM / C ;
    END
COUNT_FUNCTION      CREATE FUNCTION COUNT(PARAM) : INTEGER;
DEF ;
    COUNTER DOUBLE PRECISION ;
INIT ;
    COUNTER := 0 ;
FOR EACH ROW ;
    COUNTER := COUNTER + 1 ;
BEGIN ;
    COUNT := COUNTER ;
    END
MAX_FUNCTION      CREATE FUNCTION MAX(PARAM) ;
FOR EACH ROW ;
    IF MAX IS NULL ;
    THEN ;
        MAX := PARAM ;
    ELSE ;
        IF PARAM > MAX ;
        THEN ;
            MAX := PARAM
MIN_FUNCTION      CREATE FUNCTION MIN(PARAM) ;
FOR EACH ROW ;
    IF MIN IS NULL ;
    THEN ;
        MIN := PARAM ;
    ELSE ;
        IF PARAM < MIN ;
        THEN ;
            MIN := PARAM
SQRT_FUNCTION      CREATE FUNCTION SQRT(PARAM) : DECIMAL(60) FLOAT;
DEF ;
    X1 DECIMAL(60) FLOAT, ;
    ACC DECIMAL(60) FLOAT ;
BEGIN;
    IF PARAM <= 0 ;
    THEN ;
        SQRT := 0 ;
    ELSE BEGIN ;
        X1 := 1.0,;
        ACC := PARAM / 4 ,;
        WHILE ( ACC > 1E-12 ) DO BEGIN;
            X1 := ( PARAM / X1 + X1 ) / 2.0,;
            ACC := ( PARAM / X1 ) - X1,;
            IF ACC < 0 ;
            THEN ;
                ACC := - ACC;
            END,;
        SQRT := X1;
        END;
    END
STDEV_FUNCTION      CREATE FUNCTION STDEV(PARAM) : DECIMAL(60) FLOAT;
DEF X DECIMAL(60) FLOAT,;
    XS DECIMAL(60) FLOAT,;
    S DECIMAL(60) FLOAT,;
    ACC DECIMAL(60) FLOAT,;
    STEMP DECIMAL(60) FLOAT,;
    K DECIMAL(60) UNS;
INIT ;
    K := 0, ;
    X := 0, ;
    XS := 0;
FOR EACH ROW;
    BEGIN;
        K := K + 1, ;
        X := X + STEMP, ;
        XS := XS + STEMPM * STEMP;
        END;
 
BEGIN;
    IF K < 2 ;
    THEN;
        STDEV := 0;
    ELSE BEGIN;
        STEMP := ( XS - ( ( X * X ) / K ) ) / ( K - 1 ),;
        IF STEMP = 0;
        THEN;
            STDEV := 0;
        ELSE BEGIN;
            ACC := 1.0, ;
            S := STEMP / 4,;
            WHILE ( ACC > 1E-12 ) DO BEGIN;
                S := ( STEMP / S + S ) / 2.0,;
                ACC := ( STEMP / S ) - S,;
                IF ACC < 0 ;
                THEN ;
                    ACC := - ACC;
                END,;
            STDEV := S;
            END;
        END;
    END
SUM_FUNCTION      CREATE FUNCTION SUM(PARAM) ;
INIT ;
    SUM := 0 ;
FOR EACH ROW ;
    SUM := SUM + PARAM
UAVG_FUNCTION      CREATE FUNCTION UAVG(PARAM);
DEF ;
    SUM DEC(60) FLOAT, ;
    COUNT DOUBLE PRECISION, ;
    C INTEGER ;
INIT ;
    SUM := 0, ;
    COUNT := 0 ;
 
FOR EACH ROW ;
    BEGIN ;
        SUM := SUM + PARAM, ;
        COUNT := COUNT + 1 ;
        END ;
BEGIN ;
    C := COUNT, ;
    UAVG := SUM / C ;
    END
00001
00002
00003
00004
00005
00006
00007
00008
00009
Bulkfiles may be used to import external data into an ARES database.  The
CREATE BULKFILE command is used to describe an external file in much the same
way as a table is specified.  The primary difference is that a bulkfile has no
key fields.  The description itself is not tied to a specific file, but
describes an independent record format.
 
The LOAD command is then used to import the data.  With this command, a table
is matched to a file identifier and a bulkfile description (which describes
the records in the file).  The columns in the bulkfile description are matched
up positionally with the columns in the table.  The data types of matched
columns need not be the same; ARES converts them as long as the values are
legal.
 
The example below shows the creation of a model and the subsequent invoking
and loading of a bulkfile.
 
 : CREATE MODEL BUSINESS
 : CREATE TABLE EMP;
 +        (NAME CHAR(20),EMP_NO INTEGER,SALARY DECIMAL(8,2),;
 +         MAN_NO INTEGER,DEPT_NAME CHAR(10),GROUP_SIZE INTEGER);
 +     KEY IS PRIMARY(EMP_KEY=EMP_NO)
 
 : CREATE BULKFILE B_EMP;
 +        (NAME CHAR(20),EMP_NO DECIMAL(4),SALARY DECIMAL(10,2),;
 +         MAN_NUMBER DECIMAL(4),DEPARTMENT CHAR(10),GROUP_SIZE INTEGER)
   4 slack bits inserted before column DEPARTMENT.
 
 : COMMIT
   The model BUSINESS has been created.
 : INVOKE BUSINESS
 : LOAD EMP FROM BULKFILE1 USING B_EMP
   .. 3 records LOADed.
 : LOAD EMP FROM BULKFILE2 USING B_EMP(NAME,EMP_NO,SALARY,MAN_NUMBER,;
 +     DEPARTMENT,GROUP_SIZE)
   .. 7 records LOADed.
 
 !C BULKFILE1 TO ME(O)
 
      1 - 45 BYTES
 000000  123115.111124 110040.040040 SMITH
 000002  040040.040040 040040.040040
 000004  040040.040040 307066.234000     .6..
 000006  002127.044026 307145.100123 .W$..e@S
 000010  110117.105040 040040.040040 HOE
 000012  040000.000000 000            ....
 
      2 - 45 BYTES
 000000  101114.114105 116040.040040 ALLEN
 000002  040040.040040 040040.040040
 000004  040040.040040 307111.234000     .I..
 000006  005124.100000 307204.100124 .T@...@T
 000010  117131.040040 040040.040040 OY
 000012  040000.000000 000            ....
 
      3 - 45 BYTES
 000000  127101.122104 040040.040040 WARD
 000002  040040.040040 040040.040040
 000004  040040.040040 307122.034000     .R..
 000006  001044.024140 307204.100124 .$.`..@T
 000010  117131.040040 040040.040040 OY
 000012  040000.000000 000            ....
 
Notice that in the second LOAD command, the columns are specifically listed in
the bulkfile description.  This has no affect in this example but demonstrates
the flexibility of the command.  The order of the columns may be changed or
columns omitted.  Thus, not all the columns specified in the bulkfile need to
be in the table being loaded.
For additional information regarding changes in ARES D01, type:
HELP (ARES) CHANGES TOPICS
COMPATIBILITY      Databases created by C01, C02 or D00 ARES are compatible
with D01 ARES. No conversion process is necessary.  However, journals created
with C02, D00 or D01 ARES are not backwards compatible with C01 ARES. Should
you have databases created by versions previous to B01 ARES that have not
already been converted, you will have to convert those databases using
previously released versions of ARES. See the B00 and B01 ARES SRBs for
information about converting databases to more current versions.
 
D01 ARES requires E03 or future versions of the CP-6 operating system.
 
D01 ARES is designed to go with B01 ADAPT but existing ADAPT scripts can be
used without recompilation.
CONVERSION_NOTES      The D01 version of ARES is compatible with the C02 and
D00 versions of ARES. It is recommended though that all ARES application
programs (those that specified UNSAT(:LIB_ARES.:SYS) as part of their LINK
command) be relinked.  This will guarantee that they have the most up-to-date
version of the interface code that handles the communication between the
application program and the ARES product.
 
In D01, there have been some internal code changes with regards to UTS
conversion.  Therefore, D01 ARES should be installed with CP-6 AR3 prior to
January 1, 1993; it should not be operated with any earlier version of CP-6
after that date.
NEW_FEATURES      The following subsections describe the new features of ARES.
GENERAL_FEATURES
 
o   ARES now honors user-specified XTNSIZes.  This greatly reduces the number
    of small extents used which can result in filling the FIT unnecessarily.
o   The PRINT NEXT command now reports an end-of-file message after the last
    record of the result has been displayed.  A subsequent PRINT NEXT will
    then start back at the beginning of the result file.
DDL_FEATURES
 
o   No new features.
DML_FEATURES
 
o   No new features.
LIST_DISPLAY_FEATURES
o   No new features.
FORMAT_FEATURES
 
o   No new features.
API_FEATURES
 
o   No new features.
00009
00001
00002
00005
00006
00008
00004
00001
00007
00003
A character string constant is represented by a string of from 1 to 255
characters enclosed in apostrophes.  Embedded blanks are significant, although
trailing blanks are not.  Within the constant, two apostrophes can be used to
represent a single apostrophe.
 
    'AB''CD'    is equivalent to AB'CD
Syntax:
CHARACTER (length) [VARYING]
Parameters:
 
length  positive integer 1 <= length <= 65533.
Description:
CHARACTER data type is used to describe text fields.  Any ASCII character is
legal in a CHAR field.
Rules:
 
 1. CHAR data is stored internally as 9-bit ASCII data, one character to a
    byte.
 2. If VARYING is not specified, length is limited to a maximum of 4095 and is
    the actual size of the data field.  If the text string in the field is
    shorter than length, it is padded to the right with blanks.
 3. If VARYING is specified, the data is stored as a length field followed by
    the text.  The size of the length field is determined by length as
    follows:
        One 9-bit byte if 1 <= length <= 511
        Two 9-bit bytes if 512 <= length <= 65533
 
    The actual storage required for the field is the actual length of the data
    plus the size of the length field; there are no trailing blanks in a
    CHARACTER VARYING field.
    Note:  If VARYING is specified in a bulkfile description, ARES expects the
    data to be in the described format with the appropriate size length field
    preceding the data.
 4. If VARYING is specified, the field may not be used as part of a key.
00002
00001
00003
Syntax:
CHECKPOINT
Description:
The CHECKPOINT command informs ARES that any updates issued within the
transaction should be made permanent (as if a COMMIT command had been issued),
but that the transaction should still remain active.  Table locks will not be
affected by this command.
Rules:
 
 1. The CHECKPOINT command can only be issued within a transaction that has
    activated either the transient journal, or concurrent access control.  See
    BEGIN Command for more details.
 2. When a CHECKPOINT command is issued, the following actions are taken:
   o   All record locks are released.
   o   The records in the transient journal are erased.
   o   If the common journal is active, a CHECKPOINT record is written.
 3. If an abort or rollback occurs after the CHECKPOINT command is issued, the
    database is returned to the state it was in at the time of the latest
    CHECKPOINT command.
See also:
ABORT, BEGIN, COMMIT, ROLL_BACK
00001
00002
00003
The checkpoint facility allows the user to make updates permanent, and release
unneeded record locks without terminating the transaction.  When a checkpoint
is issued, all record locks except those which represent the current position
of open queries are released.  This can improve the overall throughput on the
database by allowing other users to access the records.
 
Placement of checkpoints should be performed cautiously.  Once the lock on a
record is released, another user may update that record.  If that other user
updates the record so that it is placed ahead of the current position of the
original user, the record may then be accessed by the first user twice.  This
type of situation may occur when the second user is updating values which are
part of a key.
CHECKPOINT
API_COBOL
API_COBOL
LIST_COLUMNS
FORMAT_COLUMN_DATE
FORMAT_COLUMN_NAME
FORMAT_COLUMN_TIMESPAN
FORMAT_COLUMN_WIDTH
FORMAT_COLUMN_WRAP
For HELP on each command, type:
!HELP (ARES) command (from IBEX)
:HELP command (from ARES)
 
Special model commands:
LOCK, RECONSTRUCT, ROLL_FORWARD, UNLOCK
Model commands:
ALTER_MODEL, CREATE_MODEL, DROP_MODEL,
INVOKE_MODEL
Table commands:
ALTER_TABLE, ALTER_COLUMN, CREATE_TABLE,
DROP_TABLE, RENAME_COLUMN
Bulkfile commands:
ALTER_BULKFILE, CREATE_BULKFILE, DROP_BULKFILE
Function commands:
ALTER_FUNCTION, CREATE_FUNCTION, DROP_FUNCTION
DML commands:
DELETE, DUMP, INSERT, LOAD, UPDATE, SELECT
Journal commands:
ALTER_JOURNAL, CREATE_JOURNAL
Transaction commands:
ABORT, BEGIN, CHECKPOINT, COMMIT, ROLL_BACK
Stored DML commands:
RR, START, STORE
Display commands:
DISPLAY, LIST
IBEX commands:
DIRECTORY, DO, HELP
Report commands:
FORMAT, FORMAT_HEADINGS, OUTPUT, PRINT, REPORT
Privilege commands:
GRANT, REVOKE
Miscellaneous commands:
ABORT, COMMIT, END, ENTER, OPTIMIZE, READ, RR, SET
COMMANDS
IBEX command variables can be referenced in any ARES command.  This is
accomplished by preceding the command variable name with a percent sign (%).
The value of the command variable is then substituted into the ARES command
and the ARES command is processed.
 
If a command variable is preceded by a double percent sign (%%), then the
command passed to ARES for processing contains a single percent and the
command variable name.  In this case, no substitution is done.
 
For either single or double percent signs, if the variable name following them
does not represent a currently defined command variable, no action is taken.
Syntax:
COMMIT
Description:
The effect of a COMMIT command is dependent on the mode the user is in.  If it
is issued in create, alter or drop mode, its effect is to perform all
previously specified DDL commands.  All additions, modifications or deletions
of elements of the model will be performed at this time.
 
If issued within a transaction in invoke mode, it issues a CHECKPOINT and ends
the transaction.  The CHECKPOINT makes all updates specified by DML commands
since the last BEGIN or CHECKPOINT command (whichever is later) permanent.
Any options specified on the BEGIN command that started the transaction are
reset and will no longer be in effect after the COMMIT command is issued.
Rules:
 
 1. In invoke mode, the COMMIT command can only be issued if a transaction is
    active (as defined by a previously issued BEGIN command).  If no such
    transaction is active, an error is reported.
 2. In invoke mode, a COMMIT command causes the following actions to occur:
 
   o   A CHECKPOINT command is issued.
   o   All record locks are released.
   o   Records in the transient journal are erased.
   o   If the common journal is active, a CHECKPOINT record is written.
   o   Current transaction is terminated.
   o   All table locks are released.
See also:
ABORT, BEGIN, CHECKPOINT, ROLL_BACK
00001
00002
00003
COMMIT
The common journal protects the user against catastrophic failures that
destroy the physical medium upon which the database is stored.  The common
journal is created using the CREATE_JOURNAL command with the COMMON option.
The user specifies the file-identifier (fid) of the file to be used as the
common journal.  ARES creates the common journal so that it has access to the
journal for any user on the system.  Therefore, no special accounts are needed
to store common journals.  For maximum protection, the common journal should
be on a different physical device than the database.  If a head crash destroys
the database, and the common journal is on the same pack, chances are that it
will also be inaccessible.
 
As a database is updated, after images are written to the common journal.
These after images contain the necessary information to reproduce the update
(which can be an insert, update, or delete).  Upon successful completion of a
transaction or when a checkpoint is performed, a checkpoint record is written
to the common journal indicating that a logical group of updates is complete.
In the event that no transaction is active, the record is written after each
DML command is completed.  These records state that the previous set of after
images form a logical unit of work.  If a transaction ends unsuccessfully or a
rollback situation occurs (either by explicit call or due to a deadlock being
detected), a roll back record is written to the common journal to indicate
that the logical group of updates was rolled back.
When a rollforward operation is performed, the journal is scanned for
checkpoint and roll back records.  These indicate which records should be
reapplied to the backup copy of the database.  All users are rolled forward to
their last clean point (CHECKPOINT or COMMIT). Records in the common journal
identify the user that wrote them.  Thus, the concept of indivisibility of a
transaction is preserved.  Similarly, if a roll back record is found, the
updates logged since the last clean point are not applied.
 
If a database is ever destroyed or damaged, the user can perform a rollforward
operation which uses the common journal to bring a backup copy of the database
up-to-date.  If the common journal is very large, such rollforward operations
can be quite costly.  Making backup copies of the database more often reduces
the need for rollforwards.  Of course, if the database is large, backup
operations can become quite costly.  It is up to the user to determine the
balance between these operations.
CHANGES
Cooperative users can request to share tables while they are being updated.
An important factor in this type of shared access is that programs must be
guaranteed to work identically regardless of the fact that tables are shared.
If this is not the case, the concept of a transaction is violated.  It would
then be impossible to write application programs since another user could be
changing the value of the data while it is being used.  Although users are
sometimes willing to share tables with each other, they are not willing to
share specific records they have examined or changed.  Therefore, ARES locks
records within tables that are being shared as they are accessed and updated.
 
For additional information, see:
GRANT, SHARING_TABLES
CONCURRENT_ACCESS
ARES supports the following constant types:
 
   Numeric Constants
   Date Constants
   Timespan Constants
   Character Constants
 
For additional information see:
HELP name_CONSTANT
Syntax:
{logical-expression                                                  }
 
{algebraic-expression1  [IS] [NOT] IN  (select-expression1)          }
 
{algebraic-expression2 comparison-operator [ANY] (select-expression2)}
{                                          [ALL]                     }
 
         [logical-operator constraint-expression]
Parameters:
 
algebraic-expression1,2  as described under ALGEBRAIC_EXPRESSIONS.
 
comparison-operator  any of the following: >, >=, =>, <, <=, =<, =, ~=.
 
logical-expression  as described under LOGICAL_EXPRESSIONS.
 
logical-operator  either AND or OR.
 
select-expression1,2  as described under SELECT_COMMAND.
Description:
A constraint-expression restricts the operation of a command to affect only
certain records in a table or group of tables.  constraint-expressions can be
specified in the WHERE clause of the SELECT, DELETE, UPDATE, LOAD, and DUMP
commands.
 
The simplest form of the constraint-expression is the logical-expression.  In
this form, constants, column-ids, function-expressions, and algebraic-
expressions are combined to form logical-expressions that evaluate to true or
false.  The expression is evaluated for each combination of records being
processed.  If the expression is true for that combination of records, the
command is processed (the record is deleted, updated, or selected).  If the
expression is false, that combination of records is skipped.
 
The IN operator returns true if the algebraic-expression1 is equal to any of
the values returned by select-expression1.  select-expression1 must specify
exactly one algebraic-expression in its select-list (see the SELECT Command).
select-expressions used in this way are known as subqueries.
 
Subqueries can also be formed by comparing algebraic-expression2  with select-
expression2.  Again, the restriction that select-expression2  must specify
exactly one algebraic-expression in the select-list applies.  The result of
select-expression2  is compared to algebraic-expression2  (as described under
LOGICAL_EXPRESSIONS) to determine its truth value.  If more than one result is
generated, an error message informs the user that this is the case.
 
The modifiers ANY and ALL may be used with comparison-operators.  These
keywords allow select-expression2  to return more than one value and are
interpreted as follows:
 
        Modifier    Interpretation
       ----------------------------------------------------------------
        ALL         The comparison-operator must be true for all
 
                    the values returned from select-expression2.
 
        ANY         The comparison-operator need only be true for
 
                    one of the values returned from select-expression2.
 
In general, subqueries are only evaluated once.  The result of this evaluation
is then used as input for the rest of the query command.  The only exception
is when the constraint-expression of the subquery references a column-id that
belongs to a table outside the scope of the subquery (not specifically stated
in the FROM clause of this subquery).  In this case, the subquery is
reevaluated repeatedly to allow for the new value of that column-id.
 
Subqueries can be nested to any level.  Each level can use identifiers from a
higher level (previously defined) subquery, but not from a lower level.  For
additional information, see SUBQUERIES.
00002
00001
CHANGES
FORMAT_COUNT
The CREATE commands are used to create the elements of an ARES database.  Both
permanent and temporary elements can be created.
 
For additional information see:
HELP (ARES) TOPICS CREATE?
Syntax:
CREATE BULKFILE bulkfile-name [COMMENT = literal1]
 
    (column-specification [, column-specification . . .])
COLUMN_SPECIFICATION:
{column-name} [datatype] [COMMENT=literal2]
{     *     }
Parameters:
 
bulkfile-name  ARES identifier naming the bulkfile.
 
column-name  an ARES column name.
 
datatype  ARES representation of a data type.
 
literal1,2  text string enclosed in single quotes with a length of 1 to
    255.
Description:
The CREATE BULKFILE command is used to describe a non-ARES file to the ARES
processor.  It provides a means of importing or exporting data files to and
from an ARES database.
Rules:
 
 1. If * is specified, the column is a filler or placeholder.  It cannot be
    referenced later in any command nor can the content of this field be moved
    or altered by any command.  Multiple * columns may be specified in one
    bulkfile.
 2. The data type description is optional on each non-filler column.  If it is
    not specified, a column with the same name must exist in another bulkfile
    in the model.  ARES uses that description for the column.  If the data
    type is specified, it must be the same as the data type specified for any
    other bulkfile column with the same name.
 3. All occurrences of a bulkfile column in the database must have the same
    COMMENT field.
 4. If the CHARACTER VARYING format is used, the field must be preceded by a
    character count.  The character count itself must be 1 or 2 bytes in
    length depending on the maximum size specified for the column (1 byte for
    <=511, 2 bytes for >511).
 5. Bulkfiles created in invoke mode are temporary and last only until a new
    mode is entered.
 6. The maximum record length allowed by ARES in a bulkfile description is
    65535 bytes.
See also:
ALTER_BULKFILE, DISPLAY_BULKFILE, DROP_BULKFILE, DUMP, LIST_BULKFILE, LOAD
00001
00003
00002
00004
00005
CREATE_BULKFILE
Syntax:
CREATE FUNCTION function-name (parameter-list) [: datatype1]
 
    [COMMENT = literal]
 
    [DEFINE function-var1 datatype2 [, function-var2 datatype3 . . .]]
 
    [[INIT assignment-statement [, assignment-statement . . .]]
        [FOR] [EACH] ROW function-statement]
 
    [block-statement]
FUNCTION_STATEMENT:
{if-statement|while-statement|assignment-statement|block-statement}
IF_STATEMENT:
IF constraint-expression THEN function-statement
    [ELSE function-statement]
WHILE_STATEMENT:
WHILE logical-expression DO function-statement
ASSIGNMENT_STATEMENT:
{function-name|function-var3} := algebraic-expression
BLOCK_STATEMENT:
BEGIN function-statement [, function-statement . . .] END
Parameters:
 
algebraic-expression  as described under ALGEBRAIC_EXPRESSIONS.
 
constraint-expression  as described under CONSTRAINT_EXPRESSIONS.
 
datatype1,2,3  ARES representation of a data type.
 
function-name  ARES identifier which names the function.
 
function-var1,2,3  ARES identifier of a function variable.
 
literal  text string enclosed in single quotes with a length of 1 to 255.
 
logical-expression  as described under LOGICAL_EXPRESSIONS.
 
parameter-list  list of ARES identifiers used as parameters to the
    function.  These parameters will be matched with the list of arguments
    passed to the function when it is called.
Description:
The CREATE FUNCTION command is used to define functions which simplify
frequently used calculations.  Functions are classified as either scalar or
row functions, depending on their definition.  (See FUNCTION_EXPRESSION for a
discussion of row or scalar.)  A function with an INIT for each row clause is
a row function; without an INIT clause it is a scalar function.
Rules:
 
 1. The only identifiers legal in algebraic expressions and logical
    expressions used in the function are:  parameters, function variables, and
    the function name.
 2. Function expressions are not allowed in the function being defined.
 3. The data type of the function is defined by datatype1.  If it is not
    specified, the data type of the function is determined by the highest
    precedence data type of any of the arguments passed to the function.
 
 4. The DEFINE clause describes local variables for use in the function.  In a
    row function, these variables will keep their values as successive rows
    are evaluated.  Thus, they may be used as counters or accumulators for the
    function.  If a function variable has never been assigned a value, either
    through the use of the INIT clause or through a function assignment, the
    NULL operation will be true for that variable.
 5. The INIT/FOR EACH ROW clause is used to control the action of row
    functions.  When the function is first entered, the INIT clause is
    processed.  As each record is read, the FOR EACH ROW clause is evaluated.
    After all the records are processed, the final block-statement is
    evaluated.
 6. The assignment-statement stores the value computed by the right side of
    the expression in the function-variable or function-name on the left.
 7. The if-statement chooses which statement to execute based on the value of
    a logical expression.  If the logical expression is true, the statement
    following the THEN is executed, and the one following ELSE is ignored.  If
    the logical expression is false, the statement following the THEN is
    skipped, and the one following the ELSE (if it exists) is executed.
 8. The while-statement executes a statement repeatedly until the value of the
    logical-expression becomes false.  If the value is false at the beginning,
    the statement is not executed at all.
 9. The block-statement specifies that its component statements are executed
    in the same sequence as they are written.  The symbols BEGIN and END act
    as statement brackets.  Commas are used to separate the statements.
10. Functions created in invoke mode are temporary and only last until a new
    mode is entered.
Example:
See BUILTIN_FUNCTIONS for examples of how some of the ARES built-in functions
are created.
See also:
ALTER_FUNCTION, DISPLAY_FUNCTION, DROP_FUNCTION, LIST_FUNCTION
00004
00005
00007
00009
00001
00002
00006
00008
00010
00003
CREATE_FUNCTION
Syntax:
CREATE JOURNAL { TRANSIENT      } [,...]
               { COMMON [=] fid }
Parameters:
 
fid  a valid CP-6 file identifier.
Description:
The CREATE JOURNAL command is used to create a journal for the database.
There are two types of journals: transient and common.  The transient journal
contains images of records before they were updated and is used to back out of
updates.  The common journal contains images of records after they were
updated and is used to roll a database forward from a backup copy.
Rules:
 
 1. The CREATE JOURNAL command can only be issued in create or alter mode.
 2. Specifying TRANSIENT indicates that a transient journal should be active
    when updates are made to the database whether within a transaction or not.
    This protects the user from partially completed updates in the case of
    soft crashes.  No fid is specified since the transient journal is kept in
    a temporary system file.
 3. Specifying COMMON indicates that a common journal should be created.  All
    updates made to the database will be logged in the common journal.  The
    fid for the common journal must specify a valid CP-6 file in an account
    the creator has write access to, and the file must not yet exist.  The
    file will be created with access controls that allow ARES to write to the
    file on behalf of users that do not have write access to the account the
    journal was created in.
See also:
ALTER_JOURNAL, BEGIN, DROP
00002
00001
00003
00004
CREATE_JOURNAL
The create mode is used to create a new database description, and is entered
by issuing the CREATE MODEL command.  The create mode commands perform the
following functions:
 
   Name the database (name the model)
   Identify the tables and columns in the model
   Assign attributes to those tables and columns
   Specify fields for uniquely identifying records
   Specify fields as alternate access paths
   Define journaling options
The creation commands are checked for errors, but are not processed until all
the model creation commands are entered.  The model creation is completed by
entering a COMMIT command, or halted by issuing the ABORT command.  Alter mode
must be used to alter or add new tables to a database.  The commands which
perform these functions are summarized in the following table:
 
For additional information see:
HELP (ARES) TOPICS CREATE?
 
           Command         Description
 
           ABORT           Cancel the creation of a model
 
           COMMIT          Complete the creation of a model
 
           CREATE BULKFILE Create a description of a non-ARES file
 
           CREATE FUNCTION Create a user function
 
           CREATE JOURNAL  Specify database journaling options
 
           CREATE TABLE    Create a table
Syntax:
CREATE MODEL fid
Parameters:
 
fid  a file name which specifies the model to be created.
Description:
The CREATE MODEL command is used to define a model for a database.  A name
must be supplied in the fid on the CREATE command.  This name becomes the
model-name for that database.
Rules:
 
 1. A model with the same name cannot already exist in the account specified.
 2. The model-name is limited to 27 characters.  In addition, the names of
    tables in the model are appended to the model-name with a separator to
    actually name the files.  This means that the maximum length of a table
    name in the model is 31 minus the length of the model-name.
 
 3. If the optional password is used, all files created as part of this
    database will require this password.  In addition, any subsequent mode
    commands must specify this password.  The mode commands are ALTER MODEL,
    CREATE MODEL, DROP MODEL, and INVOKE MODEL.
 4. It is suggested that the user of ARES not attempt to maintain files like
    model-name_? or model-name-? in the same account as the named model.  ARES
    uses several files named in this way and conflicts may occur.
Example:
 
    CREATE MODEL TEST
 
means create the model TEST in the current directory
 
    CREATE MODEL TEST.directory
 
means create the model TEST in another directory
 
    CREATE MODEL TEST..password
 
means create the model TEST with a password
See also:
ABORT, COMMIT, CREATE_MODE
00002
00004
00001
00003
00005
CREATE_MODEL
CREATE_MODE
Syntax:
CREATE TABLE table-name [COMMENT = literal1]
    (column-description [,column-description])
 
     [IS ]
KEYS [ARE] [PRIMARY] (key-name = column-name1 [, column-name2 . . .])
 
    [, (key-name = column-name3 [, column-name4] . . .)] . . .
COLUMN_DESCRIPTION:
             [COMMENT = literal2]
column-name [datatype          ] [...]
            [HEADING = literal3]
Parameters:
 
column-name  an ARES column name.
 
column-name1,2,3,4  the name of a column in the table.
 
datatype  ARES representation of a data type.
 
key-name  ARES identifier specifying the name of each key.
 
literal1,2,3  text string enclosed in single quotes with a length of 1 to
    255.
 
table-name  ARES identifier naming the table.  The maximum length of the
    table-name is determined by subtracting the length of the model-name
    from 29.
Description:
The CREATE TABLE command is used to create a table in the database.  A table
is an ordered set of columns where the data is stored in the database.  A
table consists of rows and columns; a row is a single occurrence of all
columns that make up a table.
 
One column or group of columns must be labeled as the primary key for a table.
The contents of the primary key must be unique for each row in the table.  The
first key description describes the primary key; any descriptions following
define alternate keys.  Alternate keys need not contain unique data.
Rules:
 
 1. Each table-name must be unique for that database.
 2. Each table must contain at least one column.
 3. The data type description is optional on each column, if that column name
    exists in another table in the model.  If the data type is specified, any
    other table column with the same name must be the same data type.
 4. All occurrences of a column in the database must have the same COMMENT and
    HEADING fields.  If they are specified for a column which already exists,
    they are ignored.  To change these fields once they have been entered, the
    ALTER COLUMN command must be used.
 5. In the KEY clause, the first key-name is automatically the primary key and
    is required; the column list specifies those column names which comprise
    each key.  Each successive key-name definition, after the key-name
    specified as the primary key, creates a secondary key for that table.  The
    use of secondary keys permits ARES to more efficiently access the table.
    The key-name is used to differentiate keys, if the key definitions are
    modified using the ALTER TABLE command.
 6. If the HEADING clause is used, literal3 is the default heading that is
    used by the report writer when displaying data from columns.  If no
    HEADING clauses are used in a table definition, column-names are used as
    the default headings for columns when displaying the data.
 7. The COMMENT clause is used to give a short description of the table or
    column.  This description is displayed when the DISPLAY or LIST commands
    are used.
 8. Tables created in invoke mode are temporary and only last until a new mode
    is entered.
 9. The size of any individual key defined for a table cannot exceed 511
    bytes.  The total size for all fields contained in any key of the table
    cannot exceed 4000 bytes.  (This is a restriction on the types of keys
    that can be defined, and in no way restricts the number of records that
    can be stored in a table.)
10. The maximum record length allowed by ARES in a table description is 65535
    bytes.
See also:
ALTER_COLUMN, ALTER_TABLE, DISPLAY_TABLE, DROP_TABLE, LIST_TABLE, SELECT
00001
00003
00002
00004
00005
CREATE_TABLE
GRANT_CREATOR
In an attempt to minimize the impact of using shared tables, record locks are
released as soon as possible.  This means that after a record is read from a
table, the lock on the previous record is released unless the previous record
has been updated.  Thus, at any given time there will be a much smaller number
of outstanding record locks.  This method of operation is known as currencies
only and is the default for any table on which record locks are being issued.
 
While currencies only protects multiple updaters from updating the same data,
it does not guarantee that reading records will be reproducible.  This is
because the read records are no longer kept locked and therefore can be
updated or deleted by other users.  Should the user want such protection,
currencies only can be turned off by specifying CURRENCIES=NO on the BEGIN
command.
 
Many times the Application Program Interface user wishes to use currencies
only to reduce the impact on system resources but needs to keep some records
locked that have not been updated.  In such a case, the user can call
ARES_KEEP which will prevent ARES from releasing some record locks even though
the records have not been updated.
Note that the choice of the CURRENCIES option does not affect table sharing.
However, it does reduce the impact on system resources for both interactive
and API users, and can reduce the number of deadlocks that occur.
NORMALIZATION
DATA_TYPES
API_DATATYPE_CORRESPONDENCE
The language for creating a database description is also easy to understand
and use.  It allows the user to describe the logical characteristics of the
database in a straight-forward manner.  It also allows for easy modification
of this description without rebuilding it from scratch.  In addition, there
are facilities to improve the performance of the database.  Finally, the
impact of changing the representation of the database once it is built is
reduced.  This is done by automatically performing many restructuring
functions and by producing reports of affected areas where the changes cannot
be performed automatically.
 
For additional information see:
HELP (ARES) CREATE_MODE
The ARES data manipulation language has a small number of commands and simple
command components.  The broad range of ARES capabilities enables the casual
user to achieve almost immediate results, while the experienced user can use
these simple components to create complex commands.  These capabilities remove
many of the requirements for application programs and allow ARES query
statements to take their place.
Data is presented to ARES in simple row and column table format.  The concepts
of tables and their manipulation are common ones for anyone who has kept
records.  Because the data for ARES is presented in this familiar form, users
of ARES need not have programming experience.  The simplicity of the concept
of tables reduces the training time.  In addition, users will find that the
time needed to define a database or formulate a query is relatively short
because of the familiarity with the underlying data representation.  For
example, a table might contain employee information, as  shown below.
 
     : SELECT * FROM EMP
        .. 10 records SELECTed.
     NAME   EMP_NO SALARY MAN_NO DEPT_NAME GROUP_SIZE
     ------ ------ ------ ------ --------- ----------
     SMITH    7369  18000   7654 SHOE               0
     ALLEN    7499  25000   7844 TOY                0
     WARD     7521   9000   7844 TOY                0
     JONES    7566  26000   7902 LOAN               0
     MARTIN   7654  22000   7902 SHOE               0
     BLAKE    7698  24000   7654 SHOE               0
     CLARK    7782  15600   7654 SHOE               0
     SCOTT    7788  23750   7844 TOY                0
     TURNER   7844  18000   7902 TOY                0
     FORD     7902  25500      0 PRESIDENT          0
The specification of a data type on a column describes both the physical
storage and the contents of the column to ARES. Each ARES data type has its
own features and limitations.  Some care should be taken to choose the data
type which most accurately represents the data to be stored in the column.
 
ARES accepts the following data types:
CHARACTER
INTEGER
FLOATING POINT
DECIMAL
TIMESPAN
DATE
UTS
 
For additional information see:
HELP (ARES) datatype_DATA_TYPE
When evaluating algebraic and logical expressions, the data types of the
individual components are often not compatible.  It then becomes necessary to
convert one data type to another.
 
Within arithmetic expressions, operations are performed in DOUBLE PRECISION
unless one of the operands is DECIMAL, in which case, the operation is
performed in DECIMAL.
 
Within logical expressions, converting one data type to another follows the
order of precedence listed below.  When two different data types are
encountered, the lower one in the table is converted to the higher one in the
table.
 
Order of precedence for data type conversion:
 
    DATE
    TIMESPAN
    DECIMAL
    DOUBLE PRECISION
    REAL
    INTEGER
    CHARACTER
Note that the data type used for a particular operation is determined by the
data type of the two operands on either side of the operator.  The data type
of the rest of the expression is not considered.
 
If a numeric item is included in a DATE or TIMESPAN expression, or a numeric
item is stored into a DATE or TIMESPAN field, the number is treated as a
number of days and is converted to TIMESPAN data type.  A special exception is
made if the operator is * or /, in which case the number is not converted.  If
a DATE or TIMESPAN item is stored into a numeric item, the DATE or TIMESPAN
will be converted to a number of days.
 
If a character item is included in a DATE or TIMESPAN expression, or a
character item is stored into a DATE or TIMESPAN field, the character field
will be evaluated according to fixed format rules depending upon which type is
expected.  (See the section on defaults in Date and Time Input.)   (See topic
on defaults in DATE_AND_TIME_INPUT.) These defaults may be overridden through
the use of the DATE, TIME or FORMAT function as appropriate.
 
The result of an expression involving DATE and/or TIMESPAN items is a function
of both the operands and the operators.  The result types for a few of the
more useful combinations follow:
 
                        DATE     + TIMESPAN = DATE
 
                        TIMESPAN + TIMESPAN = TIMESPAN
 
                        DATE     - DATE     = TIMESPAN
 
                        DATE     - TIMESPAN = DATE
 
                        TIMESPAN - TIMESPAN = TIMESPAN
 
                        TIMESPAN * number   = TIMESPAN
 
                        TIMESPAN / TIMESPAN = number
SET_DATE
A date constant is a character string enclosed in quotes and immediately
preceded by a "D". The string will be evaluated using the date picture string
currently in effect (see the DATE option of the SET command).
    D'07/16/57'
Syntax:
DATE
Description:
DATE data type is used to represent date and time of day information.
Rules:
 1. DATE data type is represented as a packed decimal double word whose
    contents represent elapsed time since midnight on Jan.  1, 1 A.D., in
    hundreths of seconds.
 2. Although normally accurate to the hundreths of a second, all dates are
    calculated according to the Gregorian calendar, which was devised by the
    Council of Trent in 1502, and was not used in all European nations until
    about 150 years later.  Earlier dates should therefore be treated as
    approximate, they will almost certainly not correspond to dates according
    to the calendar in use at the time.
See also:
TIMESPAN_DATA_TYPE, UTS_DATA_TYPE
00001
00002
00003
Date formats provide a flexible and convenient method to display dates and
times.  The format of dates is defined by a picture that contains identifiers
for the date and time subfields along with any desired punctuation characters.
The picture can be thought of as a template that illustrates the desired
format.
When a date or timespan is formatted, each subfield is converted with zero
suppression, case shift, and abbreviation as specified by the picture.  All
punctuation characters appear in the same positions as in the picture.  The
(!)  date/time separator does not appear.  Any subfields not in the picture
are ignored.
 
The default picture for formatting dates is:
 
    mm/dd/yy
 
For a timespan, the default picture depends on the magnitude of the value.  If
the value is one day or more, the picture is:
 
    dddddddddd.hh:mm:ss.tt
 
If the value is less than a day but not less than an hour, the picture is:
 
    h:mm:ss.tt
 
If the value is less than an hour, the picture is:
 
    :mm:ss.tt
 
In any case, trailing subfields and their associated punctuation marks are
omitted if the subfields are zero.
If a picture is specified using SET DATE, the subfields in date strings must
appear in the same order as in the picture.  Punctuation characters in the
picture must appear in the data input in the positions shown.  However, the
parsing logic is forgiving of minor discrepancies.
 
Month and weekday names are accepted with or without abbreviation.  Input is
case insensitive.  A meridian or era suffix can always be preceded by one or
more blanks.  A comma, optionally preceded and/or followed by one or more
blanks, is accepted, but not required for the (!)  date/time separator.
Leading and trailing blanks are ignored.  Multiple blanks are allowed where a
single blank appears in the picture.  Extra zeros are always accepted and are
required only on adjacent numeric subfields, but extra zeros cannot be used to
extend a subfield beyond its maximum length.
 
For the subfield identifiers Y and YY, the leading digits of the year are
assumed to be the same as for the current year.  If the year is omitted from
the picture, the current year is assumed.
 
If the picture specifies only the time, the current date is assumed.  If the
picture specifies only a date, the time is assumed to be midnight.
 
If the picture specifies the quarter of the year, the date returned will be
the first day of that quarter.  If the picture specifies the month but not the
day, the date returned will be the first day of that month.  If the picture
specifies the day but not the month or year, the current month and year are
assumed.
 
If the picture specifies the day of the week in addition to other subfields,
an error is reported if the weekday is not correct.  If the picture specifies
only the day of the week, the next date with that weekday is returned.
 
If no picture is specified via SET DATE, the date and time may appear in
either order if both are specified.  The following pictures are recognized for
the date:
 
    www
    mm/dd/yyyy      mm/dd/yy        mm/dd
    mmm dd, 'yy     mmm dd 'yy      mmm dd
    dd mmm, 'yy     dd mmm 'yy      dd mmm
    yy-mm-dd
    yymmdd
 
When converting a date from character, whether or not a picture is specified,
the following special dates are recognized:
NOW       the current timestamp, accurate to the hundredth of a second
TOD[AY]       the current date, with the time assumed to be midnight
TOMO[RROW]       the date of the next day, with the time assumed to be
midnight
YEST[ERDAY]       the date of the previous day, with the time assumed to be
midnight
 
The following pictures are recognized for the time:
 
            hh:mm:ss.tt     hh:mm:ss.ttAM
            hh:mm:ss        hh:mm:ssAM
            hh:mm           hh:mmAM
            hhAM
 
If no picture has been specified using SET TIMESPAN, the default for timespans
is the following:
 
          { ddddddddd                               }
          {                                         }
    [+|-] { [ddddddddd.] hh: [mm [: [ss [. [tt]]]]] }
          {                                         }
          { : mm [: [ss [. [tt]]]]                  }
00001
00002
00003
00004
The following subfield identifiers are for the date:
 
    M      the month, with zero suppression (1 to 12).
 
    MM     the month, without zero suppression (01 to 12).
 
    D      the day of the month, with zero suppression (1 to 31).
 
    DD     the day of the month, without zero suppression (01 to 31).
 
    Y      the last digit of the year (0 to 9).
 
    YY     the last two digits of the year, without zero suppression
 
           (00 to 99).
 
    YYY    the last four digits of the year, with zero suppression
 
           (0 to 9999).
 
    YYYY   same as YYY.
 
    YYYYY  the year, with zero suppression (1 to 316888).
 
    YYYYYY same as YYYYY.
 
    J      the day of the year, with zero suppression (1 to 366).
 
    JJ     same as J.
 
    JJJ    the day of the year, without zero suppression (001 to 366).
 
           (All of the above are case insensitive.)
 
    MMM    the abbreviated month name (JAN to DEC).
 
    MMMM   the unabbreviated month name (JANUARY to DECEMBER).
 
    W      the minimal abbreviation of the day of the week
 
           (SU, M, TU, W, TH, F, SA).
 
    WW     the day of the week abbreviated to two characters
 
           (SU to SA).
 
    WWW    the day of the week abbreviated to three characters
 
           (SUN to SAT).
 
    WWWW   the unabbreviated day of the week (SUNDAY to SATURDAY).
 
           (The above appear in the same case as the identifier:
 
           uppercase, initial capital, or lowercase.  A single lowercase, w
 
           gives a value with an initial capital.  Five or more m's
 
           or W's are equivalent to four M's or W's.)
 
    AD     results in "AD" for years Anno Domini,
 
           and "BC" for years Before Christ.
 
    A.D.   results in "A.D." for years Anno Domini,
 
           and "B.C." for years Before Christ.
 
    BC     results in nothing for years Anno Domini,
 
           and "BC" for years Before Christ.
 
    B.C.   results in nothing for years Anno Domini,
 
           and "B.C." for years Before Christ.
 
    CE     results in "CE" for Common Era years,
 
           and "BCE" for Before Common Era years.
 
    C.E.   results in "C.E." for Common Era years,
 
           and "B.C.E." for Before Common Era years.
 
    BCE    results in nothing for Common Era years,
 
           and "BCE" for Before Common Era years.
 
    B.C.E. results in nothing for Common Era years,
 
           and "B.C.E." for Before Common Era years.
 
The following subfield identifiers are for the time:
 
       H    the hour, with leading zero suppression (0 to 23).
 
       HH   the hour, without zero suppression (00 to 23).
 
       M    the minute, with leading zero suppression (0 to 59).
 
       MM   the minute, without zero suppression (00 to 59).
 
       S    the second, with leading zero suppression (0 to 59).
       SS   the second, without zero suppression (00 to 59).
 
       T    hundredths of a second, with trailing zero suppression
 
            (0 to 99).
 
       TT   hundredths of a second, without zero suppression (00 to 99).
 
            (All of the above are case insensitive.)
 
       AM   results in "AM" for times before noon, and "PM" for times
 
            after noon, and specifies that hours are presented modulus
 
            12.  Noon is 12 PM. Midnight is 12 AM.
 
       PM   same as AM.
 
       A.M. results in "A.M." for times before noon, and "P.M." for
 
            times after noon, and specifies that hours are presented
 
            modulus 12.  Noon is 12 PM. Midnight is 12 AM.
 
       P.M. same as A.M.
 
If the picture contains a meridian or era suffix, all variant spellings are
accepted.  If no meridian or era is specified where one is expected, AM or AD
is assumed.
 
When the picture specifies both date and time, an (!)  exclamation mark must
separate them.  If a blank or other punctuation is required between the date
and time, it should be placed in the picture just before or after the (!)
exclamation mark.
 
Only one occurrence of each subfield (day, month, year, weekday, and era for
dates; hour, minute, second, hundredths of seconds, and meridian for time) is
allowed in a given picture.  The Julian day and quarter of the year specify
both the month and the day for purposes of detecting duplicate subfields.
 
Time subfields must be specified in order:  hours, minutes, seconds, and
hundredths of seconds.  If any subfield is omitted, the following subfields
must also be omitted.  The meridian, if specified, must follow all other time
subfields.
 
Date subfields can appear in any order and in any meaningful combination, but
ambiguous combinations of subfields are disallowed.  An ambiguous combination
is one that does not designate a specific date and time.  For example, "March,
2PM" and "Wednesday, 1990" are ambiguous in this sense.
 
Any blanks, digits, and punctuation characters in a picture appear in the same
position in each formatted value as in the picture.  Punctuation characters
must not have a decimal value greater than 255.
 
Alphabetic characters (and anything else) enclosed in double quote marks (")
are treated as punctuation.  All alphabetic characters not enclosed in double
quotes (") must be subfield identifiers.  Double double quotes (" ") within a
double quoted string appear as a single double quote (") in formatted values.
A punctuation character is required between two alphabetic subfields.
Adjacent numeric subfields are allowed, but a zero suppressed subfield cannot
be immediately followed by another numeric subfield.  These restrictions are
required to insure that any value output through a picture can be read back in
without ambiguity.
 
The following examples illustrate how the first and last days of the year 1990
appear using various date formats:
 
                Picture         Formatted Result
               ------------------------------------------------
                MM/DD/YY      01/01/90           12/31/90
 
                MMM.D,'YY     JAN.1,'90          DEC.31,'90
 
                Q"Q"YY        1Q90               4Q90
 
                w Mmm d,yyy   F Jan 1,1990       Sa Dec 31,1990
 
                Www m/dd/yy   Fri 1/01/90        Sat 12/31/90
 
The following examples show the effect of various pictures in formatting a
given time:
 
                      Picture            Formatted Result
                     ------------------------------------
                      HH:MM:SS.TT        13:30:10.50
 
                      H "O'CLOCK"        13 O'CLOCK
 
                      H "O'CLOCK" AM     1 O'CLOCK PM
 
                      HH:MM AM           01:30 PM
 
                      H:MM:SS.T AM       1:30:10.5 PM
 
The following examples show how both date and time can be formatted as a
single value:
 
                  Picture                 Formatted Result
                  -------------------------------------------
                  MM/DD/YY! HH:MM:SS      05/06/90 13:30:10
 
                  Mmm d 'YY, !HH:MMAM     May 6 '90, 01:30PM
Syntax:
[{PACKED|UNPACKED      }]
DECIMAL (size[,fsize]) [{SIGNED|UNSIGNED|FLOAT}]
                       [{OVERPUNCHED|SEPARATE }] [...]
                       [{LEADING|TRAILING     }]
Parameters:
 
fsize  integer -31 <= fsize <= 31.
 
size  positive integer 1 <= size <= 60.
Description:
DECIMAL data type is used to represent numbers which require greater precision
than floating point numbers provide or which require more exact arithmetic on
their fractional parts.  It is also useful in bulkfiles for importing data
generated by COBOL programs.
Rules:
 
 1. The size parameter specifies the number of digits required to represent
    the data.  It should not include space for the sign, decimal point or
    exponent, as ARES includes those.
 2. The fsize parameter specifies the number of decimal digits to the right of
    the decimal point.  An fsize less than zero implies trailing zeros after
    the number and before the decimal point.  For example:
 
    DECIMAL (4,2) UNSIGNED represents numbers 00.00 thru 99.99
 
    DECIMAL (4,-2) UNSIGNED represents numbers 100 thru 999900 and 0
 
    The default for fsize is 0.
 3. If the FLOAT option is specified, the number is represented as a digit
    string, a sign, and an exponent.
 4. If the FLOAT option is specified, the SIGNED option, the attributes of the
    sign (LEADING, TRAILING, OVERPUNCHED, SEPARATE), and the fsize option are
    all illegal.
 5. If the UNSIGNED option is specified, negative values will not be allowed
    in the field.
 6. If the SIGNED option is specified, a sign is included in the
    representation of the number.  LEADING or TRAILING may be specified to
    describe the position of the sign relative to the digit string.
    OVERPUNCHED or SEPARATE may be specified to describe whether or not the
    sign is placed in the same digit position as the first or last digit.  If
    SIGNED is specified by itself or if none of the sign options are
    specified, the default is LEADING SEPARATE.
 7. The UNPACKED option is used to specify that the digit string be stored one
    digit to a byte rather than two digits to a byte.  If no packing option is
    specified, the default is PACKED.
 8. The OVERPUNCHED option is only allowed in bulkfile columns and is not
    allowed with the PACKED option.
00002
00001
00003
Syntax:
DELETE [ALL] table-name1
 
    [FROM table-name2 [table-label][, . . .]]
 
    [WHERE constraint-expression]
Parameters:
 
constraint-expression  as described under CONSTRAINT_EXPRESSIONS.
 
table-label  name associated with a table in the FROM clause, used as a
    table variable in the WHERE clause.
 
table-name1  ARES identifier specifying the name of the table whose rows
    are to be deleted.
 
table-name2  ARES identifier specifying the tables to be used in the WHERE
    constraint-expression.
Description:
The DELETE command is used to delete rows of data from a table; only entire
rows may be deleted.
Rules:
 
 1. The table-names must reference previously created table definitions.
 2. If the ALL keyword is specified, all rows of the table are deleted, and
    the WHERE expression is not allowed.  If the WHERE clause is not
    specified, the ALL keyword is required.
 3. If the FROM clause is specified, the table being deleted must be listed in
    this clause.
 4. The ALL option is not allowed within a transaction unless SHARE=NONE.
Example:
DELETE ALL EMP
 
DELETE EMP;
    WHERE EMP.EMP_NAME = 'JONES'
 
DELETE EMP;
    FROM EMP, EMP MANAGER;
    WHERE EMP.MGR_NO = MANAGER.EMP_NO;
         AND MANAGER.DEPT_NAME = 'SALES'
00002
00004
00001
00003
DELETE
NORMALIZATION
Syntax:
DIRECTORY [{[DP#setname].account|R[ESET]}]
Parameters:
 
account  specifies the new default account fid, and may consist of an
    account or a packset name and an account.
 
setname  specifies a string of 1 to 6 characters that identifies a
    packset.  Packset names are assigned by the system manager.
Description:
The DIRECTORY command is used to change the default account and packset.  If
not specified, the default account is the logon or running account and the
packset name is null.
Rules:
 
 1. The RESET option specifies that the default account is to be reset to the
    running account.
 2. If DIRECTORY is specified without parameters, the current directory is
    displayed.
00002
00001
00003
DIRECTORY
Syntax:
 
        [TABLE table-name-list1            ]
        [COLUMN column-name-list           ]
        [PREVIOUS                          ]
        [BULKFILE bulkfile-name-list       ]
        [FUNCTION function-name-list       ]
        [DML label-list                    ]
        [PRIVS [ALL                       ]]
        [      [ACCOUNT [=] account-name  ]]
        [      [TEMPLATE [=] template-name]]
        [      [PROGRAM [=] program-name  ]]          [[OVER] LP[@location]
]
DISPLAY [SET [SEPARATOR]                   ] [SYNTAX] [[INTO] fid
[(option-list]]
        [    [AUTOPRINT]                   ]          [[ON  ] ME
]
        [    [CONTINUE ]                   ]          [[TO  ]
]
        [    [INFORM   ]                   ]
        [    [OVERWRITE]                   ]
        [    [DATE     ]                   ]
        [    [TIMESPAN ]                   ]
        [STATS [FOR] table-name-list2      ]
        [MODEL                             ]
        [JOURNALS                          ]
        [FORMAT                            ]
Parameters:
 
account-name  valid CP-6 account name.
 
bulkfile-name-list  list of one or more bulkfile names.
 
column-name-list  list of one or more column names.
 
fid  a CP-6 file identifier.
 
function-name-list  list of one or more function names.
 
label-list  list of one or more stored DML statement names.
 
program-name  valid CP-6 file name and account in the form file.account.
 
table-name-list1,2  list of one or more table names.
 
template-name  valid CP-6 account name with optional embedded wildcard
    characters (?).
 
ON or TO  indicates to only honor the DISPLAY command if the file does not
    already exist.
 
OVER  indicates to honor the DISPLAY command whether or not the file
    exists.
 
INTO  indicates to merge the result of the DISPLAY command into the file
    if it exists, or to create a new one if it does not.
 
LP  directs output to the default line printer; @location specifies a
    specific line printer.
 
ME  returns the output destination to the user's terminal.
 
option-list  list of the following options separated by commas:
        O[RGANIZATION]={C[ONSECUTIVE]|U[NIT]R[ECORD]}
        F[ORM]={fprmname|'formname'}
        I[XTNSIZE]=number
        X[TNSIZE]=number
Description:
The DISPLAY command is used to display the contents of various components of
the database.
Rules:
 
 1. The database description for the requested item is displayed.
 2. If DISPLAY is issued with no additional parameter, the current ARES
    command is displayed.
 3. If PREVIOUS is specified, the command prior to the current command is
    displayed.
 4. If TABLE, COLUMN, BULKFILE, FUNCTION or DML are specified, the tables,
    columns, bulkfiles, functions or DMLs, respectively, are displayed.
 5. If PRIVS is specified, the current privileges are displayed.
 6. If PRIVS ALL is specified, all privilege records defined in the model are
    displayed.
 7. If PRIVS ACCOUNT is specified, the template record that best matches
    account-name is displayed.  These will be privileges a user from that
    account would have when using the model.
 8. If PRIVS TEMPLATE is specified, the template record that exactly matched
    template-name is displayed.
 9. If PRIVS PROGRAM is specified, the program template record that best
    matches program-name is displayed.  These will be the privileges that the
    program specified by program-name will have when using the model, if the
    user running the program has the PROGRAM privilege.
10. Only a user with CREATOR privilege may issue DISPLAY PRIVS with the ALL,
    ACCOUNT, TEMPLATE, or PROGRAM options.
11. If SET is specified with an option, the current value of the option is
    displayed.  If no option is specified, the current value of all SET
    options is displayed.
12. If STATS is specified, statistical information about the specified
    table(s) is displayed.
13. If JOURNALS is specified, then the state of the transient and common
    journal are displayed.
14. If FORMAT is specified, the current FORMAT options (if any) are displayed.
15. If MODEL is specified, a full description of all components of the current
    model is displayed.  Only a user with the CREATOR privilege may issue this
    command.
16. If the SYNTAX option is specified, the items will be displayed in a
    syntactically correct form which may be read back into ARES.
17. If fid is specified, the output from the display will be directed to that
    fid.
See also:
LIST Command
00002
00001
00003
00004
See DISPLAY_COMMAND
See DISPLAY_COMMAND
DISPLAY
See DISPLAY_COMMAND
See DISPLAY_COMMAND
See DISPLAY_COMMAND
See DISPLAY_COMMAND
See DISPLAY_COMMAND
See DISPLAY_COMMAND
See DISPLAY_COMMAND
DISPLAY_BULKFILE
DISPLAY_COLUMN
DISPLAY_DML
DISPLAY_FORMAT
DISPLAY_FUNCTION
DISPLAY_PREVIOUS
DISPLAY_PRIVS
DISPLAY_STATS
DISPLAY_TABLE
GRANT_DML
Syntax:
{DO|!} IBEX-command
Parameters:
 
IBEX-command  any legal IBEX command.
Description:
The DO command allows an ARES user to execute an IBEX command without exiting
ARES.
Rules:
 
 1. The ! (exclamation point) may be used instead of the word DO. It should be
    noted however that if the ! is used in an XEQ file, it will terminate the
    ARES session unless preceded by at least one blank.
Examples:
 
    DO DI
 
means display the current system status
 
    !LDEV LP09 TITLE='report title',PAGE=100,COPIES=3
 
means set up a title and page number for a report destination
00002
00004
00001
00003
DO
The DROP commands are used to DROP elements of an ARES database.  Both
permanent and temporary elements can be dropped.
 
For additional information see:
HELP TOPICS DROP?
DROP_COMMAND
Syntax:
 
     {BULKFILE bulkfile-name-list}
     {DML stored-DML-list        }
DROP {FUNCTION function-name-list}
     {TABLE table-name-list      }
     {JOURNAL {COMMON   }        }
     {        {TRANSIENT}        }
Parameters:
 
bulkfile-name-list  list of one or more bulkfile names.
 
function-name-list  list of one or more function names.
 
stored-DML-list  list of one or more names of stored DML statements.
 
table-name-list  list of one or more table names.
Description:
The DROP command is used to delete a prior definition from a model.
Rules:
 
 1. All names used in the DROP command must reference previously created
    relational database entities.
 2. To drop permanent definitions or use the JOURNAL option, you must be in
    alter mode.
 3. The DROP TABLE command deletes both the description of the table and all
    of its contents.
 4. To drop DML commands, you must be the owner of the DML command (the person
    who stored it) or have CREATOR privilege.
 5. Dropping a database item will invalidate any stored queries which
    reference that item.
 6. If DROP JOURNAL TRANSIENT is specified, before images of updated records
    are no longer written to the transient journal file unless the updates are
    performed within a transaction that automatically uses transient
    journaling.
 
 7. If DROP JOURNAL COMMON is specified, after images of updated records are
    no longer written to the common journal.  The file that had been
    identified as the common journal in a previous CREATE or ALTER JOURNAL
    command is not affected by the DROP JOURNAL command.
00002
00001
00003
DROP_COMMAND
DROP_COMMAND
DROP_COMMAND
This mode is a special mode that consists of only one valid command, the DROP
MODEL command.  A model is dropped by entering a COMMIT command, or halted by
issuing an ABORT command.
Syntax:
DROP MODEL fid
Parameters:
 
fid  a file name which specifies the model to be dropped.
Description:
The DROP MODEL command is used to delete the entire database and all
information about the database (model).
Rules:
 
 1. The fid must specify an existing model.
 2. The user must be the creator of the database in order to delete the model
    or database.
 3. If the model was created with a password, that password must be specified
    in the fid or the command is aborted.
 4. The command waits until exclusive use of the model is available.
 5. The model will not actually be deleted until a COMMIT command is entered.
See also:
ABORT, COMMIT, DROP_MODE
00002
00001
00003
00004
DROP_MODEL
DROP_MODE
DROP_COMMAND
Syntax:
 
     {TO  }
     {ON  }
DUMP {OVER} fid USING bulkfile-name select-expression
     {INTO}
Parameters:
 
bulkfile-name  is the name of a previously created bulkfile description.
 
fid  any valid CP-6 file identifier.
 
select-expression  any data selection expression as defined under
    SELECT_COMMAND.
Description:
The DUMP command is used to dump data from the database to a CP-6 consecutive
file.
Rules:
 
 1. The bulkfile supplies ARES with the desired form of each record to be
    placed in the file.  All data placed in each file is converted to match
    the description of the column-specification in the bulkfile description.
 2. The select-expression must select the same number of results as there are
    non-filler columns in the bulkfile description.
 3. The content of filler fields in the output file is undefined.
 4. DATE and TIMESPAN data is converted according to the default format.
    Formats established by the SET command are not used, so that stored DUMP
    commands will function correctly regardless of the format currently set.
    The FORMAT built-in function may be used in the select-statement to format
    DATE and TIMESPAN data as character string representations which differ
    from the default format picture.  Conversely, the DATE and TIME built-in
    functions may be used to convert a character string representation of a
    DATE or TIMESPAN value to a DATE or TIMESPAN datatype field according to
    the specified picture.
See also:
CREATE_BULKFILE
00002
00001
00003
00004
DUMP
Syntax:
{E[ND]|Q[UIT]|X}
Description:
The END command (or equivalent) closes all active files and exits the ARES
processor.
Rules:
 
 1. The END command will not be allowed if a COMMIT or ABORT are currently
    required.
00001
00002
END
Syntax:
ENTER [ script-fid ] [ , frame-name ] [ initial-input ]
Parameters:
 
frame-name  is the first frame of the script to execute.
 
initial-input  supplies responses to the initial prompts for the dialog.
 
script-fid  is the file identifier for the script to execute.
Description:
The ENTER program starts execution of a dialog at the ARES level.  It can be
used to run dialogs that do nothing but issue ARES commands, or to start a
dialog that invokes and runs under another program.
Rules:
 
 1. The script-fid parameter specifies the file containing the compiled script
    for the dialog to be put into execution.  The default is the current
    setting of the ADAPT$SCRIPT DCB. If the script-fid does not specify an
    account, the file of the specified name in :SYS is used if it exists;
    otherwise, the current directory account is the default.  To ensure that
    the file in the current account is used, a dot (.)  must follow the file
    name.
 2. The frame-name parameter specifies the first frame of the script-fid to be
    executed.  The default is the MAIN frame for the script.
 3. The initial-input parameter can be used to presupply responses to the
    initial prompts for the dialog.  The text supplied is put into the dialog
    input buffer before the first frame is started.  The default is no initial
    input text, which means that the user is prompted for all dialog inputs.
    Either the script-fid or frame-name must be specified if initial-input is
    provided.
 4. The dialog is put into execution at the ARES level.  It can issue IBEX
    commands by using the DO statement to pass command lines to IBEX. It can
    issue ARES commands by using the ISSUE statement to pass command lines to
    ARES. If the dialog executes any ISSUE statements to pass commands to
    ARES, the commands are simply echoed through M$LO.
 5. If any frame of the script, including the top frame, is defined to be run
    under another program (via the DO clause on the frame definition
    statement), that frame and all frames it enters run under the specified
    program, not at the ARES level.  Dialogs running under another program
    function as described under ENTER Command in the CP-6 ADAPT Reference
    (HA12) (or see !HELP (ADAPT) ENTER_COMMAND for more information).
 
 6. Terminal input for a dialog running at the ARES level is read through
    M$SI. Output to the interaction window is written through M$LO.
00002
00001
00003
ENTER
API_ERROR_CODES
Following is an example of code meant to give a general picture of how a
program might use the ARES Application Program Interface calls.
 !ARES
 ARES D01 here
 : CREATE MODEL EXAMPLES
 : CREATE TABLE EMP;
 +        (NAME CHAR(20),EMP_NO INTEGER,SALARY DECIMAL(8,2),;
 +         MAN_NO INTEGER,DEPT_NAME CHAR(10),GROUP_SIZE INTEGER);
 +     KEY IS PRIMARY(EMP_KEY=EMP_NO)
 : COMMIT
   The model EXAMPLES.XXXACCT has been created.
 :
 : INVOKE EXAMPLES
 : INSERT INTO EMP VALUES('SMITH',7369,18000,7654,'SHOE',0),;
 +                       ('ALLEN',7499,25000,7844,'TOY',0),;
 +                       ('WARD',7521,9000,7844,'TOY',0),;
 +                       ('JONES',7566,26000,7902,'LOAN',0),;
 +                       ('MARTIN',7654,22000,7902,'SHOE',0),;
 +                       ('BLAKE',7698,24000,7654,'SHOE',0),;
 +                       ('CLARK',7782,15600,7654,'SHOE',0),;
 +                       ('SCOTT',7788,23750,7844,'TOY',0),;
 +                       ('TURNER',7844,18000,7902,'TOY',0),;
 +                       ('FORD',7902,25500,0,'PRESIDENT',0)
   .. 10 records INSERTed.
 !FORTRAN API_EXAMPLE_SIF OVER *OU(LS)
 FORTRAN 77 VERSION E00  MAY 01 '90
 *  1>     1: C
    2>     2: C     A sample program to demonstrate the use of the API.
    3>     3: C     This program gives everyone in the EMP table a 10%
    4>     4: C     raise, and fills in the size of the group.
    5>     5: C
    6>     6:       IMPLICIT INTEGER(A-Z)
    7>     7:       REAL SALARY,NEW_SALARY
    8>     8:       CHARACTER*20 NAME
    9>     9:
   10>    10: C     Initialize the interface and set up an error code in
   11>    11: C     which errors will be returned
   12>    12:       CALL ARES_INIT(ERRCODE)
   13>    13:
 
   14>    14: C     Open the database
   15>    15:       CALL ARES_INVOKE('EXAMPLES')
   16>    16:       IF (ERRCODE .NE. 0) GOTO 1000
   17>    17:
 
   18>    18: C     Tell the interface that it should recognize NIL
   19>    19: C     as a nil variable
   20>    20:       CALL ARES_SETNIL(NIL)
   21>    21:
 
   22>    22: C     Start a query to get the employees
   23>    23:       CALL ARES_STARTEXT
   24>    24:      1('SELECT NAME,EMP_NO,SALARY FROM EMP',Q,'UPDATE')
   25>    25:       IF (ERRCODE .NE. 0) GOTO 1000
   26>    26:
 
   27>    27: C     Read the results until we run out of them
   28>    28: 100   CALL ARES_FETCH(Q,NAME,ENUM,SALARY)
   29>    29:
 
   30>    30: C     First see if we are out of results. Get ERRCODE=1
   31>    31: C     if this is the case. Any other code is an error.
   32>    32:       IF (ERRCODE .EQ. 1) GOTO 200
   33>    33:       IF (ERRCODE .NE. 0) GOTO 1000
 
   34>    34:
 
   35>    35: C     Compute the new salary.
   36>    36:       NEW_SALARY = SALARY * 1.1
   37>    37:
 
   38>    38: C     Display name, employee number, old and new salaries
   39>    39:       WRITE (108,900) NAME,ENUM,SALARY,NEW_SALARY
   40>    40: 900   FORMAT (X,A20,X,I5,X,F8.2,X,F8.2)
   41>    41:
 
   42>    42: C     Update the current result with the new salary. Since
   43>    43: C     we don't want to update the name and employee
   44>    44: C     number, we'll pass nil values for those.
   45>    45:       CALL ARES_UPDATE(Q,NIL,NIL,NEW_SALARY)
   46>    46:       IF (ERRCODE .NE. 0) GOTO 1000
   47>    47:
 
   48>    48:       GOTO 100
   49>    49:
 
   50>    50: 200   CONTINUE
   51>    51:
   52>    52: C     Now we're going to fill in the size of each group
   53>    53:
 
   54>    54:       CALL ARES_EXECTEXT(
   55>    55:      1'UPDATE MAN FROM EMP,EMP MAN '//
   56>    56:      2'SET GROUP_SIZE=MAN.GROUP_SIZE+1 '//
   57>    57:      3'WHERE MAN.EMP_NO=EMP.MAN_NO')
   58>    58:       IF (ERRCODE .NE. 0) GOTO 1000
   59>    59:
   60>    60: C     We're all finished now, so we can just end
   61>    61:       STOP 'Update complete.'
   62>    62:
   63>    63: 1000  CONTINUE
   64>    64:
 
   65>    65: C     This is the error handling section. We'll just
   66>    66: C     report the error and quit.
   67>    67:
   68>    68:       CALL ARES_ERRMSG
   69>    69:       STOP 'Abnormal Termination.'
   70>    70:       END
  ERRORS FOUND      : 0       TOTAL ERRORS FOUND: 0
 
 !LINK *OU OVER *RU;
 LINK E00 here
       (UNSAT(:LIB_ARES.:SYS,:LIB_SYSTEM.:SYS),;
        DCBSLOTS=100,;
        ALTSHARELIB=ARES_ASL)
 *  ARES_ASL.:SYS (Alternate Shared Library) associated.
 *  :SHARED_COMMON.:SYS (Shared Library) associated.
 *  Library file :LIB_ARES.:SYS used.
 *  Library file :LIB_SYSTEM.:SYS used.
 *  3 unsatisfied secondary reference(s).
 *  Total program size = 18K.
 
 ******** NODE = *OU                             SIZE =     17K ********
 
 ******* UNRESOLVED SECONDARY ENTRY REFERENCES *******
 
       ARES_ERROR.ZJL$INITIALIZE     ZJE$ASLENTRY.ZJE$ASLCLIMB
 
 ******* UNRESOLVED SECONDARY SEGMENT REFERENCES *******
 
       ZJ_STATUS.ZJE$ASLCLIMB
 
 !*RU
 
 SMITH                 7369 18000.00 19800.00
 ALLEN                 7499 25000.00 27500.00
 WARD                  7521  9000.00  9900.00
 JONES                 7566 26000.00 28600.00
 MARTIN                7654 22000.00 24200.00
 BLAKE                 7698 24000.00 26400.00
 CLARK                 7782 15600.00 17160.00
 SCOTT                 7788 23750.00 26125.00
 TURNER                7844 18000.00 19800.00
 FORD                  7902 25500.00 28050.00
  *STOP* Update complete.
 
 !ARES
 ARES D01 here
 : INVOKE EXAMPLES
 : SELECT * FROM EMP
   .. 10 records SELECTed.
 NAME   EMP_NO SALARY MAN_NO DEPT_NAME GROUP_SIZE
 ------ ------ ------ ------ --------- ----------
 SMITH    7369  19800   7654 SHOE               0
 ALLEN    7499  27500   7844 TOY                0
 WARD     7521   9900   7844 TOY                0
 JONES    7566  28600   7902 LOAN               0
 MARTIN   7654  24200   7902 SHOE               3
 BLAKE    7698  26400   7654 SHOE               0
 CLARK    7782  17160   7654 SHOE               0
 SCOTT    7788  26125   7844 TOY                0
 TURNER   7844  19800   7902 TOY                3
 FORD     7902  28050      0 PRESIDENT          3
Following is an example of code meant to give a general picture of how a
program might use the ARES Application Program Interface Extension calls.  The
database creation, program linkage and program execution will be the same as
that shown  under EXAMPLE_API_EXTENDED. All that is shown here is the
compilation of the application program which will accomplish the same task
except using the extension routines.
 
!FORTRAN APIEXT_EXAMPLE_SIF OVER *OU(LS)
FORTRAN 77 VERSION E00  MAY 01 '90
*    1.000>     1: C
     2.000>     2: C     A sample program to demonstrate the use of the API.
     3.000>     3: C     This program gives everyone in the EMP table a 10%
     4.000>     4: C     raise, and fills in the size of the group.
     5.000>     5: C
     6.000>     6:       IMPLICIT INTEGER(A-Z)
     7.000>     7:       REAL SALARY,NEW_SALARY
     8.000>     8:       CHARACTER NAME*20,EMP_REC*40,EMP_DESC*40
     9.000>     9:       CHARACTER UPDATE_LIST*8
    10.000>    10:
    11.000>    11: C     Initialize the interface and set up an error code in
    12.000>    12: C     which errors will be returned
    13.000>    13:       CALL ARES_INIT(ERRCODE)
    14.000>    14:
    15.000>    15: C     Open the database
 
    16.000>    16:       CALL ARES_INVOKE('EXAMPLES')
    17.000>    17:       IF (ERRCODE .NE. 0) GOTO 1000
    18.000>    18:
    19.000>    19: C     Tell the interface that it should recognize NIL
    20.000>    20: C     as a nil variable
    21.000>    21:       CALL ARES_SETNIL(NIL)
    22.000>    22:
    23.000>    23: C     Start a query to get the employees
    24.000>    24:       CALL ARES_STARTEXT
    25.000>    25:      1('SELECT NAME,EMP_NO,SALARY FROM EMP',Q,'UPDATE')
    26.000>    26:       IF (ERRCODE .NE. 0) GOTO 1000
    27.000>    27:
    28.000>    28:       CALL ARES_GETDESC(Q,EMP_DESC,'FORTRAN')
    29.000>    29:       IF (ERRCODE .NE. 0) GOTO 1000
    30.000>    30:
    31.000>    31:       CALL ARES_PUTDESC(Q,EMP_DESC)
    32.000>    32:       IF (ERRCODE .NE. 0) GOTO 1000
    33.000>    33:
    34.000>    34: C     Read the results until we run out of them
    35.000>    35: 100   CALL ARES_FETCHR(Q,EMP_REC)
    36.000>    36:
    37.000>    37: C     First see if we are out of results. Get ERRCODE=1
    38.000>    38: C     if this is the case. Any other code is an error.
    39.000>    39:       IF (ERRCODE .EQ. 1) GOTO 200
    40.000>    40:       IF (ERRCODE .NE. 0) GOTO 1000
    41.000>    41:
    42.000>    42: C     We know the SALARY is in the third field of the
    43.000>    43: C     record so get the value.
    44.000>    44:       CALL ARES_GETFIELD(EMP_REC,EMP_DESC,3,SALARY)
    45.000>    45:       IF (ERRCODE .NE. 0) GOTO 1000
    46.000>    46:
    47.000>    47: C     Compute the new salary.
    48.000>    48:       NEW_SALARY = SALARY * 1.1
    49.000>    49:
    50.000>    50: C     Display the name, employee number, old and new
    51.000>    51: C     salaries.  Need to extract the values from the
    52.000>    52: C     record buffer first.
    53.000>    53:       CALL ARES_GETFIELD(EMP_REC,EMP_DESC,1,NAME)
    54.000>    54:       IF (ERRCODE .NE. 0) GOTO 1000
    55.000>    55:       CALL ARES_GETFIELD(EMP_REC,EMP_DESC,2,ENUM)
    56.000>    56:       IF (ERRCODE .NE. 0) GOTO 1000
    57.000>    57:       WRITE (108,900) NAME,ENUM,SALARY,NEW_SALARY
    58.000>    58: 900   FORMAT (X,A20,X,I5,X,F8.2,X,F8.2)
    59.000>    59:
    60.000>    60: C     We now have the NEW_SALARY but we need to put this
    61.000>    61: C     new value in the record buffer to replace the old
    62.000>    62: C     value so we can make the update to the database.
    63.000>    63:       CALL ARES_PUTFIELD(EMP_REC,EMP_DESC,3,NEW_SALARY)
    64.000>    64:
    65.000>    65: C     Update the current result with the new salary.
    66.000>    66: C     Since we don't want to update the name and
    67.000>    67: C     employee number, we'll send the appropriate field
    68.000>    68: C     number through the UPDATE_LIST parameter.  Setup the
    69.000>    69: C     UPDATE_LIST to have one field updated and specify
    70.000>    70: C     the third field (now containing the value of
    71.000>    71: C     NEW_SALARY) to be the one to update.
    72.000>    72:       ENCODE (8,'(2A4)',UPDATE_LIST) 1,3
    73.000>    73:       CALL ARES_UPDATER(Q,EMP_REC,UPDATE_LIST)
    74.000>    74:       IF (ERRCODE .NE. 0) GOTO 1000
    75.000>    75:
    76.000>    76:       GOTO 100
    77.000>    77:
    78.000>    78: 200   CONTINUE
 
    79.000>    79:
    80.000>    80: C     Now we're going to fill in the size of each group
    81.000>    81:
    82.000>    82:       CALL ARES_EXECTEXT(
    83.000>    83:      1'UPDATE MAN FROM EMP,EMP MAN '//
    84.000>    84:      2'SET GROUP_SIZE=MAN.GROUP_SIZE+1 '//
    85.000>    85:      3'WHERE MAN.EMP_NO=EMP.MAN_NO')
    86.000>    86:       IF (ERRCODE .NE. 0) GOTO 1000
    87.000>    87:
    88.000>    88: C     We're all finished now, so we can just end
    89.000>    89:       STOP 'Update complete.'
    90.000>    90:
    91.000>    91: 1000  CONTINUE
    92.000>    92:
    93.000>    93: C     This is the error handling section. We'll just
    94.000>    94: C     report the error and quit.
    95.000>    95:
    96.000>    96:       CALL ARES_ERRMSG
    97.000>    97:       STOP 'Abnormal Termination.'
    98.000>    98:       END
 ERRORS FOUND      : 0       TOTAL ERRORS FOUND: 0
 
As you can see, the original testcase, using the field-oriented calls, was
more straight-forward than this testcase using the record-oriented calls.
Therefore, in application programs where the structure of the database is
predictable, the field-oriented calls would be a good choice.  However, if the
structure of the database and/or the queries are built in such a way that the
format of the result is unknown to the programmer, record-oriented calls are
the only way to meaningfully access the data in the database.
 
The information under the following topics hold true for the extended API
calls as well:
API_LIMITATIONS
API_BREAK_CONTROL
API_ERROR_CONDITIONS
API_DATA_TYPE_CORRESPONDENCE
API_USAGE_INFORMATION
API_LINKING_INFORMATION
API_LINKING_DIAGNOSTICS
API_MEMORY
: SELECT MAX(SALARY);
    + FROM EMP;
    + WHERE DEPT_NAME = 'SHOE'
      .. 1 record SELECTed.
 
If a row function is used in the select-list of the SELECT command, all the
elements of the select-list must also use row functions or be grouped (see
GROUP BY clause of the SELECT command).  This assures that the number of
results obtained from the SELECT command is consistent within that command.
 
The following example will produce an error:
 
    : SELECT MAX(SALARY), DEPT_NAME FROM EMP
      EMP.DEPT_NAME has not been grouped. If a row function is
      specified in the select list, all columns in the
      select list must either be specified in the GROUP BY clause
      or be arguments of a row function in the select list.
 
This example is illegal since MAX (SALARY) produces a single result whereas
DEPT_NAME produces one result, per match/per row.
: SELECT ABS(SALARY);
    + FROM EMP
      .. 10 records SELECTed.
    :
    : SELECT SALARY;
    + FROM EMP;
    + WHERE ABS(SALARY) > 1000
      .. 10 records SELECTed.
 
Row functions return a single value no matter how many sets of parameters are
used.  If a row function such as AVG (average) is used, regardless of how many
numbers are being averaged together, only one result is returned.  Row
functions can be identified by the use of the FOR EACH ROW clause of the
CREATE FUNCTION command.  Row functions can only be used in two places within
the SELECT command:   in the select-list, and in the constraint-expression of
the HAVING clause.
FORMAT_EXCLUDE
START
Expressions comprise a large part of the syntax of the ARES language.  They
are used to specify when records are to be included in the result and what
results are to be printed.
 
For additional information see:
HELP ALGEBRAIC_EXPRESSIONS
HELP FUNCTION_EXPRESSIONS
HELP LOGICAL_EXPRESSIONS
HELP CONSTRAINT_EXPRESSIONS
FILE_IDENTIFIERS
Syntax:
[DP[nn][#setname]/] name[.[account][.password]]
Parameters:
 
nn  two digit field indicating which disk resource (if the user has
    reserved more than one) is to be accessed.  This number is
    user-defined and not related to the system configuration.
 
setname  specifies a string of 1 to 6 characters that identifies a
    packset.  Packset names are assigned by the system manager.
 
name  string of 1 to 32 characters that assign an identifying name to a
    file.
 
account  string of 1 to 8 characters that identifies a file directory.
 
password  string of 1 to 8 characters assigned when the file was created.
Description:
A file identifier (fid) supplies ARES with all of the information necessary to
locate a file on the system.  If the file desired resides in the current
directory, all that is necessary is the name.  Other portions of the fid
supplement the file name with information necessary for ARES to find it in
another directory, on a private packset, or if it has a password.
00002
00001
Syntax:
{REAL              }
{DOUBLE [PRECISION]}
Description:
Floating point data type is used to represent numbers with decimal places,
exponents or both.
Rules:
 
 1. REAL is represented internally as single word, hexadecimal floating point.
    REAL data can have up to 7+ digits of precision.
 2. DOUBLE PRECISION is represented internally as double word hexadecimal
    floating point.  DOUBLE PRECISION data can have up to 18+ digits of
    precision.
 3. The range of floating point values is as follows:
        (4.661463)*(10**(-156)) to (8.379879)*(10**152))
00001
00002
Syntax:
 
       {EXCLUDE [ALL BUT] column-list1                       }
       {INCLUDE [[ONLY] column-list2]                        }
       {GROUP {[EXCEPT] column-list3|ERASE}                  }
       {SEPARATOR {n BLANK[S]|string1}                       }
       {SUBTOTAL {[EXCEPT] column-list4|ERASE}               }
       {TOTAL {[EXCEPT] column-list5|ERASE}                  }
       {COLUMN column-id {NAME [=] string2          }        }
FORMAT {                 {WIDTH [=] n[,m]           } [,...] }
       {                 {WRAP [=] n                }        }
       {                 {       {DEFAULT      }    }        }
       {                 {DATE [=] {date-format}    }        }
       {                 {       {DEFAULT      }    }        }
       {                 {TIMESPAN [=] {time-format}}        }
       {PAGE {[EXCEPT] column-list6|ERASE}                 }
       {TITLE [=] string3                                  }
       {COUNT {[EXCEPT] column-list7|ERASE}                }
       {HEADINGS [=] {ON|OFF}                              }
       {             {FIRST }                              }
Parameters:
 
column-id  column name or a number.  A number refers to the position
    within the original select-list.
 
column-list1,2,3,4,5,6,7  list of one or more column-ids separated by
    commas.
 
date-format  a date format string enclosed in single quotes (see
    DATE_TIME_PICTURES).
 
m,n  integer constants.
 
string1,2,3  string of alphanumeric characters delimited by single quotes.
 
time-format  a time format string enclosed in single quotes (see
    TIMESPAN_PICTURES).
Description:
The FORMAT command is used to reformat the query currently displayed.  A
subsequent PRINT command is necessary to actually display the reformatted
query.
Rules:
 
 1. If the EXCLUDE option is used, the specified columns are excluded from the
    result.  The ALL BUT option specifies that only those columns listed are
    included in the result.
 2. The INCLUDE option is used to reverse the effect of EXCLUDE. Columns that
    were not part of the original result cannot be referenced in the INCLUDE.
    The INCLUDE ONLY option specifies that only those columns listed are
    included in the result.  INCLUDE with no additional parameters resets the
    FORMAT command to include everything.
 3. The GROUP option is used to specify that the contents of the column be
    printed only when it is different from the previous record.  If subtotals
    are specified, the subtotals are printed each time something which has
    been grouped changes.  The EXCEPT option specifies that grouping be done
    on all columns except those specified in column-list3.  If ERASE is
    specified, grouping is suspended.  It is not legal to group a column which
    is being totaled or subtotaled.
 4. The PAGE option is used to indicate that a top of page should be performed
    in the report when the content of the column is different than in the
    previous record.
 5. The SUBTOTAL option is used to indicate which columns are to be
    subtotaled.  Subtotals are taken whenever any value changes in a column
    being grouped.  A final total is also provided unless otherwise specified
    in a FORMAT TOTAL command; column-list4 specifies the name or position of
    the columns for which subtotals are to be calculated.  The EXCEPT option
    specifies that subtotals be calculated for all columns currently being
    subtotaled except those specified in column-list4; ERASE suspends
    subtotals.  The ERASE option removes only subtotals, totals must be
    removed with the TOTAL ERASE option.  It is not legal to subtotal a column
    which is being grouped.
 6. The TOTAL option is used to indicate which columns are to be totaled.  If
    not specified, totals are provided for all columns being subtotaled;
    column-list5 is the name or position of the columns for which totals are
    to be calculated.  EXCEPT specifies that totals are to be calculated for
    all columns except those specified in column-list5; ERASE suspends totals.
 7. The COUNT option is used to indicate columns which are to be counted.  A
    count of records is printed for the column each time the value in a
    grouped column changes.  The EXCEPT option specifies that counts are to be
    calculated for all columns except those specified in column-list7.  The
    ERASE option suspends counting.  If both COUNT and GROUP are specified for
    the same column, the marker for group breaks is replaced by the count.
 8. The SEPARATOR option is used to define what is displayed between the
    columns.  This command overrides the SET SEPARATOR value for the purposes
    of this result only.  The BLANK option specifies the number of spaces to
    be displayed between the columns, and string1 specifies the alphanumeric
    character string to be displayed between the columns.  The maximum length
    of a separator is 31 characters.
 9. The COLUMN column-id option is used to format particular columns.
 
    The NAME option is used to change the column heading for the display.  The
    string2 specified is the column heading that is used for the display.
 
    The WIDTH option is used to change the width for displaying a column.  For
    character data the leftmost n characters are displayed; for numeric data
    the maximum number of significant digits is displayed.  If m is specified
    on the WIDTH option, the number is displayed with the decimal point fixed
    m characters from the right edge of the field.  The maximum width of a
    column is 511.
 
    The WRAP option is used to format a text column as a paragraph.  Each line
    of the paragraph will be n characters long.  Lines will be broken at
    blanks, commas, or semicolons as much as possible.
 
    The DATE option may be specified for columns containing DATE data.  This
    will override the SET DATE format string.  The format string specified
    will control the formatting of the column.  The default may be returned by
    using the DEFAULT option.
 
    The TIMESPAN option may be specified for columns containing TIMESPAN data.
    This will override the SET TIMESPAN format string.  The format string
    specified will control the formatting of the column.  The default may be
    returned by using the DEFAULT option.
10. The TITLE option allows the user to specify a title for the report.  The
    title string3 will be centered on the output page.  The current date will
    be displayed on the left margin, formatted according to the current SET
    DATE format.  The page number will appear on the right margin.  If the
    title string is too long to be centered between the date and the page
    number, the date and page number will not be included.
11. In all cases, FORMAT specifications are valid only for the currently
    selected results.  As soon as a new SELECT command is issued, the FORMAT
    specifications are reset.
12. The HEADINGS option controls the printing of column headings and is
    effective until the next SELECT command is issued.
 
   o   The ON option prints the column headings as usual (one set at the top
       of each page).
   o   The FIRST option prints only the first set of column headings.
   o   The OFF option prints no column headings.
   o   The default is ON.
See also:
DISPLAY_FORMAT, PRINT, SET_AUTOPRINT, SET_DATE, SET_SEPARATOR, SET_TIMESPAN
00002
00001
00003
00004
See FORMAT_COMMAND
See FORMAT_COMMAND
See FORMAT_COMMAND
See FORMAT_COMMAND
See FORMAT_COMMAND
FORMAT
See FORMAT_COMMAND
See FORMAT_COMMAND
See FORMAT_COMMAND
See FORMAT_COMMAND
See FORMAT_COMMAND
See FORMAT_COMMAND
See FORMAT_COMMAND
See FORMAT_COMMAND
See FORMAT_COMMAND
API_FORTRAN
ROLL_FORWARD
UPDATE_FROM
BUILTIN_FUNCTIONS
Syntax:
function-name (algebraic-expression[, algebraic-expression, ...])
Parameters:
 
algebraic-expression  as described under ALGEBRAIC_EXPRESSIONS.
 
function-name  an identifier.
Description:
A function-expression is a function name followed by a pair of parentheses
that enclose a list of algebraic-expressions separated by commas.  The
elements in the list represent the parameters for the function.
There are two types of functions:  scalar functions and row functions.
 
Scalar functions return a value for each set of parameters evaluated.  For
example, if ten results would normally be printed by a SELECT command,
applying a scalar function to one of the expressions in the select-list still
produces ten results.  Scalar functions can be used anywhere column-ids can be
used, except where a column-id appears to the left of an assignment clause
(such as the SET clause of the UPDATE command).
00002
00001
The first step in building a new database is to issue the CREATE MODEL
command.  This command enters the "create mode" and tells ARES that a new
database is being created.  Next, tables are created by issuing the CREATE
TABLE command.  When all the tables are created, the COMMIT command is issued
to make the database permanent.  To use the database, the INVOKE command is
issued to tell ARES which database to access.  This is the "invoke mode".
 
After invoking the database and adding data to it, another table may be
required.  To do this, the database description must be modified using the
ALTER MODEL command.  This is the "alter mode" and new tables may now be
created using the CREATE TABLE command, altered using the ALTER TABLE command,
or deleted using the DROP TABLE command.  Again, at the end of these changes,
the COMMIT command must be issued to cause the actions to take effect; below
is a sample session.
 
     : CREATE MODEL EXAMPLES
     : CREATE TABLE EMP;
     +        (NAME CHAR(20),EMP_NO INTEGER,SALARY DECIMAL(8,2),;
     +         MAN_NO INTEGER,DEPT_NAME CHAR(10),GROUP_SIZE INTEGER);
     +     KEY IS PRIMARY(EMP_KEY=EMP_NO)
     : COMMIT
        The model EXAMPLES has been created.
     :
     : INVOKE EXAMPLES
     : INSERT INTO EMP VALUES('SMITH',7369,18000,7654,'SHOE',0),;
     +                       ('ALLEN',7499,25000,7844,'TOY',0),;
     +                       ('WARD',7521,9000,7844,'TOY',0),;
     +                       ('JONES',7566,26000,7902,'LOAN',0),;
     +                       ('MARTIN',7654,22000,7902,'SHOE',0),;
     +                       ('BLAKE',7698,24000,7654,'SHOE',0),;
     +                       ('CLARK',7782,15600,7654,'SHOE',0),;
     +                       ('SCOTT',7788,23750,7844,'TOY',0),;
     +                       ('TURNER',7844,18000,7902,'TOY',0),;
     +                       ('FORD',7902,25500,0,'PRESIDENT',0)
        .. 10 records INSERTed.
     :
     : ALTER MODEL EXAMPLES
     : CREATE TABLE LOCATION;
     +        (CITY CHAR(20),;
     +         LAT_D INT,LAT_M INT,LAT_NS CHAR(1),;
     +         LON_D INT,LON_M INT,LON_EW CHAR(1));
     +     KEY(C=CITY)
     : CREATE TABLE SALES;
     +        (EMP_NO INTEGER,PART_NO INTEGER,QUANTITY INTEGER);
     +     KEY(E=EMP_NO,PART_NO)
     : CREATE TABLE SALARY_RANGE;
     +        (LOW INTEGER,HIGH INTEGER,PERCENT_RAISE DECIMAL(3,2));
     +     KEY(S=LOW)
     : COMMIT
        The model EXAMPLES has been altered.
     : INVOKE EXAMPLES
     : INSERT INTO LOCATION VALUES('DENVER',39,44,'N',104,59,'W'),;
     +                            ('DC',38,50,'N',77,0,'W'),;
     +                            ('BOSTON',42,15,'N',71,7,'W'),;
     +                            ('DES MOINES',41,35,'N',93,37,'W')
        .. 4 records INSERTed.
     :
     : INSERT INTO SALES VALUES(7369,11,500),;
     +                         (7369,12,1575),;
     +                         (7521,11,800),;
     +                         (7521,14,322),;
     +                         (7788,13,1777),;
     +                         (7788,14,2010),;
     +                         (7844,11,400)
        .. 7 records INSERTed.
     :
     : INSERT INTO SALARY_RANGE VALUES(0,9999,.10),;
     +                                (10000,14999,.14),;
     +                                (15000,19999,.16),;
     +                                (20000,29999,.12),;
     +                                (30000,99999,.8)
        .. 5 records INSERTed.
Syntax:
 
      {CREATOR                         }
      {DML                             }
      {PROGRAM                         }
GRANT {NONE                            } TO {PROGRAM program-template-list}
      {{ALL           }                }    {user-template-list           }
      {{operation-list} [ON table-list]}
Parameters:
 
operation-list  list of the following operations separated by commas:
 
        SELECT
        INSERT
        UPDATE
        DELETE
 
program-template-list  list of template character strings separated by
    commas.  Each template defines a class of programs to which operations
    are being granted.  A program template is composed of characters that
    are valid for a CP-6 file and account name plus the wildcard character
    (?).  The ?  can only appear as a trailing character in the file name
    portion of the program template.  The program template is matched
    against a program name and account to determine the valid operations
    of a given program.  Matching is done in a similar fashion to user
    templates.
 
table-list  list of table names that exist in the model.
user-template-list  list of template character strings separated by
    commas.  Each user template defines a class of users to whom
    operations are being granted.  A user template is composed of
    characters that are valid for a CP-6 account name plus the special
    character question mark (?).  The user template is matched against an
    account name to determine the valid operations for a given user.  If
    the user template does not contain any question marks, it must match
    the users account name exactly.  If the template contains question
    marks, each question mark can match an arbitrary number of characters
    in the account name to resolve the match.  Thus, a template of ABC
    only matches the account ABC, whereas a template of ABC? matches all
    accounts that begin with the letters ABC.
Description:
The GRANT command is used by the database creator to give other users and
programs permission to use and/or modify the database.  The creator, by
definition, can always perform any operation on the database.  If no GRANT
command is issued, only the creator can access the database.  Privileges are
checked when the model is invoked, dropped, altered, or created.  If
privileges are granted, the change will not be seen by the current users of
the database until one of these commands is reissued.
 
There are two types of authorization records:  user and program.  They are
identified by the use of the user-template-list or the program-template-list
in the GRANT command.  User authorization records define privileges for
classes of users.  Program authorization records define privileges for classes
of programs.
 
The access controls defined on the files should not be modified using PCL.
Rules:
 
 1. For each template specified in a GRANT command, an authorization record is
    created that contains the operations being authorized.
 2. If a template is specified that corresponds to an existing authorization
    record, the new privileges are added to that authorization record.  Thus,
    the GRANT command is additive in nature (except for GRANT NONE which is
    discussed later).
 3. When a user tries to access the database, the user's account name is
    compared to the user template.  When more than one template might match,
    the best possible match is used.  That is, if two or more authorization
    records would match the user's record because of wildcarding, the one that
    uses the most non-question mark characters is the one chosen.  As an
    example, if an authorization record existed for ABC? and ABCD?, and user
    ABCDE tries to use the database, the record corresponding to ABCD? is used
    to determine the operations allowed.
 4. If the authorization record selected for the user contains the PROGRAM
    privilege, and the user is accessing ARES through an application program,
    then the program name and account is compared to the program templates
    that have been defined.  Again, the best possible match will be used.  The
    privilege given to the program will be a merging of the user and program
    authorization records.
 5. The template question mark (?)  can be used to define the operations
    allowed for all users or programs that do not match any of the other
    authorization records.  This is because ?  always matches any account
    name.  Note that this record is only used if no better matches are found
    in the list of authorization records.
 6. If CREATOR is specified, an authorization record is created which
    indicates that the specified users have the same authority as the creator
    of the model; they can alter the model, grant or revoke privileges, as
    well as any other function usually reserved for the model creator.  If an
    authorization record for the template already exists, any privileges
    previously granted are superseded by the creator privilege.
 7. If DML is specified, the specified users are allowed to store DML commands
    (see STORE_COMMAND) in the model.  Once a DML command is stored, only the
    user who originally stored it, or users with CREATOR privilege, may modify
    or delete it.
 8. If PROGRAM is specified, the specified users are allowed to run
    application programs that may have greater privileges than the user does.
 9. If NONE is specified, an authorization record indicates that all
    operations are denied; thus, the specified user can be denied access to
    the database.  If an authorization record for the template already exists,
    any privileges previously granted are first removed.
10. If ALL is specified instead of an operation-list, all existing operations
    are authorized to the tables in the table-list.  If no table-list is
    specified, all privileges are granted to all tables and both DML and
    PROGRAM privileges are also granted.
11. If operation-list is specified, only those operations specified in
    operation-list are authorized.
12. If table-list is omitted, the operations specified are authorized to all
    tables in the model.
13. If table-list is specified, the operations are authorized to only those
    tables specified in table-list.
14. The operations are authorized for only those templates specified in the
    template list.
15. Additional privileges cannot be granted to a template record that has
    either CREATOR or NONE specified.
See also:
ACCESS_CONTROLS, DISPLAY_PRIVS, REVOKE
00002
00001
00003
00004
See GRANT_COMMAND
GRANT
See GRANT_COMMAND
See GRANT_COMMAND
See GRANT_COMMAND
See GRANT_COMMAND
FORMAT_GROUP
The GROUP BY clause of the select-statement is a concept that allows the user
to apply a function to all the rows in a table that have something in common
(as determined by an algebraic expression defined by the user).  The function
that is applied can be either a standard ARES function or a user-defined
function.  The GROUP BY option allows formulation of queries such as, "Find
the average salary of the employees under each manager".  Such a request is
shown in the following example.
 
 : SELECT AVG(SALARY),MAN_NO;
 + FROM EMP;
 + WHERE MAN_NO~= 0;
 + GROUP BY MAN_NO
   .. 3 records SELECTed.
     1 MAN_NO
 ----- ------
 19200   7654
 19250   7844
 22000   7902
 
The result of a GROUP BY can be inserted into a table and used in the future.
Following is an example.  A table is created to hold the result of the
previous query, and the result of the GROUP BY is inserted.  It is now
possible to formulate questions such as, "Find the department with the highest
average salary", as shown in this example.
 
 : CREATE TABLE AVG_BY_DEPT;
 +        (MNUMBER INTEGER,;
 +         AVG_SAL INTEGER);
 +     KEY(M=MNUMBER)
   Temporary table AVG_BY_DEPT created.
 :
 : INSERT INTO AVG_BY_DEPT;
 +     SELECT MAN_NO,AVG(SALARY);
 +     FROM EMP;
 +     WHERE MAN_NO~=0;
 +     GROUP BY MAN_NO
   .. 3 records INSERTed.
 :
 : SELECT MNUMBER;
 +     FROM AVG_BY_DEPT;
 +     WHERE AVG_SAL=(SELECT MAX(AVG_SAL);
 +                    FROM AVG_BY_DEPT)
   .. 1 record SELECTed.
 MNUMBER
 -------
    7902
 
It should be noted that the GROUP BY used here is quite different from the
FORMAT GROUP. The former, as explained above, modifies the result of a query
with optional applications of functions, and produces a result that can be
stored in tables.  The latter is strictly a report function which allows
breaks on changing values of specified fields, and to subtotal or total other
fields based on the breaks.
FORMAT_HEADINGS
Syntax:
 
HELP [(fid)] [TOPICS] [keyword1] [-] [keyword2]
 
Note:  The optional elements can be specified in any order:
 
    (fid)
    TOPICS
    [keyword1] [-] [keyword2]
 
For example, HELP (fid) keyword1 - keyword2 TOPICS is acceptable.
Parameters:
 
fid  specifies the processor name (for example, ARES). If fid is omitted,
    the current processor is assumed.
 
TOPICS  requests a list of topic or subtopic names, rather than an
    information message.
 
keyword1 [- [keyword2]]  specifies a topic, a range of topics, or a topic
    and subtopic to identify what HELP information is requested.
 
     Form
     ------------------------------------  Result
                                           --------------------------------
     HELP (fid) TOPICS                     Lists all topics
     HELP (fid) TOPICS keyword1 - keyword2 Lists all topics in the range
 
                                             specified by keyword1 - keyword2
 
     HELP (fid) TOPICS keyword1?           Lists all topics beginning with
 
                                             the prefix specified by keyword1
 
     HELP (fid) TOPICS keyword1            Lists all subtopics for the
 
                                             topic specified by keyword1
 
     Form
     ------------------------------------    Result
                                             --------------------------------
     HELP (fid) keyword1                     Displays the first level
                                               information message for
 
                                               the topic keyword1
 
     HELP (fid) keyword1 keyword2            Displays the information
 
                                               message for keyword1, but only
 
                                               the level identified by the
 
                                               subtopic keyword2
 
     HELP (fid) TOPICS keyword1[-][keyword2] Lists topic or subtopic
 
                                               names.  See TOPICS parameter.
 
    Note:   keyword1 may include the wildcard character (?)
    as the rightmost character, if TOPICS is specified.
Description:
The HELP command is used to display information online.  HELP messages have
levels.  Once the initial level has been displayed, entering a question mark
displays the next level, usually containing greater detail.  Entering two
question marks displays the entire message.
00002
00001
HELP
An identifier is a string of up to 30 alphanumeric characters beginning with a
letter.  The alphanumeric character set used by ARES consists of all letters,
digits, the underscore (_), and dollar sign ($).  Upper and lower case letters
in identifiers will be treated as identical, e.g., ABC, abc, and Abc all refer
to the same item in the database.  The only exception to this is the model
name.
 
It should be noted that many languages have restricted character sets and do
not allow the underscore and dollar sign.  It is therefore recommended that
 
these special characters be avoided if ARES is to be used through an
application program in the future.
 
model-name identifiers can only be 27 characters in length, because three
characters are needed by ARES for internal use.
 
A table-name identifier is a string of 1 or more characters that assigns an
identifying name to a file.  The maximum length of a table-name is determined
by subtracting the length of the model-name from 29.
 
column-ids are a special class of identifiers.  These are the only identifiers
that can be used in the various forms of expressions recognized by ARES. There
are also instances where only column-ids can be used.  These instances are
specifically identified in the commands in which they apply.  column-ids take
the form:
 
    [{table-name|table-label}.]column-name
 
where table-name, table-label, and column-name are all valid identifiers.
table-labels are explained under SELECT_COMMAND.
 Sharing tables works between ARES users because each invocation of ARES is
cooperating with the other by using the same locking mechanism.  ARES depends
on these locks to restrict the sharing of files, and many times opens an
individual file with a SHARE option that is less restrictive than might be
expected.
For example if the UPDATE command is issued:
 
        UPDATE EMP FROM EMP,EMP MAN;
        SET EMP.SALARY=EMP.SALARY*1.10;
        WHERE EMP.MAN_NO=MAN.EMP_NO AND MAN.DEPT_NAME='SHOE'
 
ARES opens the table EMP twice:   first FUN=UPDATE, SHARE=IN (to actually
update the table), and second FUN=IN, SHARE=ALL (to select the manager whose
department name is SHOE). Notice that the first open must specify SHARE=IN
even if the command was issued within a transaction that specified SHARE=NONE.
The table locks prevent the user from sharing the table with another user.
Even though the file is opened shared, the table lock is exclusive in that it
prevents other ARES users from sharing the table.
 
Obviously, ARES cannot always prevent the sharing of tables by non-ARES users
who open files directly.  In the example above, a different user could open
the file used to represent the table EMP, specifying FUN=IN, SHARE=ALL
simultaneously with the ARES user.
Unauthorized sharing of a table is generally not a problem.  When a database
is created by ARES, special access controls are placed on the file that
prevent everyone except the creator (identified by the CP-6 logon) from
accessing the files used to represent the model  (see ACCESS_CONTROLS). Thus,
only the model creator can access the tables in a way that might violate the
table locks ARES is issuing.  Two conditions allow additional users to
directly access files:
 1. When the model creator has specifically modified the access controls on
    the ARES files.
 2. When the account (as authorized in PIG) specifies MERGE=YES and gives
    accounts, other than the creator's, access (by specifying wildcarded
    account names with other than just a ? character).
FORMAT_INCLUDE
SET_INFORM
Syntax:
INSERT INTO table-name [{VALUES row-list|select-expression}]
ROW_LIST:
{(constant-list) [, . . .]}
Parameters:
 
constant-list  a list of constants whose values are to be inserted into
    the columns.
 
row-list  a list of rows to be inserted into the table.
 
select-expression  any data selection expression as defined under
    SELECT_COMMAND.
 
table-name  name of the table into which rows are to be inserted.
Description:
The INSERT command is used to insert rows of data into tables.  The insertions
are made one row at a time.
 
If a large number of records are inserted into a table which has secondary
keys, significant performance advantages may be gained from the use of the
BEGIN MODE=LOAD command.  This causes all of the records to be physically
inserted into the table before the alternate key structures are built or
updated.
 
The INSERT command has three different forms:
Rules:
 
 1. If neither a row-list nor a select-expression is specified, ARES prompts
    for each column of each successive row.  Records are inserted until no
    value is entered for the first column of a new row.  Long character
    strings may be entered by typing an LF (linefeed) at the end of each
    segment rather than a CR (carriage return).  A single blank entered for a
    numeric field will be treated as a zero.
 2. If the row-list option is specified, each row inserted is represented by a
    list of constants, separated by commas, and enclosed in parenthesis.  The
    number of constants within the parentheses must equal the number of
    columns in the table.  Multiple rows can be inserted by specifying
    additional constant-lists in parenthesis.
 3. If the select-expression option is specified, the row data is obtained
    from the select-expression.  The number of columns selected by the select-
    expression must be the same as the number of columns needed by the INSERT
    command.
Example:
INSERT INTO STUDENT VALUES ('JONES',35045,23),;
                               ('SMITH',74411,42)
 
This example inserts two rows into the table STUDENT.
See also:
SET_OVERWRITE
00003
00005
00002
00001
00004
00006
INSERT
Syntax:
[SIGNED  ]
INTEGER [(length)] [UNSIGNED]
Parameters:
 
length  positive integer 1 <= length <= 36.
Description:
INTEGER data type is used to describe numbers with no fractional portion.
Rules:
 
 1. INTEGER data is stored internally in binary form.
 2. INTEGER data defaults to SIGNED.
 3. The default for length is a full word (36 bits).  If length is specified,
    it gives the number of bits to use for the storage of the item.
 4. If length is specified and is not a multiple of 9 (9, 18, 27, 36), the
    field may not be used as part of a key.
 5. Adjacent INTEGER fields in bulkfile descriptions are packed together with
    no filler space between them.
 6. The range of INTEGER data is as follows:
    SIGNED:  -2**(length-1) to (2**(length-1))-1
    UNSIGNED:  0 to (2**length)-1
00002
00001
00003
SELECT_INTERSECT
Syntax:
INVOKE [MODEL] fid
Parameters:
 
fid  a file name which identifies the model to invoke.
Description:
The INVOKE command is used to specify the database to be used.  Once in invoke
mode the user may issue database access commands.
Rules:
 
 1. The fid must specify the name of a previously created model.
 2. If the model was created with a password, that password must be specified
    in the fid or the command is aborted.
 3. The command waits until there are no longer any exclusive users of the
    model.
00002
00001
00003
This mode is used to access the data in the database once it exists.  This
mode is entered by issuing the INVOKE command.  Once in this mode database
access commands may be issued.  The database access commands are commonly
referred to as the Data Manipulation Language (DML). These commands are used
to:
 
   Insert data into the database
   Extract data from the database
   Update data in the database
 
The SELECT command is the most important database access command.  It is the
basic data extraction command.  It has both simple and complex forms and can
also be used as an additional specification within the extract and update
commands.
 
The database access commands are summarized in the following table:
 
             Command Description
 
             DELETE  Delete records from a table
 
             DUMP    Dump data from a table into an external file
 
             INSERT  Insert records into a table
 
             LOAD    Load data into a table from an external file
 
             SELECT  Extract information from the database
 
             UPDATE  Update records in a table
 
Normally, DML commands are acted upon when issued, and the database is updated
on a command by command basis.  It is possible though to define logical units
of work that are larger than one command.  These units of work are called
transactions.  Once a transaction has started, only database access commands
and miscellaneous database commands can be used until it has completed.
 
The transaction commands are summarized in the following table:
 
        Command    Description
 
        ABORT      Cancel the transaction and all updates
 
        BEGIN      Define a transaction and its attributes
 
        CHECKPOINT Make pending updates permanent, and continue
 
                   transaction
 
        COMMIT     Complete transaction and make all updates permanent
 
        ROLL BACK  Continue transaction and cancel all updates
 
In addition to the database access and transaction commands, there are several
other commands that are valid in this mode.  These commands are used to:
 
o   Make temporary additions to the model
o   Control database access
o   Control the use of stored DML commands
o   Format the result of other database access commands
o   Optimize performance
 
Any model creation commands issued in this mode are temporary in nature and
only last for the current mode of ARES operation.  This group of commands is
processed immediately and do not require that a COMMIT command be issued.
This allows for the creation, alteration, and deletion of temporary tables
that are deleted when a new mode is entered.  Additional commands valid in
this mode are summarized in the following table:
 
       Command  Description
 
       ALTER    Alter temporary additions to the database description
 
       CREATE   Create temporary additions to the database description
 
       DROP     Drop temporary addition to the database description
 
       FORMAT   Change the format of the data being displayed
 
       GRANT    Permit other users to access the database
 
       OPTIMIZE Update internal information about the database
 
       PRINT    Reprint the result using the latest format
 
       REPORT   Pass query results to the XARGENT report writer
 
       REVOKE   Remove database access privileges previously given
 
       START    Execute the last command or a stored command
 
       STORE    Save DML commands
INVOKE
INVOKE_MODE
ARES employs many keywords in the syntax of its commands.  All keywords in
ARES may be abbreviated to three or more characters, e.g., SEL, SELE, SELEC,
and SELECT are all recognized as SELECT by ARES.
API_LIMITATIONS
API_LINKING_DIAGNOSTIC
API_LINKING_INFORMATION
Syntax:
 
     {TABLES     }
     {BULKFILES  } [[OVER] LP[@location]      ]
LIST {COLUMNS    } [[INTO] fid [(option-list)]]
     {FUNCTIONS  } [[ON  ] ME                 ]
     {DML [OWNER]} [[TO  ]                    ]
     {PRIVS      }
Parameters:
 
fid  a CP-6 file identifier.
 
ON or TO  indicates to only honor the LIST command if the file does not
    already exist.
 
OVER  indicates to honor the LIST command whether or not the file exists.
 
INTO  indicates to merge the result of the LIST command into the file if
    it exists, or to create a new one if it does not.
 
LP  directs output to the default line printer; @location specifies a
    specific line printer.
 
ME  returns the output destination to the user's terminal.
 
option-list  list of the following options separated by commas:
        O[RGANIZATION]={C[ONSECUTIVE]|U[NIT]R[ECORD]}
        F[ORM]={fprmname|'formname'}
        I[XTNSIZE]=number
        X[TNSIZE]=number
Description:
The LIST command is used to list the items in a database.
Rules:
 
 1. The LIST command lists the name and comment for all of the items in the
    database of the specified type.
 2. The OWNER option allows a user with CREATOR privilege to list the owner of
    the DML statements.
 3. If fid is specified, the output from the list is directed to that fid.
See also:
DISPLAY Command
00002
00001
00003
00004
See LIST_COMMAND
See LIST_COMMAND. For column definitions see CREATE_TABLE or ALTER_TABLE.
LIST
See LIST_COMMAND
See LIST_COMMAND
See LIST_COMMAND
See LIST_COMMAND
Syntax:
LOAD table-name FROM fid
 
    [SORTED] USING bulkfile-name [( expression-list )]
 
         [WHERE constraint-expression]
Parameters:
 
bulkfile-name  name of a previously created bulkfile description.
 
constraint-expression  as described under CONSTRAINT_EXPRESSIONS.
 
expression-list  list of algebraic-expressions, as described under
    ALGEGERAIC_EXPRESSIONS.
 
fid  any valid CP-6 file identifier.
 
table-name  name of the table being loaded.
Description:
The LOAD command is used to load data into the database from a standard CP-6
file.  (See Using Bulkfiles in Section 5 for further explanation and
examples.)
Rules:
 
 1. The LOAD operation is much more efficient if the records are placed into
    the table in order by the primary key fields.  The SORTED option specifies
    that the file is already sorted in this manner, and should be processed in
    the order received.  If it is omitted, ARES sorts the data before placing
    it in the table.
 2. The bulkfile supplies ARES with the form of each record in the file.  All
    incoming data is converted as necessary to match the description of the
    target column in the table.  Filler columns are ignored.
 3. If expression-list is not specified, the number of columns in the table
    must equal the number of non-filler columns in the bulkfile.  The columns
    in the bulkfile will be matched positionally to the columns in the table.
 4. If expression-list is specified, the number of expressions must equal the
    number of columns in the table.  Columns in the bulkfile, constants and
    scalar functions are all legal elements in the expressions.  The
    expressions in expression-list will be matched positionally with the
    columns in the table.
 5. If necessary, the last column in a bulkfile will be padded with blanks to
    fulfill the bulkfile description.  This will only be done if the column is
    of type CHARACTER, and the record is long enough to contain at least one
    character of the last column.
 6. Any record in the file that does not match the bulkfile description is
    automatically skipped.  Messages telling which records were skipped may be
    requested by specifying SET INFORM SKIP=ON.
 7. If a large number of records are loaded into a table which has secondary
    keys, significant performance advantages can be gained by using BEGIN
    MODE=LOAD. This causes all of the records to be physically loaded into the
    table before the alternate key structures are built or updated.
 8. DATE and TIMESPAN data is converted according to the default formats.
    Formats established by the SET command are not used, so that stored LOAD
    commands will function correctly regardless of the format currently set.
    The FORMAT built-in function may be used in the expression-list to format
    DATE and TIMESPAN data as character string representations which differ
    from the default format picture.  Conversely, the DATE and TIME built-in
    functions may be used to convert a character string representation of a
    DATE or TIMESPAN value to a DATE or TIMESPAN datatype field according to
    the specified picture.
See also:
CREATE_BULKFILE, SET_INFORM, SET_OVERWRITE
00002
00001
00003
00004
LOAD
Syntax:
LOCK fid [COMMENT = literal]
Parameters:
 
fid  a file name which identifies the model to lock.
 
literal  a comment pertaining to the LOCK command enclosed in single
    quotes.  The length of the COMMENT is limited by the length of the
    literal plus the model name.  A subsequent LOCK command either
    redefines or clears the COMMENT.
Description:
The LOCK command allows a user with CREATOR privilege to prevent other users
from accessing the model.  Only users with CREATOR privilege are allowed to
access the model until it is unlocked.
Rules:
 
 1. You must have CREATOR privilege to issue the LOCK command.
 2. The command waits until there are no longer any exclusive users of the
    model.
 3. The LOCK command will not affect users who are currently in invoke mode
    using the database.
See also:
UNLOCK Command
00002
00001
00003
00004
As each user accesses a record, it is locked (ENQed) so that other users can
access, but not update it.  When an update on a record is issued, that record
is locked so other users cannot access it.  Users trying to read records that
are locked for update by another user, or update records that are locked for
read by another user, are put in a wait state, and can only proceed when the
other user gives up their record locks.  Record locks are kept as long as the
transaction is active.  When the transaction is completed by either a COMMIT
or ABORT, or when a CHECKPOINT or ROLL BACK is issued, the record locks are
released.  At this point, any user waiting for records to be unlocked resumes
running.
 
Locking can cause a deadlock situation to occur.  A deadlock occurs when two
users each have a record locked for update and each is trying to read the
record the other has already updated.  Each user is waiting for the other user
to give up a lock.  Neither user can give up a lock since they are both put in
a wait state until a lock is released.  The situation continues indefinitely
unless some of the locks are released.  This is done by choosing the user with
the least number of locks outstanding, and giving that user a deadlock
condition.  When a deadlock condition occurs, ARES automatically issues a ROLL
BACK command (see TRANSIENT_JOURNAL), and releases the record locks allowing
other users to continue.  The rolled back user must reissue all update
commands.
LOCK
Syntax:
[NOT]  {algebraic-expression1 comparison-operator algebraic-expression2}
 
       {algebraic-expression3 [IS] [NOT] BETWEEN algebraic-expression4
             AND algebraic-expression5                                 }
 
       {algebraic-expression6 [IS] [NOT] IN (constant-list)            }
       {algebraic-expression7 [IS] [NOT] LIKE pattern                  }
       {algebraic-expression8 [NOT] CONTAINS algebraic-expression9     }
       {algebraic-expression10 [IS] [NOT] NULL                         }
 
  [logical-operator logical-expression]
Parameters:
algebraic-expression1,2,3,4,5,6,7,8,9,10  as described under
    ALGEBRAIC_EXPRESSIONS.
 
comparison-operator  any of the following: >, >=, =>, <, <=, =<, =, ~=.
 
constant  an arithmetic or character constant.
 
constant-list  a list of constants separated by commas.
 
logical-operator  either AND or OR.
 
pattern  a pattern string containing wildcard characters as described
    below.
Description:
A logical-expression is a combination of algebraic-expressions, comparison-
operators, logical-operators, constants and parentheses.  logical-expressions
always produce a result of either TRUE or FALSE. Again, as in algebraic-
expressions, the column-id in a logical-expression need not be contained in
the same table.  The symbols for the comparison- and logical-operators are
summarized in the following table.  As before, the precedence is indicated by
the magnitude of the associated number.
 
      Operator     Meaning                                    Precedence
      -------------------------------------------------------------------
       =           True if algebraic-expression1 equals           4
 
                   algebraic-expression2.
      -------------------------------------------------------------------
       ~=          True if algebraic-expression1 is not           4
 
                   equal to algebraic-expression2.
      -------------------------------------------------------------------
       >           True if algebraic-expression1 is               4
 
                   greater than algebraic-expression2.
      -------------------------------------------------------------------
       => or >=    True if algebraic-expression1 is greater       4
 
                   than or equal to algebraic-expression2.
      -------------------------------------------------------------------
       <           True if algebraic-expression1 is less          4
 
                   than algebraic-expression2.
      -------------------------------------------------------------------
       <= or =<    True if algebraic-expression1 is less          4
 
                   than or equal to algebraic-expression2.
      -------------------------------------------------------------------
       BETWEEN     True if algebraic-expression3  is greater      4
 
                   than or equal to algebraic-expression4
 
                   and is less than or equal to
 
                   algebraic-expression5.
      -------------------------------------------------------------------
       NOT BETWEEN True if algebraic-expression3  is less         4
 
                   than algebraic-expression4  or greater
 
                   than algebraic-expression5.
      -------------------------------------------------------------------
       IN          True if algebraic-expression6  is              4
 
                   equal to any of the constants in
 
                   constant-list.
      -------------------------------------------------------------------
       NOT IN      True if algebraic-expression6  is not          4
 
                   equal to any of the constants in
 
                   constant-list.
      -------------------------------------------------------------------
       LIKE        True if algebraic-expression7  matches         4
 
                   the pattern.
      -------------------------------------------------------------------
       NOT LIKE    True if algebraic-expression7  does            4
 
                   not match the pattern.
      -------------------------------------------------------------------
       CONTAINS    True if the character string generated by      4
 
                   algebraic-expression9 is contained in the
 
                   character-string generated by
 
                   algebraic-expression8.
      -------------------------------------------------------------------
       NULL        True if the value is null.                     4
      -------------------------------------------------------------------
       NOT NULL    True if the value is not null.                 4
      -------------------------------------------------------------------
       NOT         Reverses the truth value of the                3
 
                   logical expression that follows.
      -------------------------------------------------------------------
       AND         True if the logical expressions on             2
 
                   both sides of the AND are true.
      -------------------------------------------------------------------
       OR          True if the logical expressions on             1
 
                   either side of the OR are true.
 
Parentheses may be used to change the standard precedence.  Examples of valid
logical expressions are:
 
    PNAME=22
    INFO.RADIUS1~=INFO.RADIUS2
    PNUMBER=10 AND (ENAME='JONES' OR ENAME='SMITH')
    ENAME~='SMITH' AND PNUMBER IS BETWEEN 20 AND INFO.RADIUS1
 
The LIKE operator tries to match the contents of the column with the pattern.
The pattern may contain any alphanumeric character, however, special meanings
are reserved for the underscore (_) and the question mark (?), which are
wildcard characters.  The underscore matches any single character in a column,
while the question mark matches any string of zero or more characters.  Thus,
a constant of "A?" would match the contents of a column that started with a
capital letter A. Any combination of underscores or question marks is valid.
Trailing blanks are stripped from the pattern string and ignored.
Example:
SELECT NAME FROM EMP WHERE NAME LIKE 'A?D_E'
 
This example finds all names that start with "A", followed by an arbitrary
number of characters, followed by a "D", followed by one character, followed
by an "E".
 
The CONTAINS operator searches a character string to see if it contains
another character string.  The character strings can be generated using
arbitrary algebraic-expressions.  For example, if one column contains first
names and the other full names, the two columns can be matched as follows:
 
    FULL_NAME CONTAINS FIRST_NAME
 
The NULL operator only has meaning for function variables.  If it has not been
INITed or assigned to, a function variable is NULL. The NULL operator is
accepted in other expressions but will always be false.
 
When evaluating logical-expressions, the following special rules apply for
character string operations:
 1. When comparing two character strings the CP-6 ASCII collating sequence is
    used (see HELP (IBEX) ASCII).
 2. When comparing two character strings of fixed length, or a fixed and
    varying length string, the shorter string is blank filled to the right
    until the strings are of equal length.
 3. When comparing two character strings of varying length, no filling is
    performed.  In order to be equal, two varying strings must have the same
    length and the same content.
 4. logical-expressions may be used in either the WHERE clause of the SELECT,
    DELETE, and UPDATE commands, or in certain clauses within the CREATE
    FUNCTION command.
00002
00003
00001
RELATED_MANUALS
API_MEMORY
There are two primary uses for the FROM clause:
 
o   Identify default table names to use while distinguishing column names.
o   Assign table variable names to tables that are logically duplicated.
 
Another use for the FROM clause is to force tables to appear as part of the
result.
 
Assume a database with two tables.  The user might want to match each record
from the first table with every record of the second.  The sets of records can
be subsets of their respective tables, but there is no logical restriction on
the combinations of records to be applied.  This is accomplished by including
the desired tables in the FROM clause.  All combinations of these tables are
tried and the WHERE expression is evaluated.  If true, the records used in
that combination are contributed to the overall result produced by the query.
 
Below is a sample table containing the location of cities.
 
 : SELECT * FROM LOCATION
   .. 4 records SELECTed.
 CITY       LAT_D LAT_M LAT_NS LON_D LON_M LON_EW
 ---------- ----- ----- ------ ----- ----- ------
 BOSTON        42    15 N         71     7 W
 DC            38    50 N         77     0 W
 DENVER        39    44 N        104    59 W
 DES MOINES    41    35 N         93    37 W
 
To compose a mileage chart for those cities in the Northern Hemisphere, the
user must compare all such cities to all other cities, and compute the
distance based on latitude and longitude.  shown below computes the desired
distances.  Note that the WHERE expression restricts each city's latitude to
be in the Northern Hemisphere but does not contain any expression that relates
the two instances of the table containing cities.  Thus, the records of the
tables referenced in the FROM expression are combined in all possible ways.
 
 : SELECT L1.CITY,L2.CITY,DIST(L1.LAT_D,L1.LAT_M,L1.LAT_NS,;
 +                             L1.LON_D,L1.LON_M,L1.LON_EW,;
 +                             L2.LAT_D,L2.LAT_M,L2.LAT_NS,;
 +                             L2.LON_D,L2.LON_M,L2.LON_EW);
 + FROM LOCATION L1,LOCATION L2;
 + WHERE L1.LAT_NS='N' AND L2.LAT_NS='N'
   .. 16 records SELECTed.
 CITY       CITY          3
 ---------- ---------- ----
 BOSTON     BOSTON        0
 BOSTON     DC          398
 BOSTON     DENVER     1747
 BOSTON     DES MOINES 1157
 DC         BOSTON      398
 DC         DC            0
 DC         DENVER     1473
 DC         DES MOINES  900
 DENVER     BOSTON     1747
 DENVER     DC         1473
 DENVER     DENVER        0
 DENVER     DES MOINES  593
 DES MOINES BOSTON     1157
 DES MOINES DC          900
 DES MOINES DENVER      593
 DES MOINES DES MOINES    0
SELECT_MINUS
Several miscellaneous commands are available to the user.  They perform the
following functions:
 
   Set or return the setting of operational flags
   Provide information
   Correct other commands
 
The first group allows the user to control certain characteristics of an ARES
session.  This includes redirecting output from ARES and setting user
controllable flags.
 
The second group allows the user to extract information about various elements
of the database.  With these commands the user can list the format of a
specific column contained in the database, or the layout of a particular
table.
 
The third group allows the user to correct mistakes or otherwise modify a
command that has already been issued without reentering the command from
scratch.
 
The commands belonging to these three groups are summarized in the following
table:
 
             Command   Description
 
             DIRECTORY Change the default account and packset
 
             DISPLAY   Show the description of a database element
 
             DO        Execute an IBEX system command
 
             ENTER     Start execution of an ADAPT dialogue
 
             HELP      Print online information
 
             LIST      List items in a database
 
             OUTPUT    Redirect ARES output
 
             READ      Read and execute a file of ARES commands
 
             RR        Reread the last command
 
             SET       Set a user controllable flag
All files created on behalf of the user begin with the model name chosen by
the user.  Appended to that is a single character and another name.  The
single character distinguishes the database description from the user's
tables.
 
All database description file names are appended with an underscore (_).
Following the underscore is the name of the various components that make up
the description of the user's database.
 
User's table names are preceded with a dash (-) and appended to the model
name; one file is created for each table created by the user.
 
Each file created initially uses one granule of storage.  Add to that one
granule for each key (including the primary) specified in the model
description.  The database description utilizes two files and five granules of
storage.  For example, if the user creates a database with three tables and
six keys (including the primary key), nine granules for the tables plus five
granules for the database description are allocated from the user's account.
Of course, as the database grows, the number of granules used also grows.
Following is a sample of ARES generated file names:
 
EXAMPLES-EMP            EXAMPLES-LOCATION       EXAMPLES-SALARY_RANGE
EXAMPLES-SALES          EXAMPLES_MOD            EXAMPLES_RTD
 ..    6 files listed
 
 1. The files of the form "EXAMPLES-" correspond to the tables that are part
    of the database (in this case EMP, LOCATION, SALARY_RANGE, and SALES are
    all tables in the database EXAMPLE).
 2. The files of the form "EXAMPLES_" are used by ARES to represent the
    structure of the database (the table names, the column names and their
    data types, what keys exist, etc.).
The ARES relational database management system consists of five basic command
modes.  The five basic modes are:
 
   CREATE: Creating a database description (or model)
   ALTER: Altering the database description
   DROP: Deleting the database
   INVOKE: Accessing the database
   SPECIAL: Commands that function in all modes
 
For additional information see:
HELP (ARES) CREATE_MODE
HELP (ARES) ALTER_MODE
HELP (ARES) DROP_MODE
HELP (ARES) INVOKE_MODE
HELP (ARES) SPECIAL_MODE
 
Upon entering the ARES processor, the first step is to determine what mode of
operation will be used.  A command can then be issued by the user to enter
that mode.  The commands to enter the various modes within ARES are:
 
   CREATE MODEL
   ALTER MODEL
   DROP MODEL
   INVOKE
 
In the first three modes, commands are entered and checked for correctness but
are not immediately processed.  Once a set of commands has been entered
(regardless of the mode), the user must issue the COMMIT command, which causes
the commands to be processed, or the ABORT command, which nullifies the effect
of the previous commands.  In the invoke mode, commands are processed as they
are entered.
Multiple users can only access a model simultaneously if they are all in
invoke mode.  In all other instances, each user must wait for use of the
model.  Users who are invoking, locking, or unlocking the model must wait
until non-invoke, non-lock, and non-unlock users are finished.  All other
users must wait for exclusive use of the database.  When issuing a command,
ARES automatically waits until access to the database is allowed.
 
For additional information see:
HELP (ARES) INVOKE_MODE
ALTER_MODE
CREATE_MODE
DROP_MODE
INVOKE_MODE
Specifying MODE=IN restricts DML commands to retrieve data only.  Thus, ARES
knows that it is safe to allow sharing with other users that specified
SHARE=IN. MODE=UPDATE allows any DML commands to be issued.  Therefore it is
only safe to allow sharing with other users that specified SHARE=ALL.
MODE=LOAD is a special mode that allows more efficient loading of large
quantities of data.  It automatically sets SHARE=NONE for efficiency reasons.
 
Since SHARE=NONE when MODE=LOAD , mixing data retrieval commands with data
load commands may greatly decrease the efficiency of the load commands.  This
is due to the fact that under the conditions of SHARE=NONE the file cannot be
shared with other users and in this case you must share it with yourself.  For
example, if ARES_BEGIN is called with MODE=LOAD in an API program and then a
call to ARES_START or ARES_STARTEXT is made with MODE=INPUT for the same
table, the file will be closed for load mode (alternate keys will then be
rebuilt) and reopened for input.  If the input query is completed the file
will again be closed and reopened for load mode.  If such a sequence takes
place in a loop, the efficiency level drops dramatically and is actually worse
than if you just specify MODE=UPDATE in the first place (because of all the
alternate key rebuilds).
 
The following table may be used to determine how and when tables can be shared
within a model.
 
                                USER 2
      MODE                    IN                      UPDATE
            SHARE    NONE  IN    ALL   ANY     NONE  IN    ALL   ANY
            ---    --  -    --   --     --  -    --   --
        IN  NONE      -     -     -     -        -    -     -     -
U           IN        -     Y     Y     Y        -    -     -     -
S           ALL       -     Y     Y     Y        -    Y     Y     -
E           ANY       -     Y     Y     Y        -    Y     Y     Y
R
    UPDATE  NONE      -     -     -     -        -    -     -     -
1           IN        -     -     Y     Y        -    -     -     -
            ALL       -     -     Y     Y        -    -     Y     -
            ANY       -     -     -     Y        -    -     -     -
 
Sharing tables is not a transitive operation.  If user A can share with user
B, and user B can share with user C, it is not always the case that user A can
share with user C.
 
For example, if user A starts a transaction with MODE=IN, SHARE=IN, user B
with MODE=IN, SHARE=ANY, and user C with MODE=UPDATE, SHARE=ANY the
aforementioned case arises.  A and B are allowed to run together, and B and C
are allowed to run together, but if users A and C try, whichever user attempts
first, accesses the tables and locks the other user out until the transaction
is completed.
 
For additional information see:
SHARING_TABLES
SPECIAL_MODE
GRANT_NONE
When designing a database layout, one of the primary objectives is to
accurately represent the relationships between pieces of data.  To this end,
the theory of normalization has been developed.  Although a complete
discussion of normalization is beyond the scope of this  file, some discussion
is appropriate here.
 
Any time a relationship is stored more than once, the possibility arises that
the copies of the relationship will get out of sync.  For example,  as shown
below we have employees, departments and locations.  If we wanted to change a
department's location, we must update every employee record.  If we
erroneously updated only some of them, we could no longer tell what the
relationship between the department and location was.  To solve the problem,
we can split the table into two separate ones (normalize them) as shown below.
Now, each department and location is stored only once.
 
: SEL ENAME,DNAME,LOC FROM COMPANY
  .. 4 records SELECTed.
ENAME DNAME   LOC
----- ------- ---------
CLARK FINANCE CLEVELAND
JONES ISD     NEW YORK
SMITH FINANCE CLEVELAND
WARD  FINANCE CLEVELAND
 
: SEL ENAME,DNAME FROM EMP
  .. 4 records SELECTed.
ENAME DNAME
----- -------
CLARK FINANCE
JONES ISD
SMITH FINANCE
WARD  FINANCE
: SEL DNAME,LOC FROM DEPT
  .. 2 records SELECTed.
DNAME   LOC
------- ---------
FINANCE CLEVELAND
ISD     NEW YORK
 
There are many other types of duplicate relationships between data.  The
theory of normalization is devoted to identifying and eliminating them.
Before undertaking the design of a large production database, it is
recommended that the designer have a basic understanding of normalization.
One interesting side effect of normalization is that it sometimes causes a
slight increase in storage requirements.  As in our example, we now have
stored each department name twice.  If there are many employees per
department, this will still be an overall savings, but if the average number
of employees per department is less than two, this will be an increase.
 
To eliminate such data duplication, we can use artificial department numbers
to represent the departments.  Now, only the numbers are duplicated (for
CODASYL users, consider these artificial numbers as taking the place of
pointers).    This is shown below:
 
: SEL ENAME,DNUM FROM EMP
  .. 4 records SELECTed.
ENAME DNUM
----- ----
CLARK    1
JONES    2
SMITH    1
WARD     1
: SEL DNUM,DNAME,LOC FROM DEPT
  .. 2 records SELECTed.
 
DNUM DNAME   LOC
---- ------- ---------
   1 FINANCE CLEVELAND
   2 ISD     NEW YORK
The following table shows the notation conventions used in this manual to
describe commands, statements, directives, and other language elements.
 
    Notation               Description
 
    Lowercase Letters      Lowercase letters indicate that the element is
                           a variable, to be replaced with the desired
                           value.
 
    Capital Letters        Capital letters indicate a literal, to be
                           entered as shown.
 
    Special Characters     Special characters are literals, to be entered
                           as shown.
 
    Numerals               Numerals standing alone are literals, to be
                           entered as shown.
                           Numerals embedded in or affixed to a string of
                           capital letters are also literals, to be
                           entered as shown.
                           Numerals embedded in or affixed to a string of
                           lowercase letters are part of the variable
                           name to be replaced with a desired value, for
                           example fid1.
 
    Brackets               An element inside brackets is optional.  If
                           elements are stacked vertically within
                           brackets, the elements may be omitted or one
                           of them may be entered.  The brackets may be
                           elongated to contain the stack of elements, or
                           may be represented by vertically stacked,
                           printed brackets.  Example:
                               [PACKED  ]  or  [PACKED|UNPACKED]
                               [UNPACKED]
                           means that the user may omit this entry, or
                           may enter PACKED, or may enter UNPACKED.
                           When used to enclose portions of keywords,
                           brackets signify that the bracketed portion
                           may be omitted, or truncated at any point.
                           For example, the notation K[EY] means that the
                           user may enter K, KE, or KEY.
 
    Braces                 Elements stacked inside a pair of braces
                           identify a required choice.  The braces may be
                           elongated to contain the possible choices, or
                           may be represented by vertically-stacked
                           printed braces.  Example:
                               {id }
                               {ALL}
                           means that either the value for id or the word
                           ALL must be entered.
                           Alternatively, the vertical OR bar is used to
                           separate the choices, thus:  {id|ALL}
 
    OR Bar                 The OR bar separates elements in a list from
                           which one element may be, or must be, chosen.
                           Thus, {A|id} means that either the letter A or
                           the value of id must be entered.
 
    Horizontal Ellipsis    The horizontal ellipsis indicates that a
                           previous bracketed element may be repeated, or
                           that elements have been omitted.  Example:
                               name [, name] ...
                                        or
                               name1[, name2] ...
                           means that one or more name values may be
                           entered, with commas inserted between the name
                           values.
A numeric constant can be an integer or real value.
 
An integer constant is a string of decimal digits preceded by an optional
sign.  Integer constants range from -(2**35) to (2**35)-1.
 
A real constant differs from an integer constant by having a decimal point, an
exponent, or both.  The exponent follows the numeric value and consists of the
letter E followed by a signed or unsigned integer that represents the power of
ten by which the numeric value is to be multiplied.  Real constants range from
(4.661)*(10**(-156)) to (8.379)*(10**152) with 7 significant digits.  The
following forms are permissible:
 
     n.m          n.           .m
     n.mE[+|-]e   n.E[+|-]e    nE[+|-]e
 
where n, m, and e are each integers.
Each table created by the user is represented by its own indexed relational
file (refer to the CP-6 Monitor Services Reference (CE74 and CE75), for more
information about indexed relational file organization).  Of importance is the
fact that the records in an indexed relational file can be accessed directly
by key.  Each record is uniquely identified by the value of the primary key.
The primary key is indicated in the KEY IS PRIMARY clause of the CREATE TABLE
or ALTER TABLE command.
 
In addition, secondary (also known as alternate) keys can be created (again in
the CREATE TABLE or ALTER TABLE command).  These keys provide further direct
access paths into the records of the table.
 
When a DML command is issued, ARES looks at the tables and columns referenced
in the command.  It then identifies those that are keys to see if it can take
advantage of them.  The more keys found, the more ARES performance can be
optimized.  If no key can be found, ARES is forced to sequentially scan the
tables.
 
It may seem that the best way to organize the tables is to make all fields
keys.  This is not always true.  Maintaining keys can be expensive.  Each
update to a table must not only write the new record, but find all the key
values that have changed, remove the old pointer from the key value to the
record, and insert the new pointer from the key value to the record.  If the
primary access to the table is for updating, this actually reduces the
performance of the database.  Thus, the user should properly balance the
database description to reflect the common usage of the database.
 
When considering candidates for keys, certain aspects must be considered.  The
first is that the more duplicates that appear within a column (or group of
columns), the less useful that column is as a key.  For example, in a table
that has GENDER as a column, a key on that column is not that useful.  It
divides the table into two halves:  males and females.  If a DML command is
issued using this key, it only reduces the number of records accessed by one
half.  On the other hand, ARES must traverse the tree structure representing
the key for each access to the table.  This could make it more expensive to
use the key than to access the table sequentially.
 
Using another example, a table has DEPARTMENT as a column and a key on that
column.  If there are a number of departments in the company being
represented, the table has been effectively split into many small parts, each
of which can be directly accessed.  In this case, the additional overhead of
traversing a tree that represents the key is more efficient because is reduces
the number of records accessed.
 
Users should also note the difference between creating many individual keys,
and one key that contains a number of fields.  In many cases two or more
fields are commonly used together when DML commands are issued.  In a tax
table, a user might frequently ask questions specifying number of deductions
and salary.  Assume there is a key on each of these fields and a DML command
is issued.  ARES must choose one of the keys.  Either one might be better than
not using a key at all, but an even better choice is to create a key that
combines the two columns.  Then, if a command is issued that specifies values
for both, they can be combined and directly access those records that have
both required values.  In addition, the user may still use the column that
first appears independently in the key.  If only that value is specified, the
combined key may still be used to directly access the records of interest.
It should be noted that a particular column can be involved in many keys.  It
can be an individual key, the second column of one multiple-column key, and
the fourth column of another multiple-column key.  The tradeoff is that
updates become slower as more keys are created.
OPTIMIZATION
Syntax:
OPTIMIZE table-name
Parameters:
 
table-name  the name of the table for which statistics are to be
    collected.
Description:
The OPTIMIZE command is used to update the statistics that ARES keeps for each
table.  These statistics provide information about a table and its keys and
are used by ARES to determine the most efficient way to execute a DML command.
The statistics should be updated for tables which have been altered
significantly due to INSERT, LOAD, UPDATE, and DELETE commands.  Updating
statistics requires scanning all the rows and keys of a table.  This can be
relatively time consuming and it is not recommended that statistics be updated
frequently for a large table.
Rules:
 
 1. The DISPLAY STATS command helps to determine whether or not the The DI
    STATS command (see STATS) helps to determine whether or not the current
    statistics for the table need to be updated.  When the number of records
    which have been updated since the last OPTIMIZE command becomes
    significant relative to the table size (greater than about one third), the
    information that ARES is using for query optimization is likely to be out
    of date and may cause poor query execution paths to be chosen.
 2. The OPTIMIZE command rebuilds the file to make maximum use of the disk
    space it occupies, and to place the records in order physically by primary
    key.  This requires that the user have temporary disk space available
    equal to the size of the table being optimized.
 3. The statistics which are gathered by the OPTIMIZE command are primarily
    used for optimizing queries which can make use of secondary keys.  A table
    which has no secondary keys will only benefit from optimization if the
    records in the table were inserted out of order by primary key, and the
    records are out of order physically.
 4. Any ALTER of a table which results in rebuilding the table (i.e., column
    addition, deletion, or change of data type, or any key modification) will
    also bring the statistics up to date.
See also:
DISPLAY_STATS
00002
00001
00003
00004
OPTIMIZE
SELECT_ORDER
Syntax:
 
       [[OVER] LP[@location]      ]
OUTPUT [[INTO] fid [(option-list)]]
       [[ON  ] ME                 ]
       [[TO  ]                    ]
Parameters:
 
fid  any valid CP-6 file identifier.
 
ON or TO  indicates to only honor the OUTPUT command if the file does not
    already exist.
 
OVER  indicates to honor the OUTPUT command whether or not the file
    exists.
 
INTO  indicates to merge the result of the OUTPUT command into the file if
    it exists, or to create a new one if it does not.
 
LP  directs output to the default line printer; @location specifies a
    specific line printer.
 
ME  returns the output destination to the user's terminal.
 
option-list  list of the following options separated by commas:
        O[RGANIZATION]={C[ONSECUTIVE]|U[NIT]R[ECORD]}
        F[ORM]={fprmname|'formname'}
        I[XTNSIZE]=number
        X[TNSIZE]=number
Description:
The OUTPUT command is used to direct all ARES output to a destination.
Rules:
 
 1. OUTPUT with no options redirects ARES output to the original output
    destination.
 2. Output can be directed to any valid file name (fid).  If none of ON, TO,
    OVER, or INTO is specified, ON will be assumed.
00002
00001
00003
OUTPUT
Normally, only the model creator and those users granted permission by the
creator can access a model.  At times, the need arises to override the normal
security mechanism.  For example, if the logon account of a model's creator is
deleted, it should be possible to assign a new creator without having to
redefine the original logon account.
 
A user authorized with FMSEC privilege may override the ARES access mechanism
by issuing the following command before invoking ARES:
 
    SWITCH O'52500000'
 
The user is given CREATOR privilege to any model accessed under these
conditions.
ARES (A RElational System) is a relational database management system designed
to simplify the task of managing computer stored data.  ARES uses English-like
sentences (commands or queries), which make database definition, data query,
and data manipulation easy to use, even for those who have little or no
knowledge of computer programming.  This simplicity and ease of use makes the
ARES database accessible to a broad class of users, thus enhancing the
productivity of the people who work with the database.
 
The ARES relational database management system achieves the following goals:
 1. Removes the need for special data processing or programming skills in
    order to use the database.
 2. Provides a non-procedural query language which allows greater flexibility
    and ad hoc reporting capabilities.
 3. Reduces the time necessary to create a database.
 4. Reduces the time required to change a database description.
 5. Reduces the impact of changes to the database description.
 6. The data is independent of data application; changes in data or data usage
    do not require costly program modifications.
 7. Provides a database security mechanism based on logical operations on the
    data.
 
A relational database management system provides centralized data, organized
into tables accessible (within access control limits) to many users.  Some of
the advantages are:
 1. Greatly reduces redundancy of data and application programs.
 2. Minimizes data inconsistency; data relationships are contained in the
    database.
 3. Data is independent of program format and can therefore be shared.
 4. Data is stored in a centralized location, making it easier to maintain
    standards, security, and integrity.
 
For additional information see:
HELP (ARES) TOPICS
HELP (ARES) GETTING_STARTED
HELP (ARES) COMMANDS
HELP (ARES) FUNCTIONS
 
For additional information on how to use HELP see:
HELP (ARES) HELP
SET_OVERWRITE
FORMAT_PAGE
API_PL6
Syntax:
 
                  [[OVER] LP[@location]      ]
PRINT [ [NEXT] n] [[INTO] fid [(option-list)]]
                  [[ON  ] ME                 ]
                  [[TO  ]                    ]
Parameters:
 
fid  any valid CP-6 file identifier.
 
n   specifies the number of records to print.
 
ON or TO  indicates to only honor the PRINT command if the file does not
    already exist.
 
OVER  indicates to honor the PRINT command whether or not the file exists.
 
INTO  indicates to merge the result of the PRINT command into the file if
    it exists, or to create a new one if it does not.
 
LP  directs output to the default line printer; @location specifies a
    specific line printer.
 
ME  returns the output destination to the user's terminal.
 
option-list  list of the following options separated by commas:
        O[RGANIZATION]={C[ONSECUTIVE]|U[NIT]R[ECORD]}
        F[ORM]={fprmname|'formname'}
        I[XTNSIZE]=number
        X[TNSIZE]=number
Description:
The PRINT command is used to reprint the results of the previous query without
re-executing the query.
Rules:
 
 1. The user may specify a change in FORMAT or OUTPUT and PRINT the query
    results as many times as desired.  The result of the previous query is
    destroyed when any DML or mode change command is issued.
 2. If the optional destination fid is specified, the current output
    destination is overridden while the result is printed.
 3. If no options are specified, all records in the result are printed.
 4. If NEXT is not specified, n records will be reported starting from the
    beginning of the result.
 5. If NEXT is specified, n records will be reported starting with the record
    following the last record reported.
 6. Specifying n as zero without the NEXT option will position to the
    beginning of the result and will not report any records.
 7. All other FORMAT options will be honored for the records printed when n is
    specified.
 8. Any totals printed will reflect the total of all data up to the current
    record printed when n is specified.
 9. Any FORMAT command specified will position to the beginning of the result.
00002
00001
00003
PRINT
LIST_PRIVS
GRANT_PROGRAM
Since two tables may be referenced in a given ARES command, ambiguities may
arise when referencing columns.  If the same column name exists in both (as
when table variables are used), the simultaneous use of those tables causes
any reference to the common column name to be ambiguous.
This problem is resolved by qualifying the column name with a table name in
one of two ways.  Any table mentioned in the FROM clause is automatically a
default table name for any unqualified columns.  Therefore, if the column is
unique within the tables listed in the FROM clause, there is no need to
qualify it further.  If, on the other hand it is still ambiguous, the column
name can be preceded with that table name and a period as a separator (e.g.,
table-name.column-name) to distinguish it from other columns.
END
Syntax:
READ fid
Parameters:
 
fid  is a disk file containing valid ARES commands.
Description:
The READ command reads and executes a file of ARES commands.
Rules:
 
 1. A READ file may contain a READ command.  READ nesting may be continued 10
    levels deep.
 2. The IBEX ECHO flag controls whether or not to echo commands to the user as
    they are read from the file.  !ECHO and !DONT ECHO may be entered as ARES
    commands to control this action.
Example:
 
    READ COMMAND_FILE
 
means read the ARES commands contained in the file COMMAND_FILE.
00002
00004
00001
00003
READ
Syntax:
RECONSTRUCT fid
Parameters:
 
fid  a file name which identifies the model to reconstruct.
Description:
The RECONSTRUCT command attempts to properly complete an aborted ALTER,
CREATE, or DROP MODEL operation.  The user should verify that the
reconstructed database is operational.  If RECONSTRUCT is unsuccessful, report
via STARLOG and do not attempt any further use of the database.
Rules:
 
 1. The fid must specify the name of a previously created model.
 2. If the model was created with a password, that password must be specified
    in the fid or the command is aborted.
 3. The command waits until exclusive use of the model is available.
00002
00001
00003
RECONSTRUCT
Following is the list of related manuals:
           HA01  CP-6 Introduction to ARES
 
           HA02  CP-6 ARES Reference
 
           HA09  CP-6 Introduction to ARGENT
 
           HA10  CP-6 ARGENT Reference
 
           HA12  CP-6 ADAPT Reference
 
           HA16  CP-6 X Account Pocket Guide
 
           HA20  CP-6 System Support Reference (A-P)
 
           HA21  CP-6 System Support Reference (Q-Z)
 
           HA22  CP-6 System Support Reference (Appendices)
 
           CE40  CP-6 Programmer Reference
 
           CE58  CP-6 Monitor Error Message Reference
 
           CE61  CP-6 Customer Support Handbook
 
           CE74  CP-6 Host Monitor Services Reference (Descriptions)
 
           CE75  CP-6 Host Monitor Services Reference (Structures)
Syntax:
RENAME COLUMN column-name1 TO column-name2 [IN table-name]
Parameters:
 
column-name1  an ARES column name that already exists.
 
column-name2  an ARES column name.
 
table-name  the name of an existing table in the database.
Description:
The RENAME COLUMN command allows the user to rename columns within an ARES
model.  Renaming does not cause any physical changes in the table.
Rules:
 
 1. The column-name1 parameter must specify the name of a column which exists
    in a table within the model.
 2. If column-name2 already exists, its data types must be the same as those
    of column-name1.  In this case, any HEADING or COMMENT field associated
    with column-name1 will be associated with column-name2, unless a HEADING
    or COMMENT field already exists for column-name2.
 3. If the IN clause is specified, column-name1 is only renamed to
    column-name2 within the table identified by table-name.
 4. In invoke mode, columns belonging to permanent tables cannot be renamed.
00002
00001
00003
RENAME_COLUMN
Syntax:
REPORT using-clause [report-options]
Parameters:
 
report-options  valid options for the ARGENT REPORT command.
 
using-clause  a valid using-clause for the ARGENT REPORT command.
Description:
The REPORT command allows the user to pass the current query results to the
report writer.
Rules:
 
 1. The REPORT command will not function if the ARGENT product is not
    available on the user's system.
 2. The last DML command issued must have been a SELECT command.
 3. The using-clause must be specified and must reference a previously defined
    ARGENT workspace.
 
For further information about the report writer, refer to the CP-6 ARGENT
Reference (HA10), the ARGENT on-line HELP facility, or the CP-6 Introduction
to ARGENT (HA09).
00002
00001
00003
REPORT
RR
The following words are reserved for ARES use and are not allowed as the names
of tables, bulkfiles, columns or functions in the database.  In addition, any
abbreviation which is three or more characters long is also reserved, e.g.,
WHE, WHER, WHERE are all reserved words:
 
                           FROM       MINUS  SHOW
 
                           GROUP      NEXT   START
 
                           HAVING     ORDER  UNION
 
                           INTERSECT  PRIOR  WHERE
 
                           LEVEL      SET
 
The following words are reserved for use as ARES built-in functions; no user
function may be identified with one of these names:
 
                            ABS     INDEX   STDEV
 
                            AVG     LENGTH  SUBSTR
 
                            CONCAT  LOWER   SUM
 
                            COUNT   MAX     TIME
 
                            DATE    MIN     UAVG
 
                            FORMAT  SQRT    UPPER
Syntax:
 
       {CREATOR                         }
       {DML                             }
REVOKE {NONE                            } FROM {PROGRAM program-template-list}
       {PROGRAM                         }      {user-template-list           }
       {{ALL           }                }
       {{operation-list} [ON table-list]}
Parameters:
 
operation-list  list of the following operations separated by commas:
 
        SELECT
        INSERT
        UPDATE
        DELETE
 
program-template-list  list of template character strings separated by
    commas.  Each template defines a class of programs that operations are
    being revoked from.  A program template is composed of characters that
    are valid for a CP-6 file and account name plus the wildcard character
    (?).  The ? can only appear as a trailing character in the file name
    portion of the program template.
 
table-list  list of table names that exist in the model.
 
user-template-list  list of template character strings separated by
    commas.  Each user template defines a class of users from whom
    operations are being revoked.  A user template is composed of
    characters that are valid for a CP-6 account name plus the special
    character question mark (?).
Description:
The REVOKE command is used by the database creator to remove privileges that
have been previously granted.  Privileges are checked when the model is
invoked, dropped, altered, or created.  If privileges are revoked, the change
is not seen by the current users of the database until one of these commands
is issued.
Access controls on files should not be modified using PCL. For a discussion of
Access Controls on ARES Files, see ACCESS_CONTROLS
Rules:
 
 1. Each template specified is matched to the templates in the authorization
    records.  For this comparison, the templates are compared as plain
    character strings with no special meaning given to the question mark.
    (Template ABC? does not match template ABCD.)
 2. If a template is specified that does not correspond to an existing
    authorization record, the revoke is rejected.
 3. If a template is specified that corresponds to an existing authorization
    record, the privileges are removed from that record.  If, after the revoke
    is performed, no operations are left in the authorization record, the
    record is deleted.
 4. In any case where the authorization record is deleted, it could cause an
    increase in privileges if the user qualifies under some other
    authorization record that used question marks in its template.
 5. If DML is specified, the ability to store DML in the model is removed.
    Any existing DML commands stored by that user are not affected, although
    the user will no longer be able to modify or delete any DML commands.
 6. If CREATOR is specified, the authorization record that defined the CREATOR
    privilege for the user is deleted.  If the authorization record did not
    indicate CREATOR, the revoke is errored.
 7. If PROGRAM is specified, the ability to run an application program that
    has additional privileges to those given the users, is removed.
 8. If NONE is specified, the authorization record that denied any operations
    to the user is deleted.  If the authorization record did not indicate
    denial, the revoke is errored.
 9. If ALL is specified instead of an operation-list, all existing operations
    are removed from the tables listed in table-list.  If no table-list is
    specified, the template record is removed (as long as it was not a CREATOR
    or NONE template).
10. If operation-list is specified, only those operations specified in
    operation-list are removed.
11. Individual privileges cannot be revoked from a template record that has
    either CREATOR or NONE specified except for the CREATOR and NONE
    privileges themselves.
12. If table-list is specified, the operations are removed for only those
    tables in table-list.  If table-list is omitted, the operations are
    removed from all tables.
13. The operations are removed from only those templates specified in the
    template list.
See also:
ACCESS_CONTROLS, DISPLAY_PRIVS, GRANT
00002
00001
00003
00004
See REVOKE_COMMAND
REVOKE
See REVOKE_COMMAND
See REVOKE_COMMAND
See REVOKE_COMMAND
See REVOKE_COMMAND
Syntax:
ROLL { BACK                                                       }
     { [ MODEL ] model-fid FORWARD [ USING journal-fid    ] [...] }
     {                             [ IGNORING [ERRORS]    ]       }
     {                             [ TO mm/dd/yy,hh:mm:ss ]       }
Parameters:
 
journal-fid  a valid CP-6 file identifier, identifying the common journal.
 
model-fid  a valid CP-6 file identifier, identifying the model.
Description:
The ROLL command is used to roll the common journal forward, or roll the
transient journal back.  In either case, the appropriate journal must exist or
an error will occur.
Rules:
 
 1. The BACK option can only be issued within a transaction that has activated
    the transient journal.  See BEGIN Command for more details.
 2. The BACK option informs ARES to roll back the data in the model using the
    transient journal.  The following actions are taken:
 
   o   Data is restored to the state it was in when the last BEGIN or
       CHECKPOINT command was issued.
   o   All record level locks are released.
   o   Records in the transient journal are erased.
   o   If the common journal is also active, a ROLL BACK record is written.
 3. The FORWARD option can only be specified if a common journal has been
    created (via a CREATE JOURNAL or ALTER JOURNAL command).  The effect of
    this option is to roll the specified model forward using the common
    journal.
 4. If the FORWARD option is specified, the command waits until exclusive use
    of the model is available.
 5. If the USING option is specified, the journal-fid specified identifies the
    common journal to use.  If this option is omitted, the journal identified
    by the last CREATE or ALTER JOURNAL command is used.
 6. If the IGNORING option is specified, the roll forward continues in the
    presence of errors.  If this option is omitted, the roll forward operation
    halts if an error occurs.
 
 7. If the TO option is specified, only those journal records that do not
    exceed the specified date and time will be applied to the model.  If this
    option is omitted, all journal records will be applied to the model.
See also:
ABORT, ALTER_JOURNAL, BEGIN, CHECKPOINT, COMMIT, CREATE_JOURNAL, DROP_JOURNAL
00002
00001
00003
00004
When using ARES from the API, the occurrence of a rollback has implications in
the flow of control of the program.  If a rollback occurs, the programmer must
recognize this situation and reissue all update commands against the database.
 
When a rollback occurs, ARES returns control to the statement following the
most recent call to ARES_BEGIN or ARES_CHECKPOINT within the current
transaction.  This not only returns control to the logical beginning of the
current transaction (so that it may be restarted), but eliminates the need to
check for rollback errors after any other DML call.  It is up to the
programmer to reset any variables or positions within non-ARES files before
continuing with the transaction when a rollback occurs.
For consistency, if a call to ARES_ROLLBACK is issued, control is also
transferred to the statement following the last call to ARES_BEGIN or
ARES_CHECKPOINT.
See ROLL_COMMAND
ROLL
ROLL
ROLL
Syntax:
RR[EAD] [PREVIOUS|label]
Parameters:
 
label  previously created DML label.
Description:
The RR command is used to recall a command, stopping at the end of each line
to permit editing using CP-6 terminal editing functions.  When the command is
completed correctly, it is executed.
Rules:
 
 1. Issuing RR with no label rereads the current ARES DML command.
 2. If PREVIOUS is specified, the command prior to the current command is
    reread.
 3. If a label is specified, the stored DML statement identified by the label
    is reread.
See also:
DISPLAY, DISPLAY_DML, DISPLAY_PREVIOUS
00002
00001
00003
00004
RR
RR
Syntax:
select-expression [ORDER BY order-clause]
SELECT_EXPRESSION:
{(select-expression)                                        }
{ select-statement                                          }
{                   [{MINUS    }                  ]         }
{ select-expression [{INTERSECT} select-expression][, . . .]}
{                   [{UNION    }                  ]         }
SELECT_STATEMENT:
SELECT [ALL|DISTINCT] {*|select-list}
 
    FROM table-name [table-label] [, . . .]
 
        [WHERE constraint-expression1]
 
        [GROUP BY column-list]
 
        [HAVING constraint-expression2]
SELECT_LIST:
{table-label         }
{table-name          }[, . . .]
{algebraic-expression}
ORDER_CLAUSE:
{[table-name. ]            } [ASCENDING ]
{[table-label.] column-name} [DESCENDING] [, . . .]
{      element-number      }
Parameters:
 
algebraic-expression  as described under ALGEBRAIC_EXPRESSIONS.
 
column-list  list of one or more column-names separated by commas.
 
column-name  an ARES column name.
 
constraint-expression  as described under CONSTRAINT_EXPRESSIONS.
 
element-number  constant identifying the position of the element (or
    expression) within the select-list to be used for sorting the result.
 
table-label  alternate name associated with a table in the FROM clause
    which is used as a table variable in the SELECT command.  The old name
    is no longer acceptable within this SELECT command.
 
table-name  ARES identifier specifying the table from which specified
    columns are to be extracted.
Description:
The SELECT command is the primary command used to retrieve data from the
database.  The various forms of the SELECT command retrieve and display data
meeting the specified constraints.  The SELECT statement is the most commonly
used form of the SELECT command.  It is used to specify the conditions under
which data is to be displayed, the form of the data to be displayed, and the
actual data for display.
Rules:
 
 1. The keyword ALL specifies that all of the records retrieved by the select
    should be printed.  ALL is the default.
 2. The keyword DISTINCT specifies that only the unique results be printed
    (duplicates removed).  The default is ALL.
 3. All items in the select-list must be resolvable within the table(s)
    referenced by the associated FROM clause.
 4. If the * option is specified, all columns of the cited tables are
    retrieved.
 5. If the GROUP BY option is specified, it must refer to columns which are
    cited target columns or are contained in the tables listed in the FROM
    clause.  The GROUP BY option is used in conjunction with row functions in
    the select-list.  Records which satisfy the constraint-expression1 are
    sorted on the columns specified by the GROUP BY option.  All records which
    have the same value in all group columns are then considered together for
    calculating the results of the row functions, if any are present.
 6. If only some of the results of the grouping operation are to be included
    in the result, the HAVING clause can be used.  For example, counting up
    the number of employees by department, but eliminating departments with
    only one person can be done by saying "GROUP BY DEPTNO HAVING COUNT
    (EMPLOYEE) >=1".
 7. The ORDER BY option may be specified to sort the final result of the
    select-expression before presenting it to the user.  Columns in the result
    will be sorted in the order specified on the ORDER BY clause.  ASCENDING
    is the default for sorting.
 8. For performance reasons, as much memory as possible should be allocated to
    ARES with the !RES or !ORES command when using the GROUP BY or ORDER BY
    option.
 9. The UNION, INTERSECT, and MINUS operators allow the user to perform set
    operations on the results of multiple select-expressions.
 
    The UNION operator will give a result which contains all of the rows
    selected by both select-expressions.  The INTERSECT operator will give a
    result which contains only those records which were selected by both
    select-expressions.  The MINUS operator will give a result which contains
    all distinct rows selected by the left select-expression, except those
    which were also selected by the right select-expression.  All set
    operators will always return a distinct result.
 
    UNION, INTERSECT, and MINUS operators all have the same precedence and
    thus will be evaluated from left to right (unless forced to do otherwise
    by the use of parentheses).
 
    The entities on either side of the UNION, INTERSECT, or MINUS must be of
    the same cardinality or an error results.  Cardinality is defined as the
    number of columns contained in the select-list of the select-expression
    (either explicitly by naming the columns or implicitly by naming the
    tables).
 
10. When a SELECT command has been completely executed, the result is
    available for the user to display.  If the AUTOPRINT flag is on, the
    result will automatically be formatted and printed.  The user may also use
    the FORMAT, PRINT, OUTPUT, and REPORT commands to control the printing of
    the result.
See also:
FORMAT, OUTPUT, PRINT, REPORT, SET_AUTOPRINT
00006
00004
00005
00007
00008
00001
00003
00002
SELECT
See SELECT_COMMAND
See SELECT_COMMAND
See SELECT_COMMAND
See SELECT_COMMAND
FORMAT_SEPARATOR
UPDATE_SET
Syntax:
 
    {AUTOPRINT [[=]{ON|OFF}]      }
    {CONTINUE [[=]{ON|OFF}]       }
    {SEPARATOR {n BLANK[S]|string}}
    {INFORM [[=]{{ON|OFF}]       }}
    {       { SKIP [[=]{ON|OFF}] }}
SET {OVERWRITE [[=]{ON|OFF}]      }
    {DATE={DEFAULT    }           }
    {     {MODEL      }           }
    {     {date-format}           }
    {TIMESPAN={DEFAULT    }       }
    {         {MODEL      }       }
    {         {time-format}       }
Parameters:
 
date-format  a date format string enclosed in single quotes (see
    DATE_TIME_PICTURES).
 
n   an integer constant.
 
string  a string of alphanumeric characters delimited by single quotes.
 
time-format  a time format string enclosed in single quotes (see
    TIMESPAN_PICTURES)
Description:
The SET command is used to set certain flags and variables.
Rules:
 
 1. The AUTOPRINT option is used to control whether a PRINT command is
    automatically issued after a SELECT is issued.  If ON is specified, any
    time a SELECT command is issued the results are immediately printed before
    an intervening command can be issued.  If OFF is specified, the results
    are not printed until a PRINT command is manually issued.  The default is
    ON.
 2. The SEPARATOR option is used to define what is displayed between the
    columns.  This value is used as a default for all displays but can be
    overridden for a particular display by using the FORMAT SEPARATOR command.
    The BLANK option specifies the number of spaces to be displayed between
    the columns; string specifies the alphanumeric character string to be
    displayed between the columns.  The default is one blank.  The maximum
    length of a separator is 31 characters.
 3. The INFORM option is used to control classes of informational messages.
    If ON or OFF is specified without another option, all INFORM flags are set
    as specified.
 4. The INFORM SKIP option controls the printing of messages about records
    which could not be read from a file during a LOAD operation because of a
    length mismatch.  The default for INFORM SKIP is OFF.
 5. The OVERWRITE option allows INSERT, LOAD, and DUMP commands to overwrite
    existing records with the same primary key.  If reset, overwriting is not
    allowed.  The user must also have UPDATE privilege to the table in which
    the overwrite takes place.  The default for OVERWRITE is OFF.
 6. The CONTINUE option controls the execution of ARES when the user is
    issuing commands in a non-interactive manner (i.e., XEQ, READ). Normally,
    if an error occurs, ARES will exit under these conditions, but if CONTINUE
    is set, ARES will continue processing commands.  The default is OFF.
 7. The DATE option gives ARES a format specification for DATE data.  The
    input of DATE data through the date constant, DATE function or interactive
    INSERT will be affected as will all formatting of SELECT results.  If
    date-format is specified, it will become the current date format
    specification.  If the DEFAULT option is used, the current date format
    specification will be restored to the system default.  LOAD and DUMP
    operations will not be affected, so that bulkfile operations will work
    correctly regardless of the format in effect.  If the MODEL option is
    specified, the current date format specification will be set to the
    model's default if one exists, or to the system default.
 8. The TIMESPAN option gives ARES a format specification for TIMESPAN data.
    The input of TIMESPAN data through the time constant, TIME function or
    interactive INSERT will be affected as will all formatting of SELECT
    results.  If time-format is specified, it will become the current time
    format specification.  If the DEFAULT option is used, the current time
    format specification will be restored to the system default.  LOAD and
    DUMP operations will not be affected, so that bulkfile operations will
    work correctly regardless of the format in effect.  If the MODEL option is
    specified, the current time format specification will be set to the
    model's default if one exists, or to the system default.
 9. Both the DATE and TIMESPAN options can be issued in create or alter mode.
    When issued in these modes, their effect is to establish a default date
    and time format for the model.  These specifications are automatically
    activated whenever the corresponding model is invoked.  The date and time
    formats can be overridden by issuing the appropriate SET command, returned
    to the default for the model by using the MODEL option, and returned to
    the system default by using the DEFAULT option.
See also:
DISPLAY
00002
00001
00003
00004
See SET_COMMAND
SET
See SET_COMMAND. For information on data types, see DATE_DATA_TYPE.
See SET_COMMAND
See SET_COMMAND
See SET_COMMAND
See SET_COMMAND
Specifying SHARE=NONE guarantees that no other user can access the tables at
the same time.  SHARE=IN allows sharing with others who are just reading data
from tables.  SHARE=ALL allows sharing with both readers and updaters.
Specifying SHARE=ANY allows users to share with any other users in a more
efficient manner, but with certain limitations.
 
For additional information see:
SHARING_TABLES
Typically, a large application may have many application programs, each
consisting of many transactions, running simultaneously.  A large percentage
may try to issue updates against the database.  Normally, ARES only allows one
updater to access a table at any given time (locking the table from use by
other users).  If several update programs also read other tables to control
their operation, a struggle for table use will occur.  This situation can
result in a drastic reduction of throughput.  ARES solves this problem by
allowing multiple users to share tables (under the user's control).
 
To achieve maximum simultaneous use of a model, sharing is implemented at the
table level.  This means that two users can update mutually exclusive tables
in the same model without sharing the table being updated with anyone else.
 
When starting a transaction with a BEGIN command, the user has the option of
explicitly stating which tables will be accessed or updated during the
transaction.  For each table listed, a lock is issued that enforces the
specified MODE and SHARE options.  (For example, when a MODE=UPDATE
transaction is started, all tables referenced in the command are locked for
updating.)  If no tables are listed in the command, all tables in the model
are locked.  These locks remain in effect until a COMMIT or ABORT command is
issued (CHECKPOINT and ROLL BACK commands free record locks, but never free
table locks).
 
DML commands issued within a transaction do not need table locks, since all
required locks are obtained with the BEGIN command.  If a DML command is
issued that requires more restrictive locks, ARES rejects the command since it
does not conform to options specified at BEGIN time.
 
If a DML command is issued when a BEGIN is not in effect, ARES analyzes the
command, determines which locks are necessary, and issues them before the
command is executed.  These implicit locks are issued on each table referenced
in the DML command; locks are freed upon completion of the command.
 
If a DML command is started from the Application Program Interface (API) when
ARES_BEGIN is not in effect, the model is locked.  This action is taken to
prevent the unsuspecting API program from getting into deadlock situations
while trying to obtain table locks.  (If locks are issued on tables as each
ARES_START is issued, two programs could each obtain a lock on a distinct
table, and then attempt to lock the table already locked by the other causing
a deadlock.)  Although this limits the ability to share a model, users can
issue BEGIN commands (by calling ARES_BEGIN), and lock tables in the way
described above.
 
When any requests to lock the model or specific tables cannot be satisfied,
ARES waits.  Once locks can be issued (due to other users freeing their
locks), ARES proceeds with the current user's request.  The BREAK key may be
hit to cancel the waiting operation.
 
Each user can specify the following when starting a transaction with the BEGIN
command:
 
o   SHARE - specifies if the user will share with retrievers or updaters.
o   MODE - specifies if the user is retrieving or updating data.
Two users can share a table if each user's MODE is compatible with the other's
SHARE.
 
For additional information see:
MODE_OPTION
SHARE_OPTION
UPDATE_SHOW
When updating data in a table, record locks are issued so that the entire
table need not be locked.  This is an attempt to provide more concurrent
access to data in the table, while still protecting the concept of a
transaction (by preventing other updaters from changing the same records).
There are times when only one updater will ever be running at any given
instant.
 
Many sites run a single update stream and allow multiple users to extract data
while the updates are occurring.  As long as the extractors do not care that
they might see partially updated data, there is no reason for the updater to
lock records since there are no other updaters running (and thus nothing will
change the way the program runs).
 
The user can request this access by specifying MODE=UPDATE and SHARE=ANY on
the BEGIN command.  This guarantees that only one updater is operating at any
given time.  Furthermore, it only allows statistical readers (those who have
indicated they are willing to see partially updated data by specifying MODE=IN
and SHARE=ANY on the BEGIN command) to share tables.
 
As with the statistical reader, the advantage of operating in this mode is
that no record locks need to be issued.  This not only reduces overhead, but
provides better concurrent access since users never wait for locks to be
released.
The following commands apply to all modes.  They differ from the basic mode
commands (CREATE, ALTER, DROP, and INVOKE) in that they do not enter the user
into a specific mode.  In addition, after entering one of these commands, the
user will again have to issue a mode command to change modes.  These commands
are summarized in the following table:
 
           Command      Description
 
           LOCK         Lock out other users
 
           RECONSTRUCT  Complete an aborted CREATE,
 
                        ALTER, or DROP MODEL command
 
           ROLL FORWARD Apply a common journal file to the database
 
           UNLOCK       Unlock a locked database
 
These commands take effect immediately; they do not require an ABORT or COMMIT
command once they are entered.
SPECIAL_MODE
Syntax:
{START|EXECUTE} [PREVIOUS|label [(constant-list)]]
Parameters:
 
constant-list  a list of constants separated by commas.
 
label  a previously created DML label.
Description:
The START command is used to execute DML statements which have been stored
under user-supplied labels using the STORE command.
Rules:
 
 1. Issuing START with no label executes the current ARES DML command.
 2. If PREVIOUS is specified, the command prior to the current command is
    executed.
 3. If a label is specified, the stored DML statement identified by the label
    is executed.
 4. If a constant-list is specified, the constants are substituted into the
    stored command before execution.  The number of constants specified in the
    list must match the number of parameters specified when the DML statement
    identified by label was stored.
See also:
STORE Command
00002
00001
00003
00004
START
Often an application is only used to scan data in a database, with no concern
as to whether the data is being updated as it is being accessed.  The purpose
is to gather information (or statistics) from the database, so individually
updated records have no real affect on the results.  An example of this type
of application is a scan through a textual database.  As long as applications
do not update records, there is no reason to issue record locks.
 
In order to request such access, the user specifies MODE=IN and SHARE=ANY on
the BEGIN command.  This informs ARES that the user is willing to share with
any other type of user.  As long as the other user does not specify
SHARE=NONE, simultaneous access to the database is allowed.
 
Although the user might see slightly inconsistent views of data (due to
updates being issued by other users), there are two performance advantages to
using this type of access:
 1. Record locks are not issued since the user is willing to access records
    whether they have been locked for update or not.
 2. Since no locks are issued, the user never waits to see information that
    others have locked, and other users never wait to update examined records.
Syntax:
STORE label [(parameter-list)] [COMMENT=literal] [DML-statement]
Parameters:
 
DML-statement  either an INSERT, UPDATE, DELETE, LOAD, DUMP, or SELECT
    command.
 
label  an ARES identifier assigned as the label for this particular DML
    command for this database.
 
literal  text string enclosed in single quotes with a length of 1 to 255.
 
parameter-list  a list of ARES identifiers separated by commas.
Description:
The STORE command is used to store a DML command for later execution under a
user-specified label.  The STORE directive is stored preceding the DML
statement.
 
The command types permitted in a stored DML command are:
 
    DELETE
    DUMP
    INSERT
    LOAD
    SELECT
    UPDATE
Rules:
 
 1. DML commands may be stored in the model only by users with DML or CREATOR
    privileges.
 2. The label must be supplied and must be unique for that model.  If a STORE
    command is issued in which the label matches the label of an existing
    stored command, the existing command is replaced.
 3. Only the owner of the DML command or a user with CREATOR privileges may
    replace an existing DML command.
 4. The DML-statement must be an INSERT, UPDATE, DELETE, SELECT, LOAD, or DUMP
    command; attempts to store any other statement types will be rejected.
    Note that any command may contain embedded SELECT commands.
 5. If the DML-statement option is not specified, the current ARES command is
    stored under the name specified.
 6. Commands may not be stored if they reference temporary database
    items:   tables, bulkfiles, or functions.
 7. Parameters can only be specified when using the DML-statement option.  The
    DML-statement can then reference these parameters by name.
 8. Parameters can only be used where it is legal for constants to be used.
    Table names, column names or other database items may not be
    parameterized.
 9. It should be noted that the STORE directive itself is saved as part of the
    command as shown in the following example:
Example:
: STORE AVERAGE SELECT AVG(SALARY) FROM EMP
       The DML command AVERAGE has been stored.
     : DI DML AVERAGE
       STORE AVERAGE SELECT AVG(SALARY) FROM EMP
See also:
DISPLAY_DML, START
00002
00004
00001
00003
00005
STORE
Subqueries provide an alternate method for composing DML commands.  Although
providing the same basic functionality as ordinary queries, there are a few
subtle differences.  Those differences are discussed below.  To facilitate the
discussion, the EMPLOYEE table  shown under TABLE_VARIABLES and the table that
represents the sales made by each employee shown in the following table are
used.
 
 : SELECT * FROM SALES
   .. 7 records SELECTed.
 EMP_NO PART_NO QUANTITY
 ------ ------- --------
   7369      11      500
   7369      12     1575
   7521      11      800
   7521      14      322
   7788      13     1777
   7788      14     2010
   7844      11      400
 
A typical query of the two table database might be to find those employees
that have sold 1000 or more of any individual part.    This is shows in the
example below.
 
 : SELECT NAME;
 + FROM EMP,SALES;
 + WHERE EMP.EMP_NO=SALES.EMP_NO AND;
 +       SALES.QUANTITY>1000
   .. 3 records SELECTed.
 NAME
 -----
 SMITH
 SCOTT
 SCOTT
 
It should be noted that SCOTT appears twice in the result.  This is because
SCOTT actually qualifies twice:   once for part 13 and once for part 14.  The
way the query is stated, it finds every combination that qualifies.  However,
the query can be restated to find only those employees who have sold more than
1000 of any part, without seeing the name for each occurrence, as shown below.
 
 : SELECT NAME;
 + FROM EMP;
 + WHERE EMP.EMP_NO IS IN (SELECT EMP_NO;
 +                              FROM SALES;
 +                              WHERE SALES.QUANTITY>1000)
   .. 2 records SELECTed.
 NAME
 -----
 SMITH
 SCOTT
 
This query is interpreted as follows:  select the name of each employee whose
employee number is contained in the list of employees that sold 1000 or more
of a single part.  It is not important how many times the employee's number is
in the list so long as it is there; once a match is found the rest of the list
is not even checked.
 
Another form of subquery compares the value in a table to the result of
another query.  For example, assume that the user wants to print the employee
number of the person that sold the most of any individual part.  The first
query, the subquery, finds the maximum number sold, and the second query finds
the number of the employee who sold that many.    This is shown in the sample
query below.
 
 : SELECT EMP_NO;
 + FROM SALES;
 + WHERE QUANTITY=(SELECT MAX(QUANTITY);
 +                FROM SALES)
   .. 1 record SELECTed.
 EMP_NO
 ------
   7788
 
Notice that the subquery returns only one value as its result.  This is a
requirement for this form of subquery.  If there is more than one value
expected, the query must specify how to interpret the comparison operator, in
this case the equal (=) sign.  In other words, is the QUANTITY to be equal to
ALL the results from the subquery, or just ANY of the results of the subquery.
The use of these modifiers is shown in the example below, where a subquery is
used to simulate the result of the previous example without using the MAX
function.
 
 : SELECT EMP_NO;
 + FROM SALES;
 + WHERE QUANTITY >= ALL (SELECT QUANTITY;
 +                        FROM SALES)
   .. 1 record SELECTed.
 EMP_NO
 ------
   7788
 
Since the QUANTITY is greater than or equal to all other quantities in the
SALES table, it is the maximum QUANTITY.
ARES can back out partially completed updates in case of a soft crash by the
operating system.  If this occurs, the database is returned to the last clean
point of operation.  If a transaction was active, the last clean point is the
latest BEGIN or CHECKPOINT command that was issued.  If a transaction was not
active, the last clean point is the beginning of the last DML command, except
in the case of interactive insert where at most one record is backed out.
 
System recovery operates correctly only if the transient journal is active for
all DML commands that update the database.  The user can guarantee this by
specifying the CREATE JOURNAL command with the TRANSIENT option.  If this
command is not issued, only updates within transactions are protected against
system crashes.
 
If the system does crash, the operating system recovery mechanism calls ARES
if a transient journal is found.  At that time, ARES backs out any updates
recorded in the transient journal by performing a normal rollback operation.
LIST_TABLES
It may be desirable to have two logical instances of the same table.  For
example, to satisfy the question, "Which employees earn more than their
managers?", a table will typically exist that contains the employee's
identifier, employee's salary, and manager's identifier.    Following is an
example of such a table.  Therefore, to answer the question, each employee's
record is found, and the manager's record is also found (by looking up the
manager's identification in the same table), then the employee's salary is
compared to the manager's salary.  This requires that ARES distinguish between
two instances of the same table, one that represents the employee, and one
that represents the manager.
 
 : SELECT * FROM EMP
   .. 10 records SELECTed.
 NAME   EMP_NO SALARY MAN_NO DEPT_NAME GROUP_SIZE
 ------ ------ ------ ------ --------- ----------
 SMITH    7369  18000   7654 SHOE               0
 ALLEN    7499  25000   7844 TOY                0
 WARD     7521   9000   7844 TOY                0
 JONES    7566  26000   7902 LOAN               0
 MARTIN   7654  22000   7902 SHOE               0
 BLAKE    7698  24000   7654 SHOE               0
 CLARK    7782  15600   7654 SHOE               0
 SCOTT    7788  23750   7844 TOY                0
 TURNER   7844  18000   7902 TOY                0
 FORD     7902  25500      0 PRESIDENT          0
 
To solve this problem, table variables are introduced.  Table variables allow
the user to form separate logical instances of the same physical table.
Notice that the FROM clause lists the table twice; once as itself, and once
with a new logical name.  This logical name is then used to qualify the
instances of the columns that reference the manager's record versus the
employee's record.
 
 : SELECT EMP.NAME,MANAGER.NAME;
 + FROM EMP, EMP MANAGER;
 + WHERE EMP.MAN_NO=MANAGER.EMP_NO AND;
 +     EMP.SALARY>MANAGER.SALARY
   .. 4 records SELECTed.
 
 NAME  NAME
 ----- ------
 ALLEN TURNER
 JONES FORD
 BLAKE MARTIN
 SCOTT TURNER
Once the user becomes familiar with ARES and starts to build larger and larger
databases, efficient use becomes more of a concern.  The following topics
discuss some of the issues that affect the performance of the user's database.
 
For further information, see the following HELP topics:
QUALIFYING_NAMES
TABLE_VARIABLES
MERGING_TABLES
SUBQUERIES
GROUP_BY_CLAUSE
ADVANCED_UPDATE_COMMANDS
DATABASE_DESIGN
OPTIMIZATION_USING_KEYS
USING_BULKFILES
ARES uses a number of temporary files during various operations.  Most of
these files are of no particular importance to an ARES user but are listed
below just to identify all files used by ARES, and to give the user an idea of
how much temporary memory is required.
 
          model-name_CMD      or      ***ARES_CMD
          model-name_NEW      or      ***ARES_NEW
          ***ARES_RESULT
          ***ARES_INTERIMnnnn
 
 1. The prefix "model-name" is the name of the model that the temporary file
    belongs to; "nnnn" is a sequential integer number.
 2. The model-name_NEW file contains the complete model-name_MOD file when the
    user is in create or alter mode.  When in invoke mode, the temporary file
    is named ***ARES_NEW and only contains the _MOD records for the temporary
    DML commands.
 3. The model-name_CMD file, used when in create or alter mode, is known as
    ***ARES_CMD when in invoke mode.  This file contains the _MOD records on a
    command-by-command basis so that errored commands do not overwrite
    existing records on the _NEW file.
 4. The ***ARES_RESULT file contains the result relation of the current ARES
    command.  If interim relations are necessary, as in the case of joins,
    these relations are contained in ***ARES_INTERIMnnnn files.
 5. One additional temporary file that may be of some interest is the *I file.
    This is a file used to hold the transient journal.  It is a specially
    protected system file that may appear when listing temporary files, but
    cannot be updated, deleted, or accessed directly by the user.
SET_TIMESPAN
Timespan constants have a special syntax to allow specification of the maximum
accuracy allowed by the data type.
 
       {d                     }
       {                      }
 [+|-] {[d.]h:[m[:[s[.[t]]]]] }
       {                      }
       {:m[:[s[.[t]]]]        }
Parameters:
 
d   is a number of days.
 
h   is a number of hours (0 to 23).
 
m   is a number of minutes (0 to 59).
 
s   is a number of seconds (0 to 59).
 
t   is a number of hundredths of seconds (00 to 99).
Examples:
 
          2.12:       two and a half days (two days and twelve hours)
 
          03:15       three hours and fifteen minutes
 
          :01:30      one and a half minutes
 
          0:0:1.5     one and a half seconds
 
          :0:0.01     one hundredth of a second (one clock tick)
 
A time constant may also be entered as a character string enclosed in quotes
and immediately preceded by a "T". The string will be evaluated using the time
picture string currently in effect (see the TIME option of the SET command).
Example:
T'2:30'
00003
00002
00001
Syntax:
TIMESPAN
Description:
TIMESPAN data type is used to represent intervals of time.
Rules:
 
 1. TIMESPAN data type is represented as a packed decimal double word whose
    contents represent the interval in hundreths of a second.
See also:
DATE_DATA_TYPE
00001
00002
00003
Timespan pictures are similar to time pictures.  The following subfield
identifier characters are recognized:
 
    D    the number of days
    H    the number of hours
    M    the number of minutes
    S    the number of seconds
    T    the number of hundredths of seconds
 
The subfields must appear in the order shown.  One or more subfields may be
omitted from either or both ends of the list.  The first subfield character
used may be repeated up to ten times to indicate the number of digits to
reserve for the subfield.  Subsequent subfields may be indicated by one or two
characters each, and have the same meaning as they would in a time picture.
Rules for punctuation are the same as for dates and times.
Timespans that exceed the units of the first subfield specified are formatted
in terms of that unit.  Timespan values are truncated to the units of the last
subfield specified.
 
If the value is negative, the first digit of the first subfield is replaced by
a minus (-) sign.  A plus (+) sign is also recognized, but is never generated.
 
The following examples show how a given timespan appears when formatted with
different pictures:
 
                   Picture                 Formatted Result
                   -----------------------------------------
                   DDDD.HH:MM:SS.TT        1.12:15:30.50
 
                   HHHH "Hours"            18 Hours
 
                   MMMM "min," S "sec"     2175 min, 30 sec
 
                   TTTTTTTTTT              13053050
FORMAT_TITLE
FORMAT_TOTAL
A transaction is defined as an indivisible unit of work.  Thus a transaction
can only be in one of two states:   not yet started or completed.  In reality,
a transaction is usually made up of several elementary operations.  For
example, a banking application may have two elementary operations to transfer
funds from one account to another:   one to subtract the funds from the first
account, and another to add it to the second account.  It is easy to see why
the application program would group these two separate operations into an
indivisible unit.  Not only would it be invalid to leave the operation
partially completed, but in addition, allowing anyone else to view data being
updated before the update is complete would be invalid.
 
In ARES, the start of a transaction is specified with a BEGIN command.  From
the time the BEGIN command is issued until a COMMIT or ABORT command, ARES
treats all DML commands as a single transaction.  When a COMMIT command is
issued, the transaction is successfully completed.  All updates become
permanent and other users are allowed to access the updated data.  When an
ABORT command is issued, the transaction is cancelled.  All updates are backed
out using the transient journal (see the discussion under Transient Journal).
At this point, the database will appear to all users as if none of the DML
commands had been issued.
 
Sometimes an operation consists of many transactions.  Instead of having to
BEGIN and COMMIT each transaction individually, the CHECKPOINT command is
provided.  The CHECKPOINT command has almost the same effect as a COMMIT
command (the updates are made permanent and can be seen by other users),
except that the transaction is not ended.  DML commands, CHECKPOINT commands,
and a COMMIT command can be issued without issuing another BEGIN.
 
When combining several operations into a single transaction, completion of
some operations may not be possible.  In this case, it is preferable to back
out of any operations already performed in the transaction, but keep the
transaction and table locks (discussed below) active.  The ROLL BACK command
is used under these circumstances.  By issuing a ROLL BACK command, all
updates since the last CHECKPOINT or BEGIN command (whichever is later) are
backed out (like an ABORT), and the transaction is kept active.
 
When updates are backed out by a ROLL BACK command, a subsequent CHECKPOINT or
COMMIT can only make permanent updates made since the last ROLL BACK command.
When updates are made permanent by a CHECKPOINT command, a subsequent ABORT or
ROLL BACK command can only back out updates made since the last CHECKPOINT
command.
The transient journal is used to back out partially completed or aborted
transactions.  No specific file is identified by the user to be the transient
journal.  Instead, a special system file is reserved for such use.  Transient
journaling is activated by starting a transaction with the proper options (see
the BEGIN Command) or by issuing a CREATE JOURNAL command with the BEGIN
command) or by issuing a CREATE_JOURNAL command with the TRANSIENT option.
 
The transient journal contains a copy of all updated records in the database
before the updates were applied.  Thus, any time a record is added, deleted,
or updated in the database, the necessary information to restore the original
record (before image) is saved in the transient journal.  Allowing the user to
back out of updates made is known as a rollback operation.
 
As DML commands that update tables are issued within a transaction, before
images are written to the transient journal.  Upon successful completion of a
transaction (COMMIT) or when a checkpoint is issued (CHECKPOINT), the
transient journal is erased.  If a transaction is canceled (ABORT) or a
rollback occurs (due to the detection of a deadlock condition while locking
records, or from an explicit call to ROLL BACK), the transient journal is used
to return the database to the state it was in when the last BEGIN or
CHECKPOINT was issued.  After the rollback is performed, records in the
transient journal are erased.
SELECT_UNION
Syntax:
UNLOCK fid
Parameters:
 
fid  a file name which identifies the model to unlock.
Description:
The UNLOCK command allows a user with CREATOR privilege to cancel the effect
of a LOCK command.  This gives all authorized users access to the model
regardless of whether they have CREATOR privilege or not.
Rules:
 
 1. CREATOR privilege is required to issue the UNLOCK command.
 2. The command waits until there are no longer any exclusive users of the
    model.
See also:
LOCK Command
00002
00001
00003
00004
UNLOCK
Syntax:
UPDATE [ ALL ] table-name
 
    [ FROM table-name1 [table-label] [,...] ]
 
    [ SET column-name [ = algebraic-expression1 ] [,...] ]
 
    [ SHOW algebraic-expression2 [,...] ]
 
    [ WHERE constraint-expression ]
Parameters:
 
algebraic-expression1,2  any legal algebraic-expression used to determine
    replacement value(s), as described under ALGEBRAIC_EXPRESSIONS.
 
column-name  the name of a column to be updated.
constraint-expression  as described under CONSTRAINT_EXPRESSIONS.
 
table-label  the name associated with a table in the FROM clause used as a
    table variable in the WHERE clause.
 
table-name  the name of the table to be updated.
 
table-name1  the name of a table in the model.
Description:
The UPDATE command is used to modify data which already exists in a database
table.  The modification consists of a SET clause, specifying the modification
to be made to the column in the row, and a WHERE clause, specifying the
criteria which identifies what rows in the table are to be updated.
Rules:
 
 1. If the ALL keyword is specified, all rows in the table are updated and the
    WHERE expression is not allowed.  If the WHERE clause is not specified,
    the ALL keyword is required.
 2. If the FROM clause is specified, the table being updated must be specified
    in the clause.
 3. The UPDATE command will not allow fields in the primary key to be set.
 4. The SHOW clause causes the columns specified to be displayed to the user
    before the SET list is processed.  The SHOW clause is allowed only if one
    or more of the set items do not specify an algebraic-expression.  If the
    SHOW clause is omitted, and one or more of the SET items do not specify an
    algebraic-expression, the fields that comprise the primary key of the
    table being updated are shown to distinguish the records being updated.
    If any of the fields to be shown are longer than 128 characters, they will
    be followed by an ellipsis.
 5. For each SET item which has no algebraic-expression specified, the
    interactive user is prompted for replacement data in a manner similar to
    interactive INSERT. The user is prompted with the field name and the old
    contents of the field is presented for editing.  The UPDATE prompts for
    every record in the table which satisfies the WHERE clause.  A single
    blank entered for a numeric field will be treated as a zero.  If the data
    to be displayed is larger than 2047 characters, it cannot be updated in
    this way.
 6. To terminate interactive UPDATE mode before all candidate records have
    been updated, a null value must be entered after the first field prompt of
    a record.
 7. The interactive form of the UPDATE command cannot be used in batch mode.
Example:
 
     : UPDATE ALL EMP;
     +     SET SALARY = SALARY * 1.15
       .. 10 records UPDATEed.
     :
     : UPDATE EMP;
     +     SET SALARY = SALARY * 1.15;
     +     WHERE NAME = 'JONES'
       .. 1 record UPDATEed.
     :
     : UPDATE EMP;
     +     FROM EMP,EMP MANAGER;
     +     SET SALARY = EMP.SALARY * 1.25;
     +     WHERE EMP.MAN_NO = MANAGER.EMP_NO;
     +           AND MANAGER.NAME = 'FORD'
       .. 3 records UPDATEed.
00002
00004
00001
00003
See UPDATE_COMMAND
UPDATE
See UPDATE_COMMAND
See UPDATE_COMMAND
See UPDATE_COMMAND
See UPDATE_COMMAND
API_USAGE
BULKFILES
Syntax:
UTS
Description:
UTS data type is used to describe a field which contains CP-6 system
timestamps.
Rules:
 
 1. The UTS data type may only be used in bulkfile descriptions.  Its purpose
    is to allow CP-6 system timestamp data to be loaded into an ARES database.
    UTS is not allowed in table or function definitions.
 2. If a UTS item is stored into a DATE field, the proper conversion will be
    performed to accurately represent the date and time information.
See also:
DATE_DATA_TYPE
00001
00002
00003
COMMAND_VARIABLES
UPDATE_WHERE
END
