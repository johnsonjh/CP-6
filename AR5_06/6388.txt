Start by logging on to the CP-6 operating system.  Once you see the
system level prompt (!), invoke CAP by typing:
 
    CAP
The Main Menu displays the keywords that you may select to perform a
function.  The cursor (represented by the underscore character) is
positioned at the place where CAP expects input from you.
CAP User Guide- HA29-00
*************************************************************************
*
* Copyright (c) Bull HN Information Systems Inc., 1989, 1994
*
*************************************************************************
Knuth, Donald E., Computers and Typesetting, Volumes A-E (Addison
Wesley, Massachusetts, 1986). These volumes are as follows:
 
A.  The TeX book
B.  TeX: The Program
C.  The METAFONTbook
D.  METAFONT: The Program
E.  Computer Modern Typefaces
The Text Analysis menu is used to perform various tests on a document,
including spelling check, readability test, and DSL control validation.
SPELLING
Checks the spelling of words in the document against the central standard
dictionary PROOF_DIC.X and the PROOF_DIC file (if any) in your logon account.
The SPELLING option calls up the Proofreading Functions submenu.
 
                         --- Proofreading Functions ---
 
           What do you want to do with the list of misspelled words?
 
                1. DISPLAY - Display the list on the terminal
                2. PRINT - Print the list on the lineprinter
                3. REVIEW - Review the list for possible changes
                4. END - End proofreading mode (the default)
 
If you select the REVIEW option you will see the following menu:
 
                        ---- Word Review Functions ----
 
                1. ADD - Add the word to your personal dictionary
                2. CHANGE - Edit the document to change the word
                3. SEARCH - Search the dictionary for similar words
                4. NEXT - Go to the next word (the default)
                5. PRIOR - Go back to the previous word
                6. END - End word review mode
LIMITED
Checks words in the source document against a dictionary of allowable words.
The default limited word dictionary contains approximately 3000 commonly used
words.  The limited word dictionary check is valuable when writing for non-
English speaking audiences, or an audience with a limited vocabulary.  The
LIMITED option calls up the Proofreading Functions submenu.
PROHIBITED
Checks words in the source document against a dictionary of "forbidden words".
The default forbidden word dictionary displays "gender-specific" pronouns.
The PROHIBITED option calls up the Proofreading Functions submenu.
FREQUENCY
Compiles an alphabetical list of the most frequently used words in a source
document.  Word frequency is useful for determining keywords and index
phrases.  The FREQUENCY option calls up the Proofreading Functions submenu.
READABLE
Reports the number of words, the number of sentences, and the readability
level of a CAP source document.  Three standard methods of calculating
readability are applied:  Flesch, Kincaid, and FOG. Note that this function
checks only portions of the source file that are to be formatted, i.e.,
passages of words arranged in sentences.  Tabular material and lists are
generally ignored.
VALID
Checks the source document to be certain that all control calls are CAP
controls.  All non-standard macro calls are flagged.  This is useful for
checking a large document to make certain that it will format correctly and
not encounter typographical errors in the control calls.  This function also
checks for mismatched braces, and flags slashes (as opposed to backslashes) in
CAP controls as possible errors.
UNPRINT
Displays the location of all unprintable characters.  Frequently these are
responsible for unusual formatting or editing behavior.  It is a good idea to
run the unprintable test on files that appear to be keyed into the source file
correctly, but format with unexplainable spacing and/or overstriking.  If
unprintable characters are found, contact the CAP administrator for more
information.
WORD
Searches for words in PROOF.X dictionaries.  The default dictionary is
PROOF_DIC.X. The WORD option calls up the Dictionary Selection menu.
 
                        ----  Dictionary Selection ----
 
                1. SPELLING - The system spelling dictionary (the default)
                2. ACCOUNT - Your personal dictionary
                3. LIMITED - The limited word dictionary
                4. PROHIBITED - The prohibited word dictionary
                5. FREQUENCY - The word frequency excluded word dictionary
DICT
Uses the WEBSTER.X program to update the PROOF_DIC file in your logon account.
The WEBSTER program accepts six commands:
 
    ADD    adds a word to the dictionary.
 
    DELETE    removes a word from the dictionary.
    END    returns the user to the Master Menu.
 
    LIST ON ME    displays a list of all the words in the dictionary.
 
    LIST ON LP    prints a list of all the words in the dictionary on the
    default lineprinter.
 
    LIST word1 [- word2]    displays an alphabetical list of words beginning
    with the specified word1 and ending with word2.
 
See the HELP file for WEBSTER.X for more information.
00001
00002
00003
00004
00005
00006
00007
00008
00009
00009
00004
00002
00003
00005
00001
00007
00006
00008
PROGRAM_CONTEXT
CONTEXT_MENU
FORMAT_CONTEXT
GRAPHIC_CONTEXT
JOB_CONTEXT
The Context Types menu determines the CAP user's working environment.  You can
change some of these defaults:  the type of formatting that is applied to a
source document, device assignments for displaying a document and viewing
graphics, and several others.  Note that the defaults for all Context Change
options can be changed by the CAP administrator.
FORMAT
Determines how the final product will appear when printed on a hardcopy device
(how much space between letters, words, lines, paragraph and headings,
placement of tables and figures, etc.).  FORMAT also allows you to to
determine the printing device and destination account.
JOB
The Job Control Context Options menu controls the behind-the-scenes activities
of CAP, such as what to do with a job before, during, and after processing.
GRAPHIC
The Graphics Processing Context Options menu sets the parameters for
processing graphics in CAP. The default graphic accounts, graphics device,
graphics driver, and scan resolution are all established.
PROGRAM
This menu allows the user to set the default for File Editor, Electronic Mail,
Electronic Meeting, Personal Calendar, and Business Graphics.
00001
00002
00003
00004
00001
00003
00002
00004
PROGRAM_CONTEXT
Once your file is HELP-coded, display the Master Menu and format your file.
Formatting a file for HELP is very similar to formatting a document, except
for the format name and the device name, both of which are "HELP". Your screen
should look like:
 
