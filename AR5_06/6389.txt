This section describes the preparation process required for CAP. Preparing for
the installation of the CAP system is the most important phase of a CAP
installation.  The better the planning, the more likely CAP users will be
satisfied and productive.  By identifying device selection, communications,
training, and other concerns ahead of time, many problems can be avoided.
 
Planning ahead for the installation of the CAP system is very important - the
better the planning,  For information on the device drivers, see the following
help files:
 
HELP (QMS) For a description of the QMS Lasergrafix laserprinters that use the
QUIC language.  HELP (POSTSCRIPT) For a description of the PostScript
laserprinter.  HELP (HP) For a description of the HP LaserJet Plus, Series II,
and SERIES III printers.  HELP (ASCII) For a description of ASCII output
devices.  HELP (PREVIEW) For a description of the PREVIEW device.
CP-6 CAP Administrator Guide - HA30-00
*************************************************************************
*
* Copyright (c) Bull HN Information Systems Inc., 1989, 1994
*
*************************************************************************
6Edit is a screen-oriented file editor.  Instructions for inserting, deleting,
and replacing data are given by moving the cursor to the desired data on the
screen, and typing in new data.  6Edit is probably the most common CAP text
editing program.  It works on many different screen terminals and provides
functions that make text editing convenient.  Therefore, 6Edit is a good
choice for CAP sites with a variety of devices.  6Edit simplifies the training
process by allowing all users to work on a single editing program.
 
In addition, 6Edit can be customized to perform special functions or to
emulate (to a greater or lesser degree) a different editing program.  This is
useful if the prospective CAP users are already familiar with an editing
program that will not be part of the total CAP environment.  See the CP-6
6Edit Reference Manual (CE70) for more information.
Access control on file accounts is maintained by the Packset Initializer
processor (PIG), which can be run by the system manager or a designated pack
set manager.  All account controls are authorized and changed through commands
to the Packset Initializer Processor.  See the CP-6 System Support Reference
Manual - Volume I (HA20) for more information.
There are many versions of the ANVIL product.  One version, called ANVIL/4000
is available on the CP-6 operating system.  Other implementations of ANVIL
include ANVIL/1000 (a PC-based version), and ANVIL/5000 (a supercharged ANVIL
not available on the CP-6 system).
All versions of ANVIL are capable of producing a plotfile, which is a version
of a CAD graphic formatted for a simple-minded plotter.  The documentation for
each version of ANVIL describes how to produce such a file.  If ANVIL/4000 is
used to create the plotfile, CAP can convert the plot file directly.
 
If ANVIL/1000 is used, then either KERMIT or MODEM must be used to move the
plotfile to the CP-6 system.  If ANVIL/5000 is used to create the plotfile
(for instance on a non-CP-6 mainframe), the data can either be sent to the CP-
6 system via a communications link, or copied to tape and transferred to the
CP-6 system.  In either case, the system support staff for the CP-6 system
must become involved to a greater or lesser degree.  Note that ANVIL can be
used to convert IGES files.
CAP supports AutoCAD (ADE/3 Level 1) through the DMP7 plotfile feature.  To
obtain an uploadable file on the PC, AutoCAD must be configured for a DMP7
plotter, with the Plot into File option set to YES. This file can then be
uploaded to the CP-6 system using KERMIT or XMODEM.
 
Note that since CAP is a monochrome environment, it is best suited to drawings
that do not use color.  The test version of AutoCAD at LADC runs with a
monochrome graphics card.  The AutoCAD convertor program has not been tested
with graphics created by AutoCAD with a color graphics card.  Note that
AutoCAD can be used to convert IGES files.
The CAPADMIN Main Menu serves primarily as a gateway to other menus.  It
contains a selection for each kind of definition maintained by CAPADMIN. Each
of these leads to a submenu of functions for that type of definition.  It also
has selections to change the current account and to terminate CAPADMIN.
 
The administrator enters the name or number of the desired menu selection at
the "CAPADMIN Function:"  prompt.  Additional prompts depend on which function
is selected.
ACCOUNT This selection changes the account whose :CAP file is being accessed.
On entry to CAPADMIN, this is the administrator's logon account.  The current
account is shown at the bottom of all CAPADMIN menus.  When this function is
selected, the administrator is prompted for the desired new account name.  The
account name can be optionally preceded with a period (.).  A period alone is
taken to mean the administrator's logon account.  If no new account is
entered, the current account remains unchanged and the administrator is
returned to the Main Menu prompt.
 
If the specified account does not exist or its :CAP file cannot be accessed,
an error message is issued, and the current account is unchanged.  If there is
a :CAP file but the administrator is prevented from writing into it by file
management access controls, the account is changed to the one specified but
only selections that do not alter the file can be selected.  If there is no
:CAP file in the account and access controls permit the administrator to
create one, the account is changed and an empty :CAP file is created.
 
For convenience, this menu selection is also available from any of the
submenus that can be selected from the Main Menu.  This can save
administrators the trouble of returning to the main menu if they forget to
change the account before selecting a Main Menu function.
FORMAT This selection leads to a submenu of functions that allow the
administrator to maintain CAP format definitions.  New formats can be created
from scratch or copied from an existing format in the same or another :CAP
file.  Existing formats can be displayed, changed or deleted.
DEVICE This selection leads to a submenu of functions that allow the
administrator to maintain CAP device definitions.  New devices can be created
from scratch or copied from an existing device in the same or another :CAP
file.  Existing devices can be displayed, changed or deleted.
CONTEXT This selection leads to a submenu of user context option types.
Context options determine the CAP user's working environment.  Options include
the editor to be used to maintain source documents, device assignments for
viewing graphics, and many others.
END This selection from the Main Menu terminates CAPADMIN. Unlike other menus,
where a null response to the menu prompt returns to the prior menu, an
explicit END selection is required to exit from the Main Menu.
00001
00002
00003
00004
00005
00001
00004
00003
00005
00002
The form of the Cappix image file is a header record, followed by data.
 
Header record:
 
    %MACRO VA_PIXEL_HEADER(FPTN=VA_PIXEL_HEADER,
           STCLASS=STATIC);
    DCL 1 FPTN STCLASS,
         2 TYPE UBIN(9) CALIGNED,
         2 COMP UBIN(9) CALIGNED,
         2 NUM_LINES UBIN(18) CALIGNED,
         2 NUM_PIXELS UBIN(18) CALIGNED;
    %MEND;
 
    %EQU VA_BIT# = 0;
    %EQU VA_GRAY# = 1;
    %EQU VA_NO_COMP#=0;
 
There are 2 types of data storage:
 
    0 - Bit map data, 1 bit per pixel, 8 bits per byte, 0 = black, 1 = white
 
    1 - Gray scale, 1 pixel per byte, 0 = black, 255 = white.
 
The COMP byte is intended to indicate compression.
 
The "# lines" is the height of the picture in pixels.  The "# pixels/line" is
the width of the picture in pixels.
The header record is followed by the data records.  Data records can be any
size up to 1024 bytes.
 
At the time the data are sent to a device (usually the laserprinter), the
document is converted by a CAP resolver.  The resolver invokes a program,
VA$CR_LZ_AUX1, which converts the output to the format for the QMS
laserprinter.
IDENTIFYING_USERS
Two new sections have been added to this manual to document two new CAP
devices:  the HP LaserJet Device and the Preview device.
 
Knuth, Donald E., Computers and Typesetting, Volumes A-E (Addison Wesley,
Massachusetts, 1986).  These volumes are as follows:
 
A.  The TeXbook
B.  TeX: The Program
C.  The METAFONTbook
D.  METAFONT: The Program
E.  Computer Modern Typefaces
 
    Notation               Description
 
    Lowercase Letters      Lowercase letters indicate a variable, to be
                           replaced with a user-selected value.  For
                           example:
                           \IS{fid} could be entered as \IS{MyFile}.
 
    Uppercase Letters      Uppercase letters indicate a literal, to be
                           entered as shown.  For example:
                           \SP{B|5}
                           must be entered exactly as shown.
 
    Special Characters     Special characters (such as \or {) are
                           literals, to be entered as shown.
 
    Numerals               Numerals standing alone are literals, to be
                           entered as shown.  Numerals embedded in or
                           affixed to a string of uppercase letters are
                           also literals, to be entered as shown.
                           Numerals embedded in or affixed to a string of
                           lowercase letters are part of the variable
                           name to be replaced with a user-selected
                           value; for example, fid1.
 
    Braces ({})            Elements inside a pair of braces identify a
                           required choice.  For example:
                           {ON|OVER|INTO}
                           means that either a value of ON, OVER, or INTO
                           must be entered.
 
    OR Bar (|)             The OR bar separates elements in a list from
                           which one or more elements may be, or must be,
                           chosen.  See braces example above.
 
    Horizontal Ellipsis
    (...)                  The horizontal ellipsis indicates that a
                           previous braced element may be repeated, or
                           that elements have been omitted.  For example:
                           \TP{tpone|tptwo|...|tpnine}
                           means that one or more (up to nine) tp
                           parameters may be entered, with an OR bar
                           inserted between each parameter.
    Vertical Ellipsis      The vertical ellipsis indicates that controls
                           or textual passages have been omitted.  For
                           example:
                           \IT
                            .
                            .
                            .
                           \NO
                           The above means that controls and/or text
                           could be included between the \IT and \NO
                           controls.
The Formatting Options menu contains options that affect document formatting.
Some of these specify defaults for the format, device, and various accounts.
Others supply values that control the formatting process.
 
To change an option, the administrator enters an option number or name shown
in the menu at the "Option to Change:"  prompt.  For example, a prompt of "New
Document Source Account:"  is issued if 1 or DSL is entered at the menu
prompt.  The administrator should respond to this prompt with the desired
account.  New values are reflected in the menu when the menu prompt repeats.
A null response at an option prompt retains the option's current value.
DSL Specifies the default account assignment for various CAP tasks.  This
account is used whenever the user responds to a prompt for a document source
file with a fid that does not specify an account.  The default is the current
file management account.
DVI Specifies the default account where permanent device-independent files are
stored.  This account is used whenever the user responds to a prompt for a DVI
file with a fid that does not specify an account.  This option is only
meaningful if the MASTER context option is set for the user, since only these
users can create permanent DVI files.  The default is the current file
management account.  If the site has established a common account to hold DVI
files for formatted documents for later printing, the administrator should set
this option in the system :CAP file to that account.
DSF Specifies the default account where permanent device-specific files are
stored.  This account is used whenever the user responds to a prompt for a DSF
file with a fid that does not specify an account.  This option is only
meaningful if the MASTER context option is set for the user, since only these
users can create permanent DSF files.  The default is the current file
management account.  If the site has established a common account to hold DSF
files for later printing, the administrator should set this option in the
system :CAP file to that account.
FORMAT Specifies the name of the CAP format to be established as the default
when the user invokes CAP. This is only the initial default; if a different
format is used in the course of a CAP session, that becomes the new default.
Entering a double question mark (??) at the prompt for this option produces a
list of formats available to users of the current :CAP file.
DEVICE Specifies the name of the CAP device to be established as the default
when the user invokes CAP. This is only the initial default; if a different
device is used in the course of a CAP session, that becomes the new default.
Entering a double question mark (??) at the prompt for this option produces a
list of devices available to users of the current :CAP file.
SEV Specifies the default error severity level that CAP accepts when
formatting a document.  If an error whose severity exceeds this level occurs,
the document is not resolved or printed.  If the MASTER context option is set
for the user, the default severity level can be overridden by the
corresponding selection from the CAP Formatting Options menu.
 
When this option is selected, a submenu of possible severity levels appears in
the top portion of the dialog window.  These are:
 
WARNING    Specifies that formatting jobs be terminated if any warnings are
    issued.  TeX issues warnings when it is forced to do something it thinks
    is "bad".  Users may or may not agree with its assessment, or even notice
    that anything is amiss.
ERROR    Specifies that formatting jobs be terminated if any errors are
    diagnosed.  TeX errors generally indicate that the document is incorrectly
    formatted at the point where the error was detected, and possibly beyond.
    Misspelled controls or mismatched braces are common causes of errors.
    ERROR is the default severity level.
ABORT    Specifies that formatting jobs only be terminated if TeX aborts.
    Aborts are fatal errors that force TeX to terminate prematurely.  The
    formatted document will be incomplete, if one is produced at all.
TYPE Specifies the default for the type of file that is created as the final
output of a formatting job.  Users can override this by resetting options in
the CAP Formatting Options menu when they format a document.
 
When this option is selected, a submenu of possible output file types appears
in the top portion of the dialog window.  These are:
 
DVI    Specifies that formatting is to stop after producing the DVI output
    from TeX. These files can then be resolved and printed using CAP's PRINT
    function.
DSF    Specifies that formatted documents are to be resolved into DSF files,
    but not written to the final output device.  Instead, the DSF files must
    be later copied to the printer with CAP's PRINT function.
PRINT    Specifies that formatted documents are to be printed directly on the
    final output device.  In this case, a temporary DVI file is used, and no
    DSF disk file is created.  This is the default.
 
This option is only meaningful for users who have the MASTER context option
set so that they use CAP's Master Menu instead of the shorter Main Menu.  When
documents are formatted from that menu, they always print directly on the
output device.
REUSE Specifies whether TeX should reuse any existing temporary files when
reformatting a document.  TeX uses temporary files to collect entries for the
table of contents, the index and cross references.  Reusing files left over
from a previous run for the same document can save an extra formatting pass if
all of the entries from the prior run still apply.  YES specifies that these
file be reused if they exist.  NO specifies that all temporary files be
recreated from scratch for each formatting job.  The default is NO.
 
This option is only meaningful when documents are formatted online, since CP-6
deletes all temporary files at the end of a batch job and when an online user
logs off.
SEARCH Specifies accounts to be searched to find auxiliary source files that
are needed during TeX formatting.  These accounts are searched when no account
is specified on for an ADSL control file or other file that is reference
within a document.  Accounts specified here are not searched to find the
document source files that CAP user requests to be formatted; those files must
be in the account specified by the DSL option in this menu if an account name
is not explicitly provided.
 
This option accepts either a single account name or a list of up to six
accounts.  Each pair of accounts in a list must be separated by a comma.
Account names can optionally be prefixed with a period.  This option, when
combined with the other elements of the search list for TeX, must not result
in a list of more than eight unique accounts.  The default is no special
search list for source files.  To revert to the default, the administrator can
enter a minus sign (-).
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
The Graphics Processing Options menu sets options that affect CAP's graphic
conversion and display facilities.  The CAP graphics options fall into three
classes:
 
o   Default accounts:  If the site has a special account defined to hold
    graphic files, the administrator can make it the default account for all
    prompts for a graphic /fid.  A separate default accounts can be specified
    for DIGIS graphics; this is convenient when the site maintains DIGIS
    copies of graphics for online display.  Both accounts default to the
    user's current file management account.
o   Online display options:  There are several options that relate to CAP's
    online graphic display facility.  Online graphic display is most useful
    for users that have terminals with graphic capabilities that are supported
    by DIGS. However, the defaults are set to values appropriate for a simple
    ASCII terminal.
    CAP can only display DIGIS graphics, so this facility is only available to
    sites that have also purchased CP-6 DIGS. The administrator must establish
    procedures to maintain graphics in both DIGIS and CAP (SGL or Cappix)
    format; this is why there are separate default accounts for each kind of
    graphic.  In addition, users must be authorized to start an fprg to use
    this facility.
o   Site specific graphics:  Sites can use graphics that are not supported as
    part of CAP by supplying their own facilities to convert these graphics to
    and from a standard CAP format.  These can be either run units or ADAPT
    dialog scripts.  The CAP menus for graphic import and export each contain
    a selection to invoke s site-specific conversion facility.  If a run unit
    is used, it must issue prompts for input and output files and any options
    needed, since CAP does not allow for any command line parameters when the
    program is invoked.
 
To change an option, the administrator enters an option number or name shown
in the menu at the "Option to Change:"  prompt.  For example, a prompt of "New
Default CAP Graphics Account:"  is issued if 1 or RR is entered at the menu
prompt.  The administrator should respond to this prompt with the desired
account name.  New values are reflected in the menu when the menu prompt
repeats.  A null response at an option prompt retains the option's current
value.
SOURCE Specifies the default graphics account to be used for all graphics
types except DIGIS. The default is the current file management account.
DISPLAY Specifies the default account for Device Independent Graphics
Instruction Set (DIGIS) graphics.  The default is the current file management
account.
DRIVER Specifies the program that is called when a graphic is displayed by the
DISPLAY selection from the CAP Graphic Functions menu.  The default is COPY,
which is suitable for displaying graphics on the user's terminal.
DEVICE Specifies the device used to display graphics for the DISPLAY selection
from the CAP Graphic Functions menu.  The default is ME, which displays
graphics on the user's terminal.
SCAN Specifies the default number of scan lines to use when converting a
vector graphic to a raster format.  This number should match the resolution of
the user's terminal.  The default is 24, which is suitable for use with an
ASCII terminal.
IMPORT Specifies a site-specific import graphic processor.  If no account is
specified, :SYS is assumed.  The default is a null value, in which case the
CAP menu selection to import a nonstandard graphic is disabled.  To revert to
the default once another value has been specified, the administrator can enter
a minus sign (-).
EXPORT Specifies a site-specific export graphic processor.  If no account is
specified, :SYS is assumed.  The default is a null value, in which case the
CAP menu selection to export a nonstandard graphic is disabled.  To revert to
the default once another value has been specified, the administrator can enter
a minus sign (-).
SEARCH Specifies accounts to be searched to find graphic files.  These
accounts are searched by device drivers when no account is specified for
graphic that is referenced in a document.  Accounts specified here are not
searched to locate files for graphic conversion functions.
 
This option accepts either a single account name or a list of up to six
accounts.  Each pair of accounts in a list must be separated by a comma.
Account names can optionally be prefixed with a period.  This option, when
combined with the other elements of the search list for device drivers, must
not result in a list of more than eight unique accounts.  The default is no
special search list for graphic files.  To revert to the default, the
administrator can enter a minus sign (-).
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
The Job Control Options menu defines special processing to be done when CAP
executes functions.  Some options affect the contents of the JCL files that
are built for execution outside of CAP. Others control the behavior of the CAP
program itself.
 
To change an option, the administrator enters an option number or name shown
in the menu at the "Option to Change:"  prompt.  For example, a prompt of
"Give Progress Messages?"  appears on the screen 1 or CHATTER is entered at
the menu prompt.  The administrator should respond to this prompt with the
desired option value.  New values are reflected in the menu when the menu
prompt repeats.  A null response at an option prompt retains the option's
current value.
CHATTER Specifies whether or not periodic "chatty" messages are to be issued
while performing CAP tasks.  YES requests these messages, NO suppresses them.
The default is YES. This option is honored to varying degrees by different CAP
programs.
INFORM Specifies whether or not to inform the user of a completed job.  YES
requests that a message be sent to the user when a CAP job completes.  This
message also indicates whether the job encountered any errors, as determined
by the STEPCC returned by each job step.  NO specifies that no such message be
sent.  The default is NO. This option only applies when the user submits a
batch job or creates a saved JCL file.
MAIL Specifies whether or not diagnostic messages generated by a job are sent
via electronic mail when the job completes.  YES requests that all diagnostic
output (written to the M$DO DCB) be collected in a file that is sent to the
central mailbox in the user's logon account when the job completes.  NO
suppresses this mailgram; diagnostic messages appear in the job listing file
instead.  The default is NO. This option only applies when the user submits a
batch job or creates a saved JCL file.
PRINT Specifies whether or not to print a job listing.  This listing shows the
JCL used to perform the function, along with diagnostics and other messages
generated by the programs invoked.  Some users may not wish to get a printed
file, particularly if the MAIL option is set to deliver diagnostics to the
user's electronic mailbox.  NO requests that the listing file be erased at the
end of the job.  YES requests that it be printed.  The default is YES.
 
This option only applies when the user submits a batch job or creates a saved
JCL file.  In the case of saved JCL, it is effectively ignored when the JCL
file is executed online.
MASTER  Specifies whether CAP users are initially presented with CAP's Master
Menu or the simpler Main Menu.  YES requests the Master Menu, NO the Main
Menu.  The default is NO.
 
The Master Menu allows users to select from the full gamut of CAP functions.
The Main Menu provides easier access to the most common functions, while still
allowing users to enter the Master Menu to execute other functions.
 
This option also affects how formatting is done.  Main Menu users are
presented with a shorter formatting dialog that assumes that formatted
documents are to be printed directly on the specified output device.  Master
Menu users are given the choice of saving DVI or DSF files on disk for later
printing.  Master Menu users can also specify additional special processing
through selections from a Formatting Options Menu that is only presented to
these users.
MEM Specifies the minimum number of memory pages to perform a CAP function.
The default is 282 pages.  If set to less than the default, some CAP functions
may abort due to lack of memory.  The administrator must ensure that all CAP
users are authorized to request at least this much memory.  No CAP functions
benefit from memory beyond the default, but users who normally run with more
the default amount of memory available can set this option to their usual
limit; this avoids having the excess released when the user executes CAP JCL
files online.
 
For batch jobs, this value automatically supplies the MEMORY parameter on the
RESOURCE "card," so that parameter should not be specified for the RES
selection from this menu.
JOB Specifies what options (if any) are applicable to the JOB "card" during
batch jobs.  The default is no Job Card options.  Entering a minus sign (-) at
this option sets the option back to the default.
RES Specifies what resource card options (if any) are applicable to the
RESOURCE "card" during batch jobs.  The default is no resource options, except
 
for the memory limit specified by the MEM selection in this menu.  Entering a
minus sign (-) restores the default after some other value has been specified.
LIMIT Specifies what options, if any, to place on the LIMIT "card" for batch
jobs and saved JCL files.  The default is LO=9999, which allows users to
produce documents of any size.  Entering a minus sign (-) specifies no special
limits, in which case the LIMIT "card" is omitted from JCL files.
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
User context options determine the CAP user's working environment.  Due to the
large number of options available, they are presented in several submenus, one
for each type of option.  The Context Types menu asks the administrator to
select the type of context options desired.  These selections lead to submenus
of options of the specified type.  As with all second level CAPADMIN menus, a
selection to change the current account is also available.
 
The administrator enters the name or number of the desired menu selection at
the "Context Function:"  prompt.  Additional prompts depend on which function
is selected.
 
Context options are handled in a slightly different manner than format and
device options.  When accessing a user's (or administrator's) personal :CAP
file, context options have no fixed default.  Instead, the default is whatever
is set for that option in the system :CAP file.  It is only when accessing the
system :CAP file that the fixed defaults noted for each option apply.
 
