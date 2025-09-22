CAP supports Quality Micro Systems (QMS) Lasergrafix laserprinters that use
QUIC, a special computer language that controls QMS Lasergrafix devices.  In
this section, Lasergrafix printers that support QUIC are referred to as "QUIC
printers."  When a distinction is required between different models of QUIC
printers, the model number is stated.
 
This section does not contain reference information about QUIC device
protocol, which is found in the user documentation for the Lasergrafix
laserprinters.
CP-6 CAP Administrator Guide - HA30-00
*************************************************************************
*
* Copyright (c) Bull HN Information Systems Inc., 1989, 1994
*
*************************************************************************
The CAP device definition for each QUIC device has a parameter that tells
VA$DVILG which file contains the resident font information.  The default file
is
 
  VA_QMS_RES_FONTS.:LIBRARY
 
which, by default, assumes no resident fonts.  The 'resident' parameter must
be changed in the device definition to point at the new resident font file.
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
Normally, the VA$DVILG program assumes that there are no resident fonts on the
device and does not use them if they are present.  For CAP to utilize resident
fonts (RAM or ROM), it must know which fonts are available.  This is
accomplished by creating a file that contains the information that VA$DVILG
needs to intelligently utilize them.  An example that matches default CAP
usage is shown below:
 
    cmr12 1500 6000 P
    cmbx10 1500 6001 P
    cmbx10 2160 6002 P
    cmbx10 2592 6003 P
    cmbx12 1500 6004 P
    cmti12 1500 6005 P
    MEMORY 90
 
The first item on each line must be either a font name or MEMORY. If it is a
font name, it must be followed by the size of the font, followed by the
downloaded font number (in the QMS printer), followed by a flag indicating
that it is downloaded in portrait or landscape mode (P or L). If the first
item is MEMORY, then the following number is the amount of free memory
available in the printer for dynamically downloaded fonts and graphics.
\specials are commands that TeX finds in the input file that are passed
directly to the dvi file.  The following \specials are supported by DVILG:
continue, include, landscape, long, and 'literal'.
 
CONTINUE()
 
This special command disables positioning between the current special and the
next special command.
 
INCLUDE(fid,options)
 
This command allows graphics to be included with a TeX document.  The include
file must contain QUIC commands to dislpay a graphic.
 
With this facility, a user can mix text and graphics within a single TeX
document.  The syntax for this command (as TeX input) is
 
        \special include(fid,options)
 
The options are used to control the positioning of the graphic and to filter
QUIC commands.  The QUIC ON and QUIC OFF commands are always stripped.
 
The following options are available:
 
origin    places the absolute origin at the current position on the output
page.
 
zero    places both the absolute and relative positions at the upper left
corner of the page.
 
relative    places the relative position at the current position, but leaves
the absolute position at the upper left.
 
pixel    specifies that positioning commands are to be four-digit pixel
quantities, rather than five-digit fractions of an inch.
 
noorigin    removes the absolute origin commands (^IJ and ^IT).
norelative    removes the relative positioning commands (^J and ^T).
 
nofree    removes the free format on and off commands (^F and ^O).
 
fortran    ignores the first character in each record.
 
noorient    removes the orientation commands (landscape or portrait).
 
LANDSCAPE()
 
This command puts the QMS printer in landscape mode.  The TeX values for
\hsize and \vsize should be redefined when using this command.
 
LONG()
 
This command puts the QMS printer in portrait mode (8.5" x 11" paper).  This
command does not select the paper tray, which can be selected by using the
'literal' command.
 
'literal'
 
This command is used to pass an arbitrary QUIC command directly to the
printer.  Everything that appears within quotes is sent to the printer exactly
as is, without any discrimination by DVILG.
GENERATE_RAM_FONT_FILE
When the DVILG program is run in NO DEBUG mode, only error messages are
displayed.  Some of the messages are informational only, while others indicate
a problem with the document.
 
The most typical messages are
 
Couldn't find ????pk
 
and
 
Couldn't find ????pxl
 
