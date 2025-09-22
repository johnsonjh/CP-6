The Administrative Document Structuring Language (ADSL) is a
declarative administrative language that defines the structures and
page formatting parameters selected by Document Structuring Language
(DSL) controls in a document source file. CapTeX, a set of TeX macros,
associates the ADSL structures and formatting parameters
selected by the DSL controls with a specific document style.
 
ADSL structures can include DSL controls as well as TeX control
sequences; some familiarity with the TeX formatter is desirable
when modifying or building styles with ADSL.
 
For a list of the topics in the ADSL HELP facility, enter:
 
  HELP (ADSL) TOPICS
 
Please note that HELP topics or subtopics that are ADSL controls must
entered without the beginning \  character.
 
NOTE:  Because of the limitations of ASCII output devices, examples of
math mode, fonts, tables, and special characters are not truly
represented.  However, those examples that may still be of interest
appear in this HELP facility for the information they provide.
Please refer to the CAP ADSL Reference Manual (HA28) for definitive
information.
 
This section presents an overview of the CAP administrator's role and
CAP formatting concepts, followed by a description of Administrative
Document Structuring Language (ADSL) control files, structures, and
control syntax.
CAP ADSL Reference - HA28-00
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
 The boxing facility permits a box to be drawn around an insert, not including
the caption.  Boxing depends on \boxthickness to determine the thickness of
the rules, and on \boxframe to determine any extra space (both vertical and
horizontal) used as a margin around the insert.  The box fits within the
height and width specified for the insert; consequently the actual insert may
be slightly smaller,  by 2 X (\boxthickness + \boxframe) .
 
All the boxing controls can be specified both globally, to provide a default
value for all inserts, or locally, within an insert style definition, to apply
only to that style.  The controls are as follows:
\boxing
 
Specifies that, by default, figures, graphics, and tables will have a box
drawn around their perimeter.
\no_boxing
 
Specifies that, by default, figures, graphics, and tables will not have a box
drawn around their perimeter.
\boxthickness=dimen
 
Is a dimension that specifies the thickness of the rule around figures,
graphics, and tables.  The default is 0.4 pt.
\boxframe=dimen
 
Is a dimension used to separate the box from its contents.  The final box will
be reduced in size by  2 X (\boxthickness + \boxframe) in each direction to
accommodate the rules and the frame.  The default is 3 pt.
00004
00001
00003
00002
Captions for inserts are defined much like chapter titles or level heads.
The caption definition controls are local to each insert style.  The controls
are:
\caption={code}
 
Defines code to produce the caption text for inserts (tables, figures, and
graphics) and equations.
\next_caption={code}
 
Defines code to produce a second caption text for tables and figures that are
broken across several pages.  It permits different captions to be used for the
first and last segments.
\caption_space={cdimen}
Determines how much space separates the caption from its insert.  If there is
no caption, that is, when \caption={}, this control is ignored.
00001
00003
00002
Captions can be placed either above or below the insert.  In either case,
spacing between the caption and the insert is determined by \caption_space.
The caption placement controls can appear globally, as defaults for all insert
styles that do not specify otherwise, or locally, within each insert style.
The controls are:
\at_top
 
Specifies that any captions will be positioned above their insert.
\at_bottom
 
Specifies that any captions will be positioned under their insert.  This is
the default.
00002
00001
 Each table or figure definition can provide two captions:  \caption and
\next_caption.  Either or both may be empty.  Graphic styles only permit a
single caption, \caption, since graphics cannot be broken across pages.  The
following controls determine which of these captions is selected.  These
controls can appear globally, as defaults for all insert styles that do not
specify otherwise, or locally, within each insert style.
\first_only
Specifies the use of \caption for the first chunk, and \next_caption for all
the other chunks.
\last_only
 
Specifies the use of \caption for all chunks except the last, and
\next_caption for the last chunk.
 
The following table summarizes how this selection takes place:
 
            Selection    First Chunk  Other Chunks   Last Chunk
           --------------------------------------------------------
            \first_only  \caption     \next_caption  \next_caption
 
            \last_only   \caption     \caption       \next_caption
00001
00002
To produce a printed document, the CAP user must specify both a format
and a device that have been defined by the administrator. CAP then
processes the user-created document source files together with
administrator-created style control files, related to the specified
format, using the TeX formatter to produce files for output on
the specified device.
 
These concepts are described in more detail in the following
paragraphs.
Most controls used within chapter styles (including level heads), except those
that are directly related to the chapter title, can be used in the style file
outside of the scope of chapter styles.  In that case, they define the
parameters for those parts of the document that occur before any chapters are
called out, or for document styles that do not use chapter constructs at all,
like letters, reports, etc.
 
Level heads declared within the scope of a particular chapter style become a
part of that chapter style, and local to it.  In this way, you can specify
different kinds of level heads for different kinds of chapter styles.    The
ADSL HELP topic LEVEL_HEADS describes level heads in greater detail.
 
\chapter_default={SECTION}
 
\beginchapters
   \header={\vbox{\HB{||\BF\chtitle}\SPB{.05}\hrule}}
   \odd_header={\vbox{\HB{||\BF\chtitle}\SPB{.05}\hrule}}
   \even_header={\vbox{\HB{\BF\chtitle||}\SPB{.05}\hrule}}
   \footer={\vbox{\hrule\SPB{.05}\NO\HB{\IDENTIFIER||\page}}}
   \odd_footer={\vbox{\hrule\SPB{.05}\NO\HB{\IDENTIFIER||\page}}}
   \even_footer={\vbox{\hrule\SPB{.05}\NO\HB{\page||\IDENTIFIER}}}
   \first_footer={\vbox{\hrule\SPB{.05}\NO\HB{\IDENTIFIER||\page}}}
   \startup={\if@twosided\BRO\else\BRP\fi}
   \page={\number\pageno}
   \chapter_numbering
   \chnum={\number\chapno}
   \intro={}
   \title={\ALR\intro\SPB{2}\CHAP{\BF \chtitle}\SPB{3}\ALB}
   \setup={\INB{0}\ALB\parskip=\defparskip\relax}
   \indexing
   \ixstyle={}
   \contents={}
 
\newchapter{SECTION}
   \synonym={SE}
   \contents={\SPB{1}\BF \intro.\ \chtitle\dotfill\ \page}
   \intro={Section \chnum}
   \page={\chnum--\number\chappage}
   \title={\ALR\SPB{2}\CHAP\BF\intro\SPB{2}\chtitle\SPB{3}\ALB}
 
\endchapters
 
The preceding figure shows a sample set of chapter definitions.
\chapter_default is a global control, and thus appears before \beginchapters,
because \chapter_default applies to the entire document, not just a particular
chapter or set of chapters.  The \beginchapters control starts a new set of
chapter definitions and is followed by the controls common to all chapter
styles in that set.  The \newchapter{SECTION} control starts the definition of
the SECTION chapter style, followed by the controls specific to that style.
 
Level heads specific to this chapter style could be defined here if required;
otherwise, level heads can be defined outside of the chapter styles so that
they can apply to any (or no) chapter styles.
The \endchapters control ends this set of chapter definitions.  Note that any
number of additional chapter styles could be defined following the
\newchapter{SECTION} definition here.
 
The following global controls are used to define chapter styles:
\chapter_default={name}
 
Defines the default chapter style that will be used whenever no explicit
chapter style is indicated on the \CH control.  It is also used when a style
name is specified, but that style does not exist.  There is always a DEFAULT
chapter style that will be used if all else fails.
\beginchapters
 
Begins a new set of chapter definitions.  All chapter parameters are reset to
their default values.  Chapter controls following \beginchapters but preceding
the first \newchapter will be used as defaults for all the chapter styles in
this set.
\newchapter{name} Begins a new chapter style definition.  The final layout of
the pages in any chapter is determined by the controls specified for this
particular chapter, then the defaults for this set of chapters, and finally
any document defaults that may apply.
\endchapters
 
Ends this set of chapter styles.
 
Within each chapter style, the following local controls are used to specify
the various items needed to produce the page layout and chapter titles, and to
handle the table of contents entries:
Headers and Footers
 
Controls used to define headers are \header, \odd_header, \even_header, and
\first_header.  Controls for footers are \footer, \odd_footer, \even_footer,
and \first_footer.    Headers and footers defined within a certain chapter
style are local to that chapter style.
Level Heads
 
Level heads can be created within chapters using the \beginlevels, \newlevel,
and \endlevels controls.  Level heads are described on page , in  the topic
LEVEL_HEADS. Level heads defined within a chapter style are local to that
chapter style.
Initialization
 
Chapter styles use the common \startup and \setup controls.  \startup is
executed very early in the chapter style, and can be used to break the page
before the new chapter.  Common controls for structures are described under
COMMON_CONTROLS.
Title
 
The chapter title is generated using the common \intro and \title controls,
and the same information is entered into the table of contents via the
\contents control.  Common controls for structures are described under
COMMON_CONTROLS.
\section_numbering
 
Turns on section numbering within a chapter.  Section numbers will be produced
by the \sectionno control when level heads are encountered.  However, if the
DSL \Ln control uses an asterisk (*) instead of a specification number, no
section number will be produced.  This is the default.
\no_section_numbering
 
Turns off section numbering within a chapter.  In this case, section numbers
will not be produced by the \sectionno control.
\chapter_numbering If section (specification) numbers are being produced in a
chapter, this control causes chapter numbers to be included as the first
number in the complete section number.  (This is the default.)  For example,
in Chapter 1, Section 2, the \sectionno control would produce "1.2".  However,
if the DSL \CH control uses an asterisk (*) instead of a specification number,
no chapter number will be used.
\no_chapter_numbering
 
If section (specification) numbers are being produced in a chapter, this
control does not include chapter numbers in the complete section number
produced for level heads.
\indexing
 
Enables indexing within a chapter.  This is the default.
\no_indexing
 
Disables indexing within a chapter.  In this case, all \IX controls are
ignored.
\ixstyle={name}
 
Defines the default index style used within a chapter for any index entries
for which no style is specified.
\page={code}
 
Prints the current page number.  It is usually redefined within chapter styles
to provide chapter-specific page numbers.
\chnum={code}
 
Specifies code used to format the chapter number for a chapter style.  For
example, \chum={\number\chapno} would generate a numeric chapter number, like
"1", or \chnum={\LETTER\chapno} would make an upper-case letter of the chapter
number.  This control sequence can be used within other controls, like \intro
or \contents, to materialize a formatted chapter number.
00002
00001
00011
00017
00004
00005
00013
00007
00015
00006
00003
00012
00014
00010
00016
00009
00008
Column specifications for each table are defined in the \template control.  A
template can contain only the following controls:
\TV
 
Produces a vertical rule equal to the height of the current row.
\SPH{cdimen}
 
Produces horizontal space.  If this control is used adjacent to a \TV control,
it will replace the default \rulesep or \doublesep.
\TI{size|format}
 
Specifies the size and format of a cell.  The name \entry must be used to
represent the cell data to be formatted (see examples below).  The size
parameter must be either a cdimen, where the default unit of measure is a
percentage of page width, or an asterisk (*), which defines a column that is
auto-width (for small tables) or one  n-th of the remaining page width, where
n is the number of columns specified on the DSL \TB control.
\TC
 
Indicates the end of a column in the template.
\TE
 
Indicates the end of the row in the template.  This control is optional and
can only be used at the end of the template.
 
A template contains a sequence of the above instructions, using \TC to delimit
each column.  The table will nominally have as many columns as the template
defines.  However, writers can specify fewer columns, and only those columns
actually specified will be used.  Templates can also be used to specify
repeating column specifications; using \TC\TC indicates a point at which the
template will repeat until the number of columns the writer specifies is
exhausted.  For example, a template of:
 
\TV\TI{1.5in|\entry}\TV \TC\TC \TI{1in|\entry}\TV\TE
 