CAP Function: 2
  Files to format: DUCK_E00
Key SE     1     0      29 09:43 FEB 06 '89  DUCK_E00
*
  Format name (DEFAULT): HELP
  Device name (LP@UPSTAIRS): HELP
  Help SI file to create (*:CAP:HSI): :DUCK:HSI
  Help subject to create: DUCK
 
At the Help SI file to create (*:CAP:HSI): prompt you must provide a filename
for storing the HELP source information.  Type :DUCK:HSI. Help subject to
create:  prompts for a simple help subject, which is used to create a file
that fits CAP's naming convention.  This is the file you access for HELP
topics and subtopics.  If you provided the subject DUCK, CAP names your HELP
file HELP:DUCK: and stores this file in your account.  Your screen should look
like the following:
 
Document Formatting Options      (If in doubt, enter a question mark)
 
Option:                             Value:
 1. DSL - Document Source Files     DUCK_E00
 2. FORMAT - Format to use          HELP - HELP file generation
 3. DEVICE - Final output device    HELP - for HELP file generation
 4. DVI - Device-Independent File   :DUCK:HSI
 5. RESOLVE - Resolve DSF File      YES
 6. KEEP - Keep DSF File            YES
 7. DSF - Device-Specific File      HELP:DUCK:.
 8. PRINT - Print DSF File          NO
 9. SEV - Fatal Error Severity      WARNING
10. SUBSET - Subset to use          HELP
11. JCL - Print Batch JCL Listing   YES
Batch, Online, Save, Cancel, or menu option: _
 
Notice item 10.  SUBSET has been given the value of HELP by CAP.
 
At the Batch, Online, Save, Cancel, or menu option:  prompt type B or BATCH.
Your screen then looks like the following:
 
Batch, Online, Save, Cancel, or menu option: B
69157 .LHTEST running 0:00/29:59
---- Batch job for Formatting of DUCK_E00 to HELP:DUCK:. submitted.
 
Check your job report to make sure that your job ran successfully and if you
have any warnings or errors messages to be concerned about.
When CAP is used for demand printing, documents are stored on the
computer in electronic form and copies are printed when needed on
a high-speed output device. Features include:
 
o   Lineprinter copies--low-resolution draft copies are printed on
 
    demand.  This is useful for give-away drafts and quick reviews.
    Fonts and boxes are represented by ASCII characters.
 
o   Laserprinter copies--documents are printed on the laserprinter
    when needed.  A 100 page document is printed in less than 10
 
    minutes.  Graphics, fonts, and boxes have the appearance of quality
    master copies.
 
o   Integrated text and graphics--demand printed copies can have
    graphics at the resolution of the output device.
ONLINE_HELP_DOCUMENTATION
CAP has the following document assembly features:
 
o   Table of contents generation--a new table of contents can be
    generated during every formatting run; this guarantees accuracy.
 
o   Index generation--a new index can be generated during every formatting
    run. Multilevel indexing (an index within an index) and permuted
 
    indexes (multiple index terms from one index reference) are also
    available.
 
o   Automatic numbering--page, section, table, figure, and
    paragraph numbers are generated automatically.
 
o   Cross-reference resolution--the user refers to a section,
    paragraph, figure, or table by name.  In the formatted document, the
 
    reference is automatically updated to include the current number and
    page of the item.
GRAPHIC_EXPORT
CAP provides several file and text handling options to facilitate
document processing, as follows:
 
o   File conversion--consecutive or unit record files can be converted
 
    to EDIT-keyed files. Outline files can be converted to CAP DSL control
    files, with each outline topic being automatically enclosed in the
 
    appropriate DSL level heading control.
 
o   File collation/decollation--a number of files can be collated into
    a single file, and the collated file can later be decollated into its
 
    original file names. Several files can also be merged into a single file,
    but cannot be decollated later.
 
o   Substitution processor--CAP allows global substitution of text
    strings in a document. The replacement text is indicated by the user
 
    within the document file.
 
o   A00 to B00 or B01 conversion--document files created with A00 CAP can be
 
    converted to the B version (B00 or B01). The converter replaces A00 macros
    and TEXT control
    words with DSL controls.
 
o   Pretty printer--document source files can be reformatted so that
    they are easier to read and edit. The pretty printer indents stacked
 
    paragraph lists and aligns margins.
FORMAT_CONTEXT
The options for this function allow you to predetermine the default
characteristics for a formatted file (i.e., type, destination account, and
printing device).
DSL
Defines the default account assignment for various CAP tasks.  The default is
the current directory account.
DVI
Defines the default account assignment for device-independent files.  A DVI
file is created so that you may print the entire file, or a specified number
of pages.  DVI files are an intermediate form of the document that may be
converted to printable form at a later time.  The default is the current
directory account.
DSF
Defines the default account for device-specific files.  DSF files are created
to print on the printing device for which they were formatted at a later time.
The default is the current directory account.
FORMAT
Determines the style of a document as it will appear when printed.
DEVICE
Defines the default destination of a formatted CAP document.
SEV
Defines the default error level CAP allows when formatting a document.  If the
error level is exceeded, the job continues to run, and all errors are reported
to a file (*:CAP:LOG), but no output is created (except in ABORT level
errors).
TYPE
Defines the default for the type of file that CAP creates when the Format
Document is selected from the Master Menu.
REUSE
Instructs the formatter (TeX) to reuse the existing table of contents and
index files (if they exist) rather than create new ones.  This feature
eliminates the time it would take CAP to create a new table of contents and
index when formatting a document.  If a new table of contents and index is
desired, change the default value to NO.
SEARCH
Defines the default account(s) to be searched for files needed for formatting
a document.  The maximum number of accounts that may be listed is 7.
00001
00002
00003
00004
00005
00006
00007
00008
00009
00005
00003
00001
00002
00004
00008
00009
00006
00007
The Document Formatting Options menu is displayed immediately after a carriage
return at the "Device name:"  prompt.  This menu is available only for users
who have the Master Context option set.
 