Context options also differ from formats and devices in that they can be set
by individual CAP users.  The CONTEXT function from the CAP Main or Master
Menu accesses the same set of options menus as CAPADMIN does.  However, users
can only set context options for themselves in their personal :CAP file,
whereas CAPADMIN allows administrators to access or change any :CAP file on
the system, CP-6 access controls permitting.
 
The administrator can enter a minus sign (-) at any option prompt to revert to
the default, whatever that may be.  Note that explicitly setting an option in
a personal :CAP file to its default is different than reverting to the default
from the system :CAP file.  If an option is explicitly set, its setting is
retained for that user even if the system value changes.  If the default is
used, a change to the system value affects all users who do not explicitly
specify the option.
ACCOUNT This selection changes the account whose :CAP file is being accessed.
Its function is identical to that of the selection with the same name in the
main CAPADMIN menu.  Refer to the Main Menu for additional information.
FORMAT This selection leads to a submenu of options that have to do with how
documents are formatted.  Some of these specify defaults for the format,
device and various accounts.  Others supply values that control the formatting
process.  These options can be changed through selections from the submenu.
JOB This selection leads to a submenu of options that define special
processing to be done when CAP performs functions.  Some of these affect the
contents of the JCL files that are built for execution outside of CAP. Others
control the behavior of the CAP program itself.  These options can be changed
through selections from the submenu.
GRAPHIC This selection leads to a submenu of options that have to do with
graphics processing.  These include options to specify the default accounts to
use for graphic files and others that determine how graphics are displayed on
the CAP user's terminal.  These options can be changed through selections from
the submenu.
PROGRAM This selection leads to a submenus of options that specify what
program to use for file editing and other auxiliary CAP functions.  These
options can be changed through selections from the submenu.
00001
00002
00003
00004
00005
00001
00002
00004
00003
00005
The Auxiliary Program Options menu defines the programs to use for file
editing and for selections from the CAP Office Automation menu.
 
To change an option, the administrator enters an option number or name shown
in the menu at the "Option to Change:"  prompt.  For example, a prompt of "New
File Editor:"  is issued if 1 or EDITOR is entered at the menu prompt.  The
administrator should respond to this prompt with the desired program name.
New values are reflected in the menu when the menu prompt repeats.  A null
response at an option prompt retains the option's current value.
EDITOR Determines the editor to invoke when the user selects the Edit Document
function from the CAP Main or Master Menu.  The default is EDIT. If an account
is not specified, :SYS is assumed.
MAIL Determines the default electronic mail processor for the user.  This can
be either a run unit or an ADAPT dialog script.  The default is MAIL. If an
account is not specified, :SYS is assumed.
MEETING Determines the default electronic meeting processor for the user.
This can be either a run unit or an ADAPT dialog script.  The default is
DABBLE.X. If an account is not specified, :SYS is assumed.
CALENDAR Determines the default personal calendar processor for the user.
This can be either a run unit or an ADAPT dialog script.  The default is
CALENDAR.X. If an account is not specified, :SYS is assumed.
GRAPHICS Determines the default business graphic processor for the user.  This
can be either a run unit or an ADAPT dialog script.  The default is GRAF.X. If
an account is not specified, :SYS is assumed.
 
Because CAP supports many types of graphics input and different methods of
file transfer, each site will have its own set of procedures that will be
followed to integrate graphics into CAP.
 
This section contains operational information that can be used as a guideline
for creating input graphics for CAP. Exact procedures must be determined by
individual CAP administrators for each CAP site.  It is the responsibility of
the CAP administrator to test, document, and distribute this information
(along with any other material) to users who will be creating graphics.
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
The CP-6 MOVE program transfers files between two CP-6 systems or between a
CP-6 system and a GCOS6/MOD400 system.  MOVE provides many powerful features
that make it convenient to use in the CP-6 environment.  For example, multiple
files can be transferred with a single command, and a message describing the
success (or failure) of the transfer can be sent through electronic MAIL.
 
Also, MOVE does not tie up the terminal.  MOVE allows a user to request a file
on another system or to send a file to another system, even if the two systems
are not currently connected.  When the two systems are connected, MOVE (and
its various service programs) finds the requested file, packages it, transfers
it, and unpackages it, without requiring any user intervention.
Once dictionaries are customized, copies must be made in a protected place on
the system (such as tape backup).  By taking this step, the dictionaries are
not replaced inadvertantly when new versions of CAP and X account software are
installed on the CAP system.  After installation of new software, the COPY
command is used to replace the newly installed dictionaries with the
customized dictionary.  This can be done in two ways:
 
    !COPY customdict OVER supplieddict
 
replaces the supplied dictionary with the customized dictionary.
 
    !COPY customdict INTO supplieddict
 
adds the customized dictionary to the supplied dictionary.
 
The second method is used when the supplied dictionary contains a significant
number of new words that should remain in the dictionary.
 
This section suggests backup procedures which should be adhered to by the CAP
administrator.  Some functions may be performed by either the CAP
administrator or system manager.
CP-6 word dictionaries are modified using the WEBSTER.X tool.  To use
WEBSTER.X, the CAP administrator must have write access to the dictionary to
be updated.  This means that most CAP users can update only the PROOF_DIC in
the logon account.
 
The CAP administrator, however, should be given write access to the global
dictionaries so they can be modified to better serve the requirements of the
individual user site.  Normally, words are added, but sometimes words can be
deleted using VA$WT_LIMITED_AUX1.
CAP supports compressed and uncompressed Datacopy IMG files.  Once converted
to Cappix format, the scanned images can be expanded or reduced by giving
different values to the GR control.  Note that the scaling process tends to
have the best results when the image is displayed at sizes approximately 2/3
of the original.
 
Scanned line drawings should be stored on the scanning device in compressed
format and then uploaded to the CP-6 system.  Scanned images (such as
photographs) should be stored in uncompressed format and then uploaded to the
CP-6 system.  This is because the algorithm that CP-6 KERMIT uses for
compression of files during file transfer is more efficient for photographic
data than the Datacopy compressed format.  Similarly, the Datacopy compressed
format is better for line data than the CP-6 KERMIT compression.  Datacopy IMG
files must be uploaded to the CP-6 system as binary files using KERMIT.
The Device Change Functions menu allows the administrator to view and alter
any of the options for a CAP device.  It is entered after satisfying the
prompts for a CREATE or CHANGE selection from the Device Functions menu.  For
consistency with the corresponding menu for formats, the device options are
presented in a submenu.
 
The name and description of the device being created or changed appears at the
bottom of the menu, just below the line showing the current account.  This
line also appears in the submenu that can be entered from this one.
 
The administrator enters the name or number of the desired menu selection at
the "Device Change Function:"  prompt.  Additional prompts depend on which
function is selected.
 
On exit from the device change menu, if any changes have been made, the
administrator is presented with a prompt asking whether the changes should be
saved.  The default is YES. A response of NO cancels the changes, leaving the
device the way it was before the change menu was entered.  This prompt is
bypassed if no device options were actually altered.
DISPLAY This selection removes the menu window and fills the screen with a
display of the values for all options of the current device.  After viewing
the display, enter <CR> to restore the menu and reissue the menu prompt.
OPTIONS This selection leads to a submenu of the options that make up a CAP
device definition.  These options can be changed by selections from the
submenu.
DESC The device description is a brief phrase describing the characteristics
or use of the device.  The current description is shown in the menu following
the device name, separated from it by a dash (-).  Unlike the previous
selections, this one does not display a submenu.  Instead, it simply issues a
prompt for "New device description:".  The new description replaces the
previous one in the menu as soon as it is entered.  If no new description is
supplied, the current description remains unchanged.
00001
00002
00003
00003
00001
00002
The Device Functions menu is the top level menu for the part of CAPADMIN that
is concerned with maintaining CAP devices.  It contains selections for all the
functions necessary to build, modify and view device definitions.
 
The administrator enters the name or number of the desired menu selection at
the "Device Function:"  prompt.  Additional prompts depend on which function
is selected.
 