which indicate that one of the fonts that has been requested does not exist at
the requested magnification (\magstep).  In this case, the document must be
reformatted by TeX with a different font specified.  Alternatively, these
messages indicate that the search account list specified on the DVILG command
line does not specify the account in which the font definitions for the
formatted document can be found.
 
If the message
 
Cannot open bit file or printer output!
 
is printed, there is something wrong with the output_fid specified on the
DVILG command line.
 
The error message
 
Couldn't find ????:tfm
 
usually indicates that the search account list specified on the DVILG command
line does not include the account in which the font definitions for the
formatted document are found.
The first step to configuring a CP-6 system for a QUIC device is to create a
form which defines the type of paper to be used on the device.  CP-6 forms
were originally designed to support lineprinters.  Therefore, the default form
treats the QUIC device much like a lineprinter.  Step 2 shows how to create a
pseudoform that is more appropriate for CAP documents.
 
The following figure shows JCL that creates the STDQMS form, which is the
default for all QUIC devices:
 
!SUPER
REMOVE FORM STDQMS
CREATE FORM STDQMS
WIDTH=85
LIMBO=88
LENGTH=66
FIRSTLINE=0
LPI=6
CHARSET = 600
SETUP
***************************************
Special \QMS\ laserprinter form; variable format
***************************************
BANNER
REPEAT=1
EN=1,1,0,1,0,1,0,0
^PY^-
EN=2,1,0,1,0,1,0,0
^F^-^A^-^IGE^-^IL0605^IC1010^IS00404^-^DCC0001^IJ00100^IT00200^IOP^-
^DOC^Z^DAOC^-^O
EN=3,1,0,1,0,1,0,0
^PY^-
EN=4,1,0,1,0,1,0,0
%DATE
EN=4,10,0,1,0,1,0,0
%TIME
EN=4,16,0,1,0,1,0,0
%REGISTEREDNAME
EN=4,39,0,1,0,1,0,0
%SYSID
EN=4,45,0,1,0,1,0,0
.
EN=4,46,0,1,0,1,0,0
%SUBFILE
EN=4,54,0,1,0,1,0,0
WOO=
EN=4,58,0,1,0,1,0,0
%WOO
EN=4,68,0,1,0,1,0,0
WOD=@
EN=4,73,0,1,0,1,0,0
%WOD
EN=6,8,3,1,1,1,0,0
%UNAME
EN=16,8,3,1,1,1,0,0
%SYSID
EN=26,8,3,1,1,1,0,0
COMPUTER
EN=36,8,3,1,1,1,0,0
AIDED
EN=46,8,3,1,1,1,0,0
PUBLICATION
 
END
In order to gather font usage data, a font log file must be created with
processor write access for VA$DVILG. This should be a consecutive file created
by the following PCL command:
 
C NO over Font_log.:TEX(acs=((DVI?,VA$DV?),read,delr,w,u),ACC(?,e,read))
 
Each record of this file contains the following information:
 1. Date in form mm/dd/yy followed by a blank.
 2. Time in form hh:mm:ss.ss followed by a blank.
 3. Font name and size in form:  name:xxxxpxl, where a value of 1500 would be
    the magstep 0 size of this font.  The size information corresponds to the
    size that CRERES needs to know.
 4. A blank followed by the font status.  The status values are -1 for a
    stored font, -2 for a loaded font and -3 for a declared font.
 5. A blank followed by the font advantage.  The larger the value here, the
    more advantageous it is to download this font for this particular
    document.  The advantage is based upon the size of the font (because large
    fonts use up memory quickly), the number of times a character from this
    font was used, and the number of unique characters that were used in this
    font.
    Note that when DVILG downloads fonts for printing a document, only those
    characters that are actually used in the document are downloaded, whereas
    when CRERES downloads a font, every character in that font is downloaded.
 6. A blank followed by the number of unique characters that were used in this
    font.  This is always a number less than 256.
 7. A blank followed by the total number of times a character from this font
    was printed in the document.
 
You can use the information in this file to track the fonts that are heavily
used and then add them to the resident font file, generate RAM fonts for them,
or even purchase ROM font chips, for maximum throughput.
(Note that this step is skipped if ROM fonts are installed.)
 