has the second column (starting at \TI{1in|...)  repeating as many times as is
necessary.  This template defines a table of two or more columns, with all the
columns except one formatted by the template for column two.
 
The \TI control determines both the size and format of a cell.  It is the size
parameter of this control that selects the type of column.  If size contains a
specific dimension, the column will be fixed-width, and the contents of each
cell will be formatted as one or more paragraphs.  When size is set to an
asterisk (*), the results depend on the table type.
 
If the table type is \large_table, all columns with an asterisk (*) share the
available space.  These columns are still fixed-width, and behave like other
fixed-width columns, but the width is determined as a portion of the empty
space.
 
If the table type is \small_table, the column is auto-width.  Auto-width
columns put the cell into a single line, as opposed to fixed-width columns,
which build a paragraph.  The width of any column is decided by the greatest
width of any one cell in that column.
 
Both large and small tables have variable numbers (not widths) of columns and
repetitions in the template.  In small tables, the administrator can mix
fixed-width and auto-width columns as much as desired.
 
The width of the entire table is determined by the sum of the widths of its
columns, plus any boxing (space and rules) that may be used.
 
The following is an example of a template for a table that has vertical rules
on the outer edges and between the columns:
 
\template={\TV \TI{*|\entry} \TV \TC \TC \TI{*|\entry} \TV \TE}
 
Notice the double \TC above.  This tells CapTeX to repeat from this point when
it runs out of template.  Since a \TE can be used by the writer to terminate
the table early, this definition will make a table that can have from one to n
columns, all auto-width.
A table header defines the heading that will be repeated at the top of each
chunk of table.  It can contain one or more rows, as well as extra spacing to
open up the heading.  The table header is only used if \tbheading, which
contains the argument of the \TH control, is not empty.  The following is an
example of a header:
 
\header={\TS{3pt}\tbheading\TS{2pt}}
 
The contents of each cell is local to that cell; font, alignment, or other
changes disappear when the next cell starts.
 
The cells in a row are aligned along the baselines of their top line, rather
than the bottom.
 
\table_default={SIMPLE}
 
\begintables
   \space_before={2}
   \space_after={1}
   \startup={\ALC\relax}
   \tbnum={\ifx\chnum\empty\else\chnum--\fi\number\tableno}
   \intro={Table \tbnum.}
   \caption={\ALC\SL \intro\ \ \tbtitle}
   \next_caption={\ALC\SL\intro\ \ \tbtitle\ \ (part \number\chunkno)}
   \no_boxing
   \rulesep={1.4}
   \doublesep={.7}
   \header={\TS{3pt}\tbheading\TS{4pt}}
   \setup={\NO\relax}
   \aboverow={2pt}
   \belowrow={1pt}
   \contents={\intro\ \ \tbtitle\ \dotfill\ \page}
   \horizontalrules
 
\newtable{SIMPLE}
   \header={\tbheading}
   \template={\TC\TI{*|\relax\entry\relax}}
   \boxing
   \no_horizontalrules
 
\newtable{2COL}
   \large_table
   \rulesep={2}
   \template={\TV\TI{45|\ALL\relax\entry}\TV\TC
              \TI{45|\ALL\relax\entry}\TV\TE}
 
\endtables
 
The preceding table shows a sample set of table definitions.  Note that the
\begintables control in this example starts a new set of table definitions and
is followed by the controls common to the table styles in that set.  The
\newtable{SIMPLE} and \newtable{2COL} controls start the definition of the
SIMPLE and 2COL styles, respectively, followed by the controls specific to
those styles.  Any number of additional table styles could be defined here.
The \endtables control ends this set of table definitions.
00002
00004
00005
00003
00001
As mentioned above, the CAP administrator provides style control files
that contain ADSL controls to define the specific structures available
to the CAP user. Four control files are supplied with the CAP system:
Document style (VA:STYLE)      usually contains specific style
    information about a document type. This includes page layout,
    chapter styles, and level heads.
Common style (VA:COMMON)      usually contains information
    about structures that may be common to the user site, or to many
    document styles. This includes tables and figure styles, paragraph
    lists, indexing, footnote styles, and similar elements.
Font file (VA:FONTS)      contains information about fonts
    to be used. Fonts are usually defined in separate files, since
    CAP automatically associates DEVICES (as defined by
    CAPADMIN) to font files.
Error message file (VA:ERROR)      contains the error messages
    used by CapTeX. Error messages are usually kept in a file of
    their own. All the error messages used by CapTeX are already
    built in, so there is no need to provide another error message
    file, unless it is to add new error messages, or translate or
    change existing ones.
 
For more information, type ? . In the system-supplied CAP style control files,
page layout and specific
chapter and level head styles are defined in the VA:STYLE file.
Other structures that may be common to several styles are defined in
the VA:COMMON file. These files can also be further subdivided
using the DSL \IS (include source file) control to include other files.
 
Regular TeX fonts are defined in the VA:FONTS file, while
other sets of fonts appear in other control files. Fonts can be
output-device dependent, and are associated with a specific device using
CAPADMIN device definitions. For example, fonts for use with line printer
oriented output are called VA:FONTS:ASCII.
 
Note that the only requirement for the contents of control files is
that the regular TeX fonts be defined in a separate file. Otherwise,
the contents of control files is totally free-form. ADSL (and TeX)
controls defining structures can be entered in any order, and
structural definitions can be included in a single control file or
in several different ones. As in the system-supplied style control
files, structures specific to a particular document style can be
defined in individual control files for each style, while structures
common to several styles can be defined in a single control file. It
is up to the administrator to determine what is "common" and what
is "style".
 
To effectively create and maintain control files, it is advantageous
to keep like structure definitions together, and to identify and
clarify those definitions with comments in the control files.
For more information on style control files, enter
 
  HELP (ADSL) STYLE_FILES
00002
00001
00004
00003
ADSL control files are basically free-form; there can be multiple
lines per control and multiple controls per line. Names cannot be
abbreviated and are case-sensitive. (Most ADSL control names are
lower case.) As mentioned above, any controls whose name contains
the at sign (@) or underscore (_) character can only be
used in the control files. Otherwise, most ADSL controls can be used
in document source files as well as in the administrative files. In
general, ADSL controls always follow TeX syntax rules, unless some
specific deviation is noted.
 
ADSL controls use three basic forms of syntax:
\control={value}
 
The equals sign (=) and the braces ({}) are required.
value can be any one of code, cdimen, or name,
as shown below. value will not be expanded until \control
is expanded.
 
      name    type              value
      -------------------------------------------------------------------
      code    code segment      ADSL, DSL, and TeX code
 
      cdimen  CapTeX dimension  a dimension either with or without units
 
      name    CapTeX name       the name of a style or other object
\registername=value
 
The equals sign (=) is optional; there are no braces. These are
TeX registers, which can be counters, dimensions, or skip
registers, each with a different syntax for value, as shown below.
In this case, value is expanded immediately.
 
       name   register type  value
       -----------------------------------------------------------------
       num    count          a number, like 2
 
       dimen  dimension      a dimension, like 12pt
 
       skip   skip register  a skip value, like 12pt plus 3pt minus 2pt
\function and \no_function
 
These are on/off switches and have no parameters. Each state of the
switch has its own control; for example, \boxing and
\no_boxing.
00001
00003
00002
The counters described below are used throughout ADSL inside various
structural definitions:
\pageno
 
Contains the current sequential page number.  The page number can be negative;
if so, this counter is decremented when the page is output.
\chapno
 
Contains the current chapter number.
\chappage
 
Contains the current page number within the current chapter.
\equationno
 
Contains the current equation number.  This is the default counter.
\sectionno
 
Is a macro that automatically produces all the section numbers currently in
use, based on the current section level.  \sectionno uses the \level_separator
and \level_end macros to do this.
\cur@level
 
Defines the current level (that is, the last level specified by a DSL \Ln
control).  This counter must not be modified, but is available for reading.
\footno
 
Contains the current footnote number.  This is the default counter.
\figureno
 
Contains the current figure number.  This is the default counter.
\graphno
 
Contains the current graphic number.  This is the default counter.
\tableno
 
Contains the current table number.  This is the default counter.
\curpllevel
 
Contains the current paragraph list level (within a paragraph list only).
\curitem
 
Contains the current item number (within a paragraph list only).
\chunkno
 
Is for table, figure, and graphic segments (chunks) to allow part numbers, for
example, Table 1.  Table Name (part 2), to appear in the captions for these
structures when they extend over more than one page.
00002
00003
00013
00006
00012
00011
00004
00008
00007
00009
00001
00005
00010
The controls described below are macros for use with counters.  These controls
are used throughout ADSL inside various structural definitions.  They always
change the counters globally.
\newcount\counter
 
Creates a new count register.
\inc\counter
 
Globally increments a counter.
\dec\counter
 
Globally decrements a counter.
\setcounter\counter={num}
 
Globally sets a counter.
\getcounter\counter \macro
Defines \macro to contain the contents of \counter.  \counter must be a
counter; \macro is a macro.
\addtocounter\counter{num}
 
Adds a quantity to \counter.
\resetcounter\counter
 
Resets a counter to zero.
\@multiply\counter by{num}
 
Is used to multiply skip quantities correctly.  It also multiplies counters
properly when real numbers are used.  The multiplier is rounded down to two
decimal digits before use.
\numbering\counter=\type
 
Defines how numbering (for those structures that use it) is to be reset.  By
default, numbers are set to zero at the beginning and then incremented (or
set) throughout the document.  The possible values for \type are \running,
which is the default, \by_chapter, which resets the counter at each chapter,
and \by_style, which resets the counter at every chapter style change.
\number\counter
 
Produces a string containing Arabic numerals.  \the\pageno can also be used,
with counters.
\letter\counter
 
Produces an alphabetic character from a counter whose value must be less than
27.
 
\LETTER\counter
 
Same as above, but produces an upper-case letter.
\romn\counter
 
Produces a Roman numeral from a counter.
 
\ROMN\counter
 
Same as above, but produces an upper-case Roman numeral.
\raisednumber\counter
 
Produces a raised number, like a footnote, from a counter.
\raisedsign{code}
 
Same as above, but the argument is a character or string.
00008
00006
00003
00005
00002
00011
00001
00010
00009
00013
00014
00007
00012
00004
Messages are created with one of the following controls:
\write_error num \name {text}
 
Creates a CapTeX error message.
\write_warning num \name {text}
 
Creates a CapTeX warning message.
\write_message num \name {text}
 
Creates a CapTeX message.
 
Note that each of these controls has the same three syntax parameters:
num      is the number of parameters the error message uses.
name      is the name of the error message.
text      is the text of the error message.  The text may contain only those
CapTeX or TeX controls that can be expanded to simple characters, since the
messages are directed to the screen or log file.  The text may refer to the
parameters using standard TeX syntax, the #n notation.
 
This syntax is illustrated in the following examples:
 
\write_error 1 \err@nostyle {%
      The #1 style does not exist! Using the default style.}
 
\write_error 0 \err@notdraftmode {%
      It's too late to turn on draft mode.}
 
\write_error 2 \err@badgrouping {%
      You can't close #2 here, it should be #1.}
 
\write_warning 1 \wrn@RFnolabel {%
      Reference "#1" is undefined.}
 
\write_message 1 \mss@passcnt {%
      ..Starting pass \the#1.}
 
\write_message 0 \mss@changed {%
      Some pages or references have changed.}
 
In the first example above, there is an error message requiring one parameter
(so #1 should be somewhere in the message text), called \err@nostyle.  The
last parameter, enclosed in braces, is the text to be displayed as a result of
this error message, and refers to #1.  In this message, #1 will be replaced by
the parameter supplied when \err@nostyle is called, which will be the name of
the style that cannot be found.
 
Note the conventions used within CapTeX to name error messages.  All errors
have a prefix of \err@, warnings a prefix of \wrn@, and messages a prefix of
\mss@.  These prefixes are not required when creating additional messages, but
such conventions are useful to avoid naming conflicts among control sequences.
00005
00004
00006
00001
00003
00002
PAGE_SIZE
The dimensions described below are used throughout the entire CapTeX system;
they include skip registers and penalties.  The dimensions should be set when
formats are initially defined and not modified thereafter, so that the
document maintains a consistent appearance.  If they are modified, it should
be done carefully, since the results may be unexpected.  Those dimensions that
depend on font information should only be set after defining a font.    Many
of these quantities are real TeX quantities, and the defaults have usually
been left as they were set by plain TeX.
 
The dimensions are as follows:
\ACH
 
Is the current line height, which is a fixed dimension.
\ALS
Is a skip quantity equal to the current line height, with 33% stretch and
shrink.
\ACS
 
Is a skip quantity equivalent to the current font's definition for an
interword space.  It comes from \fontdimen2, \fontdimen3, and \fontdimen4.
\fontdimen quantities are described in The TeXbook.
\ACW
 
Is a dimension equivalent to \ACS, but without stretch and shrink.  It is
defined as \fontdimen2 plus .5\fontdimen3; that is, the natural size plus half
the stretch amount.  \fontdimen quantities are described in The TeXbook.
\ACI
 
Is the extra interword space to be added after sentences, for the current
font.
\quad
 
Is a TeX macro defining a medium-sized horizontal space; approximately the
same as \space\space.
\abovedisplayskip
 
Is a TeX skip quantity used above equations or display math.
\belowdisplayskip
 
Is a TeX skip quantity used below equations or display math.
\abovedisplayshortskip
 
Is a TeX skip quantity used above equations or display math, if the last line
of the paragraph above is short enough to not overlap the equation.
\belowdisplayshortskip
 
Is a TeX skip quantity used below equations or display math, if the last line
of the paragraph below is short enough to not overlap the equation.
\voffset
Is a dimension specifying a vertical offset.  The default of 0 pt reflects a
point 1 inch from the top of the page.  \voffset is automatically set by
CapTeX based on the page and device dimensions set.  This dimension should not
be changed.
\hoffset
 
Is the horizontal analog of \voffset.  The default of 0 pt reflects a 1 inch
margin.  \hoffset is automatically set by CapTeX based on the page and device
dimensions set.  This dimension should not be changed.
\vsize
 
Is a dimension that defines the size of the text on the page, including
figures and footnotes, but not including headers and footers.  The default is
8.9 in.  \vsize is automatically set by CapTeX based on the page and device
dimensions set.  This dimension should not be changed.
\hsize
 
Is the horizontal dimension of the page.  This includes the text, headers, and
footers, but does not include marginal notes.  The default is 6.5 in.  \hsize
is automatically set by CapTeX based on the page and device dimensions set.
This dimension should not be changed.
\displaywidowpenalty=num
 
Is the penalty for a widow line before a displayed equation.
\predisplaypenalty=num
 
Is the penalty inserted before a displayed equation.
\postdisplaypenalty=num
 
Is the penalty inserted after a displayed equation.
00009
00007
00001
00005
00003
00004
00002
00010
00008
00015
00012
00014
00017
00016
00006
00011
00013
Documents originate with source files written by CAP users; these
files contain DSL controls in addition to the text of the document.
DSL controls specify structural elements of the document, such as
chapters, level headings, paragraph lists, tables, and figures. DSL controls
do not specify the typographic details of the structures,
so that the user can concentrate on writing the text rather than on
the nuances of formatting.
CapTeX equation styles provide a simple mechanism to print and label displayed
equations.  These are very much like TeX displayed equations, but use equation
styles to select spacing and label positioning.  Refer to Chapter 19,
Displayed Equations, of The TeXbook for further information about displayed
equations.
 
Global controls used with equations are:
\equation_default={name}
 
Specifies the default equation style to be used if no other style is specified
with the DSL \EQ control.
\equation_numbering
 
Turns on equation numbering.  This is the default.  Equation numbering depends
on the equation style.
\no_equation_numbering
 
Turns off equation numbering.
\beginequations
 
Begins a new set of equation style definitions.  This can be followed by
default values for equation style controls.
\newequation{name}
 
Creates a new equation style.
\endequations
 
Ends equation style definitions.
 
Equation numbers are different from other captions in that they are often
positioned to one side of the equation, rather than above or below.  TeX
centers the displayed equation horizontally on the page and then aligns the
equation number vertically with the center of the equation.  CAP provides no
direct support for displayed equations, other than giving the writer access to
the full functionality of TeX for displayed math mode.
 
Equation numbers are normally reset at the beginning of each chapter, and are
incremented by one for each numbered equation.  The  \numbering control can be
used to alter this behavior.  Equations for which the writer has specified an
asterisk (*) as the number will neither print the equation number nor
increment it.
 
The following are the local controls for equation styles:
\eqnum={code}
 
Specifies code used to provide the printed equation number for the style.  If
the DSL \EQ control specifies an asterisk (*) for the equation number, \eqnum
will be empty.
\caption={code}
 
Specifies code that controls the format (placement, font style, etc.)  of the
equation number defined by \eqnum.  This control requires the use of the TeX
controls \eqno or \leqno to position the equation number.
 
\equation_default={DEFAULT}
 
\beginequations
   \eqnum={\number\equationno}
 
\newequation{DEFAULT}
   \caption={\eqno(\eqnum)}
 
\newequation{LEFT}
   \caption={\leqno(\eqnum)}
 
\endequations
 
The preceding figure shows a sample set of equation definitions.  Note that
the \beginequations control in this example starts a new set of equation
definitions and is followed by the control common to each equation style.  The
controls \newequation{DEFAULT} and \newequation{LEFT} start the definitions of
the DEFAULT and LEFT styles, respectively, followed by the controls specific
to those styles.  Any number of additional equation styles could be defined
here.  The \endequations control ends this set of equation definitions.
00004
00008
00006
00007
00001
00002
00005
00003
CapTeX error messages are provided in the VA:ERROR file.  The messages in this
file are already built into CapTeX, so there is no need to reload them.
However, administrators may want to add messages of their own or modify the
existing messages in some way, for example, by translating them to another
language.
 
Error messages come in three types:
Errors      Error messages (from the TeX \errmessage control) are issued with
the offending line(s) and a TeX trace display.  If an error occurs, CAP will
halt the formatting process after the current pass.
Warnings      Warnings are issued without printing any trace information or
the offending line(s).  CAP will not halt if only warnings are encountered.
Messages      Messages provide information to the user and have no other
consequences.
00001
00003
00002
Figures are insert structures containing text, but are not part of the normal
flow of text.  They can be used to provide examples or to summarize
information.  Figures usually appear in separate lists in the table of
contents and so serve to make certain kinds of information readily accessible.
The contents of a figure is formatted based on the style definition and
whatever the writer specifies.  Figures accept any kind of formatting
controls, but tables or graphics cannot be used within figures.  Figures may
be larger than a single page and will be broken in much the same way as a page
is broken.
 
Global controls for figures follow:
\min_figure={size}
 
Specifies the minimum size of the first piece of a figure that needs to be
broken between pages.  See \minimum_size under  the topic PAGE_BREAKING.
Defaults to .15\vsize.
\figure_default={name}
Provides the name of the default figure style to be used when no style is
specified on the DSL \FG control.
\beginfigures
 
Begins a set of figure styles.  Local figure controls can be used to provide
defaults for all figure styles.
\newfigure{name}
 
Begins a new figure style.
\endfigures
 
Ends figure style definitions.
 
\newcount\exampleno
\newclass{xmp}
\figure_default={STANDARD}
 
\beginfigures
   \space_before={2}
   \space_after={1}
   \startup={}
   \fgnum={\ifx\chnum\empty\else\chnum--\fi\number\figureno}
   \intro={Figure \fgnum.}
   \caption={\ALC\SL\intro\ \ \fgtitle}
   \next_caption={\ALC\SL\intro\ \ \fgtitle\ (part \number\chunkno)}
   \contents={\intro\ \ \fgtitle\ \dotfill\ \page}
   \caption_space={1}
   \boxing
 
\newfigure{DEFAULT}
   \synonym={STANDARD}
   \setup={\FIF\TT}
 
\newfigure{EXAMPLE}
   \class={xmp}
   \figureno=\exampleno
   \intro={Example \fgnum.}
 
\endfigures
 
The preceding figure shows a sample set of figure definitions.  Note that the
\beginfigures control in this example starts a new set of figure definitions
and is followed by the controls common to the figure styles in that set.  The
\newfigure{DEFAULT} control starts the definition of the DEFAULT style,
followed by the controls specific to that style.  The definition of the second
figure style, EXAMPLE, shows how a figure style is assigned a new insert class
and counter.  Any number of additional figure styles could be defined here.
The \endfigures control ends this set of figure definitions.
 
Controls local to figures include all the common controls described earlier,
under .  In addition to the common controls, the following local controls are
specific to figures:
\fgnum={code}
 
Specifies code to format the figure number.  This control can be referred to
elsewhere to materialize the formatted figure number.
\figureno=counter
 
Specifies a new counter to be used with a figure style.
00003
00005
00006
00007
00002
00001
00004
CapTeX uses and produces several files.  These files always have the same file
name with different extensions.  That is, the base file name is either the
name of the main source file or *:CAP, depending on how the CAP menus produce
it.  The file types and their uses are as follows:
DVI File
 
DVI files have the extension :dvi and are the device-independent output of
CapTeX.  These files need additional treatment before printing.
Log File
 
A log file is produced for every CapTeX run and contains detailed debugging
information about any errors that occur.  It also contains a list of
statistics at the end, showing, among other things, how much memory TeX used.
Log files have the extension :log.
Err File
 
A file with the extension :err is a condensed version of the log file.  It is
useful for finding and correcting errors when the errors are simple, and when
the extra information that TeX supplies for debugging is not useful.
Aux File
 
The auxiliary file contains information about the last formatting pass.  It is
used to store cross-reference information, the number of items in each insert
class, and other information that CapTeX accumulated on one pass and needs to
remember for the next pass.
Table of Contents Files
 
CapTeX writes a main table of contents file with the extension :toc and also
one for each insert class, using the same name as the insert class.  For
example, an insert class called lfg (list of figures) would write to a file
with the extension :lfg; an insert class called ltb (list of tables) would
similarly write to a file with the extension :ltb.
Index Files
CAP produces two index files.  The unsorted index file written out by CapTeX
has the extension :idx, whereas the sorted file that the next pass of CapTeX
reads back in has the extension :ids.  The sorted file is produced by the CAP
index sorter, described earlier in this section.
Adx File
 
A file with the extension :adx is produced by CapTeX after every pass.  It
sets the CAPADX control processor variable, and thereby tells the CAP outer
process what steps to perform next.  CAPADX is set to 0 if CapTeX is finished,
1 if CapTeX needs another pass, and 2 if CapTeX needs another pass but the
index sorter needs to be invoked first.
00007
00004
00001
00003
00006
00002
00005
ADSL flags are usable in normal TeX \if constructions, as follows:
 
\if.. somecode \else someothercode \fi
 
For example, the page-breaking code for chapters is usually as follows:
 
\startup={\if@twosided\BRO\else\BRP\fi}
 
The flags described below are used throughout ADSL inside various structural
definitions.
\if@boxing
 
True if boxing is enabled.
\if@twosided
 
True if two-sided is specified.
\if@landscape
 
True if the document is being formatted in landscape mode.
\if@draftmode
 
True if draft mode is turned on.  This flag must not change during a CapTeX
pass.
\if@chapternos
 
True if the current chapter is numbered.  This flag is automatically turned
off when an asterisk (*) is specified for chnum on the DSL \CH control; if the
chapter is a table of contents or front matter, \no_chapter_numbering can be
specified.
\if@sectionnos
 
True if  \section_numbering is on.  This is automatically turned off if the
level head specifies an asterisk (*) as the current level specification
number.  It can also be turned off globally or within chapter styles by the
\no_section_numbering control.
00001
00005
00004
00003
00006
00002
Fonts are grouped into families, similar to families for math mode in TeX.
However, CapTeX font families are also scaled up and down, based on sizes
defined in the font file.  CapTeX font families are compatible with TeX math
mode and use the same family numbers.  TeX defines the first eight families,
as shown in  in the following table.
 
               Family         Description              CAP Name
              --------------------------------------------------
               family 0       roman font               \RM
 
               family 1       math italic font         \MIT
 
               family 2       fixed size math symbols  \MSY
 
               family 3       extensible math symbols  \MXT
 
               family 4       text italic              \IT
 
               family 5       slanted roman            \SL
 
               family 6       bold roman               \BF
 
               family 7       typewriter type          \TT
 
               families 8-15  unassigned
 
Families 0 to 3 are used by math mode.  Family 0 is the default font for
numbers, family 1 is for letters, family 2 is the math symbol font, and
family 3 provides extensible symbols.  Changing these families must be done
carefully, if at all.
 
Each font family associates three fonts:  one for the normal size text, called
\textsize, one for subscripts or superscripts, called \scriptsize, and one for
subsubscripts, called \scriptscriptsize.  \textsize is the only one of these
used when not in math mode.
 
CapTeX font families extend TeX's font families in two ways:
 
o   Font families are used in normal text, not just math mode.
o   Font size controls determine the size of all families.
 
TeX has a hard limit of 16 font families.  The default font names are
automatically assigned families, as shown in Table .  Other font families can
be assigned family numbers sequentially, beginning with 8.  If necessary, a
new font family number can be specified for a font, but this should be
avoided.  It is very important that font families 2 and 3 have the proper type
of fonts.  Math fonts have special requirements that only the TeX math fonts
can provide.
The following controls define font families:
\newfamily name={fontlist}
 
Specifies a list of three font names, assigned respectively to \textfont,
\scriptfont, and \scriptscriptfont.  Font names are separated by a straight
bar (|).  Missing entries are copied from the previous font in use.
\Set_family name=num
 
Specifies a number for a family.  num must be in the range 0-15.  Numbers
below 7 should not be changed.  The family number must be set before the
family is defined.
00001
00002
Since font files are often selected automatically based on the choice of
output device, they must be complete unto themselves, making all the font-
related decisions.  In addition to the controls mentioned below, font files
can contain anything relevant to font selection or to a specific device.
\defaultfont=\fontname
 
Specifies the default font to be used by CapTeX.
\defaultsize=\fontsize
 
Specifies the default font size to be used by CapTeX.
\literalfont=\fontname
 
Specifies the font to be selected when literal mode (the DSL \LT control) is
used.  Since no controls can be executed in literal mode, the font specified
by \fontname cannot be changed, except via \literalfont.  If necessary, this
control can be included in \setup code segments for chapters or level heads,
but it is preferable to use only a single font.  \literalfont will honor the
current size specification, however.  The font selected should always match
the character set used to type the document source, or CapTeX may not choose
the proper characters.
\baselineskip=skip
 
Specifies the default distance between lines of text.  Although a true TeX
control, \baselineskip is mentioned here because it is used mostly in the font
file.  Font files are specific to a certain base font and type size, and
therefore also need to set the distance between baselines for normal page
layout.  Individual structures, like footnotes or certain figure styles, may
set a different baseline distance if they are using smaller type.
00004
00001
00002
00003
CapTeX uses font sizes to provide easy access to each font family in a variety
of sizes.  Each member of every font family must be available at all the
defined sizes.  New font sizes are defined with the \newsize control, as
follows:
\newsize name={sizelist}
Specifies either a magnification factor using \magstep, or a list of three
point sizes used to set the size for \textfont, \scriptfont, and
\scriptscriptfont, respectively.  With TeX fonts, \magstep controls are
usually used to magnify the primary fonts.  These controls are defined in  the
following table, where the magnification factor shown is times 1000.  Explicit
point sizes are normally used with PostScript fonts.
 
                   Magstep       Multiplier  Magnification
                   -----------------------------------------
                   \magstep0     120         1000
                                    1
                   \magstephalf  12 -
                                    2        1095
                   \magstep1     12          1200
 
                   \magstep2     122         1440
 
                   \magstep3     123         1728
 
                   \magstep4     124         2074
 
                   \magstep5     125         2488
 
At any point, the current font is selected by taking the font name from the
family and combining it with the active size.  In math mode, fonts for
subscripts are selected by combining the \scriptsize font with the \scriptsize
size.
00001
HEADERS_FOOTERS
CapTeX collects footnotes as each page is being built, and prints them at the
bottom of the page.  A rule usually separates the text from the footnotes.
Footnotes always start on the page which refers to them.
 
The following global controls are used to manage footnote layout and define
new footnote styles:
\footnote_default={name}
 
Specifies the default footnote style to be used if no other style is
specified.
\footnotelength={dimen}
 
Specifies the length of the footnote rule to be used.  Defaults to 2 in.
\footnotethickness={dimen}
 
Specifies the thickness of the footnote rule.  Defaults to .4 pt.
\footnoteheight={dimen}
 
Specifies the distance between the bottom of the text and the footnote rule,
if there is one, or the top of the footnotes, if not.
\beginfootnotes
Begins a new set of footnote definitions.
\newfootnote{name}
 
Creates a new footnote style.
\endfootnotes
 
Ends footnote style definitions.
 
The following controls are local to footnote style definitions:
\setup={code}
 
Provides initialization for the text of each footnote.  This control can be
used to print footnotes in a smaller, different font relative to the normal
text.
\indicator={code}
 
Specifies code for the footnote reference marker, which may be a letter,
number, or other character (or no character at all, so that the footnote is
unmarked).
 
By default, footnotes are numbered on a chapter basis rather than on a page
basis.  This is because CapTeX collects more than enough material for a page
before deciding where the page will break, and a footnote's number is assigned
before the pages are broken.  Footnotes use the \footno counter.  \numbering
can be used to specify that footnotes be numbered sequentially throughout,
instead of by chapter.    \raisednumber and \raisedsign are often used to
format footnote references, because they use a smaller symbol and raise it
somewhat, much like a superscript.  But \number, and its variations, may also
be used in footnote style definitions.
 
\footnote_default={NU}
 
\beginfootnotes
   \setup={\SMALL}
 
\newfootnote{NU}
   \synonym={NUMBERED}
   \indicator={\raisednumber\footno}
 
\newfootnote{UN}
   \synonym={UNMARKED}
   \indicator={}
\endfootnotes
 
The preceding figure shows a sample set of footnote definitions.  Note that
the \beginfootnotes control in this example starts a new set of footnote
definitions and is followed by the control common to the footnote definitions
in that set.  The \newfootnote{NU} and \newfootnote{UN} controls start the
definitions of the NU and UN styles, respectively, followed by the controls
specific to those styles.  Any number of additional footnote styles could be
defined here.  The \endfootnotes control ends this set of footnote
definitions.
00005
00007
00004
00002
00003
00001
00009
00006
00008
When CAP formats documents that require a table of contents or index, or use
cross-references, several format passes may be required to provide accurate
page numbers.  CAP automatically determines when another pass is required, and
may need up to four passes to guarantee correct page numbers in cross-
references.  In general, simple documents such as letters or memorandums
require only a single pass.  Using a table of contents, index, or any forward
references requires at least one more pass.  (In a forward reference, the DSL
\RF control is entered before the corresponding \LA control.  See the CAP DSL
Reference Manual, HA27, for more information.)
 
Running several format passes can use a lot of time, and having completely
accurate references is not always necessary.  During the early stages of the
document preparation cycle, writers need only draft copies.
 
CAP provides a built-in mechanism for either draft or final copy.  Selecting
\draftmode tells CAP not to make any extra passes simply to guarantee accurate
references.  The table of contents is delayed until the document is finished,
and is printed at the end.  This requires manual collation, but makes the
table of contents reasonably accurate.  \draftmode can make at most two
passes, which it may need to do to provide an index (since the index must be
sorted before being formatted), or to provide initial values for forward
references, which would otherwise have no values at all.
 
Selecting \finalmode directs CAP to make up to four passes to provide accurate
page numbers for cross-references.  The table of contents is printed in the
correct position in the front of the document.  The actual number of passes is
determined based on cross-references and the type of page numbering.
 
The controls that select either draft or final copy are global and can only be
used once.  They must appear somewhere in the control files, before the
document source is read.  This selection is usually made via the CAP menus.
As mentioned above, the controls are:
\draftmode
 
Sets draft mode, which restricts CAP to one pass if possible, or to two passes
if there are forward references or if there is an index.  The table of
contents is always printed at the end and must be manually inserted in the
correct position.
\finalmode
 
Sets final mode, in which runs might require two, three or four passes, or,
for documents without auxiliary files, only one pass.  Final runs will
correctly handle all sorting and referencing, including index, bibliography,
and glossary.
00001
00002
The ADSL control files are used as part of a CAP format definition,
which is a collection of options that define how to format a document.
In addition to the control files, these options define page dimensions
and special processing flags. Formats are created by the administrator
with the CAPADMIN program, as described in the CP-6 CAP
Administrator Guide (HA30).
 
The set of options that constitute a particular format are established
using CAPADMIN menus and saved under a given name. CAP users need not
be concerned with the individual options that constitute a format.
Instead, they simply refer to formats by their names.
 
CAP formats allow ADSL control files to be used in different ways
without duplicating most or all of the controls in separate files
for each variation. For example, there might be two CAP formats
that use identical ADSL structures, one of which is for draft copies,
the other for final, two-sided output. Or, the same style might be
used in formats that have different page dimensions, each of which
uses different sized fonts.
 
Through CAPADMIN, the CAP formats also control the specification of
output devices and the selection of user context options for
formatting and job control. See the CP-6 CAP Administrator
Guide (HA30) for more details.
The scope of ADSL controls follows logical grouping rules. Controls
described as "global" in the following sections are controls that
are used on their own, anywhere in the style files except within
structure definitions. These controls are global in scope; they affect
the entire document. Most global controls should be specified only
once; they have no effect until the style files have all been
read and document formatting starts. Global controls are used to
determine, for example, page dimensions and orientation, font
definitions, or default values for DSL controls.
 
Controls described as "local" are used only within structure
definitions and only have an effect when a particular structure
and style are used. Local controls are used to specify, for
example, spacing around a structure, the contents of titles or
captions, or special attributes of a structure.
 
Some controls are made accessible both globally and locally. These
controls are essentially local controls, but can be specified
before structure definitions to serve as defaults for the following
definitions. Some of these controls, like \boxing, have
their initial values determined by CAPADMIN.
Graphics provide a mechanism within CapTeX to import vector or bit-mapped
graphics and have them scaled and positioned on the page.  Graphics must be no
larger than a page, including any box or captions.
 
Graphics are generally similar to figures or tables.  Graphics cannot be
broken between pages, however, so they must be small enough to fit on a page.
Graphics can be mixed with normal CAP text by allowing the graphic to overlay
the text, thereby providing a mechanism for preprinted forms or for labeling
with CAP fonts inside drawings.
 
Graphics can also be positioned within a line of text, and act like a single
character.  Inline graphics do not have captions and cannot float.  Inline
graphics only use graphic styles to determine boxing and overlay capabilities.
 
The following global controls are used to define new graphic styles:
\min_graph={size}
 
Determines the minimum vertical height of any graphic.  If the DSL \GR control
specifies a height less than \min_graph, it will be replaced by \min_graph.
Defaults to 0 pt.
\graph_default={name}
 
Provides the name of the default graphic style to be used when no style is
specified on the DSL \GR control.
\gi_default={name}
 
Provides the name of the default graphic style to be used when no style is
specified on the DSL \GI control.
\begingraphs
 
Begins a set of graphic styles.  Local graphic controls can be used to provide
defaults for all graphic styles.
\newgraph{name}
 
Begins a new graphic style.
\endgraphs
 
Ends graphic style definitions.
 
\graph_default={DEFAULT}
 
\begingraphs
 
\newgraph{DEFAULT}
   \synonym={STANDARD}
   \space_before={2}
   \space_after={2}
   \grnum={\ifx\chnum\empty\else\chnum--\fi\number\graphno}
   \intro={Graphic \grnum.}
   \caption={\ALC\SL \intro\ \ \grtitle}
   \caption_space={1.5}
   \contents={\intro\ \ \grtitle\ \dotfill\ \page}
 
\endgraphs
 
The preceding figure shows a sample set of graphic definitions.  Note that the
\begingraphs control in this example starts a new set of graphic definitions.
It is not followed in this case by controls common to each graphic style, as
there are none in this example.  The \newgraph{DEFAULT} control starts the
definition of the DEFAULT graphic style, followed by the controls specific to
that style.  Any number of additional graphic styles could be defined here.
The \endgraphs control ends this set of graphic definitions.
 
Controls local to graphics include all the common controls described  the
topic INSERTS_COMMON_CONTROLS. In addition to the common controls, the
following local controls are specific to graphics:
\grnum={code}
 
Specifies code to format the graphic number.  This control can be referred to
elsewhere to materialize the formatted graphic number.
\graphno=counter
 
Specifies a new counter to be used with a graphic style.
\overlay_graph
 
Specifies that the graphics produced with a style print over any text under
them.  This allows graphics and text to occupy the same space.  \overlay_graph
leaves the current position as it was before the graphic and automatically
turns off \floating.
\no_overlay
 
Specifies that graphics produced with a style cannot have overlaid text.
00004
00006
00003
00008
00002
00007
00001
00005
00010
00009
Headers and footers are automatically selected by CAP, based on the
left/right page handling selection and the page numbers.
 
The following controls can be used, both within ADSL and by writers
using DSL, to turn headers and footers on or off.  These controls
follow the normal nesting conventions and can be used globally for
an entire document, or locally within a particular chapter.  If used
within chapter styles, or if specified from within DSL, it is
recommended that they only be used as close as possible to the beginning
of a page, after a DSL \BRP control, or at the start of a new
chapter. If not, the headers and footers may not change at the expected
places. The default status for header/footer switches is on.
\headers
 
 Activates headers. Headers will be placed on each page, automatically
selected by CapTeX, based on page handling and header definitions.
This is the default.
\noheaders
 
Cancels headers on the current page and the following pages.
\skipheader
 
Can be used within various structures. It cancels the next header
only. Headers on the following pages return to normal.
\footers
 
 Activates footers. Footers will be placed on each page, automatically
selected by CapTeX, based on page handling and footer definitions.
This is the default.
\nofooters
 
Cancels footers on the current page and the following pages.
\nopagenumbering
 
Is a synonym for \nofooters.
\skipfooter
 
 Cancels the footer on the current page. Footers on subsequent pages
return to normal.
 
Headers are selected automatically by CapTeX using the following rules:
 
o   If the page is the first page of a chapter, use \first_header.
o   If page handling is \one_sided, use \header.
o   If page handling is \two_sided, use either \odd_header if
        the page is odd numbered or \even_header if the page is even
 
        numbered. Whether the page is even or odd is determined by examining
        the \pageno counter, even if pages are numbered within chapters.
 
Footer selection follows the same rules, using the equivalent footers.
 
Headers and footers are defined as a sequence of controls and text,
where the controls may be DSL, ADSL, or TeX, in any combination.
Headers and footers are formatted to the full page width, even if the
text is being set in multiple columns. Headers are always set as
high as possible in the \headheight area, while footers are
set at the bottom of the area reserved for \footheight.
 
Many of the more common formats of headers and footers can be handled
easily with the \HB and \VB or \VT DSL controls. It is
important to select sufficiently large values for \headheight and
\footheight, to prevent a header or footer from running into the
text.
 
The following controls are used in the creation of headers and footers:
\header={code}
 
Defines a header to be used on all one-sided pages.
\odd_header={code}
 
Defines a header to be used on odd-numbered pages when
\twosided is on.
\even_header={code}
 
Defines a header to be used on even-numbered pages when
\twosided is on.
\first_header={code}
 
Defines a header to be used on the first page of a new chapter;
that is, when \chappage=1, or on the first page of a
document.
\footer={code}
 
Defines a footer to be used on all one-sided pages.
\odd_footer={code}
 
Defines a footer to be used on odd-numbered pages when
\twosided is on.
\even_footer={code}
 
Defines a footer to be used on even-numbered pages when
\twosided is on.
\first_footer={code}
 
Defines a footer to be used on the first page of a new chapter;
that is, when \chappage=1, or on the first page of a
document.
 
\header={\HB{|\docname|}\hrule}
\footer={\HB{|\page|}}
\odd_footer={\HB{\page||}}
\even_footer={\HB{||\page}}
\first_footer={}
 
 The preceding figure shows some sample headers and footers.
These examples use the DSL \HB control to align the text elements in
the headers and footers. The \header control has the document name
centered on the page, with a line under it. The three footers show how
the page number is placed centered, left, or right, and the final
control, \first_footer, is empty. In this case, no footer would
appear.
 
Since TeX collects more than enough material for a page before
actually deciding on the final layout, the normal variables
associated with level heads may not be accurate enough for use in
placing headers or footers, which are built after the page has been
broken. To solve this
problem, CapTeX uses a system of marks, which are like invisible
notes in the margin used to place headers and footers.
 Marks are described under the topic MARKS.
00014
00010
00015
00011
00012
00004
00008
00001
00005
00002
00006
00013
00009
00007
00003
LEVEL_HEADS
LEVEL_HEADS
CAP ADSL has an on-line HELP facility.  CAP users can display syntax formats,
parameters, and descriptions of controls as well as descriptions of menu items
and related information.  For a list of HELP topics for ADSL from the system
command level (!), enter the following at the terminal:
 
HELP (ADSL) TOPICS
HELP files are an alternate way of viewing a document, where the regular
chapter and level head divisions are replaced by HELP constructs.  Text is
included in or excluded from a HELP file via the DSL \HMF and \HMN controls
and via DSL subsets.  In CP-6, HELP styles provide database controls for the
HELP database preprocessor, VA$MN_HERMAN. These database controls are
basically the counterparts of regular level and chapter heads.  Although CAP
supports only CP-6 HELP, the HELP style capability provides an extensible
mechanism that can support other types of HELP databases.
 
HELP controls are honored only when \helpdev is on in a style file; in this
case, all output is prepared for use as an ASCII file.  HELP mode produces no
index or table of contents; graphics and cross-references are ignored.  HELP
mode produces a single galley, without page breaks.
 
The following global controls define HELP styles:
\caphelp_default={name}
 
Specifies the default HELP style used when no style is specified on DSL \HH
controls.
\begincaphelp
 
Begins a set of HELP styles.  Local HELP controls can be used to provide
defaults for all HELP styles.
\newcaphelp{name}
 
Begins a new HELP style.
\endcaphelp
 
Ends HELP style definitions.
 
HELP styles have two local controls:
\synonym={name}
 
Provides alternate names by which a HELP style (or any other  style) can be
called.
\text={code}
 
Specifies the text that is to be written to the output file.  If HELP controls
need to be the only items on a line in the source file, as they do in CP-6,
DSL \BRL controls need to be included.
 
The following illustrates sample HELP styles:
 
\caphelp_default={K}
 
\begincaphelp
 
\newcaphelp{A}
   \text={.*A*\BRL}
 
\newcaphelp{K}
   \synonym={DEFAULT}
   \synonym={T}
   \text={.*K* \hhtopic, \hhsynonyms\BRL}
 
\newcaphelp{B}
   \text={.*B*\BRL}
 
\newcaphelp{S}
   \text={.*B* \hhtopic, \hhsynonyms\BRL}
 
\newcaphelp{X}
   \text={}
 
\endcaphelp
 
%   Define special substitutions to simplify "HELP-only" and
%   "manual-only" subsets.
\DS\SBH{\SB{HELP}}          % \SBH HELP-only text \SB
\DS\SBM{\SB{HELP}\SB{}}     % \SBM manual-only text \SB
00002
00001
00004
00003
00005
00006
Like the table of contents, indexing also requires several coordinated
actions.  Indexing takes at least two full formatting passes.  The first pass
collects the index entries into an index file; this file is then sorted, and
the second pass formats the sorted index.  The index that is actually printed
is always the index from the previous pass.
 
Index entries are collected and written to the index file while \indexing is
on.  Indexing may be turned on and off globally or individually in each
 
chapter.  When indexing is turned on, some level heads will be automatically
indexed.  This is further described in the  ADSL HELP topic LEVEL_HEADS .
 
CAP supports indexing to two levels, with a main term and a subterm.  Each
index entry has an associated index style that determines how the entry is
formatted, with separate controls for the main term, subterm, and page number
(or other reference).  An additional feature is provided by the \permuting
control, which cross-indexes the term and subterm.  It does this by creating
two index entries for each \IX control, the second inverting the roles of the
term and subterm.  Index styles allow the administrator to highlight certain
entries by using boldface or other techniques for specific terms or their page
numbers.
 
Once the index terms are collected, CAP sorts the index file, which is then
read back when the DSL \IDX control is encountered in the document.  If there
is no \IDX control, no index is printed, even if entries have been made to the
index file.  Unlike the table of contents controls, the reading of the index
does not imply a separate chapter.  The writer is expected to begin a new
chapter, which may contain introductory text explaining the index conventions,
then issue the \IDX control to produce the index.
 
As the index is being read, the entries are collated and any duplicates are
removed; the entries are then broken into letter groups.  Entries with
different formats are considered separate entries, even if their terms are the
same.  CapTeX automatically breaks subterm lists across pages by repeating the
main term where necessary.  The administrator may specify a "continued" text
to be used in this case.
 
\index_default={X}
 
\beginindex
 
\newindex{X}
   \permuting
   \ixtext={\BF\ixterm}
   \ixsubtext={\ixsub}
   \ixnum={\BF\page}
 
\endindex
 
The following figure provides a sample index definition.  Note that the
\beginindex control in this example starts a new set of index definitions.  It
is not followed by any controls common to each index definition, as there are
none in this example.  The \newindex{X} control starts the definition of the X
index style, followed by the controls specific to that style.  Any number of
additional index styles could be defined here.  The \endindex control ends
this set of index definitions.
 
The following global controls are used to tailor the index format and create
new index styles:
\index_default={name}
 
Specifies the default index style to be used if no other style is specified
with the \IX control.
\indexing
 
Enables the collection of index entries.  Index entries are written to an
index file, which is then sorted and can be read by the DSL \IDX control.
\no_indexing
 
Disables index entries.  Index entries are not written to the index file, but
the file is left open.  If indexing is re-enabled, new entries will continue
to be written to the same index file.
\permuting
 
Enables permuting of index entries.  If an index entry is permuted, two index
entries are made, the second inverting the roles of the term and subterm.
This provides for simple cross-indexing.  \permuting has no effect if there is
no subterm.  \permuting can be used both globally and within index styles.
\no_permuting
 
Disables permuting of index entries.  Each index entry is written to the index
file; no cross-indexing is performed.  \no_permuting can be used both globally
and within index styles.
\new_letter={code}
 
Provides code that will be inserted between letter groups when the index is
formatted.  code can refer to \curletter, which will contain the current
letter, in lower case.  CapTeX executes \new_letter just before the first
index term for each letter.  \new_letter is not executed for symbols or
digits.
\index_space={cdimen}
 
Specifies horizontal spacing to be inserted between the index term and the
page number list.  This defaults to \quad.
\index_separator={code}
 
Specifies characters to separate page numbers when the list of page references
to an index term is printed.  This defaults to a comma followed by a space:
{, }.
\index_continued={code}
 
Specifies code that will follow an index term if that term is broken across
pages or columns.  This defaults to "(continued)".
\ignore={word}
 
Adds a word to the list of words that will be removed from index terms if they
are the first word.  This is usually used to remove leading articles.  The
initial list contains the articles "a", "an", and "the".
\beginindex
 
Begins a new set of index definitions.  This control can be followed by
defaults for all index styles.
\newindex{name}
 
Creates a new index style.  Within an index style, local controls determine
how each part of the entry is formatted.
\endindex
 
Ends this set of index style definitions.
 
The following controls are used with each index style to define the specific
properties of that style.  They are local to their style definition.
Permuting controls
 
The \permuting and \no_permuting controls can also be specified as a property
of an index style, to control cross-indexing on a style-by-style basis.
\ixtext={code}
 
Specifies how the main term is to be formatted.  Only formatting controls can
be used here; major DSL structures, like level heads, are not permitted.
\ixsubtext={code}
 
Specifies how the subterm is to be formatted.  Only formatting controls can be
used here; major DSL structures, like level heads, are not permitted.
\ixnum={code}
 
Specifies the contents of the reference page number.  The code usually refers
to \page to produce the page number.
 
The parameters of the \IX control are available to the index styles as \ixterm
and \ixsub.  For numbering, the recommended technique is to use the \page
control to define a page number.  Since \page is often chapter-dependent, the
index term numbering will then vary in the same way as the numbering on each
page and in the table of contents.
 
To remove leading articles and other words from the index terms (both main
terms and subterms), the \ignore control can be used to specify the words to
remove.  \ignore controls can be used in two ways.  They can be specified in
one of the style files, where the words are stored to await the opening of the
index file.  They are then written to the index file, where the indexing
program reads them and performs the actual removal of leading articles.  The
\ignore controls can also be included in the document itself, but will only
affect any index terms following them.
 
Any number of \ignore controls may be specified.  For example:
 
\ignore={a}
\ignore={an}
\ignore={the}
00011
00013
00010
00002
00009
00001
00008
00007
00017
00016
00015
00012
00006
00003
00005
00004
00014
Tables, figures, and graphics are structures that are not part of the normal
flow of document text, and are called inserts.  Inserts have the following
properties:
Numbers      Inserts can be numbered in a variety of ways, with both simple
numbers, such as Table 1, or composite numbers containing a chapter or section
number, such as Table 5-4.  Numbers can be automatically incremented, freeing
the writer from the need to keep track of them.  Each insert style can have
its own numbering sequence.
Captions      Inserts can have captions either above or below the insert, and
vary from a simple title to lengthy captions such as those found in scientific
journals.  For inserts that are so large that they need to be broken into
several pieces, two different captions can be specified to provide an
indication that the insert is to be continued.
Floating      Since inserts may be quite large and thus cause problems when
trying to make pages, they can optionally be moved, or floated, from their
original position in the source to the next available page, with the text that
follows them in the source moving forward.  This possibility applies only to
inserts that are no larger than one page in height, since any larger inserts
will need to be broken anyway.
Breaking      When inserts are so large that they occupy more than one page,
they are broken into smaller pieces and occupy consecutive pages.  In this
case, the first piece of an insert is broken to exactly fill the remainder of
the first page.
Labels      Labels can be used to refer to inserts by name, and can
automatically provide accurate page and insert numbers when referred to in the
text.
Insert Classes      Inserts are grouped into insert classes, a mechanism that
determines how each insert type is accumulated for entry into a table of
contents.  Each insert class has its own file in which to accumulate entries,
and its own counter to determine how many there are.  Each insert class also
provides an ADSL control to print the list of entries in a table of contents.
00004
00002
00003
00006
00005
00001
The following local controls are common to figures, tables, and graphics:
Spacing
 
Insert styles use the regular spacing controls, \space_before and
\space_after, to separate inserts from the surrounding text.    Spacing
controls are always local to their insert style.
Initialization
 
Inserts use the same initialization controls as other structures:  \startup
and  \setup.  However, \setup only applies to figures and tables, and provides
initialization code for the contents of the insert.  The contents of a graphic
is determined entirely by the graphics file being read.  Initialization
controls are always local to their insert style.
Insert layout
 
The controls for captions, boxing, and floating described  under the topics
PAGE_BREAKING, CAPTION_DEFINITIONS, CAPTION_PLACEMENT, CAPTION_SELECTION, and
BOXING apply to all inserts.
Table of contents
 
The \contents control  determines how each entry to the table of contents is
formatted, while the \class  control determines which class is used for the
table of contents.
00002
00003
00001
00004
The default style definitions provide three insert classes:  ltb, lfg, and
lgr, which are normally associated with tables, figures, and graphics,
respectively.  Each insert class creates a separate grouping for the table of
contents.  To do this, three entities are created for each class, as follows:
Output file:  Each class has an output file associated with it, which is
internally known as \classfile, and externally with the usual file name,
followed by the extension class.  Class names are usually kept to three
characters or less, to conform with naming conventions on MS-DOS computers,
although this is not required.  All table of contents entries for the class
are then written to this file, to be later included in the table of contents
under a single heading.
Counter:  Each class has an associated counter, named \classcount, which
automatically counts each entry to the table of contents for the class.  This
counter is saved in the aux file, where the next pass of CapTeX can read it
and determine whether or not the class has any table of contents entries.
\list_class function:  Each class has its own listing function, which is used
to materialize the entries for the class in the table of contents.  The list
function is called \list_class, and accepts one parameter that provides
heading information for the list.  If no table of contents entries exist for a
class, \list_class does nothing.
The following table provides examples of classes and the entities that are
created:
 
        Class Name  File Name    File Control  Counter    List Function
       ----------------------------------------------------------------
        lfg         jobname:lfg  \lfgfile      \lfgcount  \list_lfg
 
        ltb         jobname:ltb  \ltbfile      \ltbcount  \list_ltb
 
        xyz         jobname:xyz  \xyzfile      \xyzcount  \list_xyz
 
Creating a new insert class creates a new list of entries for the table of
contents.  Insert classes must be assigned to all insert styles, even if no
table of contents is to be generated.  The purpose of insert classes is to
provide a facility for creating new insert types based on the three basic
possibilities:  tables, figures, or graphics.  By selecting a new class and
choosing a new numbering sequence, the administrator could create a figure
style that might be labeled "Example", and would appear in the table of
contents under the heading "List of Examples".  Another possibility is to have
different insert types appear in the same list.  For example, figures and
graphics might both be called "Illustration", and be numbered in a single
sequence.    A figure under the topic FIGURES shows an "Example" figure style.
 
The following controls are used to create new insert classes:
\newclass{class}
 
Generates a new insert class.  There is a hard limit of 12 insert classes per
document.  This control can only be used globally.  Insert classes must be
created before they are referred to in an insert style.
\class={name}
 
Selects a new insert class for an insert style.  This control can appear only
locally, within insert styles.  Insert classes must be created before they are
referred to in an insert style.
00005
00002
00003
00004
00001
Page handling is selected in the FORMAT definition by
CAPADMIN.  Left/right page handling affects left and right
margins, and headers and footers. There are two choices:
\onesided
 
 Selects one-sided pages. These pages all have the same right and
left margins, and use the same headers and footers. One-sided pages
are meant for use where each page will be printed on one sheet
of paper. In this case, both the \BRO and \BRE DSL controls
are equivalent to \BRP.
\twosided
 
 Selects two-sided pages (also called recto-verso). This is meant
for use where two pages will be printed on a single sheet of paper,
with the odd numbered page on the front and the even numbered page
on the back. CapTeX keeps track of the pages, choosing the margins,
headers, and footers differently for odd and even pages. Margins
alternate, with \fmt_left on the left for even pages, and
\fmt_right on the right for odd pages. Headers and footers are
defined separately for odd and even pages.
00001
00002
Level heads are local to the chapter style where they are defined.
If defined outside a chapter style, level heads apply to all chapter
styles whenever a level head is called, and can also be used
independently of any chapter styles.
 
Level heads do not have styles; they have levels instead. Only a
single digit is used, so the administrator can define levels 1
through 9. Writers use level heads via the \Ln control,
where the n refers to the level.
 
In general, level heads are defined as follows:
 
  \beginlevels                         Starts a new set of level heads.
         .
         .                             Default values for all the following
                                       level heads.
 
    \newlevel num (1-9)                Starts a specific level head.
            .
            .                          Information particular to this level
                                       head.
 
    \newlevel num (1-9)                Another specific level head.
            .
            .                          Information particular to this level
                                       head.
 
  \endlevels                           End of this set of level heads.
 
The number on the \newlevel control is the level number, and
the control is followed by a series of elemental controls that define
various aspects of the level head and the following text.
 
Level heads can be defined globally, for the entire document, or
within chapter definitions, where they become local to that chapter.
 
The following global controls are used to create level head
definitions:
\level_separator={code}
 
Is a macro containing the string that separates each number in a
section number. The default is a period (.).
\section_numbering
 
Turns on section (specification) numbering. Section numbers are
produced by the \sectionno control when level heads are encountered.
However, if the \Ln control uses the asterisk (*) instead
of a specification number, no section number is produced. This is the
default.
\no_section_numbering
 
Turns off section (specification) numbering. In this case, section
numbers are not produced by the \sectionno control.
\chapter_numbering
 
If section (specification) numbers are being produced, this control
causes chapter numbers to be included as the first number in the complete
section number. For example, in Chapter 1, Section 2, the \sectionno
control would produce "1.2". However, if the \CH control uses
the asterisk (*) instead of a chapter number, no chapter number
is used in the section number. This is the default.
\no_chapter_numbering
 
 If section (specification) numbers are being produced, this control
does not include chapter numbers in the complete section number produced
for level heads.
\beginlevels
 
 Begins a new set of level head definitions. Following this control,
defaults for all level heads can be specified. These defaults will apply
only to level heads created in this set. Level heads not specifically
created within this set retain their previous definitions.
\newlevel num
 
 Creates a new level definition. The num must be a number between
1 and 9, specifying which level head to build. Level heads may be
defined in any order, and only those the administrator uses are
required.
\endlevels
 
 Ends level head definitions.
 
Within each new level, ADSL controls specify the various level head
functions. Controls for level heads specify how the heading is formatted,
extra vertical spacing around it, any formatting controls associated
with the level, and what, if any, table of contents entries need to
be generated for the level.
 
Specification (or section) numbers are automatically generated for
level heads, up to the current level. Each number is separated from
the next by \level_separator. The entire specification number is
available by referring to \sectionno. If the DSL \Ln control
uses the asterisk (*) instead of providing a specification number,
or if section numbering is disabled via \no_section_numbering,
\sectionno does nothing.
 
The following controls are all local to level head definitions.
Most of these controls are described in greater detail in
Section , where controls common to many structures
are defined.
\space_before={cdimen}
 
 Specifies the vertical space to be inserted before the level head.
Any CapTeX dimension may be specified here, either a bare number,
which will assume \ACH, or any TeX dimension unit. This
control acts like \SPB, indicating a good place to break.
\space_after={cdimen}
 
 Specifies the vertical space to be added after the level head. If
this is set to empty ({}), no vertical space will be added
and TeX will remain in horizontal mode. That is, the text will
continue on the same line as the header. Explicitly setting it to zero
({0}) will cause a line change, but no vertical space will be
added.
\intro={code}
 
 Specifies code to produce the introductory text. This control is
usually used in the code presented to \title, to produce
such introductions as "Section n".  \intro produces nothing
if section numbering is disabled by \no_section_numbering or by
setting the specification number to an asterisk (*) in the
DSL \Ln control.
\title={code}
 
 Specifies code to produce the level head, along with any spacing that
may be required horizontally to separate it from the following text.
\startup={code}
 
 Specifies code to be executed at the beginning of the level head.
It can be used to specify formatting controls or margins for the
following text.
\contents={code}
 
 Specifies code to be written to the table of contents file. Nothing
is written if the specification number is set to an asterisk (*)
in the DSL \Ln control.
\help={code}
 
Specifies HELP controls to be used by a level head, when \helpdev
is used. \help replaces the normal level head. If \helpdev is
not specified, \help is ignored. \help is described in detail
in Appendix .
\ixstyle={name}
 
 Defines the index style used for level heads that are to be
automatically indexed.
\mark={code}
 
 Specifies mark code to be automatically inserted by level heads. When
this code is specified, a mark is generated just before the level head,
and another just after. The mark is a double mark, keeping track of
both the level head before the page break and the one after, should a
page break occur just before the new level head. This is further
discussed in the next topic, Marks.
 
\level_separator={.}
 
\beginlevels
   \space_before={1}
   \space_after={}
   \intro={\sectionno}
   \startup={\INB{0}\FIN\ALB\BRX}
   \indexing
   \ixstyle={}
 
\newlevel 1
   \space_before={2}
   \space_after={1}
   \title={\LARGE\BF \intro\lhtitle}
   \contents={\INL{4}\RM \intro\lhtitle\ \dotfill\ \page}
   \ixstyle={LHEADS}
 
\newlevel 2
   \space_before={2}
   \space_after={1}
   \title={\BF \intro\lhtitle}
   \contents={\INL{6}\RM \intro\lhtitle\ \dotfill\ \page}
   \ixstyle={LHEADS}
 
\endlevels
 
Samples of level heads are shown in
 the preceding figure.
Note that the \beginlevels control in the sample starts
a new set of level head definitions, followed by the controls common
to all level head styles. The \newlevel 1 and \newlevel 2
controls start the definition of level 1 and level 2 styles,
respectively, followed by the controls specific to those styles.
Up to seven additional level heads could be defined here, for a
maximum of nine.
00006
00004
00014
00008
00015
00011
00016
00001
00017
00007
00005
00003
00002
00010
00009
00013
00012
 CapTeX normally processes more than a page of material before
deciding on the best place to break the page. This makes it difficult
to know precisely the range of material on a page. To provide for
running headers and footers, which need accurate information about
the sections (introduced by level heads) on a page, CapTeX uses a
system of marks, which is an extension of TeX's \mark control.
Each mark is similar to an invisible note in the margin and contains
text and/or control sequences. When the page is broken, CapTeX makes
three types of marks available for the current page:
\botmark
 
Is the mark text most recently encountered on the current page; that
is, the mark closest to the bottom of the page. If each new section
generated a mark, this would represent the section active at the bottom
of the page.
\firstmark
 
 Is the mark text first encountered on the current page. If each new
section generated a mark, this would represent the first new section on
the page.
\topmark
 
 Is the value of \botmark from the previous page. If each new
section generated a mark, this would represent the section active at
the top of the page.
 
Default marks are provided to handle level heads for running page
headers and footers, but marks have many possible uses, so CapTeX provides
controls to create new marks. Marks must be defined before
anything can be stored in them. Marks can only be read in headers
or footers.
 
The controls used to create marks are as follows:
\newmark\markname
 
 Defines a new mark. Two default marks are defined: \lastlevel
and \thislevel. These marks are token lists and can be manipulated
as such. Remember that marks are global, and storing in them should
be done globally.
\setmark\markname={code}
 
Inserts information in a mark and causes the mark to be written.
\setmark always writes all current, active marks, so the
administrator may need to set several marks at once by defining
the contents of all but the last one before calling \setmark.
\loadmark\markname={code}
 
 Loads a mark globally, expanding the mark contents (except for DSL controls).
This acts like \setmark, except that it does not write
the mark.
\getmark\marktype\markname
 
 Produces the value previously assigned to this mark, where
\marktype must be  one of \firstmark, \botmark,
or \topmark, as described earlier. \getmark can be used only
within headers or footers to materialize the information stored in
a mark.
 
CapTeX builds two marks by default. How these marks are defined
and used is shown
 in the following figure. These two marks are
designed to provide accurate information about the current level heads
for use in page headers or footers.
 
\newmark\lastlevel
\newmark\thislevel
 
\beginlevels
 
\newlevel 1
   \space_before={2}
   \space_after={1}
   \title={\LARGE\BF \intro\lhtitle}
   \contents={\INL{4}\RM \intro\lhtitle\ \dotfill\ \page}
   \mark={\global\lastlevel=\thislevel \setmark\thislevel={\lhtitle}}
   \help={\HH{\lhkey||K}}
 
\endlevels
 
\footer={\hrule\SPB{.05}\RM
         \HB{\docname|\getmark\botmark\lastlevel|\page}}
\header={\HB{|\getmark\firstmark\firstlevel|}}
 
To get marks that correctly reflect the active level head at
the top of a page, the \mark controls for level heads are
written twice: once before the level head and once after. Note
in the code for \mark in
 the preceding figure
that the first time the mark is written, before the possible page
break, \thislevel will have the new level head, while
\lastlevel will have the previous level head. After the level
head, the second time the mark is written, both \lastlevel and
\thislevel will reflect the new level head. With this system, the
administrator can refer to \lastlevel in footers and to
\firstlevel in headers, and the headers and footers will always
be accurate. The header and footer shown in Figure
do exactly that.
 
The administrator can create other marks and set them using the
\loadmark and \setmark controls wherever code is used in
styles. In particular, code fragments like \startup and
\setup are good places to define marks.
00001
00002
00007
00006
00004
00005
00003
CapTeX error messages are defined as TeX macros, and can, if needed, accept
parameters.  They therefore follow TeX syntax for \def controls.  This is only
important when translating or otherwise modifying the error messages in the
VA:ERROR file.  The administrator must retain the correct number of arguments,
and #n refers to the  nth argument.  Thus, the administrator can translate the
text, placing the arguments (if any) anywhere within the new text.  Arguments
do not need to be used in any specific order and can be used several times by
repeated use of #n.
The DSL multiple column control, \CL, can be used by the writer,
but it can also be used by the administrator in style files to
automatically initiate a special format. The default style file uses a
double column layout for the index. Columns
can also be turned on and off in chapter styles or level heads.
 
Some of the behavior of multiple columns can be determined in the style
files, via the following controls. All multicolumn controls are global.
\multicolumns
 
 Enables multiple column mode for the entire document, if the writer (or
the administrator, via the style file) decides to use multiple columns.
This is the default.
\no_multicolumns
 
 Disables multiple column mode for the entire document. In this case,
\CL controls are ignored.
\balance_cols
 
Specifies balanced columns. CapTeX attempts to fill each column with
an equal amount of text. This is the default.
\snake_cols
 
Specifies snaking columns. Starting with the first column, each column
will be completely filled with text before the next column is started.
The DSL \BRC (break column) control will work only if
\snake_cols is specified in the style file.
\column_rules
 
 Specifies that vertical rules will be put between the columns. These
rules are set in the middle of the space between columns, as defined
by \gutter. This is the default.
\no_column_rules
 
 Specifies that no vertical rules will be put between the columns.
\columnrulethickness=dimen
 
Is a dimension specifying the thickness of the vertical rule between
columns. Defaults to 0.4 pt.
\columns=num
 
 Defines the number of columns to be used if not specified on the
\CL control. \columns defaults to 2.
\gutter=dimen
 
Is a dimension that defines the default gutter size, if not specified
on the \CL control. The \gutter is the white space between
two columns. The default \gutter is 20 pt.
\columnskip=skip
 
Is a skip register defining the amount of white space to insert when
switching in and out of multiple columns. This defaults to one line
height, as defined by \baselineskip.
 
 These controls are illustrated in the following figure,
which is an extract from the default style file.
 
% For multiple columns, they are turned on here, with rules, .4pt thick.
% If \CL{} is specified with an empty parameter, we use 2 columns.
% Finally, the default gutter size between columns is set to 20pt.
% This is used if nothing is specified for the gutter on the \CL
% control.
 
\multicolumns
\column_rules
\columnrulethickness=.4pt
\gutter=20pt
\columns=2
\columnskip=13pt plus 3pt minus 2pt
00003
00007
00008
00010
00005
00009
00001
00006
00002
00004
The notation conventions used in the ADSL control syntax and examples
in this manual are presented in the following table:
 
    Notation               Description
 
    Lower-case Letters     Lower-case letters, when preceded by a
                           backslash (\), indicate a literal, to be
                           entered as shown.  For example:
 
                           \page={\romn{\pageno}
 
                           must be entered exactly as shown.
 
                           Lower-case italic letters indicate a variable,
                           to be replaced with a user-supplied value.
                           For example:
 
                           \newchapter{stylename}
 
                           could be entered as:
 
                           \newchapter{TOC}
 
    Upper-case Letters     Upper-case letters indicate a literal, to be
                           entered as shown.  For example:
 
                           \SPB{5}
 
                           must be entered exactly as shown.
 
    Special Characters     Special characters (such as \, {, or =) are
                           literals, to be entered as shown.
 
    Braces ({})            Braces delimit the parameters of an ADSL
                           control.  Braces can enclose variables or
                           literals which may be required or optional,
                           depending on the specific control.  The braces
                           themselves are required, unless otherwise
                           specified.
 
    Equals Sign (=)        The equals sign precedes the parameters of an
                           ADSL control and can optionally be surrounded
                           by spaces.  For example:
 
                           \intro={\sectionno}
 
                           The equals sign is required unless otherwise
                           indicated.
 
    OR Bar (|)             The OR bar separates elements in a list from
                           which one or more elements may be, or must be,
                           chosen.  For example:
 
                           \HB{a|b|c}
 
    Horizontal Ellipsis
    (...)                  The horizontal ellipsis indicates that a
                           previous braced element may be repeated, or
                           that elements have been omitted.  For example:
                           \title_map={var1|var2|...|var9}
 
                           means that one or more (up to nine) var
                           parameters may be entered, with an OR bar
                           inserted between each parameter.
 
    Vertical Ellipsis (.)  The vertical ellipsis indicates that controls
                           or textual passages have been omitted.  For
                           example:
 
                           \newchapter{stylename}
                              .
                              .
                           \endchapter
 
                           The above means that additional controls and
                           (or) text could be included between the
                           \newchapter and \endchapter controls.
Each type of insert (table, figure, or graphic) is initially assigned to a
different insert class and has its own sequence counter.  Thus, tables are
numbered by using \tableno, figures by \figureno, and graphics by \graphno.
CapTeX allows the administrator to change these defaults by specifying a
different counter for each insert style.    Each insert style has a local
control that has the same name as its default counter; by assigning a new
counter to this control, the insert style will use that counter.
HELP
 Inserts cause special problems when doing any page layout.  They typically
occupy large blocks, and tend to be difficult to position so that pages are
always properly filled.  CapTeX provides two techniques to solve these
problems:  page breaking and floating.
 
Graphics can never be broken into smaller pieces, but figures and tables can.
These are broken into chunks, each chunk carrying along its header and
caption.  The first chunk is usually made to exactly fill the current page,
providing it meets whatever minimum size is specified via \min_table or
\min_figure (described later in this section under Tables and Figures,
 
respectively), and the style's own \minimum_size.  The remaining chunks,
except for the last, will always be full page size.
 
Since inserts are not really a part of the text, and can be referred to by
labels, it is sometimes possible to permit tables, figures, or graphics to
float to the top of the next page.  This can only happen if the insert
occupies one page or less.  If the insert is too large, it will be broken into
pages as described above.
 
Inserts will not float unnecessarily; inserts only float when there is not
enough room for them on the current page.  They usually only float to the next
page, but several inserts in quick succession may spill over onto several
pages.
 
The following controls are used for page breaking and floating:
\floatskip=skip
 
Is a skip quantity specifying the amount of space between floating inserts and
between the inserts and the text.  Defaults to 12 pt.  plus 4 pt.  minus 2 pt.
This is a global control.
\minimum_size={cdimen}
Determines the minimum height each insert may have.  This does not include
captions, space before captions, or headings or footings in tables.  It does
include any box rules or space.  \minimum_size is used only if it is greater
than the respective \min_table, \min_figure, or \min_graph global control.
Although cdimen does not permit percentages, the administrator can use
dimensions like .3\vsize, which are essentially the same thing.
\floating
 
When specified globally, tables, figures, and graphics permit floating unless
the particular style specifies otherwise.  Defined within a style definition,
\floating specifies that the style permits floating.  This is the default.
\no_floating
 
When specified globally, tables, figures, and graphics are not permitted to
float unless the particular style specifies otherwise.  Defined within a style
definition, \floating specifies that the style does not permit floating.
00003
00003
00001
00001
00002
00002
00004
00004
PAGE_BREAKING
 The following are miscellaneous global controls that affect page layout:
\asciidev
 
 Turns on ASCII mode, which prepares output for ASCII printers or text
screens. This control must be issued after the fonts have been defined;
it cannot be turned off.
\helpdev
 
 Turns on HELP mode, which prepares output for building HELP files.
\helpdev is a variation on \asciidev, but also has many other
effects. See Appendix  for further information.
\raggedbottom
 
 Disables the CapTeX default of setting all pages flush at the
bottom. With \raggedbottom enabled, CapTeX sets as much
material as possible on each page, the bottom of each page
depending on the contents.
\normalbottom
 
 Sets all pages flush at the bottom. If necessary, CapTeX stretches spacing
slightly between paragraphs. This is the opposite
of \raggedbottom, and is the default.
\centeronepage
 
Centers the current page (but no other pages) vertically. This could
be used in the \setup (see Initialization, in Section 3) for
a letter style, for example.
\centerpage
 
Centers all pages vertically (for slides, for example).
\dontcenterpages
 
Cancels vertical page centering. This is the default.
\raggedright
 
 Forces the document to be set ragged right, instead of flush left
and right. In effect, this makes the DSL control \ALB act like
\ALL.
\landscape
 
 Turns on landscape mode for the entire document. It must appear in
the CAPADMIN file, or at the beginning of the document. A document
must be set entirely in portrait or landscape orientation.
\boxpage
 
 Draws a box around each page (for slides, for example). The
thickness of the box rule is the \boxthickness dimension;
\pageframe determines the white space frame between the page
and the box.
\noboxpage
 
Disables boxing around each page. This is the default.
\pageframe=dimen
 
 Specifies how much white space surrounds a page when it is boxed via
\boxpage. \pageframe does not affect the size of the page in
any way, but instead adjusts the box drawn around the page. This is a
global dimension.
\setup={code}
 
 Provides CapTeX with code to execute before the document starts.
This code is usually used to specify initial formatting conditions,
such as \ALB, indents, and other items not explicitly provided
for in CapTeX. It permits the administrator to set up any initial
conditions that may be required.
\nochangebar
 
 This turns off changebars so that, even if the \CB controls are
within the manual, none will be displayed.  This option is most
useful when creating the final version of a manual.
00001
00010
00005
00006
00007
00002
00009
00011
00014
00004
00012
00003
00008
00013
The \page numbering control, described below, contains code to print the page
number.  By changing its contents, many different formats of page number can
be produced.  Changing fonts or sizes is not recommended in numbering
controls, because the same control is used in a variety of situations.
Usually such changes are made when the page number is actually used.  \page is
normally used not only in headers or footers to print the page number, but
also by table of contents entries, index entries, and cross-references.
\page={code}
 
Prints the current page number.  \page is usually redefined within chapter
styles to provide chapter-specific page numbers.  For example:
 
\page={\number\pageno}
\page={\number\chapno-\number\chappage}
 
The first example above produces a simple page number, while the second
produces the sectional (2-1, 2-2, etc.)  style of numbering.  \page can be
used anywhere, simply by referring to it.  Note the use of the \pageno
counter, which is prepared for printing by using the \number control.
 
When a page is output, it uses the current contents of the three page counters
mentioned above--\chapno, \pageno, and \chappage--to determine the current
page number.  \chapno is incremented only when a new chapter starts, but
\pageno and \chappage are incremented after each page, in preparation for the
next page.  If one of these two counters is negative, the page number will
decrease.  For example, while 2 increments to 3, -2 decrements to -3.
 
As mentioned in the previous subsection, counters are always reset to zero
before they are used.  This is desirable for chapter styles in which the first
page is always 1, as in the sectional (2-1, 3-1, etc.)  numbering style.  It
is not desirable, however, for a document style in which pages are numbered
consecutively (in Arabic numerals) across chapters, except for lower-case
Roman numerals in the front matter (preface, table of contents, etc.)
section.  In this case, the first page of the first chapter will be
incremented by the preceding number of pages in the front matter, so page
numbering must be specified in a different way in the style file to have that
chapter begin at page 1.
 
This is done by starting the document with negative page numbers, printed as
positive for the front matter, and then setting the first chapter to start at
page 1 and continue numbering consecutively across any following chapters.
The following changes should be made to the style file:
 1. Let \pageno=-1 in the global (prior to any structural definitions) \setup
    control in the style file.  The \setup control can contain other global
    specifications, such as alignment controls, in addition to \pageno=-1.
    For example:
    \setup={\NORMAL\RM\INB{0}\ALB\pageno=-1}
 2. Enter \page={\romn{-\pageno}} in the front matter chapter styles, such as
    FRONT and TOC in the system-supplied style file.  The minus sign ("-")
    before \pageno makes the page number positive again so that it will print
    in the front matter.
 3. Enter \setup={\ifnum \pageno<0 \pageno=1 \fi} (plus any other desired
    \setup code) as part of the specific chapter style definition.  This tells
    CapTeX that if the page number is less than 0, then set it to 1.  This
    ensures that the first page of the chapter following the front matter
    starts on page 1 and that page numbering continues consecutively through
    that chapter and across any following chapters.
00001
Page and device sizes are normally specified as part of the
FORMAT or DEVICE definition within CAPADMIN.
CapTeX checks the format dimensions specified against the device
limits, and makes sure that the final page dimensions will fit within
the physical device limits.  These dimensions are expected to define
paper stock or device limits, and should not take account of any
margins, which are defined below.
 
All the device and page size controls are global, and must be
specified within the scope of ADSL control files. The true page size
is calculated when all the control files have been read, which is
just after the DSL \IS control. Once DSL processing begins, any
changes to these controls are ignored. However, their values can still
be used.
 
The page and device size controls are as follows:
\dev_length=dimen
 
 Specifies the overall physical length of the page, as defined for
the device. The \dev_length dimension identifies limits for the
printer or the paper stock being used.
\dev_width=dimen
 
 Specifies the overall physical width of the page, as defined for the
device. The \dev_width dimension identifies limits for the printer
or the paper stock being used.
\fmt_length=dimen
 
Specifies the overall logical page length, as defined by the format
definition. This dimension must fit within the physical constraints
set by \dev_length.
\fmt_width=dimen
 
Specifies the overall physical page width, as defined by the format
definition. This dimension must fit within the physical constraints
set by \dev_width.
\fmt_top=dimen
 
Is the top margin, specifying the amount of white space to remain
at the top of the page before encountering text or headers.
\fmt_bottom=dimen
 
Is the bottom margin, specifying the amount of white space to remain
at the bottom of the page after the last occurrence of text or footers.
\fmt_right=dimen
 
Is the right margin, specifying the amount of white space to remain at
the right edge of the page. The right margin is absolute, in the sense
that the DSL \IN? controls do not affect this margin. In
\twosided page handling (described on page ), the
left and right margins alternate depending on whether the page number
is odd or even, so that the right margin becomes the outside edge and
the left margin becomes the binding edge, or vice versa.
\fmt_left=dimen
 
Is the left margin, specifying the amount of white space to remain at
the left edge of the page. The left margin is absolute, in the sense
that the DSL \IN? controls do not affect this margin. In
\twosided page handling (described on page ), the
left and right margins alternate depending on whether the page number
is odd or even, so that the right margin becomes the outside edge and
the left margin becomes the binding edge, or vice versa.
\footheight=dimen
 
Specifies the minimum height of the footer, which defines the space from
the baseline of the page to the baseline of the footer, unless the footer
is higher than \footheight, in which case it will extend beyond
the normal bottom of the page.
\headheight=dimen
 
Specifies the minimum height of the header, which defines the space from
the baseline of the header to the baseline of the first line on the
page, unless the header is too large, in which case it may
extend into the text on the page.
 
If the page (as defined by \fmt_length and \fmt_width) fits
within the physical page (as defined by \dev_length and
\dev_width), then the \fmt values are used; if not, the
device values replace them. Landscape mode automatically adjusts
the values by exchanging \fmt_length and \fmt_width.
 
The final text height of the page (stored in \pageheight) is
determined by subtracting first the vertical margins, \fmt_top
and \fmt_bottom, then the header and footer heights,
\headheight and \footheight, from the page height. The page
height is either \fmt_length or \dev_length, as described
earlier. This is illustrated by the following equation:
pageheight =
 
      fmt_length - (fmt_top + fmt_bottom) - (headerheight + footheight)
 
 The width available for text is kept in \pagewidth.  The
left and right page margins, \fmt_left and \fmt_right, are
subtracted from the page width as follows:
 
    page_width = fmt_width - (fmt_left + fmt_right)
00001
00002
00006
00008
00003
00007
00005
00004
00009
00010
Paragraph lists (usually called plists) are structures that provide separate
formatting for lists of items, where each item is a paragraph.  Plists can be
nested one within another to handle multilevel lists.  Each item can be given
a label, either textual, supplied by the writer, or numeric values, supplied
automatically by CapTeX.  Items are composed of one or more paragraphs.
Plists keep track of the current item number and nesting level, so that
enumerated or alphabetized lists are produced automatically.
 
Plists format an entire list using specifications different from those defined
for normal text.  They also put spacing around the list to separate it from
the surrounding text.  Special spacing also applies between items, where it
replaces the regular interparagraph spacing.
 
The controls used in the paragraph list setup are as follows:
\plist_default={name}
Defines the default paragraph list style to be used if no other style is
specified by the DSL \PL control.
\beginlists
 
Begins a set of paragraph lists.  Local plist controls can be used to provide
defaults to all plist styles.
\newlist{name}
 
Begins a new paragraph list style.
\endlists
 
Ends paragraph list style definitions.
 
The following local controls for each paragraph list style determine the
layout of the paragraphs within the list:
Spacing
 
The common spacing controls \space_before and \space_after provide spacing
before and after each paragraph list.  Common controls for structures are
described under COMMON_CONTROLS.
\left_indent={cdimen}
 
Specifies an additional amount of indention from the current left margin.
This control is basically equivalent to the DSL control \INL{+cdimen}.
\right_indent={cdimen}
 
Specifies an additional amount of indention from the current right margin.
This control is basically equivalent to the DSL control \INR{+cdimen}.
\undent_size={cdimen}
 
Specifies the amount a label extends into the left margin.  This is also
called reverse indention.
\setup={code}
 
Is used to set the basic layout parameters for the list.  This might involve
changing fonts, alignment, and more.  When the plist is ended, all parameters
return to their previous state.
\intro={code}
 
Provides code that can be used by \title to format the label.
\title={code}
 
Is used to generate the item label.  Each DSL \PI control causes \title to be
executed to produce a label.  Plists expect a label to be contained entirely
on one line and make no provisions for longer labels.
\label_space={cdimen}
 
Defines vertical space to be inserted after an item label.  Paragraph lists
where the item continues on the same line as the label should set this control
to empty (that is, {}).
\item_space={cdimen}
 
Defines the vertical spacing to be added between items.  \item_space replaces
the regular paragraph spacing.
\help={code}
 
Provides default HELP controls to be applied to each list item.  These
controls are honored only if \helpmode is on.
 
\plist_default={DEFAULT}
 
\beginlists
   \space_before={1}
   \space_after={0.6}
   \item_space={2}
   \left_indent={0}
   \right_indent={0}
   \undent_size={0}
   \intro={}
   \title={\piname}
   \setup={\parindent=0pt\parskip=6pt plus 1pt}
 
\newlist{DEFAULT}
   \synonym={ST}
 
\newlist{ARABIC}
   \synonym={AR}
   \left_indent={4}
   \undent_size={4}
   \title={\ALR{\number\curitem}.\ \piname}
 
\newlist{DESCRIBE}
   \synonym={DE}
   \left_indent={4}
   \undent_size={4}
   \title={\BF{\piname}\ }
 
\endlists
 
The preceding figure shows a sample of paragraph list definitions.  The
\beginlists control in this example starts a new set of paragraph list
definitions, followed by the controls common to all paragraph list styles.
The \newlist controls each begin defining a new style, and are followed by the
controls specific to those styles.  Any number of paragraph list styles can be
defined here.  The \endlists control ends this set of paragraph list
definitions.
00002
00004
00014
00010
00013
00012
00006
00003
00001
00007
00009
00005
00011
00008
The parameters for ADSL controls can be specified directly or can
be the result of expanding other macros or calculations, in which
case it is necessary to take into account the point at which the
expansion actually occurs.
 
The different types of parameters are as follows:
code        A code segment, which is a combination of text and ADSL,
DSL, and possibly TeX controls. Code segments are similar to macros,
except that CapTeX uses them in a predefined way. Code segments must be
complete, with braces properly nested.
 
Example:
 \title={\LARGE\BF\into\ \lhtitle}
num        A number, which is an optionally signed integer. Numbers
are used primarily with counters.
 
Example:
 \newlevel 1
dimen        A dimension, which is an optionally signed real number,
followed by a unit of measure. CapTeX understands the traditional
units of measure (points and picas) for printers in English-speaking
countries, as well as their European versions, and also understands
inches and metric units. Units of measure are abbreviated to two
characters, as shown in
 the following table.
 
                       pt  printer's point
 
                       pc  pica (1pc = 12pt)
 
                       in  inch (1in = 72.27pt)
 
                       bp  big point(72bp = 1in)
 
                       cm  centimeter (2.54cm = 1in)
 
                       mm  millimeter (10mm = 1cm)
 
                       dd  didot point (1157dd = 1238pt)
 
                       cc  cicero (1cc = 12dd)
 
                       sp  scaled point (65536sp = 1pt)
 
Example:
 \boxthickness=4pt
Another possibility for dimen is to supply a dimension or skip
register name, possibly with a multiplication factor. In this case,
the value of that dimension register is used, multiplied by the
factor. If a skip register is specified, only its dimension is used.
Example:
 \boxthickness=.15\baselineskip
cdimen        A CapTeX dimension, which is a superset of dimen.
cdimen handles everything in the same way as dimen, but also
accepts numbers without any unit of measure specified. In this case,
the current value of \ACH is used as the unit of measure for
vertical dimensions, and \ACW is used for horizontal dimensions.
 
Example:
 \space_before={5}
skip        A skip value, which is also similar to dimen, but
in addition to the dimension has stretch and shrink components.
The stretch component, denoted by the keyword plus, determines
how much the dimension can be enlarged if needed, while the shrink
component, denoted by the keyword minus, determines the amount
the dimension can be reduced.
 
Example:
 \floatskip=12pt plus 3pt minus 2pt
name        A style name, which can use alphanumeric characters
plus the following from the printable symbol set: at sign (@),
underscore (_), and hyphen (-).
 
In general, any macros can be used to supply values for these
parameters, as long as they expand to the proper quantities. Many
ADSL controls refer to quantities specified as or derived from
the arguments to DSL controls. The text for titles or captions,
specification numbers, or other values may be required. CapTeX materializes
arguments to DSL controls in a control sequence formed
by using the escape character (\) followed by the argument
name. For example, the lhtitle parameter of the \Ln control
can be used as \lhtitle in the ADSL level head definitions. This
applies to all DSL structure controls, except \TP, where the
\title_map control provides alternate names for the arguments.
00004
00001
00003
00006
00002
00005
TEX_FONTS
Additional CAP information is presented in the following manuals:
 
CAP DSL Reference, Order No. HA27
CP-6 CAP User Guide, Order No. HA29
CP-6 CAP Administrator Guide, Order No. HA30
The following is an example of a typical font file.
 
%
% Font definitions for CAP manuals, B00
%
% This is the 12pt roman font file.
%
 
\baselineskip=13pt plus .5pt             % \baselineskip has a bit of
                                         % stretch.
 
\newfamily RM={cmr10|cmr7|cmr5}          %
\newfamily MIT={cmmi10|cmmi7|cmmi5}      % These are the
\newfamily MSY={cmsy10|cmsy7|cmsy5}      % font families
\newfamily MXT={cmex10}                  % used in the
\newfamily IT={cmti10}                   % CAP manual set.
\newfamily SL={cmsl10}                   %
\newfamily BF={cmbx10|cmbx7|cmbx5}       %
\newfamily TT={cmtt10}                   %
 
\newfamily SS={cmtt9}                    % small teletype font
\let\NO\RM                               % makes \NO same as \RM
 
\newsize NORMAL={\magstep1}              % normal size
\newsize LARGE={\magstep2}
\newsize CHAP={\magstep3}                % for chapter title lines
\newsize TITL={\magstep4}                % for the title page
\newsize SMALL={\magstep0}               % for footnotes
\Font APL={apl10}                        % for APL characters
 
\defaultfont=\RM                         % specifies the default font
\defaultsize=\NORMAL                     % specifies the default size
\literalfont=\TT                         % specifies literal font
 
\endfonts
 
%
% End of font definition file.
%
\whatmode     % Checks to make sure we haven't accidentally produced
              % any text that will appear in the output.
Spacing controls are used to specify the amount of extra space that needs to
be generated around an entire structure, or sometimes around a title.
Penalties are used so that initial spacing (\space_before) is always a good
place to break the page, while following spacing (\space_after) usually is
neutral.  Some structures have additional spacing controls for special
purposes, but they all act similarly.  Spacing controls use some form of the
\SP? controls, and thus have the same form of argument.  Spacing can be
negative, although this can cause overlapping text.  An empty argument, as in
\space_after={}, means that no space will be inserted, nor will any penalties.
Some cases where this is important are discussed in the description of level
heads.  Setting a space to zero, as in \space_after={0}, causes only the
penalties to be used; additional space is not inserted.  The spacing controls
are as follows:
\space_before={cdimen}
 
Specifies the amount of extra space to be added before the beginning of a
structure.  If no units are specified, this control acts exactly like \SPB, in
that it uses \bigskipamount as the default unit of measure.  \space_before is
always a good place to break a page.
\space_after={cdimen}
 
Specifies the amount of extra space to be added after a structure, or, in the
case of level heads, the amount of space to be inserted after the title.  This
is usually a neutral place to break the page, somewhat like a paragraph break.
If no unit of measure is specified, \space_after defaults to \smallskipamount,
just like \SPF.
For an example, type ?  .  Examples:
 
\space_before={3pt}
\space_after={2}
00002
00001
The following dimension or skip registers contain values used to
calculate the correct amount of spacing to use in various
circumstances.  These controls can be used anywhere, but are usually
stored in control files as part of the style definitions, where they
affect the entire document. However, they honor normal nesting
constructs, and can be changed within structures. Other, less
commonly used dimensions are described in Section .
\parskip=skip
 
Is a skip quantity that specifies the amount of extra vertical space
to be added between paragraphs. This can be modified within grouped
constructions, such as paragraph lists or other closed environments,
without affecting the rest of the document. Defaults to 0 pt.
\parindent=dimen
 
Specifies the amount of a space by which paragraphs are indented in
normal circumstances. Defaults to 20 pt.
\smallskipamount
 
Is a skip quantity that specifies the amount of space to be produced
by \SPF{1}.  It is usually set to one-half \SPB{1}. The
spacing produced by \SPF controls defaults to \smallskipamount
units if no other units of measure are specified.
\bigskipamount
 
Is a skip quantity that specifies the amount of space to be produced
by \SPB{1}. It is usually set to \ALS. The spacing produced
by \SPB controls defaults to \bigskipamount units if no other
units of measure are specified.
\forwardskipamount
 
Is a skip quantity that specifies the amount of forward space to be
produced by \SPH{1}. It is usually set to \ACS. The spacing
produced by \SPH controls defaults to \forwardskipamount
units if no other units of measure are specified.
\spaceskipamount
 
Is a dimension defining the size of a space for the DSL \IN?
and \UNL controls. It is usually set to \ACW.
00004
00005
00002
00001
00003
00006
Each control file consists of ADSL controls, interspersed with
comments, and possibly TeX and DSL controls. Blank lines are
ignored, unless they are found within certain controls.
 
When reading style files, certain characters have their normal
TeX meanings, as shown in
 the following table. In addition,
the at sign (@) and the underscore (_) become alphabetics
(except in math mode) so that they may be used in control sequence
names. In contrast, within normal document source, using DSL, only the
backslash (\), braces ({}), and tilde (~) have
special meanings.
 
        Character                 Meaning
 
            \      escape character, i.e., control sequence introducer
 
            {      begin group character
 
            }      end group character
 
            %      comment character
 
            $      math shift character
 
            &      alignment tab, used only in tables
 
            #      parameter introducer, alignment entry
 
            ^      superscript, used only in math mode
 
            _      subscript, used only math mode
 
            ~      tie character, an unbreakable space
 
For descriptions of the special uses of the hyphen, apostrophe
and accent grave, see Chapter 2 of the CAP DSL Reference (HA27).
 
Names of control sequences always begin with the escape character, the
backslash (\). They can be any length, and can contain upper-
or lower-case characters. Numbers are not permitted. The at sign
(@) and underscore (_) can also be used, but since they
can appear in control sequences only in ADSL, and not in DSL, they
should not be used in controls the writer is expected to use. On the
other hand, this is an effective way of creating controls that can
only be used in ADSL.
 
To print any of these special characters while in ADSL, the administrator
must use the explicit form, that is, the character preceded by the escape
character. For example, entering \$ prints as $ (the dollar
sign). The only exceptions are the circumflex (^) and tilde
(~), which are accents. In these cases, the accent should be
followed with empty braces, as in
\^{}, or literal mode, which is
invoked by the DSL \LT control, should be used. In literal mode, the
characters and text are printed exactly as entered in the source file; no
CAP processing is performed on them.
Special purpose fonts are used when a font is not available in all the sizes,
or when the font needs only a single size.  Since these fonts cannot scale
with size controls, they should not be used in areas where size changes may be
used, as in titles, captions, table of contents entries, or level headings.
 
Special fonts are defined with the \Font control, as follows:
\Font name={font specification}
 
Defines a font not belonging to a family.  This is used to access special
purpose fonts, as described above.  The font specification may contain a font
name followed by a size specification, as described in The TeXbook.
00001
The administrator, using ADSL, defines the structures that the writer
invokes with DSL controls.
 For more overview information, enter ? or ??, or enter
 
  HELP (ADSL) STRUCTURES_OVERVIEW TOPICS
TITLE_PAGE       The administrator controls the layout of the title page,
including
the position, spacing, and font style/size of the title page fields.
The writer supplies, via the DSL \TP control, the textual contents
of all variable fields.
TABLE_OF_CONTENTS       Tables of contents are generally formatted as
chapters; the headers,
footers, and other page layout parameters are determined by a chapter
style. A table of contents consists of one or more separate lists;
first, a list of chapters or sections, usually followed by lists of
other items, such as figures or tables. The administrator determines
what other list types there are, and what headings, if any, are to be
used for each type of list.
 
 Table of contents entries are compiled automatically by CAP, based
on the definitions of various structures.  The format and font
style/size of each type of table of contents entry is specified by
the administrator in the chapter, level head, figure, table, and
graphic definitions.
CHAPTERS      The chapter is the controlling element on which the format of a
document is based. Chapter styles determine the page layout of, and
are the highest-level structure within, CAP documents.
 
The effects of any format changes made by a chapter style or made
within the chapter are limited to that chapter. Document styles that
do not use chapters, such as letter or memo styles, get their page layout
definitions from the global parameter set, which acts like a chapter
containing the entire document.
 
Chapter styles determine the overall page layout parameters, such as
margins, headers, and footers. They also define the format and font
style/size of the chapter number and title, page numbering, and
various style elements, such as level headings and entries to the
table of contents.
 
Appendices, the table of contents, and the index are all considered
variants of chapters, as are front matter, such as a preface or an
introduction, or back matter, such as a bibliography or glossary.
LEVEL_HEADS       Level headings provide a structure in which a chapter (or
document)
is broken into numbered and/or titled sections. These are often
called topical headings or heads. CAP automatically numbers such
sections, if required. Up to 9 levels are permitted, each defined
individually.
 
 Level headings can be local to a chapter style, or can be declared
globally, to apply wherever no local level heads are specified.
The administrator controls the placement, font style/size, and
numbering of the level headings, as well as whether and in what
format the level headings are automatically entered in the table of
contents and index.
PARAGRAPH_LISTS       Paragraph lists, also called plists, provide a
convenient way of
formatting lists of items or paragraphs. Various numbering schemes
can be used, and list elements can also be labeled.
 
 The administrator can create a wide variety of paragraph lists. For
example, lists can be numbered, bulleted, or dashed; labels
(paragraph items) beginning a list can be defined in a variety of
font styles and sizes.
 
The administrator controls the placement of a paragraph list on a
page (the space before and after the regular text), space between
list items, indentation of list items, font style/size of the list
item labels, and the placement of the label relative to the list item
text.
INSERTS       Figures, graphics, and tables are all essentially the same type
of
structure, called inserts. Inserts have several properties
not shared by other structures: they may be automatically boxed,
they may have captions, and they may be permitted to float to the
next available page if they cannot fit on the current page.
 
Insert styles control the minimum size before breaking across pages,
minimum height, boxing, floating, space before and after regular
text, numbering (by section, for example), location and font
style/size of the caption, space between the insert and the caption,
and whether and in what format the caption is automatically entered
into the table of contents.
 
For figures, the administrator can provide code to provide a
particular layout, choosing, for example, the font style/size and
margins for the figure text.
 
Table styles have specific controls for vertical and horizontal rules
within the table, the position and size of the table cells, the
layout (spacing and rules) of the table heading, the space between
vertical rules and table text, and the space above and below table
rows. CapTeX provides different table types and ways of determining
column width, to accommodate table data ranging from single-line entries
that fit on one page to multiple-line, paragraphed entries that span
many pages.
EQUATIONS       TeX math mode is automatically enabled when the writer enters
an
equation via the \EQ control. For these displayed equations, the
administrator controls the placement on the page and the font style/size
of the equation and equation number.
FOOTNOTES      The administrator controls the font style/size of the footnote
text,
type and placement of the footnote marker (letter, number, or symbol),
footnote numbering, and length and thickness of the rule above the
footnote.
INDEX       CAP produces indexes automatically, from terms and subterms
specified in the document source. Indexes are produced in two
discrete phases: first, the terms and their page numbers are
collected and sorted; second, they are read back in, and the index is
formatted.
 
 During the first phase, each term has an associated index style,
which determines how that term and its page number will be
formatted. Entries that contain subterms may be permuted, that is,
cross-referenced, where the subterm is also indexed as a main term.
00003
00007
00008
00009
00006
00004
00005
00002
00001
Each of the major CAP structures consists of a set of variations, called
styles. There are chapter styles, table styles, index styles, etc.
Different chapter styles, for example, are used to create an
introduction, an index, or an appendix.
 
With the exception of the title page, structures are created in groups,
where each group is independent of other groups. Each group begins with
a \beginstructurename control and ends with an
\endstructurename control. Individual structure styles begin
with a \newstructurename control.
Initialization controls permit each structure to define its environment.  Many
structures permit two different kinds of initialization:  once before the
structure begins, thus affecting the title if there is one, and once again
just after the structure has begun, before any text is processed.  In either
case, initialization controls specify ADSL, DSL, and TeX code that will be
used to define the initial environment of the structure.
 
The initialization controls are as follows:
\startup={code}
 
Provides code that is executed at the very beginning of a structure.  This
usually occurs so early that even the passed parameters may not be set up.
Its primary use is to close earlier structures, like breaking to an odd page
in a new chapter.
\setup={code}
Provides code that is executed at the end of the structure opening, after
titles and such have been executed, and just before the regular text starts.
Its primary use is to set defaults for the structure, such as indentation,
fonts, interparagraph spacing, etc.
 
Example:
 
\startup={\ALB\INB{0}}
\setup={\ALC \parskip=10pt}
00002
00001
Most structures use some form of specification number to identify themselves.
In CapTeX, this includes chapters, level heads, inserts, equations, and
footnotes.  By default, CapTeX provides a single counter for each such
structure.  Counters can contain only integer numbers, but can be added,
multiplied, etc.
 
When the writer specifies a value in a DSL control for a specification number,
one of the following actions takes place:
 
{}(an empty counter) increments the current value by 1.
 
{*}(an asterisk) does not change the counter and does not print the \intro
sequence or the number; no automatic table of contents entries or indexes are
produced.
 
{num}(a number) sets the counter to that number.
 
{+num} or {-num}increments or decrements the counter by num.
 
Blanks are permitted before or after the number, but not between the digits.
Counters are always incremented or set before they are used; therefore they
are always reset to zero.  This is handled automatically by CapTeX, based on
the \numbering control, which specifies when each counter should be reset.
The following table shows all the counters automatically defined by CapTeX.
Administrators may define additional counters and use them as easily as the
predefined counters.
 
                    Counter                 Use
                  -------------------------------------------
                  \chapno      chapter number
 
                  \pageno      page number
 
                  \chappage    page-within-chapter number
 
                  \figureno    figure number
 
                  \tableno     table number
 
                  \chunkno     broken table chunk number
 
                  \graphno     graphics number
 
                  \equationno  equation number
 
                  \footno      footnote number
 
                  \curitem     current item number in plist
 
                  \curpllevel  current plist level
 
Counters by themselves are not sufficient to describe a full specification
number, which is often composed of several parts or may be in some other form,
alphabetic instead of numeric for appendices, for example.  Consequently,
counters are often used indirectly, through a numbering control sequence.
Each structure that uses a counter also has a specific numbering control.
Numbering controls are actually macros that print counters; the administrator
may use them anywhere simply by referring to them.
STRUCTURE_DEFINITIONS
The exact typography of all the structural elements that can be
used in a document is specified in style control files provided by
the administrator. These files contain ADSL controls that define
the specific structures available to the CAP user. Structures can
be defined in more than one style; the user therefore selects a
particular structure in a specific style with the DSL controls.
 
Note that the term "style" as used here has a twofold meaning.
The style control files contain all of the structures that
constitute a specific document style, such as might be used in
the manuals for a particular software program. Within the control
files, the individual structures have defined styles from which
the user can choose. For example, paragraph lists could be available
in numbered styles, bulleted styles, and so forth; level headings
could be defined to several levels, such as first to fifth.
 
The ADSL controls give the administrator a great deal of latitude
in defining structures that meet the particular needs of the user
site. By defining all of the necessary structures in advance, the
administrator can eliminate the need for writers to also be layout
artists. Style files also help the administrator enforce documentation
standards. When the elements of a style are contained in a file, it
is easy for writers to use standard constructs, and stylistic changes
can be effected without having to make alterations throughout the
entire document data base.
Each style file is a collection of ADSL controls. While there are
conventions for structure definitions within style files, there
are no other restrictions. Note that within the style files some
characters have special meanings, as shown in the table
 under the topic SPECIAL_CHARACTERS .
The most important of these is the percent
sign (%), which is the "comment" character for ADSL. The
percent sign and everything that follows it on the line are treated
as comments. This includes the carriage return at the end of the
line.
 
Style files can be considered as sequences of comments, global
controls, and structure definitions. Comments (preceded by a percent
sign) can appear anywhere, even in the middle of code sequences.
Global controls cannot appear within structure definitions.
 
 This section describes the ADSL controls that determine the
dimensions and layout of the page, along with the more basic
formatting style elements. Later sections in this manual describe
the different structures.
All structures except level heads (which do not have a style name) can use
synonyms to provide for alternate names.  Style names cannot be abbreviated,
and they are case-sensitive, so often there is a need for a shorter name.  The
writer can then use the synonym just like the original name in DSL controls.
Synonyms are specified with the following control:
\synonym={name}
 
Is used with all structure types and provides alternate names by which a style
can be called.  Synonyms follow the same rules as style names and need be
unique only to the structure.  If ever they are not, CapTeX always retains the
last definition.
00001
Each style is identified by a style name and consists of a series of
controls that define the behavior of that style.
 
Style names for any structure type can be of any length, upper- or
lower-case, or mixed. Upper- and lower-case are not the same, that is,
there are no caseless names. The same style name can be used in
different structure types, but can only appear once for the same
structure. Thus, there can be a chapter style called MODULE and a
paragraph list style called the same, but if the chapter style
MODULE is defined twice, only one MODULE chapter style will
exist, containing only the last definition.
 
For each type of structure, CapTeX always creates a default style
called DEFAULT. This style is used when all style matching
attempts fail, and can be redefined by the administrator. The
built-in DEFAULT styles are necessarily minimal; they usually
provide just enough to permit the DSL controls to function.
Subfiles are used within style files to load subroutines common to several
style files.  For example, subfiles are used within the system-supplied LETTER
and MEMO styles, to load common portions.  A subfile has the extension SPR.
The following control is used with subfiles:
\subfile{filename}
 
Loads a subfile, such as SGML:SPR or COMMLTR:SPR, containing common
subroutines to be used within style files.  \subfile automatically adds the
SPR extension so a file can be moved, for example, from a PC (where the
extension is .SPR) to CP-6 (where the extension is :SPR), without having to
change the period (.)  to a colon (:).  Thus, entering \subfile{SGML} would
load SGML:SPR.
00001
Subsets provide a mechanism for storing several variations of a
document in a single source file and interactively selecting the
variation to be formatted and printed. The values assigned to these
controls are referenced by the DSL \SB control, which then
selects a subset to print.
 
 There are two ADSL controls for subsets, as follows. These controls
are normally set by the CAP interactive menus.
\use_subset={name}
 
Specifies a subset to be included in the current formatting run. This
control may be used several times to select several subsets. Subset
names not encountered in the text are ignored.
\allsubsets={code}
 
 Specifies code used to print each subset when the ALL subset is
chosen. The parameters \sbtype and \sbtext contain the
information from the \SB control. For example:
 
\allsubsets={\BF{ [\sbtype: \IT{\sbtext\unskip\/}] }}
 
Subsets are multiway switches, similar to CASE statements
in traditional programming languages. If the subset ALL
is selected in any \use_subset control (even if others are also
selected), the entire list of subsets is printed, using the code
supplied by \allsubsets. Otherwise, the last match in any
\SB control will be used, or if there is no match, the text
supplied with the "else" (\SB{}) subset. Subset names are
case-sensitive, so ALL must be specified in upper-case letters.
 For more information about \SB, enter
 
  HELP (DSL) SB
00002
00001
CAP tables provide a formal structure within which to build and format tabular
material.  Tables are composed of cells organized into a column and row
format.  Tables may also have a header, a special set of cells used to
identify the contents of the table.  Tables can be very large, and when they
are broken across pages, the header is repeated on each page.  The table
header is completely distinct from the page headers and footers.
 
CapTeX provides facilities for two different types of tables, large and small.
Large tables have no limit on size, but all column widths must be fixed when
the table begins.  Small tables are limited in size by the memory CapTeX has
available.  Small tables can automatically adjust column widths to the size of
the widest cell.
The following global controls are used to define table styles:
\min_table={size}
 
Specifies the minimum size of the first piece of a table that needs to be
broken between pages.  See \minimum_size  under the topic PAGE_BREAKING.
Defaults to .15\vsize.
\table_default={name}
 
Provides the name of the default table style to be used when no style is
specified on the DSL \TB control.
\begintables
 
Begins a set of table definitions.
\newtable{name}
 
Begins a new table style definition.
\endtables
 
Ends a set of table definitions.
 
Tables have a larger and more varied set of controls than any other CapTeX
structure.  In addition to the common insert controls, tables also have
constructs to define columnar organization, headers, and the use of horizontal
and vertical rules.
 
Controls local to tables include all the common controls described  under the
topic INSERTS_COMMON_CONTROLS. In addition to the common controls, the
following local controls are specific to tables:
\tbnum={code}
 
Specifies code to format the table number.  This control can be referred to
elsewhere to materialize the formatted table number.
\tableno=counter
 
Specifies a new counter to be used with a table style.
\template={code}
 
Specifies the horizontal template for the table.  It determines the columnar
structure of the table.  This template is restricted to the \TV, \SPH, \TI,
\TC, and \TE controls.
\header={code}
 
Defines code to format the table header.  Only controls that are legal in
tables may be used within code, but it can contain several rows.
\tbheading
 
Is a read-only control used to materialize the argument of the DSL \TH
control.  \tbheading can only be used with the \header control.
\rulesep={cdimen}
 
Defines the distance between a vertical rule and whatever is next to it.
\doublesep={cdimen}
 
Specifies the distance by which two adjacent vertical rules will be separated.
\horizontalrules
 
Specifies that a rule is to be drawn after a row ending with a DSL \TE
control.  The rule is not drawn if a DSL \TX control is used.  Horizontal
rules are also automatically drawn above and below the table header and
footer, even if they are empty.
\no_horizontalrules
 
Specifies that horizontal rules will not be drawn between rows of a table.
\aboverow={cdimen}
 
Specifies extra space to be inserted above each row of a table.  This is used
to open up rows or to add space below horizontal rules.
\belowrow={cdimen}
 
Specifies extra space to be added below each row of a table.  This is used to
open up rows or to add space above horizontal rules.
\large_table
 
Specifies a table with fixed column width; the table has to have its column
width determined when the table starts, and can be as large as desired.  The
table cell contents can be paragraphed.
\small_table
 
Specifies a table with variable column width (the columns can depend on the
width of the data in them); the entire table has to go into memory before
formatting so the width of each column can be determined.  Thus, the table
cannot be as big as a table defined with \large_table.
00015
00003
00016
00012
00005
00009
00013
00017
00001
00004
00014
00011
00018
00007
00002
00010
00006
00008
A table of contents requires two distinct operations:  first, all the entries
are collected as the document is being formatted; second, they are printed.
This means that either two passes are required, or the table of contents must
be printed after the rest of the document.  \finalmode and \draftmode,
described previously, determine where the table of contents appears.  If
\draftmode is used, the table of contents will still have its true page
numbers and can be manually collated.
 
CapTeX automatically handles the first phase, collecting entries for the table
of contents, by having each major structure define its entry.  Thus, each
chapter style and level head can provide an entry to the main table of
contents, and inserts can provide entries to secondary lists, which are
collected separately.  These entries are temporarily written to auxiliary
files, to be read back when the table of contents is formatted.  Each entry is
defined in structure declarations via the \contents control
 
The second phase is printing the table of contents, which is treated as a
chapter.  The administrator selects a chapter style for the table of contents,
which then defines headers and footers, page numbering, and other layout
parameters.  Within the confines of this chapter style, the \toc control
causes the different entry files to be read and formatted.  CapTeX uses
separate table of contents entry files for the main list, which contains
chapters and level heads, and for each insert class.  When an insert class has
no entries, no list is produced, nor is there a heading for that list.
The following figure shows a sample table of contents definition.
 
\toc_style={TOC}
\toc={\list_toc
  \list_lfg {\SPB{3} \CHAP\BF\ALC List of Figures \BRX\SPB{2}}
  \list_ltb {\SPB{3} \CHAP\BF\ALC List of Tables  \BRX\SPB{2}}
  \list_lgr {\SPB{3} \CHAP\BF\ALC List of Graphics \BRX\SPB{2}}}
 
The following controls are used to generate entries and print the table of
contents.  They are all global controls.
\tocing
 
Specifies that table of contents entries are to be collected.  The document
must still use a DSL \TOC control to produce a table of contents.
\no_tocing
 
Specifies that no entries are to be collected for the table of contents.  The
\TOC control is not affected.
\toc_style={name}
 
Specifies the chapter style used to format the table of contents.
\toc={code}
 
Specifies code to format the full table of contents.  To read table of
contents files, \list_toc or \list_class controls must be used.
\list_toc
 
Initiates reading of the main table of contents file.  No heading, other than
that supplied by the surrounding chapter style, is provided.
\list_class{code}
 
Reads the contents file for an insert class.  The class parameter defines the
insert type, such as figure, table, or graphic.  The code parameter defines
the heading to be used for that section, and may include controls such as
\BRP, \SP?, and \AL?.  Formatting controls in code affect only the heading.
00006
00005
00002
00004
00001
00003
The table of contents process consists of two phases:  first, the table of
contents entries need to be collected; second, they are included in the
document and printed.    The ADSL HELP topic TABLE_OF_CONTENTS describes the
second process, constructing and printing the table of contents; this  topic
describes the entry gathering phase.  Each chapter style, level head, and
insert style automatically makes entries into the table of contents via the
\contents control.
 
Table of contents entries and indexes are only written if the structure's
specification number, as specified in the DSL control that called it, is not
an asterisk (*).  Otherwise, they are ignored.  The control for the contents
is:
\contents={code}
 
Defines the code for the table of contents.  This code is written to a table
of contents file when the page is output.  Page numbers are not expanded until
then.  If empty, that is, \contents={}, no table of contents entry is made.
 
A table of contents entry is a delayed macro; even though it is used when a
level head is called, for example, it is only written to the table of contents
file when that page is actually complete.  This happens at basically the same
time as the page headers and footers are built.  Because the page number is
not known until then, the code supplied to format the entry is only partially
expanded when it is first issued.  Page numbers are always held back until the
page is output, so they are always accurate.
00001
TeX fonts are designed so that each family has fonts in three different point
sizes, and the size control contributes a single magnification to provide a
magnified font for each of \textfont, \scriptfont, and \scriptscriptfont.
 
For example:
 
\newfamily NO={cmr10|cmr7|cmr5}
\newsize LARGE={\magstep1}
 
assigns, respectively, cmr10 to the basic font, cmr7 to the
subscript/superscript font, and cmr5 to the subsubscript font.  At size
\LARGE, each of these fonts will be scaled by a factor of 1.2.
 
PostScript fonts are organized in the other direction; each family has a
single font, but the size specification provides three point sizes, so that
the final result is the same.
 
For example:
 
\newfamily NO={psrm}
\newsize LARGE={12pt|8.4pt|6pt}
 
This example provides the same sized fonts from PostScript fonts as the
previous example, which used TeX fonts.
CAP is based on the TeX formatter, which is a portable, commodity
product. CAP's unique capabilities are provided by the CapTeX macro
package, which defines the DSL and ADSL controls used by CAP. CapTeX makes TeX
easier to use for the average writer.
 
Most CAP format options and several device options are applied during
TeX formatting. CAP builds JCL to apply these options and invoke
the programs needed to produce a document. The formatting JCL creates
a small temporary file that comprises the logical document that is
actually input to TeX. Most format options are translated into
CapTeX controls in this temporary file. Other options that specify
names of ADSL control files cause those files to be included in the
logical document. All of these controls appear at the start of the
logical document in order to establish the typographical style for
the document. They are followed by controls to include the DSL source
files that constitute the document itself.
 
Note that most TeX controls can be included in document source files
or ADSL control files and will function as expected during formatting.
The CAP administrator manages the CAP system at a particular CAP user
site. There are two major functions that constitute the administrator's
role.
 
One is the control and customization of the CAP user environment. This
includes functions such as input/output device management, account
definition, file maintenance, naming conventions, security, and
definition of document formats with the CAPADMIN program. These
functions are described in detail in the CP-6 CAP Administrator
Guide (HA30).
 
The other is the creation of document structures and control files
with ADSL, as described in this manual. This includes the maintenance
and modification of the system-supplied structures and control files,
as well as analysis of site-specific document styles to create new
structures and control files.
 
To manage the CAP system, the administrator should have an understanding
of text processing, typesetting, and document design, and be familiar
with the CAP Document Structuring Language (DSL), as described in
the CAP DSL Reference Manual (HA27).
 
Also desirable for the administrator are an understanding of programming
concepts and some familiarity with the TeX formatter.
Chapters and level heads usually print titles, while figures, tables,
graphics, and equations print captions.  Titles and captions are handled in
exactly the same way, so although this discussion refers mainly to titles, it
applies equally to captions.
 
A title is a composite object, in that it must bring together several
different parts depending on the circumstances.  There are three parts
involved, but only one of them is required.  They are as follows:
 1. The introduction, which is usually a word or term like "Table" or
    "Chapter", and serves to identify the type of structure.
 2. The specification number, which identifies the structure within its type,
    and can be printed in a variety of formats.  In the case of level heads,
    it may involve printing a series of of numbers, as in "1.2.5".  The
    specification number is usually provided automatically by CapTeX or
    manually by the DSL structure controls.
 3. The name of the structure, which is always provided by the DSL structure
    control.  It is usually a short description.
 
Titles for structures are defined as code that brings together the three parts
and specifies how they are to appear.  Since DSL structure controls allow the
use of an asterisk (*) in specification number fields to specify that the
structure not be numbered, it is necessary for titles to be defined so that
this is possible.  The \intro control, described below, defines that part of
the title that is removable when an asterisk (*) is specified.
 
The following controls define titles and captions:
\intro={code}
 
Defines code to be executed to produce introductory text, like "Chapter 7" or
"Section 15", which is independent of the actual title.  This introductory
text can be turned off by specifying an asterisk (*) in the structure
specification number field.  The \intro control combines the introductory term
(if there is one) with the specification number.
\title={code}
 
Defines code to produce the title text for chapters and level heads.  code is
executed as a group; thus any changes made within \title will not carry into
the following text.  This code may include spacing controls, font changes, the
\intro control to print the introduction, and the title text supplied by the
DSL \CH or \Ln controls.
\caption={code}
 
Defines code to produce the caption text for inserts (tables, figures, and
graphics) and equations.  code is executed as a group; thus any changes made
within \caption will not carry into the following text.  This code may include
font changes, the \intro control to print the introduction, and the title text
supplied by the DSL structure controls \TB, \FG, \GR, or \EQ.
\next_caption={code}
 
Defines code to produce a second caption text for tables and figures that are
broken across several pages.  It permits different captions to be used for the
first and last segments.  code is executed as a group, thus any changes made
within \next_caption will not carry into the following text.  This code may
include spacing controls, font changes, the \intro control to print the
introduction, and the title text supplied by the DSL \TB or \FG controls.
00003
00001
00004
00002
Title pages are constructed automatically when the DSL \TP control is
encountered in the source document.  Document styles define title pages by
providing code to format the arguments presented to the \TP control.  Unlike
other DSL structure controls, the nine parameters of \TP have no set meaning.
The administrator determines, for each document style, what these parameters
mean and how they will be arranged on the page.  Using \title_map, the
administrator assigns control sequence names to each parameter the title page
will use.  The code used to format the title page then refers to these control
sequences to get the title information.
The title page controls are as follows:
\title_page={code}
 
Provides code to format the title page.  This code must produce only a single
page and will be vertically centered on the page.  If math mode is used on the
title page, then math mode must be on when \title_page is defined.
\title_map{name1|.. .|name}
 
Permits the administrator to assign specific names to the parameters of the
DSL \TP control.  The names must contain only alphabetic characters; names are
case-sensitive, and no blanks are permitted.  Control sequence names are
assigned in the same order in which they appear.
 
The following figure shows a sample of a title page definition.
 
\title_map{TITLE|AUTHOR|IDENTIFIER|DATER|COPYRIGHT}
\title_page={\ALC
             \TITL{\TITLE}
             \SPB
             \CHAP{\AUTHOR}
             \SPB{2}
             \IT{\IDENTIFIER}
             \SPB{2}
             \IT{\DATER}
             \SPB
             Copyright \ \copyright\ \COPYRIGHT}
00002
00001
The error messages created can be used within the administrator's own macros,
simply by referring to them and providing the correct number of parameters.
For example, if the administrator needed to use the \err@nostyle message from
the preceding examples, it would be referred to as:
 
\err@nostyle{badstylename}
 
Each parameter is enclosed in a separate set of braces, if there are more than
one.