Note:  To reset the default for any of the Document Fomatting options, enter a
dash (-) at the option prompt and the original default for that option is
displayed on the menu.
DSL
Informs the you of the file that has been requested for formatting.
FORMAT
Indicates the type of format to use for the current formatting job.
DEVICE
Indicates the type of printer that the formatted document is printed on.
DVI
Specifies the name of the temporary Device-Independent file created at the
completion of the current job.  This DVI file is a temporary, intermediate
form of the file DOCUMENT that may be converted to printable form at a later
time.  The file (*:CAP:DVI) may be renamed (omit the *) as a permanent file.
RESOLVE
This option specifies whether or not to create a device-specific version of
the document.  YES specifies that a DSF file is desired.  NO indicates that
only a DVI file is wanted.  If RESOLVE is NO, the DSF, KEEP, and PRINT options
are not applicable, since they pertain only to DSF file handling.  The default
is determined by the TYPE option in the Formatting Context menu.  If TYPE is
set to DVI, RESOLVE defaults to NO, otherwise it defaults to YES.
KEEP
If value is NO, a DSF file is not created upon completion of the current job
run.  If value is YES, a DSF file is created.
DSF
If KEEP has a value of YES, DSF has a file name value (DSFvalue:DSF). See item
1 on the Document Formatting Options submenu for the DSF value.  If KEEP has a
value of NO, DSF has a value of n/a.
PRINT
If the value is YES, the DSF file is printed on the specified output device.
If the value is NO the DSF file is not printed.
SEV
Informs the user of the SEVERITY value.  The legal values for this option are:
 
    WARNING - Terminate if any errors occur.
    ERROR - Terminate only if a serious error occurs.
    ABORT - Terminate only for catastrophic errors.
 
For more information, see Context Change later in this section.
SUBSET
Selects the subsets to be used for the current formatting job.  Subsets allow
a single source file to be tailored for several different audiences or
functions.  For more information refer to the DSL Reference Manual (HA27).
JCL
If the value is YES, the job listing will be printed for a batch formatting
job.
00001
00010
00011
00002
00003
00004
00005
00006
00007
00008
00009
00003
00007
00001
00004
00002
00011
00006
00008
00005
00009
00010
GRAPHIC_CONTEXT
The Graphics Processing Context Options submenu sets the parameters for
processing graphics in CAP, such as default graphic accounts, graphics device,
graphics driver, and scan resolution.
 