Use the CRERES program to generate a RAM font file that contains the fonts
that are defined in the resident font file.  CRERES is in the :SYS account.
The syntax is:
 
   CRERES res-font-file {ON|OVER} ram-file(DEVICE={800|1200|1500|2400})
 
The DEVICE=800 option works for QMS800 and QMS1500 laserprinters that support
the QUIC language.  The DEVICE=2400 option works for QMS1200 and QMS2400
laserprinters that support the QUIC language.
 
The file thus created can be downloaded into the device with a COPY command:
 
   COPY ram-file TO LZ@CAP
Note that the ram-file must be copied to the QUIC laserprinter every time the
printer is powered up, the reset button is pushed, or a ^RESET is sent to the
device.  Fonts can be removed by the ^DF control in QUIC. See below for
potential problems with RAM fonts.
The following procedure is recommended for utilizing the resident font feature
of CAP:
Step 1:      Gather information about font usage on the device in question.
Step 2:      Create a resident font file that contains the most frequently
used fonts.
Step 3:      Generate and download a RAM font file that contains the most
frequently used fonts.  (This step is skipped if ROM fonts are purchased and
installed.)
Step 4:      Build a CAP device definition that points at the resident font
file created in step 2.
00001
00002
00003
00004
VA$DVILG is a program that produces output for the QMS Lasergrafix printers
using TeX output files (known as dvi files) as input.  This program permits
the user to specify a number of options and it implements a number of \special
commands as extensions.  (See the Device Specials subsection later in this
section.)  Normally, the CAP menus generate the correct VA$DVILG commands for
any given situation.
Syntax:
!DVILG dvi_file ON out_file[,list_file(options)]
 
or
 
!DVILG dvi_file OVER out_file[,list_file(options)]
 
Note that the list_file and (options) parameters are optional.
Parameters:
 
dvi_file  is a dvi file produced by the TeX processor.
 
out_file  is a file suitable for sending to a QUIC printer.
 
list_file  is a file containing errors and or debugging information.
 
options  are the options to be used to produce the out_file, as follows:
 
    COPIES, [NO] DEBUG, [NO] CHATTER, DEVICE, [FONT] LOG, FORM, HOFFSET,
    MAXIMUM PAGES, STARTING PAGE, [NO] PROMPT, RANGE, RESIDENT [FONTS],
    REVERSE, SRCH, and VOFFSET.
 
These options are described below.  They are presented alphabetically for
quick reference except that [NO] DEBUG and [NO] CHATTER appear together.  Note
that all options are case-insensitive.
 
CO/PIES = n
 
This option is used to request that DVILG make multiple copies of each page as
the printer is printing them.  The n parameter must be the integer number of
pages to print.  The default is 1 copy of each page.
 
[N/O] DEB/UG
[N/O] CH/ATTER
DEBUG and CHATTER are identical.  This option is used to request that DVILG
print information about each phase of the printing process.  With this option,
output is displayed on the list_file (or the ME device if list_file is not
specified).  The default is NO DEBUG, which causes DVILG to produce error
messages only.
 
The debug output appears in three sections.  The first section includes the
names and numbers of each font used in the document.  The second section
contains the font downloading information, where DVILG locates the fonts that
are to be downloaded to the device.  In the third section, DVILG generates the
output for each page, printing the page number that has just been output.
 
DEV/ICE = [QMS] {800|1200|1500|2400}
 
This option is used to specify the model number of the QMS printer for which
output is to be generated.  The currently supported model numbers are 800,
1200, 1500, and 2400.  The default device is the QMS800.
 
[FONT] LOG = fid
 
This option is used to specify a file for font usage information.  It is
recommended that a separate logging file be used for output to different
devices, since the main purpose of this information is to determine which
fonts to download permanently into the device with the CRERES program.
 
FO/RM = 'name'
 
This option is used to request that DVILG create the output file as a CP-6
unit record file with the specified default output form.  This option is
particularily useful if output is being sent directly to the device or if the
default CP-6 form for the device is not suitable for the DVILG output.  The
default is for DVILG to create a consecutive file with no default form
information.
 