Most selections result in a prompt for the name of a device.  Where
appropriate, a default device name appears in parentheses at the end of the
prompt.  The default device is initially the one named LZ@CAP. Thereafter, it
is the last device accessed.  A null response accepts the default, if there is
one.  If there is no default, a null response cancels the function and returns
the administrator to the "Device Function:"  prompt.
 
At any prompt for a device name, the administrator can enter a double question
mark (??) for a list of devices defined in the current account.  This list
appears in the dialog window and is followed by a repetition of the device
name prompt.
ACCOUNT This selection changes the account whose :CAP file is being accessed.
Its function is identical to that of the selection with the same name in the
main CAPADMIN menu.  Refer to the Main Menu for additional information.
LIST This selection lists the name and description of all devices defined in
the current account.  The list appears in the dialog window.  There are no
additional prompts.
CREATE This selection creates a new device in the current account.  The
administrator is prompted for the name to give the new device.  After
accepting the new name, CAPADMIN creates a device with default values for all
options and places the administrator in the Device Change Functions menu so
that options for the new device can be changed to their desired values.
CHANGE This selection changes a device that already exists in the current
account.  The administrator is prompted for the name of the device to be
changed.  After accepting the device name, CAPADMIN places the administrator
in the Device Change Functions menu so that the options that make up the
device can be changed as desired.
COPY This selection copies an existing device.  The device can be copied from
the current account or another one.  It is always copied into the current
account.  The administrator may need to use the ACCOUNT function to change the
current account to the one that will receive the copied device before
selecting the COPY function.
 
The administrator is first prompted for the account containing the device to
be copied.  Any account having a :CAP file the administrator can read can be
specified.  The default is the current account.
 
The next prompt asks for the name of the device to be copied.  A double
question mark (??) response at this prompt lists the devices defined in the
account that is the source of the copy.
 
The final prompt is for the name to give the new copy of the device.  If the
device is being copied from another account, the default is the name of the
device being copied.  If the device is being copied from the current account,
 
it cannot have the same name, so there is no default.  In this case, if no new
name is provided, the copy operation is cancelled.
 
After all prompts have been satisfied, the specified device is copied into the
current account under the new name given and the administrator is returned to
the "Device Function:"  prompt.  The new device is set up as the default for
subsequent operations.  The administrator will typically want to follow a COPY
with a CHANGE function to alter the new copy of the device.
DELETE This selection removes a device from the current account.  The
administrator is prompted for the name of the device to delete.  To avoid
accidentally deleting the last device accessed, there is no default for this
prompt.  A null response returns the administrator to the menu prompt without
deleting anything.  If a device is specified, it is deleted from the current
:CAP file.
DISPLAY This selection displays the settings of all options for a device on
the terminal screen.  The administrator is prompted for the name of the device
to display.  The default is the last device accessed.  After accepting the
device name, CAPADMIN removes the menu and displays the device on the terminal
screen.  After viewing the display, a <CR> clears the screen, restores the
menu, and returns the administrator to the menu prompt.
PRINT This selection produces a display of the all options for a device on a
lineprinter or in a file.  The display has the same layout as the one for the
DISPLAY function.  The administrator is first prompted for the name of the
device to print.  A second prompt asks where the display is to be printed.
The administrator can respond with either the name of a disk file to be
created or replaced, or with a CP-6 device name.  When printing to a device,
note that the display is produced in a form suitable for a lineprinter.  It
may not be printed correctly if directed to a laserprinter.
00001
00002
00003
00004
00005
00006
00007
00008
00001
00004
00005
00003
00006
00007
00002
00008
The Device Definition Options menu contains all the options that make up a
CAPADMIN device definition, with the exception of the device description.
 
To change an option, the administrator enters an option number or name shown
in the menu at the "Device Option:"  prompt.  For example, a prompt of "New
DVI Class:"  is issued if 1 or DVI is entered at the menu prompt.  The
administrator should respond to this prompt with the desired device-
independent file class.  New values are reflected in the menu when the menu
prompt repeats.  A null response at an option prompt retains the option's
current value.
DVI Specifies the class to be assigned to DVI files produced for this device.
All files with a given class can be printed on other devices with the same
class, so identical class names should be used for devices with similar
characteristics.  Class names can be up to 30 characters long and can contain
any ASCII characters.  Names that clearly show the characteristics that
differentiate the class are recommended.  For example, "8.5x11 laserprinter".
DSF Specifies the class to be assigned to DSF files produced for this device.
All files with a given class can be printed on other devices with the same
class, so identical class names should be used for devices with similar
characteristics.  Class names can be up to 30 characters long and can contain
any ASCII characters.  Names that clearly show the characteristics that
differentiate the class are recommended.  For example, "8.5x11 with QMS1200
fonts".
DEVICE Specifies the fid of the CP-6 device on which formatted documents are
to be printed.  This typically specifies both a device and workstation name.
The default is LZ@CAP.
FORM Specifies the CP-6 form to be used to print formatted documents.  The
default is QMSCAP, which is appropriate for all QMS devices.
WIDTH Specifies the width of the physical paper stock for the device.  The
default is 8.5 inches.  If the page size specified by the format fits within
the device's page dimensions, the format's page dimensions are used instead.
If either the length or width for the format exceeds that of the device,
though, the device's dimensions override those for the format.
LENGTH Specifies the length of the physical paper stock for the device.  The
default is 11 inches.  If the page size specified by the format fits within
the device's page dimensions, the format's page dimensions are used instead.
If either the length or width for the format exceeds that of the device,
though, the device's dimensions override those for the format.
RESOLVER Specifies the name of the device resolver program that generates a
device-specific version of documents formatted for this device.  This is
sometimes referred to as the device driver program.  The default is VA$DVILG,
which is the resolver program for QMS laserprinters.  An account is normally
not specified, in which case :SYS is assumed.
 
The drivers that are available for use with CAP are:
 
              VA$DVILG  for QMS devices
 
              VA$DVIPS  for Postscript devices
 
              VA$DVILP  for ASCII devices
 
              VA$DVIHP  for Hewlett Packard LaserJet Devices
 
              VA$DVIAP  for interactive display on ASCII devices
ROPT Specifies any special device driver options needed for this device.  Some
options are supplied automatically and should not be specified here.  These
are COPIES, FORM, RANGE, RESIDENT and SRCH.
 
Device definitions for QMS 1200 laserprinters should specify DEVICE=1200.  QMS
800 devices that are equipped with an output hopper should specify NOREVERSE.
Other options may apply for other devices.
 
More than one option can be specified by placing a comma between each pair of
options.  A minus sign (-) can be entered to specify no special options.
FONT Specifies a device-specific ADSL font definition file to be used.  The
default is no device-specific font file.  To revert to the default after
specifying some other value, enter a minus sign (-).  If a file name with no
account is specified, all accounts in the TeX search list will be checked for
a file with that name.
 
Most laser devices do not need device-specific font definitions, in which case
the font file defined by the format is used.  For some devices, though,
special fonts are needed.  For example, lineprinters must define all fonts to
be a single size of monospaced teletype font.  These devices should specify
the fid of the appropriate device-specific font definition file for this
option, which will override the one specified by the format.  The lineprinter
driver supplied with CAP is VA:ASCII.
RFONT Specifies the name of the file that defines any fonts that are resident
in the device, the amount of device memory available, and possibly other
device dependent information.  If a file name with no account is specified,
all accounts in the search list for the driver will be checked for a file with
that name.
The default is VA_QMS_RES_FONTS, which is suitable for use with QMS devices
having no resident fonts and 256K of available memory.  Sites with QMS
printers that are configured differently must create their own files and enter
those file names for this option.  For Postscript devices, this option should
be set to VA_PS_RES_FONTS; this system-supplied file should not be altered
except by request of CP-6 support personnel.  For ASCII devices, a minus sign
(-) should be entered to remove the value for this option.  For LaserJet
devices (HP), this option should be set to VA_QMS_RES_FONTS.
SEARCH Specifies accounts to be searched for font definition files.  This will
generally be a single account, depending on the type of device, as follows:
 
           :TEX     for QMS800, Postscript and HP LaserJet devices
 
           :TEXQMS  for QMS1200 devices
 
           :TEXLP   for ASCII devices
 
These are the standard font accounts supplied with CAP. Sites may obtain other
fonts or build their own.  The TeX documentation has a detailed description of
font handling.  The ADSL Reference Manual (HA28) also contains pertinent
information.
Although a single account is typically specified, this option accepts a list
of up to six accounts.  Each pair of accounts in a list must be separated by a
comma.  Account names can optionally be prefixed with a period.  This option,
 
when combined with the other elements of the search list for either TeX or the
device driver, must not result in a list of more than eight unique accounts.
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
00002
00001
00009
00004
00006
00007
00010
00008
00011
00005
CAP uses five dictionaries to perform various text analysis functions.
PROOF_DIC.X.      The standard CP-6 word list dictionary, supplied with the X
account product.  This dictionary, along with PROOF_DIC.logon, is used for the
Spelling Check option of the CAP Text Analysis menu item.  Words not found in
either of these two dictionaries are considered potential spelling errors.
VA$WT_LIMITED_AUX1.:LIBRARY.      A list of approximately 3000 commonly used
words in the English language.  This dictionary is used for the Limited Word
Check option of the CAP Text Analysis menu item.  Words not found in this
dictionary are considered outside of the limited English word list appropriate
for readers whose native language is not English.
VA$WT_FORBID_AUX1.:LIBRARY.      A list of several words that many users feel
should not be used in technical documents.  This dictionary is used for the
Prohibited Word Check option of the CAP Text Analysis menu item.  Words found
in this dictionary are identified as inappropriate.
VA$WT_FREQUENCY_AUX1.:LIBRARY.      A short list of the most commonly used
English words.  This dictionary is used to exclude words from the Word
Frequency Test option of the CAP Text Analysis menu item.
PROOF_DIC.logon.      The user's logon dictionary, which is created the first
time the user attempts an Add operation during the Review function of the
Spelling Check option (CAP Text Analysis).  This dictionary grows as the user
selects lists of words that are considered valid, but are not in the
PROOF_DIC.X dictionary.
00005
00001
00003
00004
00002
The CP-6 system has a Device Independent Graphics System (DIGS) which is based
upon the SIGGRAPH CORE graphics specification.  DIGS contains a set of
programming routines that are used to develop graphics applications.  Programs
written with DIGS can create a special type of file called a Device
Independent Graphics Instruction Set (DIGIS) file.  DIGIS files can be
displayed on a number of graphics devices, including many graphics terminals.
 
CAP uses the DIGIS format to store displayable versions of converted graphics.
It also uses DIGS programs to display those graphics on terminal screens.
However, many other types of programs can be implemented in DIGS, creating
many different types of computer graphics pictures.  The CAP menu allows the
conversion of DIGIS format to SGL so that drawings created by a DIGS program
can be included in a CAP document.
 
The CP-6 system comes with a set of DIGS programs that can be used to produce
business graphics for CAP. These programs are in the X account, and begin with
the letters GRAFA. Each GRAFA program has a HELP file that explains how to use
it.  To include GRAFA drawings in CAP documents, versions ending in the
characters DIG should be used.  For example, to generate a pie chart for
inclusion in a CAP document, the following command is used:
 
    !GRAFAPIEDIG.X ON *DG
 
The DIGIS file *DG can then be converted to SGL format using the Graphics
Functions selection from the CAP main menu.
 
Another important program in the X account is called GRAF. GRAF is a powerful
and flexible business graphics application that can build different kinds of
charts from various table-like data.  It, too, is documented in a HELP file in
the X account.
 
The GRAF program is called by the Business Graphics selection on the Office
Automation submenu of the CAP main menu.  A DIGIS file is created in GRAF by
using the OVER filename option of the PLOT, BAR, PIE, PIE3D, STEP, and LINE
commands.  To create a three-dimensional business graphic for inclusion in a
CAP document, the following command is used:
    PIE3D OVER *DG
 
The file *DG can then be converted to SGL format using the Graphics Functions
selection from the CAP main menu.
Direct file transfer is the least preferred method for transferring data
between a personal computer and CP-6.  Direct file transfer must usually be
performed at 1200 baud (120 characters per second) or even 300 baud (30
characters per second), because it has only rudimentary protocol between the
program running on the PC and the program running on the CP-6 system.
 
KERMIT and XMODEM have protocols available that allow the PC and CP-6 to agree
that data were transmitted correctly.  With direct file transfer, however, the
sending program dumps the data in an endless stream, never advising that the
data are sent correctly.  Therefore, direct file transfer typically is
performed at slow rates to reduce confusion.
 
There are several types of direct file transfers.  For example, files can be
transferred between CP-6 to Xerox 850 word processors using the 850READ.X and
850WRITE.X programs.  This is an example of a fairly intelligent direct file
transfer, as these programs also translate the 850-style underlining to and
from CP-6-style underlining.
 
In some cases, the PC can only send or store screens.  The CP-6 COPY command
is then used to transfer the file.  For example, to transfer a file to a PC
with direct file transfer, the PC is set up to accept the data and then the
following command is issued on the CP-6 system:
 
    !COPY file TO ME
 
Similarly, to transfer a file from a PC to the CP-6 system, the following
command is issued on the CP-6 system:
    !COPY ME TO file
 
The PC is then set up to send the screen.  At the end of the sending activity,
an ESC F entered on the PC tells the CP-6 system that the file has been
transferred.  PCTF has a special Text File Transfer mechanism that can be used
when KERMIT and XMODEM fail.
Much of the power of the CAP system lies in the ability to customize it.  Many
customization techniques are discussed in this guide.  Certain types of
customization will require that the CAP administrator obtain documentation
from other sources.
 
For example, if CAP users are editing with an off-line PC-based editor, it is
up to the CAP administrator to see that they receive proper training for that
editor.  Many PC-based editing programs include tutorial guides or even
tutorial sessions.  The same holds true for graphics packages, scanners, and
other devices that might be attached to the CAP system.
Any other types of customizations made by the CAP administrator (such as use
of a particular type of format, font, etc.)  must be documented, and all CAP
users need to be informed about their use.  The CAP administrator should
document changes or customizations as they are implemented.  This can be done
in a new document (called a "Customization Guide") or a customized version of
the supplied CAP manuals.  This document can serve as a training guide for
users that join the CAP community in the future.
 
This same document can also be converted to a HELP file, making the
descriptions of the customizations available to CAP users on-line.  Electronic
mail can also be used to inform CAP users of new facilities.
 
When using the CAP system, individual CAP users may develop special techniques
that can be useful to others.  Creating a "Tips and Techniques" manual (and
HELP file) from this type of information can also prove to be invaluable to
all users.
EDIT is a line editor, which means that changes are made to a file on a line-
by-line basis.  It uses file commands to select lines of text.  Once a line is
selected, it can be edited using keystrokes similar to those available on a
screen editor.
 
Given the popularity of screen editing programs, why would a CAP administrator
consider training users on a line editor?  There are several reasons why this
might be a good strategy.  Users that communicate with CAP through low-speed
telephone links may find 6Edit impractical, especially if their terminal is
not designed for screen editing.  Also, users that have hard-copy terminals
will not be able to use 6Edit.
 
Another consideration is the system load - 6Edit consumes more system
resources than EDIT. Thus, more people can be using EDIT on a system while
maintaining acceptable turnaround time than with 6Edit.  EDIT can be a good
alternative if a large number of users will be added to a system temporarily.
 