Note:  To reset the default for any of the Graphics Processing Context option,
enter a dash (-) at the option prompt and the original default for that option
is displayed on the menu.
SOURCE
Defines the default graphics account to be used for all graphics types except
DIGIS. The default is the user's account.
DISPLAY
Defines the default account for Device Independent Graphics Instruction Set
(DIGIS) graphics.  Default is the user's account.
DRIVER
Specifies the program that is called when a graphic is displayed at the
terminal.  The default is COPY. See the CAP administrator before changing this
option.
DEVICE
Defines the default device used to display graphics.  The default is ME. See
the CAP administrator before changing this option.
SCAN
Specifies the number of scan lines used when importing or exporting a graphic
file.  This number should match the resolution of the user's terminal.  The
default is 24, designed for output to a character mode terminal.  See the CAP
administrator before changing this option.
IMPORT
This specifies a site-specific import graphic function.
EXPORT
This specifies a site-specific export graphic function.
SEARCH
Defines the default account(s) to be searched for the specified graphic file.
The maximum number of accounts that can be specified is 6.  See the CAP
administrator before changing this option.
00001
00002
00003
00004
00005
00006
00007
00008
00004
00002
00003
00007
00006
00005
00008
00001
The "Export Graphics from CAP" selection from the Graphic Functions menu
displays the CAP Export Graphic Types submenu.  This submenu allows you to
convert one type of CAP-readable graphic file to another.
SGL
CAP standard vector graphic.
CPX
The CAP standard image file formatter.  Imported Datacopy IMG files are
converted to Cappix files.
MOVEDRAW
Converts CAP graphics to MOVEDRAW. MOVEDRAW is CAP's standard Move/Draw
format.
AUTOCAD
Converts CAP graphics to AUTOCAD. AUTOCAD is CAP's standard AutoCAD DXB
format.
DIGIS
Converts CAP graphics to DIGIS. DIGIS is CAP's standard DIGIS graphic format.
DATACOPY
Converts CAP graphics to DATACOPY. DATACOPY is CAP's standard Datacopy IMG
(Cappix) format.  Datacopy sanners are devices that attach to PC-AT and PC-XT
compatibles.
CD
Converts CAP graphics to Compressed Datacopy IMG. CD is CAP's standard
compressed Datacopy IMG format.
LOGICAD
Converts CAP graphics to LOGICAD. LOGICAD is CAP's standard LOGICAD format.
NSTD
Converts CAP graphics to your originally designed graphic.
00001
00002
00003
00004
00005
00006
00007
00008
00009
00004
00007
00002
00006
00005
00008
00003
00009
00001
The Import graphics to CAP selection from the Graphic Functions menu displays
the CAP Import Graphic Types submenu.  This submenu allows you to import any
specified graphic type file to either a Cappix file or to a Standard Graphics
Language (SGL) file.
ANVIL
Converts ANVIL plot files to Standard Graphic Language (SGL) files.  ANVIL is
a full-function Computer Aided Design (CAD) package.
PCDRAW
Converts PC-DRAW files to SGL files.  PC-DRAW is a drawing package for
personal computers.
DIGIS
Converts Device Independent Graphics Instruction Set (DIGIS) files to SGL
files.  DIGIS files are created by applications using the CP-6 Device
Independent Graphics System (DIGS). A number of these applications are
available in the CP-6 X account.
AUTOCAD
Converts AutoCAD PLT files (Houston Instruments DMP7 format) to SGL files.
AutoCAD is a full-function Computer Aided Drafting (CAD) program that runs on
personal computers.
ISSCO
Converts ISSCODumdev files to SGL files.  Dumdev files are created using two
CP-6 based graphics packages:  DISSPLA and TEL-A-GRAF, both available from
ISSCO.
MACPAINT
Converts uploaded MacPaint screens to Cappix files.  MacPaint is a pixel
painting program available on MacIntosh computers.
DATACOPY
Converts uploaded Datacopy scanner data to Cappix format.  Datacopy scanners
are devices that attach to PC-AT and PC-XT compatibles.  Accepts both
compressed and uncompressed input files.
MOVEDRAW
Converts Move/Draw files to SGL files.
INTERGRAPH
Converts Intergraph plot files to SGL files.  Intergraph plot files are
created by an Intergraph CAD system for Gerber plotters.
LOGICAD
Converts LOGICAD files to SGL files.
NSTD
Converts the user's originally designed graphic to a CAP-readable (Cappix)
format.
00001
00010
00002
00003
00004
00005
00006
00007
00008
00009
00011
00001
00004
00007
00003
00009
00005
00010
00006
00008
00011
00002
The Graphic Functions menu converts graphics into a form that can be included
in CAP documents.  On some systems, graphic conversion also creates a version
of the graphic file that can be displayed at your terminal.
IMPORT
Converts a graphic to either a Cappix or Standard Graphic Language (SGL)
graphic file.
EXPORT
Converts a Cappix or SGL graphic file to a specified graphic file.
MODIFY
Rotates a graphic 90 degrees right or left, and/or changes (inverts) a graphic
to a negative (where the black area prints white and the white area prints
black).
DISPLAY
Displays a graphic at your workstation.
00001
00002
00003
00004
00004
00002
00001
00003
The Modify CAP Graphics selection from the Graphic Functions menu displays the
CAP Graphic Modification Functions submenu.  This submenu allows you to modify
the placement of a graphic on the page.
RIGHT
This function rotates the specified graphic 90 degrees to the right on the
screen.  If the graphic is positioned with the top displayed at the top of the
terminal screen, the graphic rotates so its top is on the right side of the
screen.
LEFT
This function rotates the specified graphic 90 degrees to the left of the
screen.  If the specified graphic is positioned with the top displayed at the
top of the screen, the graphic rotates so the top of the graphic is on the
left side of the screen.
INVERT
This function inverts a graphic's solid black areas to white and vice versa.
00001
00002
00003
00003
00002
00001
ONLINE_HELP_FACILITY
This is the file that contains the actual on-line HELP messages.  To display
the default HELP message, at the bang (!), type:
 
    HELP (DUCK.)
To display the topics, type:
 
    HELP (DUCK.) TOPICS
 
To display the subtopics for a specific topic, type:
 
    HELP (DUCK.) topicname TOPICS
This file (:DUCK:HSI) is one of the two HELP-related files that you have now
created This file contains only the HELP source information for DUCK HELP
file.  The abstract message is coded as *A*, the topics are coded as *K*, and
the subtopics are coded as *B*.  The following is a copy of the HELP source
file:
 
  .*A*
  This section is about ducks that never cluck but quack instead.
  .*K* DIZZY_DUCK
  Dizzy ducks bump in to trees and other ducks.
  .*K* DUCK_LONE
  Lone ducks doesn't like ducks.
  .*B* LONE_DUCK_FOOD
  LONE DUCK FOOD      is available at my local pet store.
  .*B* LONE_DUCK_SHOES
  LONE DUCK SHOES      are tailor-made for each duck.
  .*B* LAME  WOODEN_LEG
  LAME      This lame duck lost his leg in the Battle of the Lagoon.
 
  Dirty Duck doesn't like water.
   1. One-legged ducks walk funny.
   2. My duck has a wooden leg.
  .*K* COLD_DUCK
 
  All cold ducks eat snow-flakes every day.  For more information
  about duck food, see  HELP topics:
    DUCK_FOOD DIET_DUCK_FOOD WEIGHTGAIN_DUCK_FOOD
 
The HELP source file may be helpful if you need to analyze or debug your on-
line HELP file.  If you are satisfied with your HELP messages, this file may
be deleted with no effect on your on-line HELP file.
GRAPHIC_IMPORT
CAP has the following graphics layout features:
 
o   Optimized picture placement - figures are placed at logical breaks
    in the text or can be forced to appear immediately.
 
o   Optimized picture scaling - graphic figures are automatically
    scaled to fit inside the "box size" specified by the user.  Box size
 
    is specified in various units of measure.
 
o   Figure and table boxing - CAP can put box lines around tables and
 
    figures automatically. Tables may have horizontal and vertical internal
    box
    lines.
 
o   High and low resolution - CAP automatically resolves all font, box,
    and graphic requests to the resolution of the output device.
 
    Therefore, a document can be printed on a lineprinter or laserprinter
    without changes to the user's file.
 
o   File import--CAP imports several different graphics file types,
    including LogiCADD, MacPaint, and PC-DRAW files.
 
o   File export--CAP exports to several different graphics file
    types, including AutoCAD, Datacopy, and LogiCADD files.
 
o   Inversion and rotation of graphics--CAP allows inversion and
    left or right rotation of graphic figures.
 
o   Graphic Display--CAP permits display of DIGIS graphics files at
    the user's terminal.
