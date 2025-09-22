CAP supports a large selection of HP LaserJet Plus, Series II and Series III
printers.
 
This section does not contain reference information about HP device protocol,
which is found in the user documentation for the HP laserprinters.
CP-6 CAP Administrator Guide - HA30-00
*************************************************************************
*
* Copyright (c) Bull HN Information Systems Inc., 1989, 1994
*
*************************************************************************
The CAP device definition for each device has a parameter that tells VA$DVIHP
which file contains the resident font information.  The default is
 
  VA_QMS_RES_FONTS.:LIBRARY
 
which assumes no resident fonts.  This parameter must be changed in the device
definition to point at the new resident font file.
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
 
***************************************
The VA$DVIHP currently does not use resident fonts, even though CAP needs a
resident font file containing the memory amount available in the printer for
dynamically downloading fonts.  The first line must be a comment, which starts
with a percent sign (%) or the identifier MEMORY. Comments are for
documentation purposes only.  The number after identifier MEMORY is the
virtual memory available on the device for downloading fonts only, NOT
graphics.  Some memory should be reserved for graphics, so the number
following the word MEMORY should be less than the total amount of memory in
the device.  The HP printers should have a minimum of 512k of memory, but to
be safe 2M would be better.
 
    MEMORY 250
\specials are commands that TeX finds in the input file that are passed
directly to the dvi file.  The following \specials are supported by DVIHP:
landscape, long, and 'literal'.
 
LANDSCAPE()
 
This command puts the HP printer in landscape mode.  The TeX values for \hsize
and \vsize should be redefined when using this command.
 
LONG()
 
This command puts the HP printer in portrait mode (8.5" x 11" paper).  This
command does not select the paper tray, which can be selected by using the
'literal' command.
 
'literal'
 
This command is used to pass an arbitrary HP command directly to the printer.
Everything that appears within quotes is sent to the printer exactly as is,
without any discrimination by DVIHP.
When the DVIHP program is run in NO DEBUG mode, only error messages are
displayed.  Some of the messages are informational only, while others indicate
a problem with the document.
 
The most typical messages are
 
Couldn't find ????pk
Couldn't find ????pxl
 
which indicate that one of the fonts that has been requested does not exist at
the requested magnification (\magstep).  In this case, the document must be
reformatted by TeX with a different font specified.  Alternatively, these
messages indicate that the search account list specified on the DVIHP command
line does not specify the account in which the font definitions for the
formatted document can be found.
 
If the message
 
Cannot open bit file or printer output!
 
is printed, there is something wrong with the output_fid specified on the
DVIHP command line.
 
The error message
 
Couldn't find ????:tfm
 
usually indicates that the search account list specified on the DVIHP command
line does not include the account in which the font definitions for the
formatted document are found.
The first step to configuring a CP-6 system for a HP device is to create a
form which defines the type of paper to be used on the device.  CP-6 forms
were originally designed to support lineprinters.  Therefore, the default form
treats the HP device much like a lineprinter.
 
The following figure shows JCL that creates the HPFORM form, which is the
default for all HP devices:
 
!"*M* This is the SYNCCAP job. "
REM PRO HPLJET2
M PRO HPLJET2 FROM XRX7015
SETUP_CHR=NUL,NUL,NUL,NUL,NUL,NUL,NUL,NUL,NUL,NUL,NUL,NUL,
NUL,NUL,NUL,NUL,NUL,NUL,NUL,NUL,NUL,NUL,NUL,NUL,ESC,
'E',ESC,'&l2E',ESC,'&a0R',ESC,'&l7.45c66F'
FRMFED_CHR=X'0C',X'0D';DVCFLWCTRALG=DC1DC3
CHARSETNAME=ASC95; LOWERCASEPRINTS=YES; DVCFLW=DC1DC3; FF_FLUSH = YES
END
REM FORM HPFORM
CR FORM HPFORM
CHARSET=PSJCHR
WIDTH=85
LIMBO=88
LENGTH=66
FIRSTLINE=0
LPI=6
SETUP
***************************************
Special HP LASERJET II form; 6lpi, 66 lines
***************************************
 
BANNER
REPEAT=1
EN=1,1,0,1,0,1,0,0
 E &l2E &a0R &l7.45c66F
EN=2,1,0,1,0,1,0,0
 
EN=3,1,0,1,0,1,0,0
 
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
Although the driver tries to avoid out-of-memory problems by downloading only
as many fonts as will fit into the memory specified in the resident font file,
it can still easily run out of memory if it only has 512k.  The driver doesn't
check whether any graphics will cause the memory in the printer to overflow,
and will truncate any such graphics.  As an aside, this driver, like the QMS
and PostScript drivers, downloads only the characters actually used in a font,
so there's no unnecessary space used up in the printer.  The recommended
memory size for an HP printer to not run out of memory is 2Mb.
 
Two things the driver makes no attempt to handle:  a) HP has a limit of 32
fonts total downloaded for a document, b) and no more than 16 fonts can be
used on any one page, even though font numbers can range up to 256.  The
driver will not print anything for fonts that exceed these limits.
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
by which the HP printer is attached to the system.  It is important that the
baud rate or SPEED (as it is stated in the JCL below) match the baud rate set
in the HP printer.
 
The following JCL configures line .4700 on communications processor number 1
for a HP LaserJet series II printer:
 
!NETCON
SEL N=1
CONFIG  ``*1-*'' .4700
SPEED=19200,LOGON='LJ01,,SECRET',SAL=NO,LOGONTIMEOUT=0,;
    READTIMEOUT=0,PROFILE='HPFORM',FLOWC=YES,HARD=YES,;
    REENABLE=YES, ``LASERJET''
KILL .4700
ENAB .4700
END
HP printers come in many different models and are offered by many different
vendors.  To accommodate any differences, CAP uses a concept called device
classes.  These device classes are described in detail later in this section.
If a site chooses to use a HP device for non-CAP purposes, nothing needs to be
changed.  CAP does no permanent setup on the device, thus allowing it to be
used at random by other applications.  However, CAP does expect the HP device
to be free of any resident files, which can be left over by other
applications.
HP printers must have the RS232 asynchronous communications daughter board
option to be connected to the CP-6 system.  No other options are required or
supported.
The next step is to assign the device to a workstation.  Workstations
determine (among other things) the logical location of output devices on the
system.  By assigning the HP printer to a workstation, you can control access
to the device.
 
REM DEVICE HPLJET01
CR DEVICE HPLJET01 FOR STATION CAP
PASS=BYTEME
USE=OUT
FORM=HPFORM
PROFILE=HPLJET2
TYPE=LJ
UPLOCKED=NO
END