EDIT can be customized using the IMP processor.  Special key sequences and
editing sequences can be created that make EDIT more convenient.  Information
on keyboard customization with the IMP processor and EDIT is available in the
CP-6 Programmer Reference Manual (CE40).
The CP-6 Efficient File Transfer (EFT) processor provides file maintenance
safeguards to prevent the loss of data due to natural disasters, hardware
malfunctions, and user error.  EFT also provides the capability for
transferring files by account or accounts from one system to another.
 
EFT capabilities cover three general functions:  backup, archiving, and
moving.  File backup usually involves backing up files for possible
restoration in case of a catastrophe such as a disk head crash.  File
archiving involves preserving files on tape when further modification or
access of the files is unlikely.  File moving usually involves transferring
files from one CP-6 system to another.  The EFT commands available to the CAP
administrator are the STOW, FETCH, UNFETCH, UNSTOW, and UNARCHIVE commands.
These are accessible directly from IBEX. For detailed information see the EFT
processor, in the CP-6 System Support Reference Manual Volume I (HA20).
Two commands, FETCH and STOW, are available to the CAP administrator for
archiving files.
Line drawings are already in machine-readable format, but not in a format that
CAP understands.  The following paths can be taken to resolve this situation:
Most CAD systems support some level of the IGES transfer protocol.  While CAP
does not support IGES directly, CAP does support two programs that can convert
IGES into a format that CAP does support.  These two programs are ANVIL and
AutoCAD.
Most CAD systems support a plotfile feature that allows the insertion of
plotter instructions into a file.  That file is then transferred to the CP-6
system and converted to CAP format by a conversion program that may have to be
created for the individual CAP site.  Note that the AutoCAD plotfile (which
CAP supports) contains Houston Instruments DMP7 instructions.
Line drawings can be scanned by a Datacopy scanner, and then converted as in
the first method.  This method should only be considered if methods 1 and 2
are unsuccessful.
Selection of a graphics processing method depends on several factors:
Are the graphics drawings or photographs?  How much detail is there in each
graphic?  Will data be lost if a color image is converted to monochrome?
GRAPHICS_IN_MACHINE_FORMAT      Are the graphics from a CAD system?  Are there
any hand drawings that need to be entered?  Will there be technical artists
using computer graphics to create new drawings?
The quality of the output media:      Is there a need for high resolution
photography?  Will readers be accessing graphics directly on their terminals?
 
These factors are interrelated, which means that there may be some trade-offs
when selecting the best solution given the available graphics processing
methods.
 
Because there are so many variables that depend on the environment, it is
impossible to discuss all graphics processing requirements separately in this
manual.  For the purposes of this discussion, it is assumed that the best
solution is to display graphics data on both a hard-copy laserprinter and on
graphics terminals.
00002
00003
Syntax:
FET[CH] fid1[, fid2] ...
Parameters:
fid1, fid2    specify CP-6 file identifiers.
Description:
The FETCH requests the return to disk of the file(s) in the archive system.
The most recent copy of the file from the archive tapeset is obtained by
FETCH. To prevent update activity, the file is locked until it is returned
from tape at the next RETRIEVE run, performed by the system manager.
Usage Notes:
00002
00001
00003
Suppose a need arises for a new technical manual, and it is given the manual
number "NS01".  This means that all files (CAP source files, graphics files,
and device-specific files) should contain "NS01" somewhere in their names.
 
Individual chapters or sections are named by appending a numeric descriptor to
the first half of the name.  The numeric descriptor is used during document
assembly to order the files.  The following table shows how section descriptor
numbers can be organized:
 
    Descriptor             File Identified
 
    _00                    Identifies the front matter section which may
                           include a Preface, Title Page, and a call to
                           the Table of Contents file.
 
    _01 through _4n        Identifies the numbered document sections.
 
    _50 through _5n        Identifies the appendixes.
 
    _90                    Identifies the glossary.
 
Section 5 of the manual described above would be called "NS01_05", while
Appendix B would be called "NS01_51".
 
This descriptor schema ensures that files will be included in the proper
sequence during file collation; that is, that documents will always be
collated in the following sequence:
 
                           Descriptor Sequence
 
                           _00        Front Matter
 
                           _01        Section 1
 
                           _02        Section 2
 
                           _03        Section 3
 
                            .           .
 
                            .           .
 
                            .           .
 
                           _50        Appendix A
 
                           _51        Appendix B
 
                            .           .
 
                            .           .
 
                            .           .
 
                           _90        Glossary
 
File names are not assigned to the Table of Contents and Index files.  These
files are created and included in a hard copy manual during file collation.
 
Within accounts, source file naming conventions simplify locating individual
documents.  By systematically assigning common prefixes or suffixes to related
source files, the files are grouped and listed together.  Thus, the rules of
alphabetizing cause the related source files to form automatic groups.  The
CAP collation and decollation features can then be used to replace whatever
text or letters are in the prefix, suffix, or both.
 
The following examples show how naming conventions can be used to shortcut
specification of grouped files:
 
    File pattern to collate: NS01_?
    Target File: S:NS01
 
collates all files beginning with "NS01_" into a single file named "S:NS01".
 
    File pattern to collate: ?01.:DOC
    Target File: S:ALL_01.:DOC
 
collates all file names ending with "01" in account :DOC into a single file
named "S:ALL_1", also in :DOC.
 
    File pattern to search:  ?CADCAM?
 
searches all files whose names contain "CADCAM".
 
If SGL and Cappix (raster graphics) files are to be stored in the same account
as the CAP source files, they should be named so that they are identifiable,
but not so they are collated with the CAP text files.  For example, the
graphics for "NS01" could be stored using the following file naming
convention:
    G:NS01_cc_nn
 
where "cc" is the chapter in which the graphic appears, and "nn" is the
sequential figure number.  Thus the fifth graphic in chapter two would be
"G:NS01_02_05".
 
By putting a "G:" at the beginning of graphic file names, accidental collation
of graphics files with text files is avoided.
 
A similar naming technique should be followed with device-specific files
created by the formatting process.
 
Whatever naming conventions are established, it is particularly important that
they be documented and enforced.  If not, the CAP accounts will soon be filled
with file names such as "BILLS_OLD_FILE" and "FRED", which will be meaningfull
only to whomever first created them.
File-only accounts do not have associated logons.  A file-only account is used
to group and store related data (documents), to facilitate usage and location
of similar data (files), and to control access to the data.  Logon accounts
are granted access as required to the file-only accounts associated with the
CAP environment.  Control is implemented by limiting account access and file
permissions.
 
Account naming conventions provide a systematic way to control file access for
updating.  Access to files for updating is limited to one user at a time and
updating takes place only in one account at a time.  Once updating is
complete, files are placed in controlled accounts to restrict any further
updating activity.
 
File-only account names are most useful if the name reflects the contents of
the account.  One rule which must be observed is that a CP-6 account name
cannot be more than eight characters long (not including the period).  Note
that in the example below, the colon has been used as part of the account name
to differentiate the file-only accounts from the logon accounts.
 
    .:MEMOZ     contains memos and letters
    .:PRPOSAL   contains customer proposals
    .:CONTR     contains customer contracts
    .:MANUALZ   contains user documentation and manuals
 
This section describes CAP naming conventions.  CAP production features
include automatic document assembly, table of contents, and indexes.  For
these features to work, document assembly must be performed in a standard way,
which means files must be assigned standard names.  A file without a standard
name tends to become lost and cannot be integrated into a document.
 
Using file naming conventions within different accounts is helpful in the
management and control of the CAP environment.  System privileges are
generally associated with the user's logon account.  By using naming
conventions, account and file permissions can be added or deleted by group.
 
Consistent file naming conventions help keep track of CAP source documents.
Each name of a file defines the file's place in the account.
 
Because the CP-6 system supports from 1- to 31-character file names, naming
conventions can have a number of different fields.  A good policy is to assign
each document a unique number that will be used in all the files that make up
that document.
File security ensures that only authorized users can access computer-stored
information.  File security features differ depending on whether the medium is
disk or tape files.  If the medium is disk files, the packset owner controls
who can create accounts on the packset and establishes default values for
account permissions.  If the medium is tape files, ANS label protection
features are available.  The level of tape volume protection used is
controlled by an installation option.  As stated under the section on Physical
Security, the system manager can specify that tape volumes are to be fully
protected, semiprotected, or unprotected.  The volume owner may, at volume
creation time, specify protection for labeled tape.
 
The owner of an account and the owner of the file need not be the same users.
While, typically, the account owner also owns all files in the account,
particular application requirements may dictate other usage.  For example, a
teacher may set up an account whose files are owned by the members of the
class.
 
The levels of security have a hierarchical relationship.  A failure at one
level prevents progression to the next level.  A user who wishes to access a
file must first pass security at the account level, then at the individual
file level.  The user then gains access to the file's data, where the ability
to read the data depends on security at the data level.
At each level, the user is granted access to more information.  Only the
user(s) who can pass account level security checks can know the names and the
types of the files in the account.  Only the user(s) who can pass security at
the file level can obtain other catalog information about the file.  If there
is security at the data level, the file data is meaningful only if the user
can supply the required security information.
 
An understanding of file security features assumes a clear understanding of
the difference between logon accounts and file accounts.  Whereas the logon
account is the account that the user supplies to gain entry to the system, a
file account is the account name under which a file is cataloged.  A file
account need not have a corresponding logon account, and a logon account need
not have a corresponding file account.
The following file types are referenced throughout this manual:
ANVIL PLT Files:      Created using ANVIL/4000.
AutoCAD PLT Files:      Created using AutoCAD DMP7 plotting routines.
DIGIS (Device Independent Graphics Instruction Set):      Created using the
CP-6 Device Independent Graphics System (DIGS).
Dumdev Files:      Created with TELL-A-GRAF and DISSPLA by ISSCO.
IMG Files:      Created using Datacopy scanners.
Intergraph Plotfiles:      Created by Intergraph CAD systems for Gerber
plotters.
MacPaint Files:      Created using MacPAINT by Apple Computers.
PCDRAW Files:      Created using PCDRAW by Micrografx.
00001
00002
00003
00004
00005
00006
00007
00008
The Format Change Functions menu allows the administrator to view and alter
any of the options for a CAP format.  It is entered after satisfying the
prompts for a CREATE or CHANGE selection from the Format Functions menu.  Due
to the large number of format options, they are presented in several submenus.
This menu asks the administrator to select the type of option desired.  Each
of these selections lead to a submenu of options of the specified type.  There
is also a selection to display all options on a single screen.
 
The name and description of the format being created or changed appears at the
bottom of the menu, just below the line showing the current account.  This
line also appears in all menus that can be entered from this one.  The
administrator enters the name or number of the desired menu selection at the
"Format Change Function:"  prompt.  Additional prompts depend on which
function is selected.
 
On exit from the format change menu, if any changes have been made, the
administrator is presented with a prompt asking whether the changes should be
saved.  The default is YES. A response of NO cancels the changes, leaving the
format the way it was before the change menu was entered.  This prompt is
bypassed if no format options were actually altered.
DISPLAY This selection removes the menu window and fills the screen with a
display of the values for all options of the current format.  After viewing
the display, enter <CR> to restore the menu and reissue the menu prompt.
PAGE This selection leads to a submenu of options that define the size and
shape of the page.  These options can be changed through selections from the
submenu.
LAYOUT This selection leads to a submenu of options that determine various
kinds of special processing that can be done during formatting.  These options
can be changed through selections from the submenu.
FILES This selection leads to a submenu of options that define the auxiliary
files that specify detailed formatting rules, and other related information.
These options can be changed through selections from the submenu.
DESC The format description is a brief phrase describing the characteristics
or use of the format.  The current description is shown in the menu following
the format name, separated from it by a dash (-).  Unlike the previous
selections, this one does not lead to a submenu.  Instead, it simply issues a
prompt for "New format description:".  The new description replaces the
previous one in the menu as soon as it is entered.  If no new description is
supplied, the current description remains unchanged.
00001
00002
00003
00004
00005
00005
00001
00004
00003
00002
The File Specification Options menu defines the auxiliary files that specify
detailed formatting rules and other related information.
 
To change an option, the administrator enters an option number or name shown
in the menu at the "Format File Option:"  prompt.  For example, a prompt of
"New Format Style File:"  is issued if 1 or STYLE is entered at the menu
prompt.  The administrator should respond to this prompt with the desired file
name.  New values are reflected in the menu when the menu prompt repeats.  A
null response at an option prompt retains the option's current value.
All options that require a fid accept a full disk fid, but only the file name
is required, and that is usually the only part specified.  All options have an
appropriate default for the account.  For options where the default is a
specific account, it might be desirable to explicitly specify it for purposes
of clarity.  In the case of options that specify ADSL control files, though,
the default is a list of accounts to be searched.  Not specifying an account
when the default is a search list offers some advantages.
 
The accounts in a search list are checked in the order they are specified.
Several options from other menus determine the contents of the list, but the
current directory and logon account always come first, and :LIBRARY is always
last.  The standard control files delivered with CAP reside in :LIBRARY.
Administrators can privately test altered versions of these files in their own
accounts.  Versions with tested alterations can be copied into some common
account that is also put on the search list.  Thus, the administrator can test
and install new control files without changing the format definition.  If
account names were explicitly specified, the administrator would have to alter
the format or maintain multiple copies to do this.
STYLE Specifies the fid of the style-specific ADSL control file to use.  This
file is intended to contain those structure definitions that are most likely
to change from format to format.  Definitions can be moved between this and
the common elements file as necessary to meet the needs of the site.  The
default is VA:STYLE. If no account is specified, all accounts in the TeX
search list will be checked for a file with the given name.
ERROR Specifies the fid of the ADSL control file that defines CAP error
messages.  The default is VA:ERROR. If no account is specified, all accounts
in the TeX search list will be checked for a file with the given name.  The
file in :LIBRARY that is supplied with CAP will normally be used.  This file
should not be changed unless the administrator wishes to change the wording of
some of CAP's messages, or to translate them all into a language other than
English.
COMMON Specifies the fid of the ADSL control file that defines elements that
are used in common for many or all styles.  This file intended to contain
those structure definitions that are common to many or all formatting styles.
Definitions can be moved between this and the style-specific file as necessary
to meet the needs of the site.  A minus sign (-) can be entered to specify no
common structures file, in which case all structures available to the format
are found in the style-specific file.  The default is VA:COMMON. If no account
is specified, all accounts in the TeX search list will be checked for a file
with the given name.
FONT Specifies the default ADSL font control file to use with this format.
This may be overridden at formatting time by device-specific font definitions
if a document is formatted for a device that requires special fonts.  The
default is VA:FONTS. If no account is specified, all accounts in the TeX
search list will be checked for a file with the given name.
LIB Specifies the version of the CpTeX macro library to be used with this
format.  The default is VA:CAPTEX. If no account is specified, all accounts in
the TeX search list are checked for a file with the given name.  The file in
:LIBRARY that is supplied with CAP will normally be used.  This file should
only be changed in exceptional circumstances, on the request of authorized
CP-6 support personnel.
PROGRAM Specifies the version of the TeX formatter to use.  The default is
TEX. If an account is not specified, :SYS is assumed.  This option should only
be changed in exceptional circumstances, on request by authorized CP-6 support
personnel.
DSLDEF Specifies the file that defines all CAP controls and their
characteristics.  The default is VA$DSLDEF. If an account is not specified,
:LIBRARY is assumed.
 
