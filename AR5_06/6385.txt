CAP supports a large selection of ASCII output devices.  These devices range
from CRTs to line printers.  They all require vertical format control (VFC)
characters.  Because these VFCs are handled similarly between ASCII devices, a
single file may be used on many different devices.
CP-6 CAP Administrator Guide - HA30-00
*************************************************************************
*
* Copyright (c) Bull HN Information Systems Inc., 1989, 1994
*
*************************************************************************
The CAP device definition for each ASCII device has a parameter that tells
VA$DVILP which file contains the correct device information.  This parameter
is not currently supported.
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
ASCII devices come in many different models and are offered by many different
vendors.  To accommodate any differences, CAP uses a concept called device
classes.  These device classes are described in detail later in this section.
\specials are commands that TeX finds in the input file that are passed
directly to the dvi file.  The following \specials are supported by DVILP:
continue, include, landscape, long, and 'literal'.
 
CONTINUE()
 
This special command disables positioning between the current special and the
next special command.
INCLUDE(fid,options)
 
This command allows graphics to be included with a TeX document.  The include
file must contain ASCII commands to dislpay a graphic.
 
With this facility, a user can mix text and graphics within a single TeX
document.  The syntax for this command (as TeX input) is
 
        \special include(fid,options)
 
The options are used to control the positioning of the graphic and to filter
commands.
 
The following options are available:
 
origin    places the absolute origin at the current position on the output
page.
 
zero    places both the absolute and relative positions at the upper left
corner of the page.
 
relative    places the relative position at the current position, but leaves
the absolute position at the upper left.
 
pixel    specifies that positioning commands are to be four-digit pixel
quantities, rather than five-digit fractions of an inch.
 
LANDSCAPE()
 
This command puts the printer in landscape mode.  The TeX values for \hsize
and \vsize should be redefined when using this command.
 
LONG()
 
This command puts the printer in portrait mode (8.5" x 11" paper).  This
command does not select the paper tray, which can be selected by using the
'literal' command.
 
'literal'
 
This command is used to pass an arbitrary command directly to the device.
Everything that appears within quotes is sent to the device exactly as is,
without any discrimination by DVILP.
When the DVILP program is run in NO DEBUG mode, only error messages are
displayed.  Some of the messages are informational only, while others indicate
a problem with the document.
 
If the message
 
Cannot open bit file or device output!
 
is printed, there is something wrong with the output_fid specified on the
DVILP command line.  The error message
 
Couldn't find ????:tfm
 
usually indicates that the search account list specified on the DVILP command
line does not include the account in which the font definitions for the
formatted document are found.
The first step to configuring a CP-6 system for a ASCII device is to create a
form which defines the type of paper to be used on the device.  CP-6 forms
were originally designed to support line devices.  Therefore, the default form
treats the ASCII device much like a line device.
 
The following figure shows JCL that creates the STDPRF form, which is the
default for all ASCII devices:
 
 REMOVE FORM STDPRF                      "     ???           STDPRF
 CREATE PSEUDO STDPRF FOR STDLP          "     ???           STDLP
 WID=110
 LEN=51
 LIMBO=0
 FIRSTLINE=0
 BANNER
 REPEAT=2
 EN=51,1,0,1,0,1,0,0
 %$
 EN=7,1,0,1,0,1,0,0
 %DATE
 EN=7,10,0,1,0,1,0,0
 %TIME
 EN=7,16,0,1,0,1,0,0
 %ACCN
 EN=7,25,0,1,0,1,0,0
 %UNAME
 EN=7,39,0,1,0,1,0,0
 %SYSID
 EN=7,45,0,1,0,1,0,0
 .
 EN=7,46,0,1,0,1,0,0
 %SUBFILE
 EN=7,54,0,1,0,1,0,0
 WOO=
 EN=7,58,0,1,0,1,0,0
 %WOO
 EN=7,68,0,1,0,1,0,0
 WOD=@
 EN=7,73,0,1,0,1,0,0
 %WOD
 EN=7,83,0,1,0,1,0,0
 CP VERSION
 EN=7,96,0,1,0,1,0,0
 %VERSION
 EN=7,101,0,1,0,1,0,0
 %SITENAME
 EN=10,8,1,2,1,1,0,0
 %UNAME
 EN=18,16,0,1,0,1,0,0
 %JOBNAME
 EN=21,16,1,1,1,1,0,0
 %SYSID
 
 END
VA$DVILP is a program that produces output for standard ASCII devices using
TeX output files (known as dvi files) as input.  This program permits the user
to specify a number of options and it implements a number of \special commands
as extensions.  (See the Device Specials subsection later in this section.)
Normally, the CAP menus generate the correct VA$DVILP commands for any given
situation.
Syntax:
!DVILP dvi_file ON out_file[,list_file(options)]
 
or
 
!DVILP dvi_file OVER out_file[,list_file(options)]
 