In addition CAP's ability to interface with a variety of text editors,
both on line and local, CAP allows the user to access several outside
applications to gather and display information. These are:
 
   Electronic mail
 
   Electronic meetings and bulletin boards
 
   A personal calendar
 
   A business graphics package
The Job Control Context Options submenu controls the behind-the-scenes
activities of CAP, such as what to do with a job before, during, and after
processing.
Note:  To reset the default for any of the Job Control Context options,
enter a dash (-) at the option prompt and the original default for
that option is displayed on the menu.
CHATTER
Prints controls and other information during formatting runs.  The default is
determined by the CAP administrator.
INFORM
Specifies whether or not to inform you on-line of a completed job.  The
default is determined by the CAP administrator.
MAIL
Specifies whether or not diagnostic messages generated by a job are sent via
electronic MAIL when the job completes.  The default is NO.
PRINT
Specifies whether or not to print a job listing.  The default is determined by
the CAP administrator.
MASTER
Specifies the default menu that is displayed when CAP is initiated.  The
default is NO.
MEM
Specifies the amount of memory resources required to process the current job.
The default is determined by the CAP administrator.
JOB
Specifies what options (if any) are applicable to the job "card" during batch
jobs.  The default is determined by the CAP administrator.  See the CAP
administrator before changing this option.
RES
Specifies what resource card options (if any) are applicable to the resource
"card" during batch jobs.  The default is no resource card options, except for
the memory limit specified by the MEM option (6) in this menu, which is
determined by the CAP administrator.  See the CAP administrator before
changing this option.
LIMIT
Specifies the maximum amount of resource available during a batch job.  The
default is determined by the CAP administrator.
00001
00002
00003
00004
00005
00006
00007
00008
00009
00001
00002
00007
00009
00003
00005
00006
00004
00008
JOB_CONTEXT
The Main Menu displays the keywords that you may select from to perform
a function.
EDIT      Invokes a text editor such as 6Edit or EDIT for creating or editing
a CAP source document.
FORMAT      Submits a CAP source document for formatting, using one of the
standard
format definitions provided by the CAP administrator.
SPELLING      Checks the spelling of words in the document against the central
standard
dictionary PROOF_DIC.X and the PROOF_DIC file (if any) in your
logon account.
READABLE      Reports the number of words, sentences, and readability level of
a CAP source document.  Three standard methods of calculating readability are
applied:  Flesch, Kincaid, and FOG.
Note that
this function only checks portions of the source file that are to be
formatted, i.e., passages of words arranged in sentences.  Tabular
material and lists are generally ignored.
MASTER      Places you in the Master Menu.  The Master Menu is the next menu
level
in CAP, which allows you additional flexibility in document processing.
END      Exits the Main Menu, clears the terminal screen, and returns
you to the system level prompt (!)
00001
00002
00003
00004
00005
00006
00001
00006
00005
00002
00005
00004
00004
00003
The Master Menu is displayed on the screen in the same format as the CAP Main
Menu , with a top and bottom window.  The Master Menu contains 10 selections,
with some leading to submenus.
 
To bypass the Main Menu each time CAP is invoked and access the Master Menu
directly, do the following:
 1. Select CONTEXT from the Master Menu.
 2. Select JOB from the Context Types menu.
 3. Select MASTER from the Job Control menu and enter a new value of NO.
ANALYZE
Performs readability tests, spelling checks, and other functions that comprise
a "writer's toolkit".
TEXT
Peforms text conversion and file manipulation functions.
GRAPHIC
Converts graphics from various sources into a format that CAP can understand,
so that pictures can be included in a document when formatted.  Also, displays
and modifies graphic files.
PRINT
Allows the user to print a Device-Specific file (DSF) or Device-Independent
(DVI) file that may be copied to an appropriate device.
 
When specifying a page number, you may use the wildcard feature.  To print
pages 3 and 4 of Section 1, use the following sequence:
 
Starting page number:  ?.1.3
Ending page number:  ?.1.4
 
The * may be used as a wildcard also.
To print the entire file, enter  <CR> at the "Starting page number:"  prompt.
 
To print the entire section, either omit Z (last digit in the number) or
replace it with a wildcard.  An example of how to print all of Section 1 is as
follows:
 
Starting page number:  ?.1 or ?.1.?
Ending page number:  ?.1 or ?.1.?
 
Note:  Preliminary CONTEXT submenu changes may have to be made prior to using
this function (see the FORMAT_CONTEXT subtopics).
SEARCH
Searches text and graphics files for specified words and phrases, and searches
multiple accounts for a given file name.
CONTEXT
Defines context parameters that control the operation of CAP. Allows the user
to change the default options for formatting files, Job Control Language (JCL)
files, graphic handling, and auxiliary programs.
OFFICE
Invokes office automation tools such as electronic mail, electronic meeting,
personal calendar, and graphics programs.
END
Exits the Master Menu, clears the terminal screen, and returns you to the
system level prompt (!)
EDIT      The Edit Document function initiates the user's editor for the
purpose of creating or editing a CAP source file.  The default file editor is
EDIT. The editor can be changed by selecting the Context Change function.
 