This file is used by the PRETTY and VALID selections from CAP's Text
Manipulation and Text Analysis menus, respectively.  Although it is defined in
the format because different formats may use different site-specific controls,
this file does not affect the actual formatting process.
CHARS Specifies the CAP control delimiters used.  This option takes the form
of a string of three characters.  The first is the control introducer, the
second denotes the start of a control's parameter list, and the third is the
parameter list delimiter.  The default is "\{}".  Values other than the
default are not currently supported.
00001
00002
00003
00004
00005
00006
00007
00008
00008
00003
00007
00002
00004
00005
00006
00001
The Layout Options menu contains flags that determine various types of special
processing during formatting.  These flags all have a value of either YES or
NO.
 
To change an option, the administrator enters an option number or name shown
in the menu at the "Format Layout Option:"  prompt.  For example, a prompt of
"Ragged Right?"  is issued if 1 or RR is entered at the menu prompt.  The
administrator should respond to this prompt with the desired setting for the
option.  New values are reflected in the menu when the menu prompt repeats.  A
null response at an option prompt retains the option's current value.  When
specifying flag option values, YES and NO can be abbreviated to Y and N.
RR YES specifies that uniform spacing be used between characters and words
leaving a ragged right margin.  NO specifies that documents be formatted so
that the right margin is smooth.  The default is NO.
RB YES specifies that documents be formatted with a bottom margin for the text
area that may differ from page to page.  NO specifies that documents be
formatted so that the bottom margin is the same on all pages (except at the
end of a chapter).  The default is NO.
LAND YES specifies that the document be produced in landscape mode.  This
means that pages are formatted "sideways," with the top of page being the left
margin and the bottom of the page as the right margin.  NO specifies that the
document be produced in portrait mode.  The default is NO.
PNUM YES specifies that all \Ln controls generate a specification number.  The
number is included in the table of contents as well as on the formatted page.
NO specifies that no specification numbers are to be generated.  The default
is NO.
ENUM YES specifies that all \EQ controls generate an equation number by
default.  NO specifies that no equation numbers are to be generated, unless
specifically requested by the equation style.  The default is NO.
DRAFT YES specifies that the document be generated as a draft copy.  In draft
mode, extra passes through the document to correctly resolve all page
references are omitted.  NO specifies that the document be generated as a
final copy, with all page references correctly resolved.  The default is NO.
No more than two passes will ever occur to format a document as a draft, but
the table of contents, if present, will appear at the end.  Final copies may
require up to four passes, but have the table of contents in its proper place,
and all references completely resolved.
BOX YES specifies that boxes be drawn around figure, tables and graphics.  NO
specifies that these structures not be boxed.  The default is YES. This
applies only to structures whose style definition does not mention boxing.  An
explicit specification in they structure definition overrides this option.
FLT YES specifies that figures, tables and graphics float to a point where
they will fit entirely on one page.  NO specifies that these structures always
appear at the point where they are declared.  The default is NO. This applies
only to structures small enough to fit on one page, and whose style definition
does not mention floating.  An explicit specification in they structure
definition overrides this option.
2SIDE YES specifies that the document be formatted with recto and verso
headings and footings, where the left and right portions of these areas are
reversed on alternating pages.  This option is intended for producing masters
for double-sided reproduction.  NO specifies that the same heading and footing
layout be used for all pages.  The default is NO.
GENHELP YES specifies that a help file be created instead of a normal
document.  Page headings and footings are ignored, level headings are replaced
by help topic directives, blank lines are suppressed except between
paragraphs, and other special processing is done.  The default is NO.
 
The default should generally be used for all formats other than the predefined
HELP format.  Formats that produce help files should only be used with the
predefined HELP device.  Both of these are supplied in the system :CAP file
that is delivered with CAP. They contain all of the options needed to produce
CP-6 help files, and generally should not be changed.
CHBAR YES specifies that change bars be displayed in the manual.  NO specifies
that change bars not be displayed, which may be useful when producing the
final version of a manual.  The default is YES.
00001
00010
00011
00002
00009
00003
00004
00005
00006
00007
00008
00009
00007
00011
00006
00005
00008
00010
00003
00004
00002
00001
The Format Functions menu is the top level menu for the part of CAPADMIN that
is concerned with maintaining CAP formats.  It contains selections for all the
functions necessary to build, modify and view format definitions.
 
The administrator enters the name or number of the desired menu selection at
the "Format Function:"  prompt.  Additional prompts depend on which function
is selected.
 
Most selections result in a prompt for the name of a format.  Where
appropriate, a default format name appears in parentheses at the end of the
prompt.  The default format is initially the one named DEFAULT. Thereafter, it
is the last format accessed.  A null response accepts the default if there is
one.  If there is no default, a null response cancels the function and returns
the administrator to the "Format Function:"  prompt.  At any prompt for a
format name, the administrator can enter a double question mark (??) for a
list of formats defined in the current account.  This list appears in the
dialog window and is followed by a repetition of the format name prompt.
ACCOUNT This selection changes the account whose :CAP file is being accessed.
Its function is identical to that of the selection with the same name in the
main CAPADMIN menu.  Refer to the Main Menu for additional information.
LIST This selection lists the name and description of all formats defined in
the current account.  There are no additional prompts.  The list appears in
the dialog window.
CREATE This selection creates a new format in the current account.  The
administrator is prompted for the name to give the new format.  After
accepting the new name, CAPADMIN creates a format with default values for all
options and places the administrator in the Format Change Function menu so
that options for the new format can be changed to their desired values.
CHANGE This selection changes a format that already exists in the current
account.  The administrator is prompted for the name of the format to be
changed.  After accepting the format name, CAPADMIN places the administrator
in the Format Change Functions menu so that the options that make up the
format can be changed as desired.
COPY This selection copies an existing format.  The format can be copied from
the current account or another one.  It is always copied into the current
account.  The administrator may need to use the ACCOUNT function to change the
current account to the one that will receive the copied format before
selecting the COPY function.
 
The administrator is first prompted for the account containing the format to
be copied.  Any account having a :CAP file the administrator can read can be
specified.  The default is the current account.
The next prompt asks for the name of the format to be copied.  A double
question mark (??) response at this prompt lists the formats defined in the
account that is the source of the copy.
 
The final prompt is for the name to give the new copy of the format.  If the
format is being copied from another account, the default is the name of the
format being copied.  If the format is being copied from the current account,
it cannot have the same name, so there is no default.  In this case, if no new
name is provided, the copy operation is cancelled.
 
After all prompts have been satisfied, the specified format is copied into the
current account under the new name given and the administrator is returned to
the "Format Function:"  prompt.  The new format is set up as the default for
subsequent operations.  The administrator will typically want to follow a COPY
with a CHANGE function to alter the new copy of the format.
DELETE This selection removes a format from the current account.  The
administrator is prompted for the name of the format to delete.  To avoid
accidentally deleting the last format accessed, there is no default for this
prompt.  A null response returns the administrator to the menu prompt without
deleting anything.  If a format is specified, it is deleted from the current
:CAP file.
DISPLAY This selection displays the settings of all options for a format on
the terminal screen.  The administrator is prompted for the name of the format
to display.  The default is the last format accessed.  After accepting the
format name, CAPADMIN removes the menu and displays the format on the terminal
screen.  After viewing the display, a <CR> clears the screen, restores the
menu, and returns the administrator to the menu prompt.
PRINT This selection produces a display of the all options for a format on a
lineprinter or in a file.  The display has the same layout as the one for the
DISPLAY function.  The administrator is first prompted for the name of the
format to print.  A second prompt asks where the display is to be printed.
The administrator can respond with the fid of a disk file or a CP-6 device.
The default is the administrator's default lineprinter (LP@).  When printing
to a device, note that the display is produced in a form suitable for a
lineprinter.  It may not be printed correctly if directed to a laserprinter.
00001
00002
00003
00004
00005
00006
00007
00008
00001
00004
00005
00003
00006
00007
00002
00008
The Page Dimension Options menu defines the size and shape of the page.
 
To change an option, the administrator enters an option number or name shown
in the menu at the "Format Page Dimension Option:"  prompt.  This results in a
prompt for a new value for the option.  For example, a prompt of "New Page
Width:"  is issued if 1 or WIDTH is entered at the menu prompt.  The
administrator should respond to this prompt with the desired page width.  New
values are reflected in the menu when the menu prompt repeats.  A null
response at an option prompt retains the option's current value.
 
All dimensions are specified in terms of some number of some unit.  Numbers
can contain a decimal point to denote a fractional number of units.  The units
can be any of the following:
 
                       pt  printer's point
 
                       pc  pica (1pc = 12pt)
 
                       in  inch (1in = 72.27pt)
 
                       bp  big point(72bp = 1in)
 
                       cm  centimeter (2.54cm = 1in)
 
                       mm  millimeter (10mm = 1cm)
 
                       dd  didot point (1157dd = 1238pt)
 
                       cc  cicero (1cc = 12dd)
 
                       sp  scaled point (65536sp = 1pt)
 
If a number is entered with no units, inches are assumed.
WIDTH Specifies the width of the physical page stock for which this format is
designed.  The default is 8.5 inches.
 
If the page size specified for the format does not fit within the page
dimensions defined for the device, the device's dimensions will be used
instead.  To always mold documents to the page size for the device, a minus
sign (-) can be entered to remove the format's page width.
LENGTH Specifies the length of the physical page stock for which this format
is designed.  The default is 11 inches.
 
If the page size specified for the format does not fit within the page
dimensions defined for the device, the device's dimensions will be used
instead.  To always mold documents to the page size for the device, a minus
sign (-) can be entered to remove the format's page length.
TOP Specifies the amount of white space that appears at the top of each page.
The default is 1 inch.
BOTTOM Specifies the amount of white space that appears at the bottom of each
page.  The default is 1 inch.
LEFT Specifies the amount of white space that appears at the left edge of each
page.  The default is 1 inch.
RIGHT Specifies the amount of white space that appears at the right edge of
each page.  The default is 1 inch.
HEAD Specifies the size of the area at the top of each page reserved for page
headings.  The default is .375 inches.
FOOT Specifies the size of the area at the bottom of each page reserved for
page footings.  The default is .375 inches.
00001
00002
00003
00004
00005
00006
00007
00008
00004
00008
00007
00005
00002
00006
00003
00001
There are several types of graphics processing methods that can be used with
CAP. The following discussion is meant to assist the CAP administrator in
selecting the graphics processing method appropriate to the site.
Because computer graphics is a complex application, CAP uses two forms of
graphic storage to accomplish its various tasks:
 1. SGL files, which are vector graphics (X and Y coordinate data).
 2. Cappix files, which are raster graphics (bit-map or gray-scale data).
 
CAP graphics convertor programs convert various forms of graphics input into
either SGL or Cappix format.  CAP accepts files in either format.  Both types
of graphics are included using the GR control.  The CAP resolvers can
correctly process either file type.
 
The graphics conversion capabilities of CAP permit the transfer of information
between various graphics formats.  The PIXEL.X program can also create Cappix
files.  (See the HELP file for PIXEL.X for further information.)
 
The following subsections discuss some of the available products for creating
and converting graphics.
The highest resolution that B01 CAP supports is 300 dpi or 90,000 pixels per
square inch.  But resolution cannot be computed in terms of raw output device
capabilities because the effective resolution is affected by two other
factors:  the scanned resolution and the reproduction resolution.
 
The scanned resolution is the density of the scanned image.  For example, if a
picture is scanned at 200 dpi and printed on a 300 dpi device, the picture
will look best at 2/3 the original size.  Similarly, if a picture is scanned
at 600 dpi and printed on a 300 dpi device, it will look best at twice the
original size.  Thus a 300 dpi device is indeed capable of producing an
effective resolution of 600 dpi, depending on the input data.
 
Reproduction resolution is the density of the printing process.  This is a
combination of the native resolution of the printer and the amount of photo-
reduction applied during the plate-making process.  For example, an offset
printer is capable of approximately 500 dpi with normal paper.  If a 300 dpi
master is photo-reduced by 2/3, it will match the resolution of the printer.
Thus the 600 dpi drawing will now return to a size and resolution that more or
less matches the original scanned resolution, even though the masters were
printed on a 300 dpi device.
 
Misunderstanding of the interaction of these factors is often responsible for
unrealistic resolution requests.  For example, it is unrealistic to use 1000
dpi typeset output to produce copy for xerographic reproduction - the copier
simply does not have the resolution to display that level of detail.
 
Thus, while high resolution photography proposes some challenges, these are
surmountable by the correct application of effective resolution.
Another planning task is to identify and categorize the users of the CAP
system.  The user-grouping scheme that is implemented by the system manager
will have profound implications upon the performance of the CAP system.
Users can be grouped by
 
o   shared interest,
o   existing organizational structure,
o   common accounting requirements, or
o   arbitrary schemes.
 
Some of these methods of categorizing users may overlap.  For example, users
may be grouped according to an existing organizational structure, but within
several projects there may be common support functions which can be identified
as such.  This can be useful in accounting or in statistical analysis.  Use of
arbitrary schemes is not recommended as it tends to complicate the assignment
of file and system access using standard CP-6 facilities (e.g., wildcarding).
The following are examples of how words can be included or excluded from
dictionaries:
 
o   To prevent a particular word (such as a company name) from being flagged
    by the various checking mechanisms, the tool WEBSTER.X is used to add the
    company name to PROOF_DIC.X, VA$WT_LIMITED_AUX1, VA$WT_FREQUENCY_AUX1, but
    not to add it to VA$W_FORBID_AUX1 (because the company name should not be
    considered an invalid word).
o   To write documents at a third-grade level, words can be added to or
    deleted from VA$WT_LIMITED_AUX1 until it contains only 1000 very common
    words in the third-grade vocabulary.
o   To make sure that a particular word does not appear in documentation, it
    can be added to VA$WT_FORBIDDEN_AUX1.
Before any work can be performed by the system manager and CAP administrator,
some degree of planning must take place.  Consideration must be given to the
user environment because CAP must be able to service its users effectively.
The following questions must be addressed:
 
o   What is the physical location of users and devices?
o   What services should the CAP system provide?
o   What types of financial restrictions are there?
 
Cost is a major factor during the planning stages.  For example, it may be too
expensive to have three laserprinters.  Therefore, a method must be agreed
upon to accommodate the number of users with the available number of
laserprinters.
 
Most organizations are scattered throughout more than one floor, building, or
city.  Therefore, physical proximity between users becomes an issue in
planning as well.
 
A list of devices must be made based on what a site has or is planning to
purchase.  With this information, a diagram can be drawn that depicts the
workstation configuration for the site.
Files from an Intergraph CAD system can be transferred to the CP-6 system by
magnetic tape.  The transfer format is called PC-800 GERBER OUT FORMAT. This
plotfile format should have the following characteristics:
 
1.  ASCII (or converted from EBCDIC).
 
2.  Absolute or incremental mode.
 
3.  English or metric.
 
4.  Leading, trailing, or no zeros omitted.
5.  * as end of block.
 
6.  Variable format.
 
7.  Variable record size.
 
Tool select and photo flash are ignored, as are apertures and pen
verification.
 