Note that the list_file and (options) parameters are optional.
Parameters:
 
dvi_file  is a dvi file produced by the TeX processor.
 
out_file  is a file suitable for sending to an ASCII device.
 
list_file  is a file containing errors and or debugging information.
 
options  are the options to be used to produce the out_file, as follows:
 
    COPIES, [NO] DEBUG, [NO] CHATTER, [FONT] LOG, FORM, HOFFSET,
    MAXIMUM PAGES, STARTING PAGE, [NO] PROMPT, RANGE,
    REVERSE, SRCH, and VOFFSET.
 
These options are described below.  They are presented alphabetically for
quick reference except that [NO] DEBUG and [NO] CHATTER appear together.  Note
that all options are case-insensitive.
 
CO/PIES = n
 
This option is used to request that DVILP make multiple copies of each page as
the device is printing them.  The n parameter must be the integer number of
pages to print.  The default is 1 copy of each page.
 
[N/O] DEB/UG
[N/O] CH/ATTER
 
DEBUG and CHATTER are identical.  This option is used to request that DVILP
print information about each phase of the printing process.  With this option,
output is displayed on the list_file (or the ME device if list_file is not
specified).  The default is NO DEBUG, which causes DVILP to produce error
messages only.
 
The debug output appears in two sections.  The first section includes the
names and numbers of each font used in the document.  In the second section,
DVILP generates the output for each page, printing the page number that has
just been output.
[FONT] LOG = fid
 
This option is used to specify a file for font usage information.  It is
recommended that a separate logging file be used for output to different
devices, since the main purpose of this information is to determine which
fonts are more widely used for each device.
 
FO/RM = 'name'
 
This option is used to request that DVILP create the output file as a CP-6
unit record file with the specified default output form.  This option is
particularily useful if output is being sent directly to the device or if the
default CP-6 form for the device is not suitable for the DVILP output.  The
default is for DVILP to create a consecutive file with no default form
information.
 
HOFF/SET = count
 
This option is used to change the default 1 inch horizontal margin that DVILP
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
 
In this case, DVILP starts printing the document at page 8 (STAP=8) and prints
5 pages (MAXP=5), which are pages 8, 9, 10, 11 and 12.
 
[N/O] PROM/PT
 
This option is used to request that DVILP prompt the user for all the options
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
[N/O] REV/ERSE
 
This option is used to request that DVILP produce the output, starting at the
first page through the last page (NO REVERSE) or starting at the last page
through the first page (REVERSE). The default depends on the DEVICE option.
The default is REVERSE since most ASCII devices produce the pages face up.
 
{SEARCH|SR/CH}(fid,fid,fid,...fid)
 
This option is used to search for input files.  All files (including tfm
files) other than those specified on the command line, and those without an
account specification, are searched for through the list of accounts specified
on the command line SRCH option.
 
The SRCH accounts are specified by providing a series of one to six CP-6 fids
within parentheses separated by commas.  The filename portion of each fid
specification should be empty.  Every search list is assumed to terminate with
the account specification
..,.:TEX.,.:LIBRARY. For example
 
(SRCH(.:TEXTEST,DP#LADC.HISACCT))
 
causes DVILP to search for files in the :TEXTEST account first.  If the file
does not exist there, DVILP searches for the file on the packset DP#LADC in
the HISACCT account.  If the file still cannot be found, DVILP searches in the
current file management account, the :TEX account, and :LIBRARY account.
 
STA/RTING [P/AGE] = n [.n [.n...]]
 
The starting page is specified with a sequence of 1 to 10 numbers or
asterisks, separated by periods.  For example, the specification
 
STARTING PAGE=1.*.-5
 
can be used to refer to a page produced by TeX when \count0=1 and \count2=-5.
An asterisk matches any number, so the * in 1.*.-5 means that the value of
\count1 is ignored when specifying the starting page.  If several pages match
the given specification, DVILP starts with the earliest such page in the dvi
file.  The default specification STARTING PAGE=* matches all pages and
therefore denotes the page at the beginning of the file.
 
VOFF/SET = count
 
This option is used to change the default 1 inch vertical margin that DVILP
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
00001
Finally, you must tell the CP-6 system about the physical connection or line
by which the ASCII device is attached to the system.  It is important that the
baud rate or SPEED match the baud rate set in the ASCII device.  In some
devices, the baud rate is set using dip switches inside the controller box.
In other devices, the baud rate can be set in the software.  The CP-6 LP@LOCAL
line configuration should be used.  See your device documentation for further
information.
If a site chooses to use an ASCII device for non-CAP purposes, nothing needs
to be changed.  CAP does no permanent setup on the device, thus allowing it to
be used at random by other applications.
ASCII devices usually require no options.
The next step is to assign the device to a workstation.  Workstations
determine (among other things) the logical location of output devices on the
system.  By assigning the ASCII device to a workstation, you can control
access to the device.  The standard CP-6 LP@LOCAL workstation should be used.