HOFF/SET = count
 
This option is used to change the default 1 inch horizontal margin that DVILG
uses when printing.  The default value for count is 300 (1 inch) and can range
from 0 to 900 (3 inch horizontal margin).
 
MAX/IMUM [P/AGES] = n
 
This option limits the number of pages for which output is generated to the
number specified.  The default MAXIMUM PAGES is 1000000.  The maximum number
of pages to print can be used with the STARTING PAGE option to print a subset
of the TeX document.
 
For example, to print pages 8 through 12 of a document, the following options
are entered:
 
(STAP=8,MAXP=5)
 
In this case, DVILG starts printing the document at page 8 (STAP=8) and prints
5 pages (MAXP=5), which are pages 8, 9, 10, 11 and 12.
[N/O] PROM/PT
 
This option is used to request that DVILG prompt the user for all the options
that affect the output.  The default is NO PROMPT.
 
RANGE = a[.b[.c...j]] [ TO k[.l[.m...t]]
 
Syntax
a,k    are values for count0.
b,l    are values for count1.
c,m    are values for count2.
j,t    are values for count9.
 
This option is used to selectively print a range of pages that are identified
by the values of \count variables in the dvi file.  This option causes the
pages to be printed in ascending or descending order of the non-* \count
values specified.
 
The values specified before the TO keyword select the \count values, and the
values specified after the TO keyword select the page values.
 
A value of * can be entered for a \counter.  In the starting range, this
selects pages starting at page -1; in the finishing range, this selects  + 1
as the finishing page.
 
Not all of the counter values are sorted.  For a \count value to be used to
sort the pages, a non-* value must be specified for the starting or finishing
count.  For the page sort, ascending page count values are:
 
- 1-2;-3;:;-1;01;2::+1
 
When multiple counters are specified for the page sort, the lowest value
counter has the most significant effect upon the sort.
 
A page is included in the output if it is greater than or equal to the
specified starting range and it is less than or equal to the specified finish
range.  When a page is being checked to see if it can be printed, the only
counters that are compared are those for which a non-* value is specified.
 
A page is considered to be within range if both of the following are true:
 
o   All of the starting counter values are equal to the counters for this page
    or the page counter value for the first counter that is not equal to the
    start value is greater than the start value.  Comparison of starting
    values stops at the first nonequal counter value.
o   All of the finishing counter values are equal to the counters for this
    page or the page counter value for the first counter that is not equal to
    the finishing value is less than the finishing value.  Comparison of
    finishing values stops at the first nonequal counter value.
 
RANGE=*
 
This does not select any count values at all for printing; therefore, this
option is ignored.
 
Range=0
 
This prints all pages whose \count0 value is greater than or equal to 0.
These pages are printed in the order indicated by printing all pages with
\count0 equal to 0 before pages with \count0 equal to 1, etc.  This is also
equivalent to RANGE=0 TO *.
 
RANGE=*.2 TO *.2
 
This prints all pages whose \count1 value is equal to 2.  These pages are
printed in the order indicated by sorting \count1, which causes them to be
printed in the order in which they are found in the dvi file because all of
their values are equal.  Note that \count0 is not used in the sort, because a
non-* value must be entered for a \count.
Range = *.2 to *.3.4
 
This prints all pages whose \count1 value is 2 or 3 and whose \count2 value is
less than 5 when \count1 is equal to 3.  That is, the value of \count2 is
checked only when \count1 is equal to 3.  This means that pages 2-1, 2-2, 2-3,
2-4, 2-5,..., 2-n would be printed, followed by pages 3-1, 3-2, 3-3 and 3-4.
 
Range = *.4.6 to *.7.3
 
This prints the following pages:
 
o   All pages whose \count1 values are 4 and whose \count2 values are greater
    than or equal to 6.
o   All pages whose \count1 values are 5 or 6 regardless of their \count2
    values.
o   All pages whose \count1 values are equal to 7 and whose \count2 values are
    less than or equal to 3.
 
RES/IDENT [FONTS] = fid
 
This option is used by DVILG to locate the file that contains the names and
identities of the fonts residing on the output device.  The resident fonts can
vary from device to device at an installation, so you should make sure that
the specified file is the correct one for the device.  If this option is not
specified, the default file tex_resident_fonts.:TEX is assumed.  Note that
this file is subject to the SRCH option if a specific account is not present.
 
[N/O] REV/ERSE
 
This option is used to request that DVILG produce the output, starting at the
first page through the last page (NO REVERSE) or starting at the last page
through the first page (REVERSE). The default depends on the DEVICE option.
If DEVICE=QMS800, the default is REVERSE; otherwise, it is NO REVERSE.
 
{SEARCH|SR/CH}(fid,fid,fid,...fid)
 
This option is used to search for input files.  All files (including tfm, pk
and pxl files) other than those specified on the command line, and those
without an account specification, are searched for through the list of
accounts specified on the command line SRCH option.
 
The SRCH accounts are specified by providing a series of one to six CP-6 fids
within parentheses separated by commas.  The filename portion of each fid
specification should be empty.  Every search list is assumed to terminate with
the account specification
..,.:TEX.,.:LIBRARY. For example
 
        (SRCH(.:TEXTEST,DP#LADC.HISACCT))
 
causes DVILG to search for files in the :TEXTEST account first.  If the file
does not exist there, DVILG searches for the file on the packset DP#LADC in
the HISACCT account.  If the file still cannot be found, DVILG searches in the
current file management account, the :TEX account, and :LIBRARY account.
 
STA/RTING [P/AGE] = n [.n [.n...]]
 
The starting page is specified with a sequence of 1 to 10 numbers or
asterisks, separated by periods.  For example, the specification
 
        STARTING PAGE=1.*.-5
 
can be used to refer to a page produced by TeX when \count0=1 and \count2=-5.
An asterisk matches any number, so the * in 1.*.-5 means that the value of
\count1 is ignored when specifying the starting page.  If several pages match
the given specification, DVILG starts with the earliest such page in the dvi
file.  The default specification STARTING PAGE=* matches all pages and
therefore denotes the page at the beginning of the file.
VOFF/SET = count
 
This option is used to change the default 1 inch vertical margin that DVILG
uses when printing.  The default value for count is 300 (1 inch) and can range
from 0 to 900 (3 inch vertical margin).
00007
00009
00002
00001
00004
00002
00003
00008
00005
00006
00001
00002
00003
00004
00001
Finally, you must tell the CP-6 system about the physical connection or line
by which the QUIC printer is attached to the system.  It is important that the
baud rate or SPEED (as it is stated in the JCL below) match the baud rate set
in the QUIC printer.  In 1200/2400 devices, the baud rate is set using dip
switches inside the controller box.  In the 800 device, the baud rate can be
set in the software.  See the QMS documentation for further information.
 
The following JCL configures line .4700 on communications processor number 1
for a Lasergrafix 1200 printer:
 
!NETCON
SEL N=1
CONFIG  ``*1-*'' .4700
SPEED=19200,LOGON='LZ01,,SECRET',SAL=NO,LOGONTIMEOUT=0,;
    READTIMEOUT=0,PROFILE='QMS1200',FLOWC=YES,HARD=YES,;
    REENABLE=YES, ``LASERPRINTER''
KILL .4700
ENAB .4700
END
There are four QUIC printer models:  the 800, the 1200, the 2400, and the
1500.  As of this writing, all of these models have been discontinued, except
for the 1500.
 
The 1200 and the 2400 are functionally identical, except that the 2400 can
hold more paper, can print twice as fast, and is rated for printing more pages
per month.
 
The 800 is based upon a different laserprinting technology than the 1200/2400
device.  The 1500 is reputed to be functionally identical to the 800.
 
Although both the 1200/2400 devices and the 800/1500 devices both support the
QUIC language, there are some subtle differences.  As a result, documents that
have been formatted and resolved for a 1200/2400 device cannot be successfully
displayed on an 800/1500 device using the CP-6 COPY command.  CAP uses the
concept of device classes to accomodate such differences.  Device classes are
discussed in further detail later in this section.
There are slight differences in the way that the 800/1500 and 1200/2400
devices handle margins.  Normally, CAP accommodates both types of devices.
However, if a site has both types of printers and there is a need to use the
devices for non-CAP purposes, the following procedures should make them
perform in a more parallel fashion:
 1. The "zero adjust" for left and top margins, as described in the QMS800
    installation manual, should be performed.  The left margin should be moved
    about (6*16)/300ths of an inch (0.32 inches) further to the left to make
    the graphics alignment of the QMS800 match the graphics alignment of the
    QMS1200, setting options 46 and 47 to ON on the 800.
 2. The default banner for STDQMS now specifies a left margin offset of 0.35
    inches (changed from 0.2 inches) and a top margin of .1 inch (no change)
    to guarantee that text copied to the device in "line printer" mode appears
    intact (^IT00350).  The creation of CP-6 banners is discussed in the next
    subsection.
QUIC printers must have the RS232 asynchronous communications daughter board
option to be connected to the CP-6 system.  No other options are required or
supported.
The next step is to create a pseudoform that is appropriate for CAP documents.
A pseudoform can be considered a "form within a form."  The pseudoform QMSCAP
exists inside the STDQMS form.  This makes it possible to use the laserprinter
both as a lineprinter (using STDQMS) and as a laserprinter (using QMSCAP). The
pseudoform makes it appear to CP-6 communications that the device is a
lineprinter with very large margins.
 
The following figure shows JCL that creates the QMSCAP pseudoform:
 
!SUPER
REMOVE FORM QMSCAP
CREATE PSEUDO QMSCAP FOR STDQMS
WIDTH=250
LIMBO=66
LENGTH=88
FIRSTLINE=0
BANNER
REPEAT=1
EN=7,1,0,1,0,1,0,0
^PY^-
EN=8,1,0,1,0,1,0,0
^F^-^A^-^IGE^-^IL0805^IC1400^IS00010^-^DCC0001^IJ00100^IT00200^IOP^-
^DOC^Z^DAOC^-^O
EN=9,1,0,1,0,1,0,0
^PY^-
EN=10,1,0,1,0,1,0,0
%DATE
EN=10,10,0,1,0,1,0,0
%TIME
EN=10,16,0,1,0,1,0,0
%REGISTEREDNAME
EN=10,39,0,1,0,1,0,0
%SYSID
EN=10,45,0,1,0,1,0,0
EN=10,46,0,1,0,1,0,0
%SUBFILE
EN=10,54,0,1,0,1,0,0
WOO=
EN=10,58,0,1,0,1,0,0
%WOO
EN=10,68,0,1,0,1,0,0
WOD=@
EN=10,73,0,1,0,1,0,0
%WOD
EN=12,8,3,1,1,1,0,0
%UNAME
EN=22,8,3,1,1,1,0,0
%SYSID
EN=32,8,3,1,1,1,0,0
COMPUTER
EN=42,8,3,1,1,1,0,0
AIDED
EN=52,8,3,1,1,1,0,0
PUBLICATION
 
END
Question:  What is the relationship between the font names supplied by the QMS
startup sheets and the TeX names?  That is, what is the relationship between
CORB and ambx10?
 
Answer:  None.  TeX does not use the QMS startup fonts.  To be used, they
would have to have tfm files (TeX Font Metrics) which tell TeX and VA$DVILG
the size and shape of each character.  Unless QMS publishes this information
(if indeed they have that information) there is no practical way to change
this situation.  However, QMS does make ROM fonts that are compatible with
TeX.
 
Question:  How does one specify the already installed ROM fonts in the
res_font_file for CRERES to know about, since the format is font_name size
downloaded_font_number (P or L)?
 
Answer:  This information comes with the ROM font.  To use a combination of
RAM and ROM fonts, CRERES must be invoked using a resident font file that
contains only the fonts that are to be downloaded (RAM fonts).  Then the ROM
numbers are added to the resident font file to inform the driver as to which
fonts (RAM or ROM) are on the device.
 
Question:  Where do you get the correct RAM or ROM name?
 
Answer:  The name of a font is determined by TeX conventions.  The :TEX
account contains numerous files beginning with cm; these are pixel
representations and tfm files for the "Computer Modern" font group.  These
names are used in the VA:FONTS file to determine how the CAP names (e.g., \IT,
\BF) are mapped into actual fonts.  These names are standard TeX conventions.
There is another older family of similar fonts called am for "Almost Modern".
 
Question:  Where do you get the font size?
Answer:  For a given size to be available, there must be a pixel file that
represents the font in that size.  However, sizes can be magstepped at
mathematically regular intervals (multiples of 1.2), which in effect "clones"
larger fonts.  This means that TeX supplies several hundred font files in
various resolutions and sizes.
 
There are two types of pixel file names.  The first and most common is called
a pk or packed pixel file, the form name:xxxpk.  The string name is the name
of the font, as in cmr12; xxx is the device resolution multiplied by the
magnification.  The common magnifications are 1.1, 1.2, 1.44, 1.7, 2.07, and
2.5 (known as half magstep and magstep 1 through magstep 5), which result in
the following packed file names for font cmr10 on a 300 dpi device.
 
      Magstep               Packed Pixel
                            File Name             Pixel
                                                  File Name
      0                     cmr10:300pk           cmr10:1500pxl
 
      0.5                   cmr10:329pk           cmr10:1643pxl
 
      1                     cmr10:360pk           cmr10:1800pxl
 
      2                     cmr10:432pk           cmr10:2160pxl
 
      3                     cmr10:518pk           cmr10:2592pxl
 
      4                     cmr10:622pk           cmr10:3110pxl
 
      5                     cmr10:746pk           cmr10:3732pxl
 
The second pixel file type, called a pxl or pixel file, is uncommon because it
uses excessive disk space.  Pixel file names have the form name:xxxxpxl, as
illustrated in the above table.  The string name is the name of the font, and
xxxx is a function of the device resolution and the magnification.
 
The size values to use when defining the downloaded fonts are in the first
column of the following table.  Note that the fourth column, Effective Size,
is a sample size corresponding to a 10 point font magnified to the indicated
magstep.  For example, a 10 point font at magstep 1 is 12 point.
 
          Size       Magstep     Magnify     Effective
                                             Size        pk Size
 
          1500       0           1           10          300
 
          1643       0.5         20          11          329
 
          1800       1           44          12          360
 
          2160       2           73          14.4        432
 
          2592       3           107         17.3        518
 
          3110       4           250         21          622
 
          3732       5           300         25          746
 
Question:  Where do you get the QMS font number to use for downloaded fonts?
 
Answer:  You select numbers that are not used by ROM fonts on the device and
are not in the range 5000 to 5999.
 
Question:  Does CRERES have to know about all of the above?
 
Answer:  CRERES is driven by the resident font file; if the font exists as a
pixel file, CRERES creates a downloadable version of it.  You only run CRERES
once to produce a file, which can then be saved and downloaded whenever TeX is
to use the device.
 
Question:  How do you specify the installed fonts to VA$DVILG?
 
Answer:  VA$DVILG looks at the resident font file to determine which fonts are
on the device.  The resident font file is stated in the device determination
area of CAPADMIN.
There is are several difficulties that may be encountered with RAM fonts:
 
o   Because they are not permanent, they can accidently be removed.  If this
    happens, VA$DVILG has no way of verifying whether the information in the
    resident font file is no longer true.  In this case, QUIC uses the lowest
    numbered font (usually 14 pitch EDS) to represent fonts that aren't
    actually present on the device.
o   Because resident fonts take up space, special applications (such as non-
    CAP graphics) that use QUIC memory may fail.  If the special application
    clears font memory first, then the difficulty above becomes even worse.
o   If there is a line interrupt while fonts are being downloaded, the QUIC
    device is sometimes left in a state where it thinks that everything it
    sees is part of a font.  In this case it consumes data until you power it
    off or press the RESET button.  This removes fonts from RAM as well.
 
ROM fonts are therefore far more reliable; however, they tend to be expensive
and cannot be changed easily.
QUESTIONS_ON_RESIDENT_FONTS
The following two figures show sample status settings for the models 1200 and
800 QUIC printers:
QMS(R) INC. --- Lasergrafix (TM) 1200
Version = QUIC : 3.20 Firmware : 2.93   Date 3/13/89
 
(list of ROM fonts)
 
The default page orientation is Portrait
 
Default Fonts : (two default fonts...not significant for CAP)
 
Current Page Margins: Expressed as inches
    Top Margin  = 0.10       Bottom Margin = 11.00
    Left Margin = 0.35       Right Margin  = 8.50
 
Lines per inch = 6.12    Characters per inch = 10.71
 
Page Formatting Options:
   Paper tray  = Top             Stacker offset = No
   Page size   = 8.5 X 11        Copy count     =    1
 
Overlay Functions Defined:      Index     Size
          None encountered
 
Class 1 of 4    Interface Options:
 01  03  06  24
 
Class 2 of 4    EDP Setup Options:
 02  11
 
Class 3 of 4    Printer Simulation Options:
 02
 
Class 4 of 4
 (none)
Lasergrafix 1200 has 375 blocks of dynamic memory free
out of 396 blocks available.
 
QMS(R) INC. --- Lasergrafix (TM) 800-C
Version = QUIC : 3.20 Firmware : 1.44C   Date 3/13/89
 
(list of ROM fonts)
 
The default page orientation is Portrait
 
Default Fonts : (two default fonts...not significant for CAP)
 
Current Page Margins: Expressed as inches
    Top Margin  = 0.10       Bottom Margin = 11.00
    Left Margin = 0.35       Right Margin  = 8.50
 
Lines per inch = 6.12    Characters per inch = 10.71
 
Page Formatting Options:
   Paper tray  = Top             Stacker offset = No
   Page size   = 8.5 X 11        Copy count     =    1
 
Overlay Functions Defined:      Index     Size
          None encountered
 
Class 1 of 4    Interface Options:
 01  03  06  24  41  43  46  47
 
Class 2 of 4    EDP Setup Options:
 02  11
 
Class 3 of 4    Printer Simulation Options:
 02
 
Class 4 of 4
 (none)
 
Lasergrafix 800-C has 378 blocks of dynamic memory free
out of 401 blocks available.
A resident font is assumed to be inside QUIC memory.  There are two types of
resident fonts, ROM and RAM.
 
ROM fonts are stored on special chips that are inserted into the QUIC
motherboard.  ROM fonts are permanently available.  QUIC makes a set of ROM
fonts that are compatible with TeX. (See your font catalog for more
information.)  Installation of ROM fonts is usually done by a QMS
representative when the fonts are delivered.  It is not recommended that
customers install their own ROM fonts.
 
RAM fonts are downloaded into the QUIC device via a CP-6 COPY command.  RAM
fonts are not permanent and are deleted from QUIC memory whenever the device
is powered down or if a ^RESET control is sent to the device.  They can also
be removed by the ^DF control.  CP-6 TeX comes with a large number of fonts
that can be downloaded as RAM fonts.  However, a special procedure must be
followed to create a downloadable font file.  This procedure is described
later in this section.
 
Normally, the VA$DVILG program downloads the fonts that it needs to print a
given document.  It does this dynamically and efficiently, managing the
device's memory for optimum performance in trading off transmission time and
available memory on the device.
Resident fonts decrease the amount of font information that VA$DVILG needs to
download.  VA$DVILG can pull the font information that it needs to print the
document from the resident fonts.
The next step is to assign the device to a workstation.  Workstations
determine (among other things) the logical location of output devices on the
system.  By assigning the QUIC printer to a workstation, you can control
access to the device.
 
The following JCL creates a workstation and a device.
 
!SUPER
CR STATION CAP
CR DEVICE LZ01 FOR STATION CAP
PROFILE=QMS1200
USE=OUT
TYPE=LZ
FORM=STDQMS
PASS=SECRET
END
CR WSN CAP FOR STATION CAP
ACCESS = ?
DFORM LZ STDQMS
END
END