This section only touches the surface of the complex issue of file transfer
and system-to-system communcations.  However, it should serve as a guideline
for the CAP administrator who needs to add these capabilities to a CAP
application.
 
A file transfer mechanism consists of two parts:  the communications protocol
and a transfer program.  A communications protocol is a set of rules for data
transfer, agreed on by both sending and receiving devices.  A transfer program
is a piece of software that packages a file on the sending system (so it can
be transferred), and unpackages the file on the receiving system.
 
File transfer mechanisms vary according to whether the file is being exchanged
between host systems or between a personal workstation and a multiuser system.
A personal workstation can be an IBM-compatible personal computer, a
MacIntosh, a word processor, or even a lap computer.  A multiuser system is a
CP-6 system or other computer system that has more than one user connected to
it.  Following is a discussion on file transfer to and from personal
workstations and CAP.
The CAPADMIN program is invoked at the CP-6 system command prompt (!) as
follows:
 
    !CAPADMIN [(commands)]
 
Normally, CAPADMIN is invoked without specifying commands.  This displays the
CAPADMIN Main Menu.  The administrator can then respond to prompts for menu
selections and other information to perform CAPADMIN functions.
 
If commands are provided, they are processed as if they had been entered
starting at the Main Menu prompt, but without presenting any menus or prompts.
Multiple prompt responses can be entered by separating them with semicolons.
The first prompt issued is the one that follows the last response supplied on
the command line.  This allows experienced administrators to bypass some
prompts by presupplying responses they know will be requested.  For example,
if you type
    !CAPADMIN [2;1]
CAPADMIN will list the formats in the current account.
ISSCO (Integrated Software Systems Corporation) products are supported via the
DUMDEV file output.  For more information on how to create DUMDEV files in
TELL-A-GRAF and DISSPLA, see the DISSPLA Users Manual and the TELL-A-GRAF
Users Manual.
KERMIT works especially well with IBM PCs and is the best choice for
transferring files such as Datacopy IMG and AutoCAD PLT. Many terminal
emulators have a KERMIT capability, including the CP-6 terminal emulator
program called PCTF. The version of KERMIT that runs on the CP-6 system (CP-6
KERMIT) is described in the CP-6 PC Terminal (PCT) Facility Reference Manual
(HA15).
 
CP-6 KERMIT does not come with the CP-6 operating system.  It can be ordered
as part of the CP-6 Microcomputer Support product package.
 
The key to making KERMIT work effectively in a CAP environment is to match the
settings of the PC KERMIT with the commands that are given to the KERMIT
program on the CP-6 system.  This often takes some experimentation before it
works correctly.
 
CP-6 KERMIT and the KERMIT in the PCTF program can work together as file
servers, meaning that multiple files can be transferred with a single KERMIT
command.  In addition, a file called :KERMIT_INI can be created on the CP-6
system to set up CP-6 KERMIT to communicate with PCTF KERMIT. An example of a
:KERMIT_INI file is shown below; see the CP-6 PC Terminal (PCT) Facility
Reference Manual (HA15) for descriptions of the various KERMIT commands.
 
LOG INTO :KERMIT_LOGXXACCT
SET DELAY 10
SET FILE MODE AUTO
SET FILE WARNING OVER
SET TAB EXP OFF
SET FILE EXT='IMG','P01','COM','EXE','PLT', 'DGM'
SER
A logon account is the default account associated with a logon.  Each CAP user
obtains access to the CP-6 system through a CP-6 logon account identification,
with system access governed by the permissions associated with the logon.
Logon accounts are usually authorized to contain a controlled number of
granules (units of disk file space).
 
User logons consist of three separate segments:
 
    account-identifier, username, password
 
Through the use of naming conventions, the account-identifier and username
fields of the logon can be used to group accounts by department, job
description, exempt versus non-exempt, etc.  The logon account is usually
determined by the system manager and the CAP administrator according to user
site standards.  The system manager then creates each logon account using the
SUPER processor.  See the CP-6 System Support Reference Manual (HA21) for more
information.
    ELFENGR,5111,KOSMIC              TABENGR,5112,RADACK
     |    |  |     |                   |   |   |     |
     |    |  |     v                   |   |   |     v
     |    |  v     password            |   |   v     password
     |    v  non-exempt employee       |   v   exempt employee
     v    department/environment       v   department/environment
     user initials                     user initials
 
    Note: The user initials and department,  account, and passwords
          are for illustrative purposes and are not meant to represent
          actual systems administration practice.
A CAP user must give a valid name, account, and password to gain access to the
CAP system.  The logon authorization is defined by the system manager using
the SUPER processor.  Although the password is optional when defining logon
accounts, supplying a password for every account increases overall system
security.  CAP users may change their own password at any time via a simple
terminal command.  Requiring the use of passwords and establishing policies to
change them often is a strongly recommended practice, as very little privilege
is needed to see other name/account combinations.
 
In a CAP environment, the logon password should be monitored by the CAP
administrator.  If the files that the logons are permitted to access are
confidential or classified, the logon passwords should be changed
periodically.  Remember that if a logon is written down, the piece of paper
can be used by anyone to illegally access the system.  Passwords must be
remembered by the user of a logon.  Note that if passwords are assigned with
obvious regularity, it defeats their purpose.
MacPaint files must be uploaded to the CP-6 system before they can be
 
converted.  They can be uploaded with MODEM.X by issuing the following command
on the CP-6 system:
 
    !MODEM.X ON myfile(BM)
 
where myfile is the file name of the CP-6 uploaded file.  The terminal
emulator on the MacIntosh is then activated to send, using XMODEM protocol.
Once the file is transferred to the CP-6 system, CAP can convert the uploaded
MacPaint file to Cappix format.  The recommended terminal emulator for
connecting a MacIntosh to the CP-6 system is Red Ryder.  Note that CP-6 PCTF
does not support the MacIntosh.
Transferring files to and from personal computers ties up the PC while the
file transfer is taking place.  This may be acceptable for a personal
workstation, but it is inappropriate for file transfer between multiuser
systems.
 
As with personal workstations, file transfer between multiuser computers is
accomplished by running a program on each computer, which communicates with
the other through a protocol connection.  Sometimes, the hardware is a
magnetic tape and, in other cases, a direct communications line.  This
subsection discusses the two most common file transfer mechanisms on the CP-6
system:  the MOVE program and Tape Transfer.
A full consideration of operational security must include a discussion of the
physical site and the way in which computer center operators are trained.
Some aspects of operational security relate directly to appropriate use of the
CP-6 system.
For purposes of this discussion, operational security is divided into two
categories:  physical security and output security.
An optical character reader (OCR) is the only practical way to enter large
amounts of textual material that is not in machine-readable form into the CAP
system.  CAP supports input from the Datacopy OCR PLUS software.  Many other
OCR devices can create an ASCII file or magnetic tape that the CP-6 system can
understand.  As with WP Editing, a user must add controls and edit OCR-created
documents to make them CAP-compliant.
Policies must also be established by the system manager on controlled listing
distribution and controlled writing to tapes.
 
Controlled listing distribution may include shredding sensitive listings
before disposing of them, disposing of carbons, and establishing secured
areas.  In addition, operations planning should decide how operator consoles
are to be defined.
CAP supports a subset of the PC-DRAW package.  The Fill option is not
supported, nor are the color options.  In addition, a special DGM file
(VA$GR_PCDRAW_DGM.:LIBRARY) must be used for the entry of characters.  This
file must be downloaded into the PC-DRAW data disk and used for all textual
entry.  Only P01 files are supported (pages 1 through 4).  The P01 file must
be uploaded to the CP-6 system as a binary file.  See the CP-6 PC Terminal
Facility manual (HA15) for more information about binary file transfer.
 
In a CAP environment that uses PC-DRAW, VA$GR_PCDRAW_DGM (on the CP-6 system)
should be renamed to ASCII_DGM, downloaded to a diskette (where it will be
ASCII.DGM), and then distributed on diskette to the various PC-DRAW users.
PC editing is distinguished from word processor (WP) editing by the operation
of the program used to edit.  If the editing program formats the edited input
into pages, then it is considered a word processor.  If the editing program
can edit a document without formatting it into pages, then it is considered a
 
PC editor.  Note that the page formatting features of some WP programs can be
disabled so that they function like PC editors.
 
Interactive editing can be performed off-line on personal computers.  When a
document is ready to be formatted, the document file is transferred to the CP-
6 system via a communications program (PCT) and then submitted to CAP for
formatting.
 
Using a PC-based editor is advantageous in that it puts no load on the CAP
host system during text editing, thereby freeing more computer power for
formatting, using electronic mail, and other tasks.  Also, many PC editors
provide additional features that the user may appreciate.  This makes PC
editing a good choice for environments where personal computers can be
purchased for many CAP users.
Personal workstations (called personal computers or PCs in this discussion)
are connected to the CP-6 system using a terminal emulator program.  A
terminal emulator makes it possible to use the PC to interact with CAP and the
CP-6 system.
 
To transfer a file from the PC to the CP-6 system (or vice versa), the
terminal emulator must be able to package and unpackage files.  Similarly, CP-
6 must be able to understand how the terminal emulator accomplishes this.
Thus, during any PC/CP-6 file transfer there are two programs running
simultaneously, one on the personal computer and the other on the CP-6 system.
These programs must be told how to communicate with one another before a file
can be transferred.  Similarly, the two programs need to agree on a protocol
that they can use (the rules to be followed during the file transfer).
 
CP-6 supports three file transfer languages:  KERMIT, XMODEM, and COPY. For
file transfer to be successful, the terminal emulator must support KERMIT,
XMODEM, or some method of direct file transfer.  Direct file transfer is a
simple mechanism for transferring a file to the screen.
KERMIT and XMODEM have a number of different protocols, in that the KERMIT or
XMODEM programs running on the CP-6 system must have the same protocols as the
KERMIT or XMODEM programs running on the PC. Only then is the personal
computer able to transfer files correctly to and from the CP-6 system.
 
The three methods of PC/CP-6 file transfer are discussed below.
Physical security is the responsibility of each installation.  Each site must
ensure that dial-up phone lines are protected, offices with hardwired lines
are locked, and that access to data processing rooms is restricted.
 
Some tape security features are linked closely with physical security.  The
CAP administrator should meet with the system manager and weigh the advantages
and disadvantages of the fully protected and semiprotected modes of physical
security.
 
The CAP administrator should also ask the system manager to establish labeling
techniques to guarantee that cross-mounting of tapes and private packs cannot
occur, thereby assuring that only appropriate users can mount tapes and
private packs.
Record security has two aspects:  granule stamp validation and data
encryption/decryption.
 
Granule stamp validation ensures that one user does not accidentally read
someone else's data.  The granule stamp ensures that only data actually
written to the file may be read as part of the file.  This level of security
is automatically supplied to all files in the system, and is transparent to
CAP users and administrators.
 
Data encryption/decryption provides an optional, computer-generated data
encoding and decoding capability.  The owner of a disk file can request that
data in the file be encrypted.  Encryption is available for all file
organizations except indexed and IREL files.
 
Data can be encrypted and decrypted through both the EDIT and PCL processors.
Data are encrypted by replacing each character with a computed substitute
character.  The characters are generated from an algorithm which uses as its
base a starting number, called a seed, supplied by the user.  Because the seed
can be specified on each read and write, it can be different for each record.
The seed is not recorded anywhere in the system, which secures it from
unauthorized detection.  However, this added measure of security places a
responsibility on the CAP user to remember the seed.
File backup procedures ensure that copies of files are made periodically so
that the files can be recovered in case of a disaster.  Backup processing is
characterized by the following features:
 
o   Backup is done to an installation-controlled schedule, and files are
    restored at the discretion of the installation.
o   Each installation determines operational parameters controlling backup (in
    particular, whether disk or tape is the storage medium) and which accounts
    are eligible for backup.
o   The system does not back up all files, just those qualified by the CAP
    administrator.
 
The CAP administrator must consider which files to qualify for backup.
Normally, files that are unique should be backed up; files that can be derived
from other files should not be.  (Therefore, source files are usually
candidates for backup, whereas run units are not.)
 
Under special circumstances, the administrator may want to back up files that
are not usually qualified for backup.  This capability is made available
through the IBEX BACKUP command.  The administrator can issue this command to
request that a file be included in the next regularly scheduled backup.  The
administrator does not control when backup occurs.  If the file is modified
after a backup is requested, there is no control over what the contents of the
file are when it is backed up.
If your site has an existing base of documents that contain graphics which
have never been entered into machine-readable form, selecting a graphics
processing method to enter and display this material on a laserprinter and
graphics terminal can be challenge.  The graphics may include a mixture of
photographs and line drawings.
 
If the requirement is only to print the documents on the laserprinter, the
task is rather simple.  The graphics (line drawings and photographs) can be
scanned and included using standard CAP facilities.  However, if the
requirement is that the data be displayed meaningfully on a graphics terminal,
a scanned line drawing will probably not be readable.  Thus, special steps
must be taken to ensure that the line drawings will be readable.
 
Line drawings can be scanned on a Datacopy scanner and then converted via
CADCamera to vector format.  The vector format is edited using AutoCAD to
remove spots and other visual "noise".  These drawings are then uploaded to
CAP and converted to a format that CAP understands.  One result of this
process is that the scanned line drawings can be updated using AutoCAD or
exported (via IGES protocol) to other CAD systems.
The average size of each line drawing must be estimated, along with the
average time to scan, convert, edit, upload, and convert each drawing.  This
time depends on the power of the PC devices and the size of the CP-6 system.
This throughput must then be compared to the number of drawings to be entered,
along with the personnel that will be assigned to process them.  The result is
the number of scanning/conversion workstations that should be part of the
overall CAP system.
There are five text editing/entry methods that can be selected to edit and
create textual material for use with CAP:
6Edit:      The CP-6 screen editor.
EDIT:      The CP-6 line editor.
PC Editing:      Off-line editing on a PC.
WP Editing:      Off-line editing on a word processor.
OCR:      Optical character reader.
 
Any given CAP site may use one, several, or all of these text entry/editing
methods.  It is up to the CAP administrator to select the best method for the
different types of CAP users that the system will serve.
00001
00002
00005
00003
00004
Selection of output devices for a CAP application depends on the way CAP
documents will be viewed or distributed.  CAP supports the following devices:
HELP:      Format used for HELP file generation.  HELP files can be used for
storing and querying information online.
LJ@CAP:      HP LaserJet/II printer at the CAP workstation for final printed
copies.
LP@LOCAL:      Lineprinter for draft copies.
LZ@CAP:      QMS1200 laserprinter at CAP workstation for final printed copies.
LZ@POST:      PostScript LaserJet at POST workstation for final printed
copies.
ME:      Display directly on the terminal.
PREVIEW:      Interactive preview facility.  Simulates the final format for
display on ASCII terminals.
00001
00002
00003
00004
00005
00006
00007
In general, CAP devices (terminals and laserprinters) are connected to the
system as asynchronous devices.  The CP-6 system connects to a large number of
asynchronous terminals and it is relatively easy to connect a new type of
asynchronous terminal to the CP-6 system.  The fastest line speed that can be
supported in this environment is 19.2KB. The CP-6 system also supports
IOM-connected lineprinters and FEP-connected lineprinters.
 