The CAP source file to be created or edited is entered at the "File to edit:"
prompt.  The default is the last edited or formatted file.  CAP source files
can be edited using the 6EDIT screen editor, the EDIT line editor, or any
other host-based editor on the CP-6 system.
FORMAT      The Format Document function calls the TeX formatter to produce
CAP DVI and DSF files, and print formatted files.
00009
00008
00010
00001
00002
00003
00004
00005
00006
00007
00001
00006
00009
00008
00010
00003
00007
00004
00005
00002
GRAPHIC_MODIFY
OFFICE_MENU
The Office Automation menu allows you to perform a number of office automation
functions, including use of electronic MAIL, a personal CALENDAR, electronic
meetings, and business graphics.
MAIL
Accesses CP-6 MAIL, allowing you to process incoming and outgoing mail while
in a CAP session.  See the CP-6 MAIL Reference Manual (HA04) for additional
information.
MEETING
Invokes DABBLE.X, allowing you to display information from an electronic
bulletin board randomly or sequentially, and to list and respond to messages.
See the HELP file on DABBLE.X for more information or type HELP at the
greater-than (>) prompt upon entering `Electronic Meeting'.
CALENDAR
Accesses CALENDAR.X, allowing you to set up a personal calendar on a day-to-
day basis.  See the HELP file on CALENDAR.X for additional information or type
HELP at the colon (:)  prompt upon entering Personal Calendar.
GRAPHICS
Invokes the GRAF.X business graphics package.  This tool is used for creating
word
slides/transparencies.  See the GRAF.X HELP file for more information or type
HELP at the colon (:)  prompt upon entering Business Graphics.
 
Level headings (\Ln) automatically become HELP topics and paragraph list items
(\PIs) become HELP subtopics, unless a HELP heading (\HH) is used to override
the default.  HELP headings are also used to specify HELP topic or subtopic
synonyms.
 
The \HH control on line 1 of this source file identifies the HELP ABSTRACT or
default message for this HELP file.  The \HH control overrides the \L1 level
head control.  The title ABSTRACT does not print and is optional.  The letter
A (last field) tells CAP that all the following text is the default HELP
message.  This text prints in the manual version as well.  Line 2 is the text
of the default HELP message.
 
Line 3 contains a level two heading that creates HELP topic DIZZY_DUCK. Line 4
is the text for topic DIZZY_DUCK.
Line 5 contains a \HH control with an overriding title of DUCK_LONE, and the K
indicates that it is a HELP topic.  Line 6 is the text for topic DUCK_LONE.
Line 7 begins a paragraph list named DESCRIBE. Lines 8 and 9 contain paragraph
list labels that become subtopics under the topic DUCK_LONE. Line 10 contains
the ending control for paragraph list DESCRIBE.
 
Line 11 contains a \HH control with an overriding title of LAME followed by
one synonym (WOODEN_LEG). The last field contains an S indicating that this is
a subtopic under the topic DUCK_LONE.
 
Line 12 contains the text for subtopic LAME.
 
Line 13 contains an X in the last field of the \HH control that tells CAP to
omit this heading as a HELP topic.  However, the text that follows this
heading (line 14) is included in the previous topic:  DUCK_LONE, under the
subtopic LAME.
 
Line 15 names a new paragraph list.  Lines 16-17 will be numbered "1."  and
"2."  when this paragraph list is formatted.  Line 18 ends the ARABIC
paragraph list.  This paragraph list style will be part of the HELP message
text for DIRTY_DUCK; only labeled paragraphs are turned into subtopics.
 
Line 19 contains a level two heading that defaults to topic COLD_DUCK.
 
Line 20 contains a help mode off (\HMF) control that turns HELP off (see line
22).
Line 21 will not appear in HELP, but it will appear in the formatted manual
version of this source.
 
Line 22 contains a help mode on (\HMN) control that turns HELP back on (see
line 20).
 
Line 23 contains the first line of text for the topic COLD_DUCK.
 
Line 24 contains a subset (\SB) control labeled HELP. The subset is used to
isolate HELP-only information and manual-only information so that the same
source can produce a manual as well as accurate HELP messages.
 
Lines 26-28 are part of HELP-only information.
 
Line 29 contains an unlabeled \SB control, which defaults to manual-only
information, and is ended with an \SB control.
00001
00002
00003
00004
00003
00004
00001
00002
CAP allows the user to search for information on line, with the
ability to generate and display that information. Features include:
 
o   Hierarchical structure--on-line HELP documents are arranged into a
 
    tree structure.  This makes it easy to retrieve information
    on the system.
 
o   On-line message lists--lists of messages and submessages are
    generated automatically. This makes the on-line HELP facility easy
 
    to update and maintain.
CAP has an on-line HELP facility.  CAP users can display syntax formats,
parameters, and descriptions of controls as well as descriptions of menu items
and related information.  For a list of HELP topics for CAP from the system
command level (!), enter the following at the terminal:
 
HELP (CAP) TOPICS
In CAP, a document format is not dependent on a particular output
device. Any document format available to the user can be produced on
any device supported by CAP. CAP  supports the following output devices:
 
   Monospaced devices
 
   QMS QUIC devices
 
   PostScript devices
The Computer Aided Publication (CAP) system automates and manages the
authoring, formatting and maintenance of technical
publications.  Text editing and graphics processing are performed on
the CP-6 system or on a workstation connected to C-6. The resulting
data is then converted to standard CAP files. A formatting program
(TeX) reads the CAP text files and, using a predefined format,
creates a version of the document broken into pages but without any
device-specific codes. A CAP resolver merges graphic
images with paged text and adds
other device-specific information. The end product is a device-specific
file that can be displayed on a particular output device, such as a
laserprinter or lineprinter.
 
The CAP user creates document text and defines structural elements
(such as sections, headings, paragraphs, tables, and figures) in the
document with formatting instructions that CAP understands. These
formatting instructions, called controls, constitute the Document
Structuring Language (DSL).
 
After creating a document file, the CAP user selects a format style
(predefined by the CAP administrator) in which to format and print
the document. CAP then automatically interprets the DSL controls
to create the document in the desired appearance on the designated
output device.
A wide variety of formatting and style options are available to the
CAP user, as follows:
 
o   Odd and even page styles--different headings, footings, and
 
    layouts conditional on the facing of the page can be defined.
 
o   Heading styles--section, chapter, module, and paragraph headings
 
    can be defined to appear in various type styles and locations on the
    page, with and without page numbering and related headers and footers.
 
o   Named structures--most structural elements in a document (chapter,
    heading, paragraph, table, figure, index, etc.) can have multiple
 
    named variations. For example, a chapter structure can be specified as
    front matter, a section, an appendix, or an index; a table can be
 
    specified as being from 1 to 10 columns, etc.
 
o   Paragraph lists--items can be listed in various format styles.
 
    Numbered, lettered, and bulleted lists are automatically indented and
    spaced based on the particular style selected; additional DSL controls
 
    for indenting and spacing are not required.
 
o   Table definition--simple and complex table formats are available.
 
    Tables can be internally formatted, so that multiple-column tables can
    have formatted passages inside each column.
 
o   Page numbering styles--CAP supports Arabic page numbers as well
    as upper- and lower-case Roman page numbers, as a function of chapter
 
    style.
 
o   Running headers and footers--these are a function of the title
 
    page and chapter style, and are invoked automatically whenever a
    document is formatted.
 
o   Widow control--paragraphs tend to stay on one page.  The CAP formatter
    automatically "walks copy" to achieve an attractive
    appearance.
 
o   Keep-together blocks--passages which should not be split over
    two pages can be flagged and moved to the next available full page,
 
    if necessary.
 
o   Footnote generation--footnotes are defined next to the passage
    to which they refer.  During formatting, they are automatically
 
    numbered and placed on the current page.
 
o   Hyphenation--the CAP formatter automatically applies an
 
    algorithmic formula to determine where a word should be divided. An
    exception dictionary, user global exceptions, and discretionary
 
    hyphenation are available.
 
o   Extended character handling--proportional spacing, multiple
 
    fonts, and foreign language characters are available.
 
o   Mathematical typesetting--documents can include complex
 
    mathematical formulas, either inside a line or set apart as equations.
 
o   True horizontal justification--lines are automatically stretched
 
    to fit the right margin.
 
o   True vertical justification--pages are automatically stretched to
 
    fit the entire page.
The Auxiliary Programs submenu allows you to set defaults for various programs
that can be accessed from CAP.
 
Note:  To reset the default for any of the Auxiliary Program Context options,
enter a dash (-) at the option prompt and the original default for that option
is displayed on the menu.
EDITOR
Determines the type of editor used when the Edit Document function (Master
Menu) is invoked.  This option prompts for the fid of the new editor.  If an
account is not specified, :SYS is assumed.
MAIL
Determines the default electronic mail system for the user.  Enter either the
name of the run unit or dialog script for the new electronic mail processor.
If an account is not specified, :SYS is assumed.
MEETING
Determines the default electronic meeting processor (bulletin board) for the
user.  Enter either the name of the run unit or diaglog script for the new
electronic meeting processor.  If an account is not specified, :SYS is
assumed.
CALENDAR
Determines the default personal calendar processor for the user.  Enter either
the name of the run unit or diaglog script for the new personal calendar
processor.  If an account is not specified, :SYS is assumed.
GRAPHICS
Determines the default business graphic processor for the user.  Enter either
the name of the run unit or diaglog script for the new business graphic
processor.  If an account is not specified, :SYS is assumed.
00001
00002
00003
00004
00005
00004
00001
00005
00002
00003
The CAP system ensures quality publications with the following
features:
 
o   Readability test--CAP includes a fast readability program,
    capable of processing hundreds of pages in less than a minute.
 
    The program produces a report that includes FOG, Kincaid, and
    Flesch readability indexes, as well as a plain-language summary of
 
    the readability level.  The report also tells how many multisyllabic
    words and sentences are in the subject document.
 
o   Spelling check and correction--CAP recognizes over 125,000
    words.  Words it does not recognize are flagged.  The user
 
    can request a list of similar correct words, add the word to a
    personal dictionary, or correct the word in the document. While
 
    correcting words, the user can move both forwards and backwards in
    the list of flagged words.
 
o   Dictionary maintenance--CAP provides tools to expand and
    maintain both the central dictionary and personal dictionaries.
 
o   Limited word dictionary--CAP can be used for limited word
    applications.  CAP reports all words in a document that are not
 
    in a list of allowable words.  This is especially useful when writing
    for an audience whose native language is not English.
 
o   Prohibited word dictionary--CAP can be used for prohibited word
    checking.  CAP reports all words in a document that are in a list
 
    of prohibited words.  This is especially useful when writing for an
    audience that is sensitive to words such as "he" or "she".
 
o   Word frequency check--CAP reports the most frequently used
    words in a document.
 
o   Word lookup--CAP can be used to check the central and other
    dictionaries for the presence of particular words.
 
o   Unprintable character test--CAP can be used to check on and
    report the presence of unprintable characters in a document.
 
o   Control validation--Before formatting a document, CAP can
    be used to check the DSL control syntax structure in a document
 
    file and report any errors.
 
o   Standard formats--CAP guarantees consistency from publication
 
    to publication by making a set of administrator-defined standard
    formats available to the user.
Additional CAP information is presented in the following manuals:
 
CAP DSL Reference, Order No. HA27
CAP ADSL Reference, Order No. HA28
CP-6 CAP Administrator Guide, Order No. HA30
SEARCH_MENU
The Search Functions menu is used to search files for text strings or search
accounts for files.
FILES
Searches a file or files (using a question mark (?) as a wildcard) for a
specified string of characters.  First, you are prompted for the file(s) to be
searched.  The file name is usually wildcarded.  If a file name is not
specified, all files in the current file management account are searched.
Next, you must indicate where the output information should be stored.  Each
record in the specified file(s) is searched for an occurrence of any of the
specified string(s).  If any string is found in a record, the record is output
(along with its EDIT key or record number) to the location you specify.  This
feature is not case-sensitive; all forms of a specified word is searched for.
See the HELP file on GOPHER.X for more information.
ACCOUNTS
Searches a range of accounts (using a question mark (?) as a wildcard) for a
given file name.  First, you are prompted for the name of the file you are
looking for.  (You may use a wildcarded name.)  Next, you must specify a range
of accounts to be searched.  (The search accounts have been determined in
Formatting Context Options menu, option 9.)  Note that the wildcard feature
can be used only in a limited way on this option; that is, the question mark
(?)  can be entered only at the end of an account name.  The default is the
current working account.  Finally, you are prompted for a file name in which
to store the results.  See the HELP file on FIND.X for more information.
00001
00002
00002
00001
PAGE_FORMATTING
ANALYZE_MENU
The following facilities can be used to create text for use with
CAP:
 
o   6EDIT - the CP-6 screen editor runs on virtually any asynchronous
 
    screen terminal device, and can be customized to suit the user's
    needs.  If the user is already accustomed to a particular editing
 
    program, 6EDIT can be set up to duplicate familiar keystroke sequences.
    The Input Manipulation Processor (IMP) can be used to assign the
 
    keystroke sequences to the terminal function keys.  6EDIT is documented
    in the CP-6 6EDIT Reference Manual (CE70).  IMP is documented in
 
    the CP-6 Programmer Reference Manual (CE40).
 
o   EDIT - the CP-6 line editor is used for nonscreen terminals (such
    as the new "lap" computers). EDIT provides a simple and convenient
 
    way of editing text files.  EDIT is documented in the CP-6
    Programmer Reference Manual (CE40).
 
o   PC - a personal computer word processor or text editor can be used
    to create and edit document files. These files can be uploaded to the
 
    CAP system and/or downloaded for off-line editing using the PC Terminal
    Facility (PCTF). PCTF is documented in the CP-6  PC Terminal Facility
 
    Reference Manual (HA15).
The Text Manipulation menu is used to assist in document processing.
KEYED
Converts a consecutive or unit record file to an EDIT-keyed file.  Note that
this option actually runs the file through the ELBBIRD.X tool.
 
This function is especially useful when you want to use information contained
in a DRIBBLE file or a mailgram.  However, some editing may be required after
the conversion due to extraneous DRIBBLE messages or mailgram-essential data.
OUTLINE
Builds a CAP control file from an outline based on the column in which the
item in the outline starts.
PRETTY
Performs a "wordwrap" on the specified file, but does not modify the control
calls.  A wordwrap smooths out the long and short lines in a CAP source file,
making them all more or less the same length.  Wordwrap only applies to areas
in the source file that are to be formatted, such as sentences.  Wordwrap
skips over areas that have been flagged with an \FIF control.  The \FIF
control specifies that all text following this control print exactly as
entered.  For more information, see the DSL Reference Manual (HA27).
 
This selection issues several prompts that allow the user to modify the type
of wordwrap.  For example, the "sentences" prompt (if Y is answered) makes
every sentence start on a new line - a useful feature when editing with the
EDIT line editor.
MERGE
Combines several files into a single file.  Wildcarding and ranges are
permitted on the input file list.  Files created in this way can be any legal
PCL fid.  The created file cannot be decollated; however, a range of files or
list of files can be used as a criteria for file selection.  This is a fairly
complex operation and should be used only if the user understands how CP-6
handles multiple files.
COLLATE
Collates a number of similarily named files into a single file.  The files to
collate are specified using a double question mark (??) as a wildcard
character.  For example, to collate all files beginning with X25, enter X25?
at the first prompt.  The target file for collation can be decollated at a
later time.  This is a fairly complex operation and should be used only if the
user understands how CP-6 handles multiple files.  WARNING: When collating
files, you have the option of deleting the input files.  If you choose to do
this, make sure the name of the target (collated) file does not match the
wildcarded string (of input files), otherwise the collated file mistakenly
will be deleted also.
DECOLLATE
Decollates a collated file into its original file names.  If the files still
exist, they will be replaced.  This is a fairly complex operation and should
be used only if the user understands how CP-6 handles multiple files.
SUBS
Converts specified string(s) within a file containing comment controls to the
specified conversion string(s).  An example of a substitution string is as
follows:
 
    \*{SUB{A00},{B01}}
 
where A00 is the string CAP searches for and B01 is the substitution string.
 
Substitution begins immediately after CAP encounters a substitution control in
the specified file and continues until end-of-file.
A00
This function converts an A00 CAP file to a B01 CAP file.  A00 CAP macros are
converted into B CAP corresponding controls.
 
Note that B CAP does not convert every A00 CAP macro.  For the exceptions, see
Appendix B of the DSL Reference Manual (HA27).
00001
00002
00003
00004
00005
00006
00007
00008
00008
00005
00006
00001
00004
00002
00003
00007
In many environments, the data included in a document set must be
carefully controlled.  Changes from one version to the next must be
tracked closely.  CAP provides for controlled updating with the
following features:
 
o   Global search--sometimes there is a need to change every
 
    reference to a certain part or item.  If such references are
    contained in hundreds of files, it could take days to make the
 
    changes on a word processor.  The CAP system can search hundreds
    of documents and thousands of pages with a single request.  Even
 
    searches of more than 5000 pages take less than 10 minutes.
 
o   Change marks--changes to a document can be flagged with change
 
    bars, and deletions flagged with deletion marks.  The printing
    of these symbols is automatic, but can be suppressed on request.
The user interacts with CAP via a set of consistently structured
menus, submenus, and prompts for menu selections.  Defaults values are
automatically displayed with the prompts. A HELP facility is
available to provide additional information at the menu prompt level.
 
All of the DSL formatting controls have a consistent, similar syntax
structure, for ease of use. The controls can be placed anywhere on a
line in the document source file; there can be multiple controls per
line as well as multiple lines per control.
 
The CAP menus are described in detail in Section 3.