Personal computers that are IBM-PC compatible can be connected to the CP-6
system using an appropriate terminal emulation package.  PCT, the CP-6 special
terminal emulator, works well in this instance.  MacIntosh users should use
Red Ryder to communicate with the CP-6 system.  In general, The CP-6 system is
relatively tolerant of terminal emulators.  For file transfers, the KERMIT or
XMODEM protocols are recommended.  3270 terminals can also be used with CAP,
but the 6Edit screen editor will not operate on 3270 terminals.
The first logical record of the file which, if it is present, must be the
entire first physical record, can be an identification record.  It starts with
the characters "*M*" and a blank in the first four bytes, and can contain any
other characters to the end of record.  The occurrence of such a record in any
other position in the file can be treated as an error.
 
The use of any other record initiated by an "*" character is reserved for
future definition.
 
Any logical records not initiated by an "*" character can be blocked into
physical records; the maximum size of such physical records is limited to 256
bytes.  Logical records are separated from their predecessors in a block by an
"*" character.
 
Two constructs are employed:
 
a)  a comment consists of a string initiated by a " character, which can be
    preceded by insignificant blank characters, containing any characters
    other than a ", and terminated by a " character.
b)  a number consists of an optional "-" character, followed by zero or more
    numeric characters, optionally followed by a "."  character and zero or
    more numeric characters.  There must be at least one character in a
    number.  Only the most significant six numeric characters are considered
    in evaluating a number, and only the initial six digits following a
    "."character, significant or not, are considered evaluating a number for
    internal computational processes.  Optional insignificant blank characters
    can precede or follow a number.  A number containing no digit characters
    represents the value zero.
 
A logical record can consist of a comment only, and any record not beginning
with an "*" can be terminated by an optional comment.
 
A range record must appear as the second record in an SGL file; it cannot be
preceded by any records other than the "*M* " record.  The first character of
a range record is the "R" character followed by a blank.  There must follow
four or six numbers separated by one or more blank characters.  The
significance of these numbers is, in order, maximum x, minimum x, maximum y,
minimum y, maximum z, and minimum z.  For two dimensional specifications, the
final two numbers should represent zero values (they are optional).
 
An SGL file can contain any number of move and draw records, with formats as
follows:
 
a)  the first byte must contain either the character "M" for move, or the
    character "D" for draw.
b)  the second byte must contain a blank.
c)  there must follow two (for two dimensional specifications) or three (for
    three dimensions) numbers separated by one or more blank characters.
 
The import of these records is to specify a movement from the previous
position to the specified position with the pen up (M) or down (D). There is
an implied first position specification of "M 0 0" or "M 0 0 0" depending on
the dimensionality of the specification.  It is an error for any of the
numbers specified on move and draw records to violate the specifications of
the range record.
 
Note that the specification of consecutive move records, although inefficient,
is not illegal.  However, the specification of large magnitude numbers on
insignificant move records which affect the range specification can have a
quite deleterious effect of shrinking the image presented.
This new file format is preferred (over the older move/draw format) for B01
CAP; however, if a recognizable move/draw file is appropriately presented for
processing instead of the SGL format, it is accepted.  Processing of the SGL
format files is more efficiently accomplished than is that for move/draw
format files.  The processor, VA$GR_MDSGL, is available in B01 CAP to convert
move/draw format files into the SGL format.
 
For the B01 release of CAP, the following restrictions apply:
 
a)  the first record must start with "*M* " in the first four character
    positions,
b)  the range record information must initiate the second record, and
c)  comments are not supported.
Syntax:
STO[W] [{A[CTIVE]|I[NACTIVE]}] fid1 [,fid2,...]
Parameters:
fid1, fid2    specify CP-6 file identifiers.
Description:
The STOW command requests that the specified file(s) be entered into the
archive system, with the following results:
 
o   The file is locked to prevent updating and is queued for STOW.
o   When the system manager performs an ARCHIVE run, the file is written to
    tape and the FIT is updated with the time, date, and serial number of the
    tape to which the file was copied.
o   Files designated as ACTIVE are retained on disk and made accessible to
    users (read only).  Files designated as INACTIVE are retained on tape
    only.
Both ACTIVE and INACTIVE files can be removed from the queue for archiving via
the UNSTOW command.  If a file previously stowed as ACTIVE and not UNSTOWed is
made STOW INACTIVE, its disk granules are immediately released.  If neither
ACTIVE nor INACTIVE is specified, the default is INACTIVE.
Usage Notes:
 
 1. This command can be used only if a) the account is authorized with the
    STOW attribute (see PIG, STOW/NOSTOW option) and the current user is the
    file creator; or b) the account is authorized with the STOW attribute and
    the current user has the FMSEC privilege active.
 2. The file cannot be updated while it is queued for STOW or FETCH.
 
This appendix describes the command syntax of all service programs used by
CAP. All of the CAP service programs reside in the :SYS account.  They are as
follows:
 
o   Graphics Conversion
o   Post Processors
o   Text Conversion
o   Writer's Toolkit
 
Each service program is discussed in the following subsections.
 
Each of the graphics conversion programs available with CAP is described
below.
00002
00001
00003
Tape transfer is the most convenient way to transfer large amounts of data,
such as thousands of graphics or manual pages.  Tape transfer holds the data
in an extremely compact form which can be loaded onto the receiving system far
more swiftly than through communications lines.
 
As with other forms of file transfer, there is a program on each computer:
one that writes the data to the tape and another that reads the data from the
tape.  As with other forms of file transfer, the two programs must understand
each other's protocol, which in this case refers to the way that the data is
compacted onto the tape.
 
The CP-6 system is multilingual and can usually determine automatically how
the tape was created.  This makes the transfer of tapes from other systems to
the CP-6 system relatively easy.
 
More care must be taken when transferring tapes from the CP-6 system to other
systems.  The requirements of the receiving system must be clearly defined,
and the tape must be created on the CP-6 system so the receiving system can
understand the data.  The options for creating and reading tapes on the CP-6
system are described in the CP-6 Application Programmer's Handbook (CE55).
 
This section discusses updating and maintaining the word dictionaries used by
CAP_CAP dictionary checks use the PROOF.X tool, documented in the PROOF.X HELP
file.
Graphics from uncommon devices usually require a special program to convert
them to CAP standard graphics.  The architecture of the CAP internal graphics
files is documented in Appendix A.
 1. If an active file is fetched, the tape copy replaces the current disk
    file, and the file remains stowed on tape.
 2. The administrator may be able to FETCH an inactive file, but will be
    unable to access it if access controls for the file exclude the
    administrator.
 3. This command can be used a) if the user is the creator of the file; b) if
    the user has FMSEC active via !PRIV FMSEC; or c) for stowed inactive
    files, if the user is able to create files in the account.
 4. The file cannot be updated while it is queued for STOW or FETCH.
 5. If the file management account limit is exceeded, FETCH requests are
    ignored by the RETRIEVE process unless the FETCH request was made with
    FMSEC active.
Example:
 
    !FETCH TESTFILE
 
requests retrieval of the file TESTFILE. At the next RETRIEVE run, the most
recently archived version of the file is returned to disk (over the current
copy of the file).
00001
Every CAP user is identified by a name and an account number.  When random
numbers or names are assigned as logon accounts, there is, in effect, no
grouping scheme.  For example, if each CAP user within a project uses the same
account number for accounting purposes, but the number has no classification
or grouping scheme in mind, it becomes laborious and time consuming to assign
different projects access to common files (as CP-6 wildcarding cannot be used
to achieve this).  Although this method may be advantageous for security
reasons, it does not work well in a CAP environment.  The larger the number of
accounts in this type of scheme, the more unwieldy the handling of accounts
becomes, from the standpoint of granting file access.  Using this arrangement
would not allow the system manager to exclude certain users from having access
to a particular device form, for example.  Therefore, the CAP administrator
must decide which users will log on to the system, what accesses they need,
and the devices which are required.
 
With these factors in mind, a scheme can be developed that incorporates
wildcarding so access to devices can be overlapped, and the system can be used
to its maximum advantage.
 
This section describes how CAP accounts are defined.  The CAP administrator
works with the system manager to determine the accounts that will be needed
for the CAP application.  The following types of accounts are used in a CAP
application:
Logon accounts:      These are the CAP users' personal accounts in which they
can temporarily store documents, graphics, or other material that they are
working on.
File only accounts:      These are accounts in which more permanent versions
of files are stored.
00002
00001
Syntax:
!VA$GR_ANV2SGL source {ON|TO|OVER} output [(options)]
Parameters:
 
source  specifies an ANVIL PLT file.
 
{ON|TO|OVER}  specifies file creation or replacement.
 
output  specifies the SGL file to create or replace.
 
options  specifies one or more of the following options:
 
    [N]C  specifies whether or not to chatter (print) informational
        messages.  The default is C.
 
    H='caption'  specifies a comment describing the contents of the
        SGL file.
Description:
 
The VA$GR_ANV2SGL program converts an ANVIL PLT file to an SGL file.
00002
00001
Syntax:
!VA$GR_CPX2CCK source {ON|TO|OVER} output [(options)]
Parameters:
 
source  specifies a Cappix file.
 
{ON|TO|OVER}  specifies file creation or replacement.
 
output  specifies the Cappix file to rotate.
 
options  specifies the following option:
 
    [N]C  specifies whether or not to chatter (print) informational
        messages.  The default is C.
Description:
The VA$GR_CPX2CCK program rotates a Cappix file 90 degrees counterclockwise.
00002
00001
Syntax:
!VA$GR_CPX2CLK source {ON|TO|OVER} output [(options)]
Parameters:
 
source  specifies a Cappix file.
 
{ON|TO|OVER}  specifies file creation or replacement.
 
output  specifies the Cappix file to rotate.
 
options  specifies the following option:
 
    [N]C  specifies whether or not to chatter (print) informational
        messages.  The default is C.
Description:
The VA$GR_CPX2CLK program rotates a Cappix file 90 degrees clockwise.
00002
00001
Syntax:
!VA$GR_CPX2IMC source {ON|TO|OVER} output [(options)]
Parameters:
 
source  specifies a Cappix file.
 
{ON|TO|OVER}  specifies file creation or replacement.
 
output  specifies the Datacopy IMG file to create or replace.
 
options  specifies the following option:
 
    [N]C  specifies whether or not to chatter (print) informational
        messages.  The default is C.
Description:
The VA$GR_CPX2IMC program converts a Cappix file to a Datacopy IMG file with
compression.
00002
00001
Syntax:
!VA$GR_CPX2IMG source {ON|TO|OVER} output [(options)]
Parameters:
 
source  specifies a Cappix file.
 
{ON|TO|OVER}  specifies file creation or replacement.
 
output  specifies the Datacopy IMG file to create or replace.
 
options  specifies the following option:
 
    [N]C  specifies whether or not to chatter (print) informational
        messages.  The default is C.
Description:
The VA$GR_CPX2IMG program converts a Cappix file to a Datacopy IMG file.
00002
00001
Syntax:
!VA$GR_CPX2SGL source {ON|TO|OVER} output (options)ns)]
Parameters:
 
source  specifies a Cappix file.
 
{ON|TO|OVER}  specifies file creation or replacement.
 
output  specifies the SGL file to create or replace.
 
options  specifies the following options:
 
    [N]B[ANTER]  specifies whether to print informational messages.
        The default is BANTER.
 
    C[OMMENT]='string'  specifies a a comment that describes the
        graphic.  If specified, this will be saved in the first record
        of the output file.
 
    DEVICE=M  specifies the type of device being used.  This option
        must be specified.
 
    H[EIGHT]=number  defines number of vertical scan lines to use to
        create the SGL representation.  This option must be specified.
        The picture will look better if the number specified is close
        to the resolution of the display device.
Description:
The VA$GR_CPX2SGL program converts a Cappix file to an SGL file.
00002
00001
Syntax:
!VA$GR_DGS2SGL source {ON|TO|OVER} output [(options)]
Parameters:
 
source  specifies a DIGIS file.
 
{ON|TO|OVER}  specifies file creation or replacement.
 
output  specifies the SGL file to create or replace.
 
options  specifies one or more of the following options:
 
    [N]C  specifies whether or not to chatter (print) informational
        messages.  The default is C.
    H='caption'  specifies a comment describing the contents of the
        SGL file.
Description:
The VA$GR_DGS2SGL program converts a DIGIS file to an SGL file.
00002
00001
Syntax:
!VA$GR_DMP2SGL source {ON|TO|OVER} output [(options)]
Parameters:
 
source  is an AutoCAD PLT file.
 
{ON|TO|OVER}  specifies file creation or replacement.
 
output  specifies that an SGL file be created or replaced.
 
options  specifies one or more of the following:
 
    [N]C  specifies whether or not to chatter (print) informational
        messages.  The default is C.
 
    H='caption'  specifies a comment describing the contents of the
        SGL file.
Description:
The VA$GR_DMP2SGL program converts an AutoCAD PLT file (in Houston Instruments
DMP7 format) to an SGL file.
00002
00001
Syntax:
!VA$GR_DUM2SGL source {ON|TO|OVER} output [(options)]
Parameters:
 
source  specifies an ISSCO DUMDEV file.
 
{ON|TO|OVER}  specifies file creation or replacement.
 
output  specifies that an SGL file be created or replaced.
 
options  specifies the following option:
 
    H='caption'  specifies a comment describing the contents of the
        SGL file.
Description:
The VA$GR_DUM2SGL program converts an ISSCO DUMDEV file to an SGL file.
00002
00001
Syntax:
!VA$GR_GER2SGL source {ON|TO|OVER} output [(options)]
Parameters:
 
source  specifies an Intergraph Gerber plotfile.
 
{ON|TO|OVER}  specifies file creation or replacement.
 
output  specifies the SGL file to create or replace.
 
options  specifies the following option:
 
    H='caption'  specifies a comment describing the contents of the
        SGL file.
Description:
The VA$GR_GER2SGL program converts an Intergraph Gerber plotfile to an SGL
file.
00002
00001
Syntax:
!VA$GR_IMG2CPX source {ON|TO|OVER} output
Parameters:
 
source  specifies a Datacopy IMG file.
 
{ON|TO|OVER}  specifies file creation or replacement.
 
output  specifies the Cappix file to create or replace.
Description:
The VA$GR_IMG2CPX program converts a Datacopy IMG file to a Cappix file.  The
source file may be compressed or uncompressed.
00002
00001
Syntax:
!VA$GR_LOG2SGL source {ON|TO|OVER} output [(options)]
Parameters:
 
source  specifies the output from a LOGITECH HP-7445A plotter.
 
{ON|TO|OVER}  specifies file creation or replacement.
 
output  specifies an SGL file be created or replaced.
 
options  specifies one or more of the following options:
 
    [N]C  specifies whether or not to chatter (print) informational
        messages.  The default is C.
 
    H='caption'  specifies a comment describing the contents of the
        SGL file.
Description:
The VA$GR_LOG2SGL program converts LOGITECH HP-7445A plotter output from
LOGICAD, a generic CADD package, to an SGL file.
00002
00001
Syntax:
!VA$GR_MAC2CPX source {ON|TO|OVER} output
Parameters:
 
source  specifies a MacPaint file.
 
{ON|TO|OVER}  specifies file creation or replacement.
 
output  specifies the Cappix file to create or replace.
Description:
The VA$GR_MAC2CPX program converts a MacPaint file to a Cappix file.
00002
00001
Syntax:
!VA$GR_MDF2SGL source {ON|TO|OVER} output [(options)]
Parameters:
 
source  specifies a Move/Draw file.
 
{ON|TO|OVER}  specifies file creation or replacement.
 
output  specifies the SGL file to create or replace.
 
options  specifies the following option:
 
    [N]C  specifies whether or not to chatter (print) informational
        messages.  The default is C.
Description:
The VA$GR_MDF2SGL program converts a Move/Draw file to an SGL file.
00002
00001
Syntax:
!VA$GR_P012SGL source {ON|TO|OVER} output [(options)]
Parameters:
 
source  specifies a PCDRAW P01 file.
 
{ON|TO|OVER}  specifies file creation or replacement.
 
output  specifies an SGL file be created or replaced.
 
options  specifies one or more of the following:
 
    [N]C  specifies whether or not to chatter (print) informational
        messages.  The default is C.
 
    H='caption'  specifies a comment describing the contents of the
        SGL file.
Description:
The VA$GR_P012SGL program converts a PCDRAW P01 file to an SGL file.
00002
00001
Syntax:
!VA$GR_SGL2CCK source {ON|TO|OVER} output [(options)]
Parameters:
 
source  specifies an SGL file.
 
{ON|TO|OVER}  specifies file creation or replacement.
 
output  specifies the SGL file to rotate.
 
options  specifies the following option:
 
    [N]C  specifies whether or not to chatter (print) informational
        messages.  The default is C.
Description:
The VA$GR_SGL2CCK program rotates an SGL file 90 degrees counterclockwise.
00002
00001
Syntax:
!VA$GR_SGL2CLK source {ON|TO|OVER} output [(options)]
Parameters:
 
source  specifies an SGL file.
 
{ON|TO|OVER}  specifies file creation or replacement.
 
output  specifies the SGL file to rotate.
 
options  specifies the following option:
 
    [N]C  specifies whether or not to chatter (print) informational
        messages.  The default is C.
Description:
The VA$GR_SGL2CLK program rotates an SGL file 90 degrees clockwise.
00002
00001
Syntax:
!VA$GR_SGL2CPX source {ON|TO|OVER} output [(options)]
Parameters:
 
source  specifies an SGL file.
 
{ON|TO|OVER}  specifies file creation or replacement.
 
output  specifies the Cappix file to create or replace.
 
options  specifies the following option:
 
    [N]C  specifies whether or not to chatter (print) informational
        messages.  The default is C.
Description:
The VA$GR_SGL2CPX program converts an SGL file to a Cappix file.
00002
00001
Syntax:
!VA$GR_SGL2DXB source {ON|TO|OVER} output [(options)]
Parameters:
 
source  specifies an SGL file.
 
{ON|TO|OVER}  specifies file creation or replacement.
 
output  specifies the AUTOCAD DXB file to create or replace.
 
options  specifies the following option:
 
    [N]C  specifies whether or not to chatter (print) informational
        messages.  The default is C.
Description:
The VA$GR_SGL2DXB program converts an SGL file to an AUTOCAD DXB file.
00002
00001
Syntax:
!VA$GR_SGL2LOG source {ON|TO|OVER} output
Parameters:
 
source  specifies an SGL file.
 
{ON|TO|OVER}  specifies file creation or replacement.
 
output  specifies the LOGITECH HP-7445A plotter output to create or
    replace.
Description:
The VA$GR_SGL2LOG program converts an SGL file to LOGICAD, a generic CADD
package by LOGITECH.
00002
00001
Syntax:
!VA$GR_SGL2MDF source {ON|TO|OVER} output [(options)]
Parameters:
 
source  specifies a SGL file.
 
{ON|TO|OVER}  specifies file creation or replacement.
 
output  specifies the Move/Draw file to create or replace.
 
options  specifies the following option:
 
    [N]C  specifies whether or not to chatter (print) informational
        messages.  The default is C.
Description:
The VA$GR_SGL2MDF program converts a SGL file to an Move/Draw file.
The post processors available with CAP are described below.
00002
00001
Syntax:
!VA$MN_FMTCLASS fid (options)
Parameters:
 
fid  is a DVI or DSF file.
 
options  specifies one of the following options:
 
    GET(suboption)  requests information about the file to be
        retrieved and puts into IBEX command variables.  The
        information requested is specified by one or both of the
        following suboptions:
 
        CLASS=cmdvar  requests that the file class be returned in
            the specified command variable.
 
        TYPE=cmdvar  requests that the file type be returned in
            the specified command variable.
 
    SET(suboption)  specified that information about the file is to be
        saved in the file.  The information to be saved is specified
        by one or both of the following suboptions:
 
        CLASS='string'  requests that the file class be set to the
            specified string.
 
        TYPE={DVI|DSF}  requests that the file type be set as
            specified.
Description:
VA$MN_FMTCLASS saves and retrieves information about formatted CAP document
files.  This information is used when printing the file to ensure that it is
not inadvertently printed on a device that is not compatible with the way the
document was formatted.
 
Each formatted CAP document contains both a file type and class.  The file
type is either DVI or DSF. The class is a string of up to 30 characters that
is assigned by the administrator to identify the characteristics of the target
device.  A file that does not contain this information cannot be printed by
CAP.
00002
00001
Syntax:
!VA$MN_HERMAN textfile {ON|TO|OVER} hermanfile ([N]C)
Parameters:
 
textfile  is the output of the TeX formatting process.
 
hermanfile  is the HERMAN source file to create.
 
[N]C  specifies whether or not to chatter (print) messages as each graphic
    is encountered.  The default is C.
Description:
VA$MN_HERMAN creates a file that can be passed to HERMAN to create a CP-6 HELP
file.
00002
00001
Syntax:
!VA$MN_INDEXSORT source {ON|TO|OVER} output
Parameters:
 
source  specifies the index file to be sorted.
 
{ON|TO|OVER}  specifies file creation or replacement.
 
output  specifies the sorted index file to create or replace.
Description:
The VA$MN_INDEXSORT program sorts a CpTeX index file for use in a subsequent
formatting pass.  CpTeX produces unsorted index files with a suffix of :idx,
and expects the sorted index file to have a suffix of :ids.
00002
00001
Syntax:
!VA$PP_ERRMESS source {ON|TO|OVER} output
Parameters:
 
source  specifies a TeX log file.
 
{ON|TO|OVER}  specifies file creation or replacement.
 
output  specifies the error message file to create or replace.
Description:
The VA$PP_ERRMESS program converts a TeX log file into a more easily readable
error message file by removing the extensive diagnostic information that is
usually meaningful only to CAP developers.
 
The programs used to modify textual representations are described below.  For
a description of the text conversion program VA$PP_A002B00, see the CP-6 DSL
Reference (HA27).
00002
00001
Syntax:
 
!VA$PP_SUBS capfile {ON|OVER|TO}
    newfile (I[NTRO]='\',L[EFT]='{',R[IGHT]='}')
Parameters:
 
capfile  is a CAP file.
 
newfile  is the new CAP file containing new substitution strings.
 
options:
 
    I[NTRO]  is the introducer character.  The default is '\'.
 
    L[EFT]  is the left delimiter character.  The default is '\'
 
    R[IGHT]  is the right delimiter character.  The default is '}'.
Description:
The VA$PP_SUBS program scans CAP files for substitutions of textual strings in
the format:
 
    \*{SUB{str1},{str2}}
 
where
 
str1  is the string to look for.
 
str2  is the string to substitute for str1.
 
Substitution with str2 occurs whenever str1 is encountered.  A special case is
where a substitution statement is given and another substitution statement is
encountered later in the document, substituting the first string with itself
again.  Substitution occurs only after a substitution statement is
encountered; the remaining text in the document then applies to this
substitution criteria.
00002
00001
Syntax:
 
!VA$TI_COLLATE fid1 {ON|TO|OVER|INTO}
    fid2 (S[TART]='startmark',E[ND]='endmark')
Parameters:
 
fid1  specifies one or more input files.  These files are usually
    specified with the wildcard character (?).
 
fid2  specifies the output file.  This file contains all of the files
    specified in fid1.
 
options  specifies one or more of the following options:
 
    S[TART]  specifies a file marker that indicates the beginning of a
        file.  The default starting file marker is '\*{*** '.
 
    E[ND]  specifies the end of a file marker that is denoted by the
        'endmark'.  The default ending file marker is ' *****'.
Description:
The VA$TI_COLLATE program collates a group of source files into one file.  The
files to be collated are specified with the wildcard character (?).  A marker
is inserted before the first line of each file so that these files can later
be separated again.  A marker is also inserted at the end of each file to
denote the end of that file.  The file created as fid2 is a keyed file.
00002
00001
Syntax:
 
!VA$TI_DECOLLATE fid1 {ON|TO|OVER|INTO}
    .acct (S[TART]='startmark',E[ND]='endmark')
Parameters:
 
fid1  is the file that contains one or more files separated by beginning
    and ending file markers.
 
     .acct - is the account into which the new files are created.
 
options  specifies the following options:
 
    S[TART]  is an optional file marker that indicates the beginning
        of a file.  The default is \*{*** .
 
    E[ND]  is an optional file marker that indicates the end of a
        file.  The default is  *****.
Description:
The VA$TI_DECOLLATE program divides one file into separate files by searching
for the beginning and ending file markers.  Each file that is found is then
separated and named according to the file name inside the start marker.  The
separated individual files are created as keyed files.
00002
00001
Syntax:
!VA$TI_OUTLINE sourcefile {ON|INTO|OVER} outputfile [([N]C)]
Parameters:
 
sourcefile  specifies the outline file to convert.
 
outputfile  specifies the CAP file to create.
 
[N]C  specifies whether or not to chatter (print).  The default is C.
Description:
The VA$TI_OUTLINE program converts a file of indented records into CAP level
head controls.  See the CP-6 CAP User Guide (HA29) for a description of this
function.
00002
00001
Syntax:
VA$TI_PRETTY_PRINT in_file,dsl_file {TO|ON|OVER} out_file [[(options)]]
Parameters:
 
in_file  is the B01 CAP file containing DSL controls.
 
TO|ON  creates a keyed output file.  If file exists, an error message is
    issued and the program aborts.
 
OVER  creates a keyed output file over an existing file, if it exists.
 
dsl_file  is the file containing a list of DSL controls that tells the
    pretty printer which one turns fill mode on/off, and if it is accepted
    as a DSL control.
 
out_file  is an optional place to put the reformatted output.
 
options  is one or more of the following options, separated by commas:
 
    IND[ENT]=n  specifies how many characters to indent for non-
        directives.  n is the number of characters to indent.  Default
        is 4.  Range is 0 - 15.
 
    LEN[GTH]=n or WID[TH]=n or RECS[IZE]=n  sets the length of the
        records formatted by the pretty printer.  Default is 69, range
        is 20 - 255.
 
    SENT[ENCES]  starts each sentence on a new line.  Sentences ending
        in the characters :  ?  !  .  followed by two spaces.  Default
        is paragraphs beginning on new lines.
 
    NWA[RN]  prevents warning messages about unknown controls or
        duplicate words from being printed.
 
    NS[UMMARY]  suppresses the wordcount summary line print after the
        file is processed.
 
    KEYIN[CREMENT]=n  changes the default key increment in the output
        file.  Default key increment is 1.000.
 
    INT[RODUCER]=char  specifies the activator character for the DSL
        control.  Default is \.
 
    L[EFT]=char  specifies the left delimiter for the arguments to the
        DSL controls.  Default is {.
 
    R[IGHT]=char  specifies the right delimiter for the arguments to
        the DSL controls.  Default is }.
Description:
The pretty printer program tunes a B01 CAP DSL file so that it is more easily
edited with the CP-6 editors.  It reformats DSL controls located anywhere in
the input file.
 
The writer's toolkit programs are described below.
00002
00001
Syntax:
!VA$WT_PRESCAN_B00 capfile,usrfile (I[NTRO]='\',D[ELIM]='{')
Parameters:
 
capfile  is a CAP text file with control commands.
 
usrfile  is a user supplied/defined file with controls to validate the
    controls in the capfile.
 
options  specifies one or more of the following options:
 
    I[NTRO]  specifies the character that introduces the controls.
        The introducer character can be set by the user.  The default
        is the backward slash (\) character.
 
    D[ELIM]  specifies the character that delimits the end of the
        controls.  The delimiter character can be set by the user.
        The default is the left brace ({) character.
Description:
The VA$WT_PRESCAN_B00 program scans CAP source files for control commands that
are between the introducer and delimiter characters.  If a control command is
found, a search is made for this control in the user-defined control file.  If
the control is not found in the file, an error message is issued.  The user
can specify the introducer and delimiter characters at the command line.  If
the optional characters are not given, the defaults for these characters
apply.  The length of the controls should not exceed 24 characters.
 
The following special characters are accepted as part of the text, rather than
control commands.  They are all preceded by an introducer character:
 
    '\ '
    '\{'
    '\}'
    '\|'
    '\~'
 
The following characters are used to delimit the controls:
 
     <EOL>
     ' '
     '{'
 
The last delimiter '{', can be changed with the DELIM option.
00002
00001
Syntax:
 
!VA$WT_READABLE.X textfile [ON|TO|OVER|INTO ,listfile]
Parameters:
 
textfile  contains the text to be analyzed.
 
M$LO  is used to report the analysis results.
 
M$SI  is used to read the text source.
 
Description:  READABLE estimates the required education level for
    understanding a passage of text.
 
The file formats described in this appendix are subject to change.  Bull HN
cannot guarantee that programs designed to use this file format will work
partially or completely with subsequent versions of CAP.
00001
WP Editing is often not as practical as PC Editing because such systems often
insert numerous codes into the document file that must be converted after
being transferred to the CP-6 system.  Thus, the best choice for this
environment is to disable all page-oriented features so that the WP system
emulates a nonpage PC editor.
 
Many WP programs have an ASCII output function which produces a file that can
be more conveniently transferred to other programs.  This method is the best
way to get WP-created data into a form that CAP can understand.
 
In most cases, WP files transferred to the CP-6 system must be decoded into a
form that CAP can understand.  Decoding is performed by a program; if no
decoding program exists for the WP files, a program must be written.
Depending on how clever the program is, the resulting file will require a
greater or lesser amount of user intervention to raise it to CAP standards.
In particular, it may be necessary to add controls that make CAP understand
the structure of the document.
00003
00002
00001
XMODEM can sometimes be a better choice for transferring files than KERMIT,
especially when the connection between CP-6 and the personal computer is clean
(i.e., there is not much static on the line).  XMODEM can transfer data in
larger packages, thus reducing the overhead that it takes to move files back
and forth.
Most terminal emulators have an XMODEM capability, including CP-6 PCT. The
version of XMODEM that runs on the CP-6 system is described in the CP-6 PC
Terminal (PCT) Facility Reference Manual (HA15).  Some information on MODEM.X
is also contained in the MODEM.X HELP file.
 
MODEM.X can be used to transfer files to and from many different personal
computers including MacIntoshes, Wang Personal Computers, and Atari 800XL home
computers.  The main concern is to match the various settings on the personal
computer with the MODEM.X options; this varies from emulator to emulator.  PCT
makes XMODEM transfers extremely convenient by providing special files on the
CP-6 system that assist in the setting of various options.  See the CP-6 PC
Terminal (PCT) Facility Reference Manual (HA15) for more information.
