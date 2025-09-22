A CAP document source file contains two kinds of information:  the text and
Document Structuring Language (DSL) controls.    For a list of DSL controls,
type
 
HELP (DSL) CONTROL_SUMMARY
 
For information about a particular DSL control, type
 
HELP (DSL) control
 
where control is a 2- or 3-character control name entered without the
beginning \ character.  A display of the syntax of the DSL control appears.
For additional information on this control, enter ?  or ??.
 
For information about a particular aspect of a DSL control, type
 
HELP (DSL) control subtopic
 
where control is the name of a DSL control and subtopic may be one of the
following:  PARAMETERS, DESCRIPTION, EXAMPLES, ADMINISTRATION, DEFAULTS.
NOTE: Because of the limitations of ASCII output devices, examples of math
mode, fonts, tables, and special characters are not truly represented.
However, those examples that may still be of interest appear in this HELP
facility for the information they provide.  Please refer to the CAP DSL
Reference Manual (HA27) for definitive examples.
CAP DSL Reference - HA27-00
*************************************************************************
*
* Copyright (c) Bull HN Information Systems Inc., 1994
*
*************************************************************************
Syntax:
\*{comment}
Parameters:
 
comment  specifies any text or instructions to be included in the source file
    but ignored during document formatting.
Description:
The \* control creates comments in a source file.  Comments are completely
invisible in the formatted document.
 
Instructions can be passed to preprocessors and auxiliary processors within
comments.
 
Braces ({}) can be nested inside comments, as long as each opening brace has a
matching closing brace.
 
Comments can appear inside tables in a source file, but should be placed
before the TE or TX control, so that the comment is in a table cell rather
than between table rows.
Example:
 
\*{I wrote this last Tuesday.}
This was what I wrote, when I sat down to write. \*{After that, I
planned on writing more.}
 
When formatted, the above appears as:
 
This was what I wrote, when I sat down to write.
00002
00003
00001
Abort messages generally contain the phrase:
 
PASCAL RUNTIME ERROR.
Notify the administrator immediately if such a message is encountered.
TeX provides control sequences for the most commonly used accents.  Entering
an accent control sequence before a letter will print the accent over (or
under) the letter when the document is formatted.
 
For example:
 
                      Accent Type        Enter Prints As
 
                      Grave               \`a  a
 
                      Acute               \'a  a
 
                      Circumflex ("hat")  \^a  a
 
                      Umlaut              \"a  a
 
                      Tilde               \~a  a
 
                      Cedilla             \c a a
 
Note that the last of these sequences is a control word which requires a space
following it; the rest are control symbols which do not require following
spaces.  Additional accents are described in The TeXbook.
DSL also provides for change marks, multiple columns, and subsets, as
described below.  The controls that activate these capabilities are described
in detail in Section 3.
Knuth, Donald E., Computers and Typesetting, Volumes A-E (Addison
Wesley, Massachusetts, 1986). These volumes are as follows:
 
A.  The TeX book
B.  TeX: The Program
C.  The METAFONTbook
D.  METAFONT: The Program
E.  Computer Modern Typefaces
Syntax:
\AL{altype}
 
The altype parameter and the braces are optional.
Parameters:
 
altype  specifies the type of alignment to be applied to subsequent text, as
    follows:
 
    L   indicates left-aligned.  Areas in fill mode will be ragged right.
        This is the default if altype is not specified.
 
    R   indicates right-aligned.  Areas in fill mode will be ragged left.
 
    C   indicates centered-aligned.  Areas both in and out of fill mode
        will be ragged right and ragged left.
 
    B   indicates right- and left-justified.  Areas in fill mode will be
        right- and left-justified.
Description:
AL defines the type of line justification to be applied to passages of
formatted text.
Examples:
 
\ALB
This is a test of alignment mode. These paragraphs will be aligned
differently because different \TT{AL} controls have been applied to
them. Note the considerable differences in alignment when the paragraphs
are formatted.
 
\ALR
This is a test of alignment mode. These paragraphs will be aligned
differently because different \TT{AL} controls have been applied to
them. Note the considerable differences in alignment when the paragraphs
are formatted.
 
\ALL
This is a test of alignment mode. These paragraphs will be aligned
differently because different \TT{AL} controls have been applied to
them. Note the considerable differences in alignment when the paragraphs
are formatted.
 
\ALC
This is a test of alignment mode. These paragraphs will be aligned
differently because different \TT{AL} controls have been applied to
them. Note the considerable differences in alignment when the paragraphs
are formatted.
 
The above, when formatted, appears as follows:
 
This is a test of alignment mode.  These paragraphs will be aligned
differently because different AL controls have been applied to them.  Note the
considerable differences in alignment when the paragraphs are formatted.
 
           This is a test of alignment mode.  These paragraphs will be aligned
differently because different AL controls have been applied to them.  Note the
      considerable differences in alignment when the paragraphs are formatted.
 
This is a test of alignment mode.  These paragraphs will be aligned
differently because different AL controls have been applied to them.  Note the
considerable differences in alignment when the paragraphs are formatted.
 
      This is a test of alignment mode.  These paragraphs will be aligned
differently because different AL controls have been applied to them.  Note the
   considerable differences in alignment when the paragraphs are formatted.
00002
00003
00001
AL
AL
AL
AL
AL
CH
FF
Like space characters, blank lines are treated by DSL as delimiters.  Blank
lines are used by DSL as paragraph delimiters rather than for vertical
positioning.  Multiple blank lines are compressed to a single blank line when
formatted.
 
A paragraph delimiter is treated as a logical breakpoint for the formatter.
The blank line tells DSL that the current paragraph has ended and a new one is
to begin.
 
Blank lines are normally not required before or after structural controls for
chapter titles, level heads, tables, figures, graphics, and paragraph lists,
nor are they required between paragraph list items.  The administrator-defined
styles for these structures usually include the delimiting blank lines.  The
writer can add blank lines in the source file to make it easier to read; these
blanks will not be added to the blank lines defined around the structures by
the administrator.
 
An exception to the above is when the document style uses indented paragraphs.
In this case, a blank line should not be included between a level head and the
paragraph immediately following it.
 
The \SP control can be used to insert a required amount of vertical space.
(\SPB causes a paragraph break; \SPH does not.)
Syntax:
\BR{brtype}
 
The brtype parameter and the braces are optional.
Parameters:
 
brtype  specifies the type of break to be generated, as follows:
 
    X   indicates a bad place to break a page.  This parameter holds two
        structures together so that they appear on the same page.
 
    B   indicates a good place to break a page.  This is the default if
        brtype is not specified.
 
    N   indicates an even better place to break a page than BRB.
 
    P   means that a page must be broken here.
 
    O   means that a page must be broken here and continued on the next
        odd page number.  The intervening (even) page prints with only
        header and footer.
 
    E   means that a page must be broken here and continued on the next
        even page number.  The intervening (odd) page prints with only
        header and footer.
 
    L   means that a line must be broken here.
 
    C   in multicolumn mode, means that a column must be broken here.  BRC
        works only if the administrator has specified snaking text columns
        for multicolumn mode.  See the CL control description for more
        information.
Description:
BR performs page and line breaks.  This allows the writer to change some of
the pagination normally performed automatically by CAP.
 
CAP always chooses what it considers to be the most desirable place to break a
page.  The writer uses the BRB and BRN controls as suggestions to CAP as to
what the most desirable place to break might be.  For example, BRB could be
used to indicate a page break after an item in a list; BRN could be used to
indicate a page break before or after the entire list.
Examples:
 
\BRP
 
means break to the next page.
 
\BRX
 
means do not break the page here.
 
This is a \BRL broken line.
 
When formatted, the above appears as:
 
This is a
broken line.
00002
00003
00001
BR
BR
FORMATTING_BREAK
BR
BR
BR
BR
BR
Syntax:
 
\CB{cbtype}
   .
textual data
   .
\CB
 
The cbtype parameter and the braces are optional.
Parameters:
 
cbtype  specifies the type of changed area to be delimited, as follows:
 
    A   indicates an area that has been added.
 
    D   indicates an area that has been deleted.
 
    M   indicates an area that has been modified.
 
    F   marks the end of the change area.  This is the default if cbtype
        is not specified.  F is not required with the closing CB.
Description:
CB draws change (add or modify) and deletion marks in the right margin of the
page, to identify material that has been added, modified, or deleted.
Administration:
 
The administrator is responsible for the style and placement of the change and
deletion marks.
Defaults:
 
The system-supplied add or modify mark is a vertical bar; the deletion mark is
a horizontal bar.
Note:
The \CB should not include DSL controls within the changed text otherwise
spacing errors could occur.  For example when when making changes for an \PI
section, the \CB should be placed after the \PI line.
Examples:
 
This is an example of some existing text to which \CBA some new,
additional information has been added. \CB
 
\CBM
This is an example of some text which has been extensively modified
to include a vast amount of totally updated information.
\CB
 
\CBD \CB
00003
00004
00002
00006
00005
00001
CB
CB
CB
CB
TC
Syntax:
\CH{chtitle|chnum|chstyle}
 
All parameters are optional.
Parameters:
 
chtitle  is the title to be printed on the first page of the section and
    entered in the table of contents.  If omitted, no title is used.
chnum  is the number of the section within the document.  The chapter style
    defines this number as a number, letter, or other character when the
    document is formatted.  If not specified, the last-encountered chnum is
    incremented and used for the current chnum.  If * is specified, the
    section is unnumbered and will not be entered into the table of contents.
chstyle  defines the chapter style to be used for the section.  The style is
    administrator-defined.  If not specified, a default chstyle is used.  By
    default, the chnum counter is set to 1 automatically when a new style is
    selected; this can be changed by the administrator.
Description:
CH begins a new section or chapter.  The section can be titled or untitled,
numbered or unnumbered, and a selected style can be used.
 
Chapters (of any style) defined by the CH control are entered automatically
into the table of contents, even if they are unnumbered, unless the
administrator-defined chapter style specifies otherwise.
Administration:
The administrator controls the following:
 1. Placement of the title information on the page.  This includes whether the
    chapter starts on a new page, the next odd page, or the same page as the
    previous text.
 2. The font used for printing the heading text.
 3. Content and style of headers and footers, including page numbering styles.
 4. Definition of level heads as local to a chapter style, or as applicable to
    all chapter styles.  This definition can include automatic indexing of the
    level heads.
Defaults:
The system-supplied chstyle defaults are as follows.
 
FRONT or FR  specifies a front matter section.  Paging is continuous; page
    numbering is lowercase Roman.  The chnum parameter is ignored.  Page
    numbers appear on the outside of the footer of the page.
 
SECTION or SE  specifies a section.  Paging is by section; page numbering
    is Arabic.  The section number is included with the Arabic page number
    (e.g., 2-1 for the first page of Section 2) on the outside of the
    footer of the page.  Page numbering is set to 1 for each section.
 
CHAPTER or CH  is identical to SECTION except that it prints as "Chapter"
    rather than "Section" in the headings and table of contents.  This is
    the default style used if chstyle is not specified.
 
APPENDIX or AP  specifies an appendix.  Identical to SECTION, except that
    uppercase letters are used rather than Arabic numerals (e.g., Appendix
    A) and the structure is labeled "Appendix" rather than "Section".  The
    chnum parameter is entered as a number, which the APPENDIX style
    automatically converts to an appendix letter:  1 becomes A, 2 becomes
    B, etc.  Uppercase letters and Arabic numerals (A-1, A-2, etc.)  are
    used for page numbering.
 
MODULE or MO  specifies a tutorial module.  Identical to SECTION, except
    that the structure is labeled "Module" rather than "Section" and
    paging is continuous rather than by section.
INDEX or IX  specifies an index.  Identical to SECTION, except that the
    structure is labeled "Index" rather than "Section" and a lowercase i
    and Arabic numerals (i-1, i-2, etc.)  are used for page numbering.
 
NULL or NU  starts a new page and turns on page numbering (in Arabic), but
    does not print a chapter title or number.  This is primarily for small
    documents.
 
The default effect upon the footer differs according to the selected style.
Example:
 
\TP{My Book}
\CH{My Preface||FR}
\CH{My Chapter|1|SE}
\CH{||AP}
 
The above example defines a simple document skeleton, consisting of a title
page, a single front matter section, a single chapter (style SECTION), and a
single appendix without a title.
00003
00004
00002
00005
00001
CB
CB
Change (add or modify) and deletion marks can be placed in the page margin to
identify material that has been added, modified, or deleted.  The \CB control
is used to specify the type of changed area to be delimited with an
administrator-defined mark.
CH
Syntax:
 
\CL{columns|gutter}
   .
textual data
   .
\CL
 
The columns and gutter parameters are optional; if only one is included, the
default value is used for the other.  A CL without parameters turns off
multicolumn mode.
Parameters:
 
columns  is a number that specifies the number of columns on the page.  Up to
    five columns can be specified.
gutter  is a dimension that specifies the width of the gutters separating the
    columns.  Width is calculated in units of Average Character Width (ACW) if
    a numeric value only (without a unit of measurement) is specified; points,
    picas, inches, and metric units can also be specified.
Description:
CL activates multicolumn mode, in which page contents are formatted into
columns.  Multicolumn mode provides multiple columns only in text.  Headers,
footers, footnotes, figures, tables, graphics, etc.  all break columns and
take up the entire page width.  As with any other group, columns have to be
properly nested with respect to controls such as PL, CH, TB, etc.
 
Multicolumn mode remains active until disabled by a CL control without
parameters.  Columns are calculated based on the current page width, and are
balanced on the page when possible.
Administration:
 
The administrator controls the default column structure and whether column
text is balanced or snaking.  With balanced columns, CAP attempts to fill each
column with an equal amount of text.  With snaking columns, each column
(starting with the first) is completely filled with text before the next
column is started.  The BRC control can be used only with snaking columns.
Defaults:
 
The system-supplied default multicolumn structure is two columns with 20 point
gutters.  This can be specified by entering CL{}.  The default column
separator for all column structures is a vertical rule.  Column text is
balanced, by default.
Example:
 
\CL{4|10pt}
This is a test. This is a test. This is a test. This is a test. This is
a test. This is a test. This is a test. This is a test. This is a test.
This is a test. This is a test. This is a test. This is a test. This is
a test. This is a test. This is a test. This is a test. This is a test.
This is a test. This is a test. This is a test. This is a test.
\CL
 
The above specifies a 4-column layout with gutters that are 10 points wide.
 
When formatted, the above appears as:
 
                   |                   |                   |
This is a test.    |This is a test.    |This is a test.    |This is a test.
This is a test.    |This is a test.    |This is a test.    |This is a test.
This is a test.    |This is a test.    |This is a test.    |This is a test.
This is a test.    |This is a test.    |This is a test.    |
This is a test.     This is a test.     This is a test.
00003
00004
00002
00005
00001
CL
*
The controls are summarized by function in the table below; they are then
described in detail, in alphabetical order.
 
The controls marked with  an asterisk (*) in the following table have default
styles that are supplied with CAP DSL to each user site.  These system-
supplied defaults are the ones described  here.  The defaults can be changed
by the CAP administrator to suit the requirements of a particular site.
 
  Function                             Controls
 
  Structural Controls                  \CH  Chapter  *
                                       \Ln  Level Heading *
                                       \PI  Paragraph Item *
                                       \PL  Paragraph List *
                                       \TP  Title Page *
 
  Formatting Controls                  \AL  Alignment
                                       \BR  Page and Line Breaks
                                       \CL  Column Structure *
                                       \FI  Fill Mode
                                       \HB  Horizontal List
                                       \IN  Indentation
                                       \SP  Spacing
                                       \UNL  Undentation
                                       \VB  Vertical List, Bottom Aligned
                                       \VT  Vertical List, Top Aligned
 
  Font Style Controls                  \ff  Font Style.  Defaults are: *
                                          \BF  Boldface
                                          \IT  Italics
                                          \RM  Roman *
                                          \SL  Slanted
                                          \SS  Small Teletype
                                          \TT  Teletype
  Font Size Controls                   \fs  Font Size.  Defaults are: *
                                          \CHAP  Chapter
                                          \LARGE  Large
                                          \NORMAL  Normal *
                                          \SMALL  Small
                                          \TITLE  Title
 
  Table Controls                       \TB  Table Build *
                                       \TC  Table Cell
                                       \TE  Table Cell End
                                       \TH  Table Heading
                                       \TJ  Table Join
                                       \TR  Table Rule
                                       \TS  Table Space
                                       \TX  Table Cell Exit
 
  Figure Controls                      \FG  Figure *
                                       \GI  Inline Graphic *
                                       \GR  Graphic *
 
  Area Controls                        \CB  Changed Area *
                                       \EQ  Equation Area *
                                       \FN  Footnote Area *
                                       \KT  Keep Together Area
                                       \SB  Subset Area
 
  Cross-reference Controls             \IX  Index Term *
                                       \LA  Label
                                       \RF  Reference
 
  File Controls                        \IDX  Index File
                                       \IL  Include Literal File
                                       \IS  Include Source File
                                       \TOC  Table of Contents File
 
  Character Interpretation Controls    \LT  Literal Mode
                                       \MT  Math Enable
 
  HELP Controls                        \HH  HELP Heading *
                                       \HM  HELP Mode
 
  Miscellaneous Controls               \*  Comment
                                       \DM  Define Macro
                                       \DS  Define Substitution
                                       \HY  Hyphenation Exception
                                       \ST  Strikethrough
                                       \UL  Underline
To create a table, a writer provides the following information:
 1. The title.
 2. The column headings.
 3. The contents of each cell within the table.
 4. The administrator-defined table style.
 
Items 1, 2, and 3 are then merged with the table style named in item 4,
resulting in a formatted table.
 
Note that writers do not create ad hoc table structures; the administrator
creates the table styles that are available to the writer.  However, the
writer can vary the behavior of a table by including DSL controls inside the
table cells.
Page numbers; structure numbers; and titles, headings, and captions can be
cross-referenced within a document source file.
 
Cross-references are created by labeling the item to be referenced with the
\LA control and then referencing it anywhere else in the source file with the
\RF control.
The control words in the following table can be inserted in a source file to
print date and time information from the system clock when the file is
formatted.  This is useful for documents that are produced on a regular basis
and must contain current date information.  Note that the time at which TeX
begins formatting the document is considered the current time, and is not
changed thoughout the entire formatting run.
 
          Enter       Prints
 
          \today      The current month, day, and year.
 
          \clock      The current time, in 24-hour time.
 
          \clockam    The current time, in 12-hour time.
 
          \theweekday The current day of the week.
 
          \themonth   The current month of the year
 
          \time       The current time, in minutes since midnight.
 
          \day        The current day of the month, as a number.
 
          \month      The current month of the year, as a number.
 
          \year       The current year.
 
These control words are used as shown in the following example:
 
I am sending this letter on \today, at \clock\ or \clockam. The letter
is sent every \theweekday\ in the month of \themonth.
 
which prints as:  I am sending this letter on December 13, 1994, at 11:15 or
11:15 am.  The letter is sent every Tuesday in the month of December.
 
A control space (\ ) is used after the \clock and \theweekday control words in
the example above.  The control space tells TeX where the control word ends
and inserts a space between what the control prints and the following word.
 
Note that the last four control words in the table above must be preceded by
the TeX \the control sequence.  For example:
 
The day of the month is \the\day, in month \the\month\ of the year, which
is \the\year.
 
which prints as:
 
The day of the month is 13, in month 12 of the year, which is 1994.
DM
DS
When CAP is used for demand printing, documents are stored on the
computer in electronic form and copies are printed when needed on
a high-speed output device. Features include:
 
o   Lineprinter copies - low-resolution draft copies are printed on
 
    demand.  This is useful for give-away drafts and quick reviews.
    Fonts and boxes are represented by ASCII characters.
 
o   Laserprinter copies - documents are printed on the laserprinter
 
    when needed.  A 100 page document is printed in less than 10
    minutes.  Graphics, fonts, and boxes have the appearance of quality
 
    master copies.
Some DSL controls have parameters that allow the writer to specify dimensions
such as height, width, and indentation.  These include formatting controls
(\IN, \UNL, \SP, and \CL) and figure, graphic, and table controls (\FG, \GR,
and \TB).
 
Dimensions can be specified in two ways:  as a numeric value only, or as a
numeric value followed by a unit of measurement.
 
When only a numeric value is specified, DSL calculates the dimension in units
of Average Character Width (ACW) or Average Character Height (ACH). An ACW is
the width of the average character in the current font.  An ACH is the height
of the average character in the current font.  For example, specifying \SPF{5}
inserts vertical space equal to five times the height of an average character.
Use of only a numeric value is recommended for specifying dimensions within
text, such as spacing and indentation.  Since ACW and ACH are font-dependent
quantities, their use in formatting text will ensure the appearance of
consistent, logically spaced text regardless of the font size currently in
use.
 
Specific units of measurement can be used for dimensions in tables, figures,
graphics, and between columns (with \CL). For example, specifying \TB{My
Table|*|COL|3|5in} produces a three-column table that is 5 inches wide.
 
DSL accepts the following units of measurement:
 
   points (pt)
   picas (pc)   1pc = 12pt
   inches (in)   1in = 72.27pt
   big points (bp)   72bp = 1in
   centimeters (cm)   2.54cm = 1in
   millimeters (mm)   10mm = 1cm
   didot points (dd)   1157dd = 1238pt
   ciceros (cc)   1cc = 12dd
   scaled points (sp)   65536sp = 1pt
Syntax:
\DM\name{contents}
 
All parameters are required.  Note that the syntax of this control is
different than the syntax of other DSL controls so that DSL controls can be
included within the contents area.
Parameters:
 
name  specifies the name of the defined macro.  Only alphabetic characters are
    permitted as defined macro names.
contents  defines the contents of the macro.  This can include other DSL
    controls as well as TeX macros.  Macros defined with DM permit up to nine
    parameters, which can be referred to within contents as \parone, \partwo,
    and so on, up to \parnine.
Description:
DM defines a macro whose contents are executed whenever the macro name (\name)
is encountered.  DM macros always require parameters.
 
When using defined DM macros, multiple parameters are separated by an OR bar
(|), making these macros similar in syntax to DSL controls.  Each parameter
can contain other DSL controls and can be on multiple lines, but cannot
contain an implicit paragraph break, such as a blank line.
 
Macros generated with the DM control cannot be used in data that are written
to an auxiliary file, like the index or table of contents.  This means the
macros cannot be used within the parameters of the IX, CH, TB, GR, or FG
controls, or in level heads that appear in the table of contents.  This
restriction does not apply to substitutions generated with the DS control.
Example:
 
\DM\quote{"\SMALL{\parone}"}
\DM\flip{\BF{\parone} or \IT{\partwo}}
 
The DM controls above define macros named \quote and \flip.  \quote contains a
single parameter in small font, surrounded by quotes.  \flip contains two
parameters, one in bold font and the other in italics, separated by the word
"or".
The following sentence shows how these macros could be used in text:
 
Words in \quote{quotes} are sometimes better highlighted by using
\flip{bold face|italics}.
 
When formatted, it appears as:
 
Words in "quotes" are sometimes better highlighted by using bold face or
italics.
00002
00003
00001
CAP has the following document assembly features:
 
o   Table of contents generation - a new table of contents can be
 
    generated during each formatting run.
 
o   Index generation - a new index can be generated during each
 
    formatting run. Multilevel indexing (an index within an index) and
    permuted indexes (multiple index terms from one index reference) are
 
    also available.
 
o   Automatic numbering - page, section, table, figure, and
    paragraph numbers are generated automatically.
 
o   Cross-reference resolution - the user refers to a section,
 
    paragraph, figure, or table by name.  In the formatted document, the
    reference is automatically updated to include the current number and
 
    page of the item.
Syntax:
\DS\name{contents}
 
All parameters are required.  Note that the syntax of this control is
different than the syntax of other DSL controls so that DSL controls can be
included within the contents area.
Parameters:
 
name  specifies the name of the defined substitution.  Only alphabetic
    characters are permitted as defined substitution names.
contents  defines the contents of the substitution.  This can include other
    DSL controls as well as TeX macros.
Description:
DS defines replacement text, DSL controls, and/or TeX macros to be used
whenever a substitution name is encountered.  That is, contents is substituted
whenever \name appears in the source file.
Example:
 
\DS\CPSIX{\IX{CP-6}\SL{CP-6}}
 
The \CPSIX\ operating system has strengths that are not common
in other operating systems. With \CPSIX, you can...
 
Note that the space preceded with the backslash (control space) in "\CPSIX\
operating system..."  above is used to keep the space between "CP-6" and
"operating" when the passage is formatted.  If a space is to be maintained
each time a substitution is performed, a blank space can be inserted after the
contents parameter on the DS control.  In the above example, this would appear
as \SL{CP-6 }.
 
Note also that the CPSIX sequence automatically enters the term "CP-6" in the
index.
00002
00003
00001
The general syntax of a DSL control is:
 
\mn{param[|param]...}
data
\mn
 
where mn is a two- to four-character mnemonic and param is a parameter that
modifies the processing of the control.  The parameters, data area, and
closing control are not always used.  For example:
 
\CH{My Chapter|1}
 
defines a new chapter called "My Chapter" that begins numbering with chapter
number 1.
 
Note that DSL controls are case-sensitive; they must always be entered in
uppercase.  There can be multiple lines per control and multiple controls per
line.
A DSL group is a syntactical construct used to limit the effect of DSL
controls to a particular area of the source text.  Actions can be indicated
within a group to change text or formatting; outside of the group, the text or
formatting reverts to what it was previously.
 
Groups can be delimited by (begin and end with) brace ({}) characters.  For
example, to change a text area to italic font, the desired text area would be
enclosed in braces on the \IT control:  \IT{desired text area}.  The text
within the braces is considered a group.  When the document is formatted, only
this group is printed in italics.  The text before and after the \IT control
remains in the normal font for the particular document style.
 
Groups can be nested to several levels.  In this case, each opening brace or
DSL control must be matched by a corresponding closing brace or control.  For
example:
 
{This is the text that starts group1
   {This is the text that starts group2
      {This is group3}
    This is the text that ends group2}
 This is the text that ends group1}
 
Here, group1 includes all of group2 and group3, and group2 includes all of
group3.
 
Groups can also be delimited by beginning and ending DSL controls.  For
example, tables are defined within \TB controls, and paragraph lists are
defined within \PL controls.
 
As another example:
 
   \PL{plstyle1}                       Begins paragraph list group 1.
 
     \PI                               Item inside paragraph list group 1.
 
     \PL{plstyle2}                     Begins paragraph list group 2.
 
       \PI                             Item inside paragraph list group 2.
 
       \PI                             Item inside paragraph list group 2.
 
     \PL                               Ends paragraph list group 2.
 
     \PI                               Item inside paragraph list group 1.
 
   \PL                                 Ends paragraph list group 1.
 
(Paragraph lists are described later in this section.)
As described above, text can be entered on-line or off-line using any ASCII-
compatible editing program.  However, DSL reserves the following characters
for its own use:
 
o   backslash (\), which invokes a DSL control.
o   left brace ({), which delimits a DSL control.
o   right brace (}), which delimits a DSL control.
o   tilde (~), which ties two words together with a required space.
o   OR bar (|), which separates parameters inside a DSL control.
 
To use these characters in text, the user puts a backslash in front of them.
For example, \\\{ prints as \{.  A backslash is not required in front of the
OR bar (|) outside of a DSL control, but a font in which the OR bar is
available must be used.
 
The double quote ("), underscore (_), and hyphen (-) characters require
special consideration in DSL.
 
The double quote is not normally used.  Instead, opening and closing quotes
are created by typing two accent grave or apostrophe characters.  For example:
 
"QUOTE"
 
prints as
 
"QUOTE"
If a file contains a double quote character ("), it appears in a form
determined by the font currently being used.  However, a double quote can be
printed by calling it out in the teletype (TT) font as follows:
 
\TT{"string"}
 
prints as
 
"string"
 
DSL contains a special control (\UL) that underscores passages.  Individual
underscore characters (as in MY_FILE) can be entered without any controls, as
DSL maps this character to the font being used.  However, the underscore
character looks better when used with a font that actually contains it as part
of its character set, such as the teletype (or ASCII) font.
 
In DSL, two hyphens (--) print as a single dash or en-dash (-); three hyphens
(---) print as a double dash or em-dash (--).  A single hyphen (-) prints as
entered from the keyboard.
Documents are entered in outline-structured format (the DSL controls
provide the structure), interspersed with text. The outline structure
is the basis for automatic creation of indices, tables of content, and
resolution of cross-references.  The outline structure also defines the
placement and formatting of tables and illustrations.
 
Text for a CAP document can be created and edited either on-line or
off-line, with any ASCII-compatible editing program. If editing is
performed with a personal computer editing program, the file must be
uploaded for formatting with CAP.
 
DSL controls that determine the format of a document are included in
each CAP file.  The controls do not appear when the document is formatted
and a hard copy is created.  A backward slash (\) and a mnemonic (in
uppercase) distinguish controls from text.
Syntax:
 
\EQ{eqnum|eqstyle}
   .
   .
 data
   .
\EQ
 
The eqnum and eqstyle parameters are optional.
Parameters:
 
eqnum  specifies an optional equation number.  If not specified, the current
    value of eqnum is incremented by 1.  If * is specified, no equation number
    is included.
eqstyle  specifies an administrator-defined equation style for the location
    and number of the equation.  If not specified, a default style is used.
Description:
EQ defines an equation area, in which math mode is automatically enabled.
 
See the MT control description for the inclusion of inline mathematical
formulas.
Administration:
The administrator controls the following:
 1. The placement and font style of the equations.
 2. Whether or not equations are numbered, as determined by the format
    definition.
 3. The placement and font style of the equation numbers.
Defaults:
The system-supplied eqstyle defaults are as follows:
 
DEFAULT  break the current paragraph and insert, center, and number the
    equation on the right page margin.
 
LEFT  same as DEFAULT, but number the equation on the left page margin.
Example:
 
\EQ{2}
x^2-y^2 = (x+y)(x-y)
\EQ
 
When formatted, the above appears as:
 
                               2
                              x - y2=(x +y)(x-y)                           (2)
00003
00004
00002
00005
00001
EQ
There are three types of error conditions that can take place during the
formatting of a document:  warning, error, and abort (by increasing level of
severity).
 
CAP keeps track of the errors that are encountered during formatting.  CAP
does not print a document unless it formats successfully.  Normally, this
means that warning messages are tolerated, but error or abort messages are
not.
 
The writer can modify CAP to tolerate error (as well as warning) messages or
to not tolerate even warning messages.  The writer modifies CAP by changing
the tolerance level in the CONTEXT submenu of the CAP program.
Messages are generally displayed on the screen during formatting.  They are
also written to a log file called *:CAP:LOG, which can be examined using a
text editor after formatting is complete.
Error messages have the following general structure:
 
!message
       tracking information (multiple lines)
l.nnn
 
where
message      is a message identifying the problem.
tracking information      is a set of internal TeX codes that identify the
actual failure point.  This information is of interest only to the
administrator.
nnn      is the sequential line number (not the EDIT key) of the line on which
the error occurred.
 
The most common error messages are the following:
Runaway argument      This message is printed when the user fails to
completely enclose a control.  For example, \L1{My Heading) prints this
message because a right parenthesis was accidentally typed rather than the
right brace.
 
Fix the control by adding the omitted brace.
Undefined control sequence      This message is printed when the user
misspells a DSL control.  Fix the control so that it is spelled correctly.
00001
00003
00004
00002
00005
Syntax:
\ff{data}
 
The ff parameter is administrator-defined; the {data} area is optional.
Parameters:
 
ff  specifies a two- to four-character mnemonic that the administrator has
    defined as a font style.
 
{data}  if present, the string "data" appears in the specified font style.
    If the string is not present, subsequent text appears in the specified
    font style until a different font style control is encountered or the
    current group ends.
Description:
\ff prints a textual area in an administrator-defined font style.  When \ff is
not specified, the text is printed in the default "normal" font style defined
by the administrator.
 
See also the \fs (font size) control later in this section.  Font style and
size controls can be used together.  See Fonts in Section 2 for more
information.
Administration:
The administrator controls the following:
 1. The font style control names.  These are the only DSL control names the
    administrator can change.
 2. The default font style used when \ff is not specified.
 3. The font definitions (style and size) given to each font style control
    name.
Defaults:
The system-supplied \ff font style control defaults are:
 
\BF  boldface font style.
 
\IT  italic font style.
 
\RM  Roman font style.  This is the normal or default font used when \ff
    is not specified.
 
\SL  slanted font style.
 
\SS  small teletype (ASCII) font style.
 
\TT  teletype (ASCII) font style.
Examples:
 
\BF
This is a boldface passage, but \RM{these words} are
not boldface.
\RM
These words aren't boldface either. But \BF{these words} are.
 
\IT
This is an italicized passage, but \RM{these words} are
not italicized.
\RM
These words aren't italicized either. But \IT{this} is.
 
The TeX "italic correction" macro (\/) can be used to maintain an equal amount
of space between the italicized and normal text.  For example,
 
\IT{But}\/ these words\/ \IT{are not italicized}.
 
\SL
This is a slanted passage, but \RM{these words} are
not slanted.
\RM
These words aren't slanted either. But \SL{this} is.
 
The TeX "italic correction" macro (\/) can also be used here to maintain an
equal amount of space between the slanted and normal text.  For example,
 
\SL{But}\/ these words\/ \SL{are not slanted}.
 
\SS
This is a small teletype passage, but \RM{these words} are
not small teletype.
\RM
These words aren't small teletype either. But \SS{THIS} is.
 
\TT
This is a teletype passage, but \RM{these words} are
not teletype.
\RM
These words aren't teletype either. But \TT{THIS} is.
00003
00004
00002
00005
00001
Syntax:
 
\FG{fgtitle|fgnum|fgstyle|fgwidth}
   .
   .
 data
   .
\FG
 
All parameters are optional; however, the introducing FG must include the
braces.
Parameters:
 
fgtitle  specifies an optional title to appear at the bottom of the boxed area
    and in the table of contents.
fgnum  specifies the number to be assigned to the figure.  If not specified,
    the current value of fgnum is incremented by 1.  If * is specified, the
    figure is not numbered and is not included in the table of contents.
fgstyle  specifies an administrator-defined figure style.  If not specified,
    the default figure style is used.
fgwidth  is a dimension that specifies the width of the figure to be printed.
    Width is expressed in either percentage of the textual area of the page
    (minus headers and footers), or as an absolute horizontal dimension in
    inches, metric units, points, or picas.  The percent sign (%) should not
    be used when entering percentages; percentage is assumed when explicit
    units are not specified.  The default is one-half the currently available
    area of the page.
data  specifies the textual data to be included inside the figure area.
Description:
FG defines an area of text that can be optionally titled and placed.
Administration:
The administrator controls the following:
 1. Format (spacing and font style) of figure contents.
 2. Ability of figures to float to the next available page.
 3. Presence, position, and format of figure numbers and captions.
 4. Space around the figure.
 5. Boxing of figures.
 6. Thickness of box lines and distance between the box and figure contents.
 7. Presence of figure numbers and captions in the contents' list of figures.
 8. Creation of new figure styles.
Defaults:
The system-supplied fgstyle defaults are:
 
DEFAULT  In this style, text inside a figure is unformatted (an FIF is
    implicit) and is displayed in teletype font.  The figure is boxed,
    numbered by chapter, and captioned, with an entry in the table of
    contents (unless the user specifies otherwise).  Synonym:  STANDARD.
 
COMPRESSED  Same as DEFAULT, but the figure text is displayed in a small
    teletype font to allow 80 columns to fit on the page.  Synonym:
    COMPR.
 
FLOATING  Same as DEFAULT, but allows the figure to float to the next page
    or beyond, if there is not enough room for it on the current page.
    Synonym:  STDFLT.
 
COMPRFLOAT  Same as COMPRESSED, but allows the figure to float to the next
    page or beyond, if there is not enough room for it on the current
    page.  Synonym:  CMPFLT.
Example:
 
\FG{Test Figure|*|}
  some stuff
  some stuff
  some stuff
  some stuff
  some stuff
\FG
 
When formatted, the figure appears as follows:
 
  some stuff
  some stuff
  some stuff
  some stuff
  some stuff
00003
00004
00002
00005
00001
Syntax:
\FI{fitype}
 
The fitype parameter and the braces are optional.
Parameters:
 
fitype  specifies the type of formatting to be applied to subsequent portions
    of the text, as follows:
 
    F   means fill off; no wordwrap takes place during formatting, and the
        spacing of each output line is the same as the spacing at input
        (in the source file).  However, character transformations are
        still made, and other DSL controls are interpreted normally.
 
    N   means fill on; lines are wordwrapped when formatted, spaces are
        made all the same size (multiple occurrences of spaces are
        compressed into a single space), and all spaces count.  This is
        the default if fitype is not specified.
Description:
FI defines whether or not wordwrapping and uniform spacing (fill mode) takes
place during formatting.  Note that fill mode controls only wordwrapping and
spacing; the alignment of the wrapped text is defined by the AL control.
 
If fill is turned off or on within a DSL group, it automatically reverts to
what it was previously when the group ends.  For example, FIF within a KT area
reverts to FIN when the KT area is closed.
Example:
 
\FIN
It is wonderful to get away from the yelling and howling
of what might be called the present-day Creepy Time melodies
and lyrics (and I apologize to both of those fine words).
One
of these gibberings poses the
question:
\FIF
"What is love?"
and answers it with:
"Five feet of heaven in a pony tail."
 
When formatted, the above appears as:
 
It is wonderful to get away from the yelling and howling of what might be
called the present-day Creepy Time melodies and lyrics (and I apologize to
both of those fine words).  One of these gibberings poses the question:
"What is love?"
and answers it with:
"Five feet of heaven in a pony tail."
00002
00003
00001
FI
FG
Figures are formatted with the \FG control.  \FG defines a boxed area of text
that can be titled and numbered, and formatted in an administrator-defined
figure style.  In the default figure style, data inside the boxed area are
unformatted (\FIF) and displayed in teletype font.
 
The \GR control is used to place and scale a CAP graphic on a page.  Using a
file containing graphics data that have been converted to CPX or SGL format,
the \GR control allows the user to number and title a graphic figure, format
it in an administrator-defined style, and specify its size on the page.
 
The \GI control (inline graphic) is also used to place and scale a CAP graphic
on a page, but the graphic is handled as though it were a single character.
No spacing, boxing, number, or title is used.  \GI is useful for incorporating
logos or other single-line graphic data in places where words or characters
would be appropriate.
 
The \FG, \GR, and \GI controls are described in detail in Section 3.
FI
FI
Syntax:
 
\FN{fnstyle}
   .
 data
   .
\FN
 
The parameters are optional; however, the introducing FN must include the
braces.
Parameters:
 
fnstyle  is an administrator-created footnote style name.  The default style
    is determined by the administrator.
Description:
FN marks an area of textual material to be generated as a footnote at the
bottom of a page.  Note that footnotes cannot be called inside tables or
figures.
Administration:
If rigidity is on, the fnstyle parameter is disabled and only default style
footnotes are generated.  The administrator controls the placement and style
of the footnote marker (number or symbol) and the footnote text.
Defaults:
The system-supplied fnstyle defaults are:
 
NUMBERED  Notes laid down at the bottom of the page using standard
    reference superscripts:  1, 2, etc.  Synonym:  NU.
 
UNMARKED  Notes laid down at the bottom of the page, but with no marker
    either in the text or in the note.  Synonym:  UN.
Example:
 
This is some text that will have a footnote\FN{NU}This is a footnote!\FN.
Note that the footnote number appears exactly where it is called.  In this
case, the footnote number appears before the period in the "This is
some...footnote."  sentence.
00003
00004
00002
00005
00001
DSL can provide a wide variety of fonts.  The actual fonts available to the
writer are determined by the administrator.  The administrator selects font
styles and sizes, and assigns control names to them.  Font controls are the
only DSL controls whose names can be changed by the administrator.  For
example, the default "normal" font style supplied with CAP is a Roman font
that is assigned the control name \RM; the administrator can redefine and
rename this (and all) fonts as desired.
 
There are two types of font controls in DSL: font styles (specified with the
\ff control) and font sizes (specified with the \fs control).  The control
names are defined by the administrator as parameters available to the writer
on the \ff and \fs controls.  The default font controls supplied with CAP
include font styles such as \IT (italic) and \BF (boldface), and font sizes
such as \LARGE and \SMALL. The default font controls can be defined
differently by the administrator at a particular CAP user site.  Note that in
addition to the "normal" font style (\RM as supplied with CAP), there is also
a "normal" font size; \NORMAL is the CAP default.
 
Font style and size controls can be used together.  When switching font
styles, the current font size is maintained; and when switching font sizes,
the current font style is maintained.
 
For example:
\LARGE{\BF{This text is large and bold}} and this text is normal.
\LARGE{\BF{This text is large and bold} and this text is large.}
\NORMAL
 
prints as:
 
This text is large and bold and this text is normal.  This text is large and
bold and this text is large.
 
The \NORMAL control above returns the text following the example to normal
size.
 
Interword and intersentence spacing depend on the current font.
 
All of the font controls are described in detail in Section 3.
 
DSL provides access to many characters not normally provided on computer
terminal keyboards; these, however, must be entered as special TeX sequences.
For example, the following sentence:
 
?But aren't Kafka's Schlo? and AEsop's OEuvres often naive vis-a-vis the
daemonic phoenix's official role in fluffy souffles?
 
was produced by the following input lines:
 
?`But aren't Kafka's Schlo{\ss} and {\AE}sop's {\OE}uvres
often na{\"\i}ve vis-\`a-vis the d{\ae}monic ph{\oe}nix's official r\^ole
in fluffy souffl\'es?
 
See TeX Control Sequences later in this section for more information.
FS
FF
FN
Pressing the break key during a formatting run causes formatting to halt and a
question mark to be issued as a prompt.  If the user enters a question mark in
response to this prompt, TeX responds with the options that can be entered.
 
To exit the formatter, enter X. To continue formatting, press return.
This section describes the use of structures, paragraphs, blank space,
indentation, alignment and hyphenation in formatting text with DSL.
Occasionally, TeX will get so confused that it will request help from the
user.  When it does this, a question mark (?)  appears on the screen and
formatting stops.  In this case, enter i\bye and ignore all the resulting
messages.  If this does not work, enter X at the next ?  prompt.  This forces
TeX to exit, returning control to the CAP menu.
CH
Syntax:
\fs{data}
 
The fs parameter is administrator-defined; the {data} area is optional.
Parameters:
 
fs  specifies a two- to four-character mnemonic that the administrator has
    defined as a font size.
 
{data}  if present, the string "data" appears in the specified font size.
    If the string is not present, subsequent text appears in the specified
    font size until a different font size control is encountered or the
    current group ends.
Description:
\fs prints a textual area in an administrator-defined font size.  When \fs is
not specified, the text is printed in the default "normal" font size defined
by the administrator.
See also the \ff (font style) control earlier in this section.  Font size and
style controls can be used together.  See Fonts in Section 2 for more
information.
Administration:
The administrator controls the following:
 1. The font size control names.  These are the only DSL control names the
    administrator can change.
 2. The default font size used when \fs is not specified.
 3. The font definitions (size and style) given to each font size control
    name.
Defaults:
The system-supplied \fs font size control defaults are:
 
\CHAP  chapter font size.  This is the default size automatically called
    for the chapter title when the writer uses the CH control.  CHAP can
    also be used separately anywhere in the source file.
 
\LARGE  large font size.  This font is about 20% larger than the
    system-supplied normal font size.
 
\NORMAL  normal font size.  This is the normal or default font used when
    \fs is not specified.
 
\SMALL  small font size.  This is the default size automatically called
    for footnotes when the writer uses the FN control.  SMALL can also be
    used separately anywhere in the source file.
 
\TITL  title font size.  This is the default size automatically called for
    the document title when the writer creates the title page with the TP
    control.  TITL can also be used separately anywhere in the source
    file.
Examples:
 
\CHAP
First Chapter \NORMAL{and} Second Chapter \NORMAL are the chapter
titles. This is text and this is the \CHAP{Chapter Title}.
 
\LARGE
This is a large passage, but \NORMAL{these words} are not large.
\NORMAL
These words aren't large either. But \LARGE{this} is.
 
\SMALL
This is a small passage, but \NORMAL{these words} are not small.
\NORMAL
These words aren't small either. But \SMALL{these words} are.
 
The format of the title page is as follows:
 
\TITL{Document Title}
 
\INL{6} \IT{Manual Number}
00003
00004
00002
00005
00001
Syntax:
\GI{grfile|grstyle|grheight|grwidth}
 
All parameters except grfile are optional.
Parameters:
 
grfile  is the name of a file containing graphics data that have been
    converted to CPX or SGL format.  If grfile is not included, the driver
    programs that produce output for the printing devices will be unable to
    locate the file to include and an error message will be issued.
grstyle  specifies an administrator-defined style for the graphic.  If not
    specified, the default style for inline graphics is used.
grheight  is a dimension that specifies the height of the graphic to be
    printed.  Height is expressed in either percentage of the textual area of
    the page (minus headers and footers), or as an absolute vertical dimension
    in inches, metric units, points, or picas.  The percent sign (%) should
    not be used when entering percentages; percentage is assumed when explicit
    units are not specified.  The default is the current average character
    height (ACH).
grwidth  is a dimension that specifies the width of the graphic to be printed.
    Width is expressed in either percentage of the textual area of the page
    (minus headers and footers), or as an absolute horizontal dimension in
    inches, metric units, points, or picas.  The percent sign (%) should not
    be used when entering percentages; percentage is assumed when explicit
    units are not specified.  The default is one-quarter the currently
    available width of the page.  If used in multiple columns, the default is
    one-quarter of the current column width.
Description:
GI places and scales a CAP graphic on the page, as though the graphic were a
single character.  GI does not insert vertical or horizontal space, rules, a
caption, or a graphic number, and can appear anywhere.
Administration:
The administrator controls the following:
 1. Boxing of graphics.
 2. Overwriting the graphic with text.
Defaults:
The GI control shares the same styles as the GR control.  The system-supplied
default style for GI is NOBOX, which prints the graphic as is, without a box,
number, caption, or table of contents entry.
Example:
 
How can the \GI{DOC_01_01.:STAR|||3} graphic appear in this sentence?
 
The spacing around the graphic produced by the GI control above is the same as
if the graphic were just a character or a single character word.  The most
common use for the GI control is to incorporate logos or other graphic data in
places where words or characters would be appropriate.
00003
00004
00002
00005
00001
Syntax:
\GR{grtitle|grnum|grfile|grstyle|grheight|grwidth}
 
All parameters except grfile are optional.
Parameters:
 
grtitle  is the title of the graphic to be printed on the page and entered
    into the table of contents.
grnum  specifies the number to be assigned to the graphic.  If not specified,
    the current value of grnum is incremented by 1.  If * is specified, the
    graphic is not numbered and is not entered in the table of contents.
grfile  is the name of a file containing graphics data that have been
    converted to CPX or SGL format.  If grfile is not included, the driver
    programs that produce output for the printing devices will be unable to
    locate the file to include and an error message will be issued.
grstyle  specifies an administrator-defined style for the graphic.  If not
    specified, the default style is used.
grheight  is a dimension that specifies the height of the graphic to be
    printed.  Height is expressed in either percentage of the textual area of
    the page (minus headers and footers), or as an absolute vertical dimension
    in inches, metric units, points, or picas.  The percent sign (%) should
    not be used when entering percentages; percentage is assumed when explicit
    units are not specified.  The default is one-half the current page height.
grwidth  is a dimension that specifies the width of the graphic to be printed.
    Width is expressed in either percentage of the textual area of the page
    (minus headers and footers), or as an absolute horizontal dimension in
    inches, metric units, points, or picas.  The percent sign (%) should not
    be used when entering percentages; percentage is assumed when explicit
    units are not specified.  The default is one-half the current page width.
Description:
GR places and scales a CAP graphic on the page.
Administration:
The administrator controls the following items.
 1. Ability of graphics to float to the next available page.
 2. Boxing of graphics.
 3. Space around the graphic.
 4. Presence, position, and format of graphic numbers and captions.
 5. Presence of graphic numbers and captions in the contents' list of figures.
 6. Creation of new graphic styles.
Defaults:
The system-supplied defaults are not to float to another page and to box.
Three default graphic styles are provided:
 
DEFAULT  with a box, graphic number by chapter, caption, and an entry in
    the table of contents.  This is the style used in the examples below.
 
BOX  a simplified graphic style, providing only a box, but no caption,
    graphic number, or table of contents entry.
 
NOBOX  similar to BOX, but without even a box around the graphic.  This is
    the style used for inline graphics produced with the GI control.
Examples:
\GR{USS Enterprise||DOC_01_01.:STREK||33}
 
The above example associates the graphic picture in file DOC_01_01.  The
picture is scaled so that it takes up 33 percent of the text height of the
page, while occupying the entire width.  In this case, the height turns out to
be approximately  2 3/4 inches high.  The figure is labeled "USS Enterprise",
is boxed, and does not float to another page.
 
\GR{USS Enterprise|2|DOC_01_01.:STREK||3in}
 
This example is similar to the previous one, except that the graphic is scaled
inside a box that is exactly 3 inches high and the graphic number is 2.
00003
00004
00002
00005
00001
GR
MATH_CHARACTERS
Syntax:
 
\HB{left|center|right}
Parameters:
 
left  contains text and DSL controls that are to be positioned and aligned to
    the left.
center  contains text and DSL controls that are to be positioned and aligned
    with equal amounts of space to the left and to the right.
right  contains text and DSL controls that are to be positioned and aligned to
    the right.
Description:
HB creates a single line from the three discrete parts, with the contents of
the left, center, and right parameters positioned and aligned as described
above.  The three parts can contain text and other DSL controls, but cannot
contain another HB control.  They are single-line entries, and any paragraph
format controls, like IN, are ignored.  Explicit paragraph breaks are not
permitted and are considered errors.  The line created by the HB control is
always the full current page or column width.
 
The HB control is closely related to the VB and VT controls, which provide a
more flexible vertical analog.
Examples:
 
\HB{On the left.|\BF{Centered}, in bold.|On the right, \SL{slanted}.}
 
When formatted, the above appears as:
 
On the left.             Centered, in bold.             On the right, slanted.
00002
00003
00001
ONLINE_HELP_FACILITY
Unless specified otherwise by the user (with the HM control), the contents of
figures (defined with the FG control) are automatically included in the HELP
file during formatting, but without the enclosing box.  HELP topics and
subtopics can be created for the figure contents with the HH control.  Figure
titles and numbers are automatically excluded from the HELP file during
formatting.
HH
Level headings are defined with the Ln control which has the following syntax:
 
\Ln{lhtitle|lhnum|lhsort}
 
where:
n      is the level heading number, 1 through 9.
lhtitle      is the text of the level heading.
lhnum      defines a specification number.
lhsort      specifies a nonprinting index sort key for lhtitle.
 
As defined by the administrator, level headings can automatically generate
HELP topics during HELP formatting runs.  The system-supplied default is to
generate topics (not subtopics) for level 1, 2, and 3 headings; the topics are
produced from lhsort if it is specified, or from lhtitle if lhsort is not
specified.  The HELP topics contain the first 31 characters of lhsort or
lhtitle, with all internal spaces converted to underscores.
 
If a HELP topic different from the default is required, it can be specified
with the HH control, described earlier in this section.
 
The following figure is an example of a document source file containing level
headings and HELP controls:
 
\L1{Angel Types}
There are three types of angels: Cherubs, Seraphs, and Archangels.
\SB{HELP}Related HELP topics: CHERUBS, SERAPHS, ARCHANGELS \SB
 
\L2{Cherubs} \HH{||S}
Cherubs resemble little babies with wings.
 
\L2{Seraphs} \HH{||S}
Seraphs resemble little heads with wings.
 
\L2{Archangels} \HH{||S}
Archangels wear long and flowing robes.
 
When formatted as a printed document, this example appears as follows:
 
Angel Types
 
There are three types of angels:  Cherubs, Seraphs, and Archangels.
Cherubs
 
Cherubs resemble little babies with wings.
 
Seraphs
 
Seraphs resemble little heads with wings.
 
Archangels
 
Archangels wear long and flowing robes.
 
When the topics in the example are queried in HELP, the messages appear as:
 
!HELP (ANGELDATA) TOPICS
   ANGEL_TYPES
 
!HELP (ANGELDATA) ANGEL_TYPES
   There are three types of angels: Cherubs, Seraphs, and
   Archangels.
   Related HELP topics:  CHERUBS, SERAPHS, ARCHANGELS
 
!HELP (ANGELDATA) ANGEL_TYPES TOPICS
   CHERUBS    SERAPHS    ARCHANGELS
 
!HELP (ANGELDATA) ANGEL_TYPES CHERUBS
   Cherubs resemble little babies with wings.
00003
00004
00002
00001
HM
Like level headings, paragraph list items can be defined by the administrator
to automatically generate HELP topics during HELP formatting.  The system-
supplied default is to generate HELP subtopics for paragraph list styles
(\PL{plstyle}) with named paragraph items (\PI{piname}).  The default styles
are DESCRIBE, DESCRIBE_ITALICS, WIDEDESCRIBE, SYNTAX, and ITEM.
 
If a HELP subtopic different from the default is required, it can be specified
with the HH control, described earlier in this section.
 
Note that only first-level paragraph list items become HELP subtopics; nested
paragraph lists are considered part of the previous paragraph list item.
Paragraph lists enclosed in tables or figures also do not generate HELP
subtopics, unless HH controls are inserted to create them.
 
The following figure is an example of a document source file containing a
paragraph list and HELP controls:
 
\L1{TE (Table Cell End)}
\HH{TE|TE_CONTROL TABLE_CELL_END TABLE_END|K}
 
\PL{ITEM}
\PI{Syntax:}
 
\TT{\\TE}
 
\PI{Description:}
\TT{TE} marks the end of the data for the current row of table cells.
 
\PI{Examples:}
See the other table control descriptions for examples of \TT{TE}.
\PL
 
This example, when formatted as a printed document, appears as:
 
TE (Table Cell End)
 
Syntax:
 
\TE
 
Description:
 
TE marks the end of the data for the current row of table cells.  Examples:
 
See the other table control descriptions for examples of TE.
 
When the topics in the example are queried in HELP, the messages appear as:
 
!HELP (DSL) TE
   \TE
 
!HELP (DSL) TE TOPICS
   DESCRIPTION        EXAMPLES
 
!HELP (DSL) TE DESCRIPTION
   Description:
   TE marks the end of the data for the current row of table
   cells.
 
!??
   Examples:
   See the other control descriptions for examples of TE.
Subsets (specified with the SB control) can be used to define textual areas
that are to be included in or excluded from HELP files.  The SB control is
used when the content of the HELP file is required to differ from the content
of the document.
 
Subsets can delimit HELP-only text from document-only text if SB is used in
the form:
 
... text that appears in both the manual and HELP message ...
\SB{HELP} HELP-only text ... \SB{} manual-only text ... \SB
... text that appears in both the manual and HELP message ...
 
For example, the following shows this use of the SB control in a document
source file:
See \SB{HELP} HELP (DSL) SYNTAX_SUMMARY \SB{} Table A-1, DSL Control
Syntax Summary, \SB for further information.
 
When formatted for a printable document, this example appears as:
 
See Table A-1, DSL Control Syntax Summary, for further information.
 
When formatted for a HELP file, this example appears as:
 
See HELP (DSL) SYNTAX_SUMMARY for further information.
 
If the SB control is used in the form:
 
\SB{HELP} ... \SB
 
then the contents of the subset will appear only when the document is
formatted for HELP; the subset has no effect on printable document text.
Unless specified otherwise by the user (with the HM control), the contents of
tables (defined with TB and related controls) are automatically included in
the HELP file during formatting, but without the enclosing box and internal
rules.  HELP topics and subtopics can be created for the table contents with
the HH control, which should be used within table cells.  Table titles and
numbers are automatically excluded from the HELP file during formatting.
HH
Syntax:
 
\HH{hhtopic|hhsynonyms|hhstyle}
Parameters:
 
hhtopic  specifies the topic or subtopic to be used in the HELP file.  If not
    specified, the previous level heading is used as the topic or subtopic.
hhsynonyms  specifies the synonyms for the topic or subtopic.  If not
    specified, no synonyms are used.
hhstyle  specifies the level and handling of the topic, as follows:
 
    A   specifies that the material following is to be the abstract or
        default message for the HELP file.  A HELP file can have only one
        abstract or default message.
 
    K   specifies a topic.  This is the default if hhstyle is not
        specified.
 
    S   specifies a subtopic.
 
    B   specifies a null topic.  This provides a break point for HELP
        messages longer than a screen's worth of information.  (Note that
        the <ESC><A> function and the TERMINAL PAGEHALT command on CP-6
        make it possible for the user to view a HELP message one screen at
        a time; therefore it is not a requirement that messages be limited
        to one screen of information.)
 
    X   Cancels the HELP topic or subtopic name (but not the related text)
        specified by the previous level heading or paragraph item, until
        the next Ln, PI, or HH control is encountered.
Description:
 
HH is used to create HELP topics and subtopics to be used when a document
source file is formatted to create a HELP file.  HH controls can be used
anywhere in the source file, and are ignored during normal document
formatting.
 
Level headings specified by the Ln control create HELP topics by default
during HELP file formatting.  The HH control can be used to generate a HELP
topic or subtopic (including an abstract or default topic) that is different
from the level heading default, generate a topic or subtopic where no level
heading exists, or establish synonyms for the topic or subtopic.  In the same
way, HH can add to or modify the default HELP subtopics generated by the PI
control in paragraph lists (also described later in this section).
 
When used to modify the HELP actions of Ln and PI, the HH control should be
entered immediately following the Ln or PI control (on the same or the next
immediate line in the source file).
HELP topics, subtopics, and synonyms are limited to 31 characters and are
entered in all capitals, with underscores representing spaces between words.
Synonyms entered with the HH control are separated by spaces.
 
The actions specified by an HH control are in effect only until the next HH
control (or Ln or PI control) is encountered.
Examples:
 
The following figure shows a segment of a document source file containing an
abstract (default) HELP message:
 
\L1{CAP System Invocation} \HH{||A}
CAP is invoked by typing "CAP" at the system level prompt (!) as
follows:
 
\TT{!CAP}
 
After CAP is invoked, the user's screen is cleared of any previous
data and the CAP main menu is displayed.
\L2{CAP Main Menu}
     .
 
Querying the HELP file for the abstract message appears as:
 
!HELP (CAP)
CAP is invoked by typing "CAP" at the system level prompt as follows:
 
!CAP
 
After CAP is invoked, the user's screen is cleared of any previous
data and the CAP main menu is displayed.
 
The following figure shows HH used in a document source file to create and
modify topics and subtopics, and to create synonyms:
 
\L1{CAP Structure Styles} \HH{STRUCTURE_STYLES}
This is the first block of information.
 
\L2{Paragraph List Styles}
\HH{|PARAGRAPH_STYLES PARAGRAPH_LISTS PARAGRAPHS|S}
This is the second block of information.
 
\L2{Figure, Table, and Graphic Styles}
\HH{FIGURE_AND_TABLE_STYLES||S}
This is the third block of information.
 
\HH{GRAPHIC STYLES||S}
This is the fourth block of information, which has a HELP subtopic,
but no level heading in the document.
\L2{Other Structure Styles} \HH{||X}
This is the fifth block of information. The level head appears in the
manual, but does not appear as a topic in HELP. The text appears in
both the manual and HELP.
 
In the example above, note that:
 1. The first HH control changes the heading title for HELP.
 2. The second HH control establishes synonyms and changes the default topic
    (from the second level heading) to a subtopic.
 3. The third HH control changes the heading title for HELP and changes the
    default topic (from the second level heading) to a subtopic.
 4. The fourth HH control creates a new subtopic where no level heading
    exists.
 5. The fifth HH control excludes the level heading as a topic from the HELP
    file (but keeps the text), until the next HH or Ln control is encountered.
 
When formatted in document mode, the above example appears as:
 
CAP Structure Styles
 
This is the first block of information.  Paragraph List Styles
This is the second block of information.
 
Figure, Table, and Graphic Styles
 
This is the third block of information.
 
This is the fourth block of information, which has a HELP subtopic, but no
level heading in the document.
 
Other Structure Styles
 
This is the fifth block of information.  The level head appears in the manual,
but does not appear as a topic in HELP. The text appears in both the manual
and HELP.
 
When HELP is queried for the above example (assuming the HELP subject is
STYLEDATA), the messages appear as:
 
!HELP (STYLEDATA) TOPICS
   STRUCTURE_STYLES
 
!HELP (STYLEDATA) STRUCTURE_STYLES
   This is the first block of information.
 
!HELP (STYLEDATA) STRUCTURE_STYLES TOPICS
   PARAGRAPH_LIST_STYLES   FIGURE_AND_TABLE_STYLES   GRAPHIC_STYLES
 
!HELP (STYLEDATA) STRUCTURE_STYLES PARAGRAPHS
   This is the second block of information.
 
!HELP (STYLEDATA) STRUCTURE_STYLES FIGURE_AND_TABLE_STYLES
   This is the third block of information.
 
!HELP (STYLEDATA) STRUCTURE_STYLES GRAPHIC_STYLES
   This is the fourth block of information, which has a HELP subtopic,
   but no level heading in the document.
 
   This is the fifth block of information. The level head appears in
   the manual, but does not appear as a topic in HELP. The text appears
   in both the manual and HELP.
 
The following figure shows, in a document source file, the use of the B
parameter on the HH control to specify a null topic name and therefore provide
a break point for HELP messages longer than a screen's worth of information:
 
\L1{Maintaining CAP Dictionaries}
        .
   lots and lots of text
        .
\HH{B}
        .
        .
   lots more text
        .
00002
00003
00001
Syntax:
 
\HM{hmtype}
 
The braces are optional.
Parameters:
 
hmtype  controls the generation of text for the HELP file, as follows:
 
    F   specifies HELP mode off, meaning that formatting for HELP will not
        include the subsequent text in the HELP file.  The text is
        included, however, in the document when it is formatted for
        printed copy.
 
    N   specifies HELP mode on, meaning that formatting for HELP will
        include the subsequent text in the HELP file.  The text is also
        included in the document when it is formatted for printed copy.
        This is the default if hmtype is not specified.
Description:
 
HM turns generation of text on or off for a HELP file.
 
An entire chapter or section can be removed from HELP by entering HMF at the
beginning of the chapter source file.  HMF and HMN can also be entered around
individual topics and subtopics (and associated text) to remove them from
HELP. Paragraph lists, tables, and figures can be similarly removed from HELP,
if necessary.
Example:
 
The following shows the HM control used to turn HELP mode off for a paragraph
item and nested paragraph list:
 
\L1{TH (Table Heading)}
\PL{ITEM}
\PI{Syntax:}
 
\TT{\\TH\{heading1 \\TC heading2...\}}
 
\HMF
\PI{Parameters:}
  \PL{SY}
  \PI{heading} specifies the text for a table column heading.
  \PL
\HMN
 
\PI{Description:}
\TT{TH} specifies the heading text for the columns of a table.
\PL
 
HELP querying for the above example appears as:
 
!HELP (DSL) TH
   \TH{heading1 \TC heading2...}
 
!??
Description:
TH specifies the heading text for the columns of a table.
 
Note that the paragraph item and nested paragraph list do not appear in the
HELP query above.
00002
00003
00001
HM
HM
IN
HB
UNL
Syntax:
\HY{hyph-word1 hyph-word2 ...}
Parameters:
 
hyph-word  specifies suggested hyphenation points for a word that the TeX
    hyphenation algorithm is unable to break correctly, thus resulting in an
    overfull hbox message .  Hyphenation points are marked by the hyphen (-)
    character.  Hyphenation for multiple words can be specified with one HY
    control.
Description:
TeX uses algorithmic hyphenation, which applies a formula to determine where a
word should be broken.  In addition, TeX has an exception dictionary of
several hundred words that hyphenate at "odd" points, different from the way
the algorithm would normally break them.  HY temporarily adds a word to the
exception dictionary, so that TeX knows the correct point to break an "odd"
word for hyphenation.  HY defines hyphenation for all occurrences of the word
in the source file.
 
The most logical place to enter the HY control is on a line by itself before
the paragraph containing the word to be hyphenated, although the control can
be entered anywhere in the source file before that word.
NOTE:
 
Another way to hyphenate a word is with the TeX macro \-, or "discretionary
hyphen".  The \- macro defines all hyphenation points for a single occurrence
of a word; the word is not added to the exception dictionary.
 
The \- macro is used within the word itself in the source file; it is not
separate from the word, as is the HY control.
 
The \- macro can be used to specify hyphenation for accented words, since only
alphabetic characters and the hyphen (-) can be specified in the hyph-word
parameter of the HY control.
Example:
Suppose that the word "monospaced" is at the end of a line and that TeX cannot
break it.  The writer specifies hyphenation points to TeX by entering:
 
\HY{mon-o-spa-ced}
 
The word can also be broken with the \- macro by entering:
 
mon\-o\-spa\-ced
00002
00003
00001
HY
When it becomes necessary to break a word during text formatting, TeX uses an
algorithmic hyphenation formula to determine where the word should be broken.
TeX also has an exception dictionary of several hundred words that hyphenate
at unusual points, different from the way the algorithm would normally break
them.
 
When a word cannot be broken correctly and the word is not found in the
exception dictionary, TeX issues an overfill hbox message.  (See Appendix C.)
 
When this happens, there are two ways to break the word correctly.  The first
way is with the \HY control, which defines hyphenation for all occurrences of
the word in the source file and temporarily adds the word to the exception
dictionary.  For example, if the word "noolo" existed and it contained three
syllables, entering \HY{no-o-lo} would tell TeX how to break it.
 
The second way to break a word is with the TeX macro \-, or "discretionary
hyphen".  This is used to define all hyphenation points for a single
occurrence of a word; the word is not added to the exception dictionary in
this case.  Using \- with "noolo" would look like:  no\-o\-lo.
 
The \- macro can also be used to specify hyphenation for accented words, since
only the hyphenation of alphabetic characters can be specified with the \HY
control.
 
See the description of the \HY control in Section 3 for more information.
Syntax:
\IDX
Description:
IDX includes an index in a document.  Indexes are generated from IX and Ln
controls.  The index is created as an auxiliary file during formatting, but
does not appear in a document unless the IDX control is encountered.  When IDX
is encountered, the document is reformatted with the index included at the
point marked by the control.
 
To have the index begin in a new section called "Index", with pages numbered
as i-1, i-2, etc., the CH control using the system-supplied INDEX style should
precede the IDX control.
 
If desired, text (but not index terms) can be inserted in the source file
between the CH control and the IDX control.
 
Note that the inclusion of the IDX control can significantly increase the
amount of time that it takes to completely format a document.  This is because
the formatter must make at least two passes through the document.
 
See the IX and CH control descriptions for additional information.
Example:
The following shows a complete document skeleton that includes a table of
contents and an index:
\CH{Preface|*|FRONT}
\TOC
\CH{Introduction|1|CHAPTER}
 
  (remainder of document)
 
\CH{|*|INDEX}
\IDX
 
Note in the above example that the \CH{|*|INDEX} control begins a new section
entitled "Index" to contain the index terms generated by IDX. Text can be
inserted between these two controls if desired.
00001
00002
Syntax:
\IL{fid}
Parameters:
 
fid  is a disk file identifier.
Description:
IL includes a literal file in a CAP source document without affecting DSL
controls.
 
IL is different from LT in that LT controls are themselves handled literally
in the included file.  See the LT control description for related information.
Example:
 
\IL{DSLSAMPLE}
 
The above example includes a literal file called DSLSAMPLE in the source
document.
00002
00003
00001
Syntax:
\IN{intype|distance}
 
The intype and distance parameters are required.
Parameters:
 
intype  specifies the type of indentation to be applied, as follows:
 
    R   defines a temporary right margin.  Offset is calculated from the
        right.
 
    L   defines a temporary left margin.  Offset is calculated from the
        left.
 
    B   defines matching temporary left and right margins.
 
    This parameter does not need to be enclosed inside the braces.
distance  is a dimension that specifies the distance of the indentation.  This
    parameter must be enclosed inside the braces.  Distance is calculated in
    units of Average Character Width (ACW) if a numeric value only (without a
    unit of measurement) is specified; inches, metric units, points, and picas
    can also be specified.
Description:
IN moves the left or right margins horizontally.  These margins are in effect
until the current group ends.
 
IN uses the concept of Average Character Width to calculate distances.  An ACW
is the width of the average character in the current font.
Examples:
 
This is some data that allows us to show the current margins for
comparison before and after the \TT{IN} control has been issued,
thereby altering the margins in a rightward and leftward direction.
\INL{5}
This is some data that allows us to show the current margins for
comparison before and after the \TT{IN} control has been issued,
thereby altering the margins in a rightward and leftward direction.
\INR{0.5in}
This is some data that allows us to show the current margins for
comparison before and after the \TT{IN} control has been issued,
thereby altering the margins in a rightward and leftward direction.
 
When formatted, the above appears as follows:
 
This is some data that allows us to show the current margins for comparison
before and after the IN control has been issued, thereby altering the margins
in a rightward and leftward direction.
 
     This is some data that allows us to show the current margins for
     comparison before and after the IN control has been issued, thereby
     altering the margins in a rightward and leftward direction.
 
     This is some data that allows us to show the current margins for
     comparison before and after the IN control has been issued, thereby
     altering the margins in a rightward and leftward direction.
00002
00003
00001
IN
IL
IS
The left margin is defined by the CAP administrator based on the output device
characteristics.  Indentation of text can be set, reset, and adjusted with the
\IN control.  Left indentation (\INL), right indentation (\INR), and
indentation of both margins (\INB) can be set for blocks of text.  The undent
control (\UNL) affects only the next immediate line of text and is used to
temporarily reverse the set indentation.
Alignment of text can be specified with the \AL control.  Left alignment
(\ALL), right alignment (\ALR), centered alignment (\ALC), and right and left
justification (\ALB) can be set for blocks of text.  The \AL control is used
in conjunction with the fill (\FI) control.
 
See the descriptions of the above controls in Section 3 for more information.
IX
IDX
IX
IN
The entry of DSL controls is free-form.  DSL controls can appear anywhere in a
line, and spaces can be inserted anywhere within a DSL control mnemonic and
its parameters.  For example:
 
the \IT{big} fish
the \IT {big} fish
the \IT    {big} fish
 
all print as
 
the big fish
 
A parameter or textual data enclosed in braces modifies the processing of a
control only if it is on the same line as the control mnemonic.  If it is not
on the same line, the braces are ignored and the processing indicated by the
control continues until another control is encountered.  For example, while
 
the \IT{big} fish
 
prints as
 
the big fish,
 
the \IT
{big} fish
 
prints as
 
the big fish
 
A blank space following an in-line control without parameters is treated as a
delimiter and does not generate a space.  For example:
 
the \IT big\NO fish
 
prints as
 
the bigfish;
 
the \IT big \NO fish
the \IT big\NO   fish
 
both print as
 
the big fish
 
DSL controls and text can be grouped to limit text manipulation to a
particular area of the source file.  See DSL Groups, later in this section.
 
All the DSL controls are described in detail in Section 3.
GI
IN
Syntax:
\IS{fid}
Parameters:
 
fid  is a disk file identifier.
Description:
IS includes a CAP source file inside another CAP source file.
Example:
 
\IS{DP#STATUS/MYMACROS.COSMIC.SECRET}
 
The above example includes a passworded file on volume STATUS.
00002
00003
00001
FF
Syntax:
\IX{ixterm|ixsub|ixstyle|sortterm|sortsub}
 
All parameters are optional except ixterm.
Parameters:
 
ixterm  specifies a word or phrase to be indexed.
ixsub  specifies a subterm to be indexed under the term.
ixstyle  specifies an administrator-defined style for the index term.  If not
    specified, the default style is used.
sortterm  specifies a nonprinting sort key for ixterm.
sortsub  specifies a nonprinting sort key for ixsub.
Description:
IX defines an index term.  Index terms are inserted into a file that is
automatically collated and included at the point in the document where an IDX
control is encountered, thus creating an index.
 
An IX control defining an index term should be placed as close as possible to
the term in the document source file, usually following the paragraph in which
the term appears in text.
The IX control can appear inside tables in a source file, but should be placed
before the TE or TX control, so that the index entry is in a table cell rather
than between table rows.
 
The IX may cause extra space while in fill-off mode.  If there were 10 \IX on
10 lines, you will get 10 lines of space.  But, if you have 10 \IX on 1 line
then you will get 1 line of space.  If this is occuring turn the fill mode on
(\FIN before defining the \IX and spacing will be normal.
 
The system-supplied default index style creates a permuted index.  That is,
for every index entry in the form ixterm|subterm, a second entry in the form
subterm|ixterm is created automatically.
 
The sortterm and sortsub parameters are used only when the index term or
subterm does not sort where desired.  This can occur when the term or subterm
is a macro (such as \TeX) or begins with a backslash character (\).  For
example, if \TeX is the ixterm, TeX prints at the beginning of the "T's" in
the index.  The word "tex" can then be entered as the sortterm so that TeX
will sort correctly in the index.
 
Note that sortterm and sortsub are optional.  When used, they do not print.
They are used only for sorting instead of ixterm and ixsub.  Macros can be
used in sortterm and sortsub, but only if they expand strictly to text.  Font
changes or other DSL or TeX controls, except for substitutions, cannot be
used.  See the Ln control description for additional sorting information.
 
See the IDX control description for additional information on indexes.
Administration:
 
The administrator controls the following:
 1. Permuting or no permuting of index entries.
 2. Font styles of index terms, subterms, and page numbers.
 3. Automatic indexing of level heads.
Defaults:
 
The system-supplied ixstyle defaults are:
 
DEFAULT  specifies the index term, subterm, and page numbers in the normal
    font for the selected document style.  The term and subterm are
    permuted.
 
NP  Same as the DEFAULT style, but the term and subterm are not permuted.
 
X   specifies the index term and page number in boldface.  The term and
    subterm are permuted.
 
Y   specifies the index subterm and page number in boldface.  The term and
    subterm are permuted.
 
LHEADS  includes level heads in the index, with the heads in italics and
    page numbers in normal font.
Examples:
 
Now is the time for all good men to come to the aid of
their country. \IX{country|aid}\IX{men}
The above example generates three terms in the index:
 
aid
  country - 1
country
  aid - 1
men - 1
 
Note that the first term ("aid") is the permuted index entry.
 
In the following example, the sortterm "tex" and the sortsub "clock" are used
to sort the entries alphabetically within the index (the default style is
used):
 
\IX{\TeX time and date macros|\clock||tex|clock}
00003
00004
00002
00005
00001
KT
Syntax:
 
\KT{ON}
   .
 data
   .
\KT
 
The ON parameter is required.
Description:
KT forces textual or structural data to remain on a single page.  Both the
opening and closing KT controls are required.
 
The area created by KT constitutes a group, and as such the enclosing KT
controls must be properly nested relative to any other DSL controls contained
between or outside them.  Any DSL controls activated within a KT area will be
deactivated (everything returns to its previous state) when the end of the KT
area is reached.  For example, if fill mode is turned off (FIF) and not turned
on again (FIN) between the KT controls, it will automatically be turned on
when the KT area ends.
 
KT areas should be kept as small as possible, or excessive white space or
other problems may result.  A KT area enclosing more than a page of text will
cause overfull pages.  KT should therefore be used carefully.
Example:
 
The following shows a correct use of KT:
 
\KT{ON}
This is a table that is to stay together.
\TB{My Table||2COL}
Data \TC Data \TE
Data \TC Data \TB
\KT
 
The table above will not be split across pages.
 
The following shows an incorrect use of KT:
 
\KT{ON}
This will not work because it splits the table.
\TB{My Table||2COL}
Data \TC Data \TE
\KT
Data \TC Data \TB
00001
00002
LN
LN
LN
LN
Syntax:
\LA{label}
 
The label parameter is required.
Parameters:
label  is a name that marks a position to be referenced in a document source
    file.
Description:
LA creates a symbolic name, or label, for a position inside a document.
Labels are referenced with the RF control.  Page numbers; structure numbers;
and titles, headings, and captions can be associated with labels and then
retrieved by using RF.
 
The label parameter can consist of any alphanumeric characters.  The
recommended characters for separating words or parts of a label are normal
punctuation characters such as hyphens, semicolons, periods, and commas.
Spaces can be used, but only if fill mode is on (FIN). Characters that are
part of DSL syntax, such as \, |, {}, and $, cannot be used.  Underscores (_)
also cannot be used.
 
Labels can be entered in most places in the source file.  A label always
refers to the word or heading immediately preceding it in the formatted
document; nested headings are honored.
 
Labels are entered in tables, figures, and graphics as follows:
 
LA controls in tables must go into a table cell and will indicate the page
number on which that cell appears.  Labels are not permitted with the TH
control, as TH creates headings that repeat from page to page.
 
LA controls in figures can go anywhere, and will indicate the actual page on
which the immediately preceding word appears, even if the figure is broken
across pages.
LA controls associated with graphics must immediately follow the GR control,
on the same or the next line, with no intervening blank lines, as the label
cannot go inside the graphic.
 
Note that cross-referencing may cause multiple formatting passes.  See the RF
control description for further information.
Example:
 
Why is this great and glorious country called America?
\LA{america-question} Principally because that is its name.
 
Assuming the above appeared on page 20 of a document, the following use of the
RF control
 
And if we examine the question that was asked on page
\RFP{america-question}, we see that there is really no valid answer.
 
would produce the following reference when formatted:
 
And if we examine the question that was asked on page 20, we see that there is
really no valid answer.
 
Additional examples of LA are presented in the RF control description.
00002
00003
00001
LA
MATH_CHARACTERS
LN
LN
SPECIAL_CHARACTERS
BR
HB
LT
IL
LT
Syntax:
\Ln{lhtitle|lhnum|lhsort}
 
All parameters are optional.
Parameters:
 
n   specifies the heading level number, 1 through 9.
lhtitle  is the text of the level heading.  If not specified, a heading is not
    printed, but the specification number is printed if the administrator has
    activated this feature.
lhnum  defines a specification number.  If the administrator-defined style
    does not use specification numbers, this parameter is ignored.  If the
    document style does use specification numbers, lhnum appears to the left
    of lhtitle when printed.  Specification numbers can include the chapter
    number.
    If lhnum is set to *, the associated heading is considered to be a "minor"
    heading.  In this case, no specification number will be printed or
    generated automatically if the document style uses specification numbers.
    Also, the heading will not be entered into the table of contents or index.
lhsort  specifies a nonprinting index sort key for lhtitle.
Description:
Ln defines the structure of information within a chapter or section.  The
levels can be compared to an outline, where each indentation represents a
deeper level of information.
 
The level number (n) determines the placement of the heading relative to other
headings and text, and the font style and size used to print the heading, all
based on administrator-defined defaults.
 
The specification number (lhnum) serves as an identifier or reference for
lhtitle, the level heading text, and reflects the level number (n) of that
text.  Each deeper heading level adds an additional number to the end of the
specification number.  For example, the first level 1 heading in Section 3 of
a document might be represented by a specification number of 3.1.  The first
level 2 heading under 3.1 would be 3.1.1.  The second level 2 heading under
3.1 would be 3.1.2.  The second level 1 heading would be 3.2.  The first level
2 heading under 3.2 would be 3.2.1, and so on.
 
Automatic generation of specification numbers and specification number styles
are determined by the administrator.
 
The lhsort parameter is used only when the level head style includes level
heads in the index, and lhtitle does not sort where desired.  This can occur
when lhtitle is a macro (such as \TeX) or begins with a backslash character
(\).  For example, if \TeX Control Sequences is the lhtitle, "TeX Control
Sequences" prints at the beginning of the "T's" in the index.  The words "tex
control" can then be entered as the lhsort key so that the level head title
will sort correctly in the index.
 
Note that lhsort is optional.  When used, it does not print.  It is used only
for sorting instead of lhtitle.  Macros can be used in lhsort, but only if
they expand strictly to text.  Font changes or other DSL or TeX controls,
except for substitutions, cannot be used.  See the IX control description for
additional sorting information.
Administration:
The administrator controls the following:
 1. Placement of the level heading text on the page.
 2. Font sizes used for printing the heading text.
 3. Changes to headers and footers as a result of the Ln control.
 4. Whether or not specification numbering is a default.
 5. Automatic generation of specification numbers.
 6. The style and placement of the specification numbering.
 7. Whether or not indexing is a default.
Defaults:
The default font sizes and types for headings are determined by the system-
supplied default document styles and corresponding level heading styles, which
can be redefined by the administrator.
 
There are no default effects to the footer.
 
By default, headings are entered into the table of contents and index.
Examples:
 
\CH{Angels|1}
\L1{Michael}
\L2{Auriel}
\CH{Demons}
\L1{Asmodeus}
\L2{Piewacket}
The above example defines a simple document skeleton, with two chapters each
containing two level headings.
00003
00004
00002
00005
00001
Syntax:
 
\LT{ON}
   .
   .
literal data
   .
\LT
 
The ON parameter is required.
Parameters:
 
ON  specifies that literal processing is to be turned on.
Description:
LT disables the special handling of brace characters and backslashes, turns
off fill mode, automatically invokes a monospaced font, and treats blank
spaces as horizontal tabulations equal to a character size.  During literal
mode, all characters are treated and printed as ASCII characters in the
monospaced font.  Literal mode continues until another LT control is
encountered.
 
Since the LT control is used to terminate literal mode, it cannot itself be
included in the literal text unless that text is in a file included with the
IL control.
 
LT honors carriage returns on a line, so if LT is on a line by itself, spacing
is not the same as with an LT inserted inside a line.
 
Literal mode can be defined inside a macro, but LT cannot be used in the text
that a macro acts on.
 
LT cannot be used inside parameters of other DSL controls.
Example:
 
\LT{ON}
This describes the \BRL control.
\LT
 
The above example, when formatted, appears as:
 
This describes the \BRL control.
 
Note that the BRL (break line) control was not activated because the passage
was in literal mode at the time BRL was encountered.
00002
00003
00001
DM
Macros and substitutions can be defined in DSL to make source file creation
easier.
 
Macros are defined with the \DM control, and contain a name and associated
contents.  The contents can include DSL controls and TeX macros as well as
text characters.  Once defined, a macro name can be used in the source file
like a DSL control.  For example, a macro could be defined to place a term in
teletype font, put a backslash (\) in front of the term, and enter the term in
the index, thus combining several actions into one.
 
Substitutions are defined with the \DS control, and also contain a name and
associated contents.  The contents can include DSL controls and TeX macros as
well as text characters.  When the substitution name is encountered in the
source file during formatting, the contents is substituted for it.  For
example, assume "CPSIX" is defined as a substitution name and "\SL{CP-6}" is
defined as its contents.  Then, whenever "\CPSIX" is encountered in the source
file, it will appear as "CP-6" when formatted.
 
Placement of macros and substitutions in a document assembly file is described
in the CP-6 CAP User Guide (HA29).
Commonly used math characters such as +;-=;><; and = can simply be entered
from the keyboard while in DSL math mode.  Other math characters require the
use of control words.
 
TeX provides control words for a wide variety of mathematical characters and
Greek letters, most of which must be entered in DSL math mode.
 
The following table shows several examples of these control words.  Note that
in the last two examples the character printed differs depending on whether
the first letter of the control word is upper- or lowercase.
 
          Character                  Enter (in math mode)  Prints As
 
          Alpha                      \alpha                 ?
 
          Beta                       \beta                  ?
 
          Circle                     \circ                  ?
 
          Multiplication sign        \times                 ?
 
          Division sign              \div                   ?
 
          Square root sign           \sqrt{n}               p-
                                                             n
          Ellipsis (horizontal)      \ldots                 ...
 
          Ellipsis (vertical)        \vdots                 .
 
          Greater than or equal sign \ge                    ?
 
          Less than or equal sign    \le                    ?
 
          Lambda                     \lambda, \Lambda       ?;?
 
          Pi                         \pi, \Pi               ?;?
 
The following is an example of the use of some of these characters in math
mode:
 
\MT{ON}
The result of $\alpha \div \beta$ turns out to be $\ge \pi$.
\MT
 
which prints as:
 
The result of ?? ?turns out to be  ??.
 
Additional examples of and further information on DSL math mode can be found
under Math Fonts earlier in this section, and in the \MT control description
in Section 3.  All of the math characters and Greek letters are described in
detail in The TeXbook.
DSL also supports TeX-style mathematical typesetting.  To enter mathematical
typesetting mode, math mode must be enabled using the \MT control.  When \MT
is ON, the dollar sign ($) is interpreted as a flag that moves in and out of
math mode.
 
For example:
 
\MT{ON}
This is a math area: $\left( \sum_{k=1}^n A_k \right)$
\MT
 
prints as:
 
                      -P           n
This is a math area:               k
                         =1A             k
                             ?
Within math mode, the dollar sign can be included as text by preceding it with
a backslash (\$).
Note that math mode uses its own font styles, which differ from the normal DSL
font for the currently defined document style.
Within the dollar sign flags, the circumflex (^) and underscore (_) characters
are used to indicate superscripts and subscripts, respectively, as in the
above example.  See The TeXbook for further information.
MT
Syntax:
 
\MT{ON}
   .
   .
 data
   .
$mathstuff$
   .
 data
   .
\MT
 
The ON parameter is required.
Parameters:
 
ON  activates mathematics processing.
 
data  represents normal textual data.
 
$mathstuff$  represents TeX mathematical typography controls.
Description:
MT turns on TeX math mode, in which the dollar sign ($) is a special flag that
allows the inclusion of mathematical symbols in text.  When math mode is
active, a dollar sign can be included in text by entering \$.  When math mode
is inactive, the dollar sign is entered and printed normally.
 
Note that math mode has its own font styles, which differ from the normal DSL
font for the currently defined document style.
 
Within the dollar signs, the circumflex (^) and underscore (_) characters are
used to indicate superscripts and subscripts, respectively.
Example:
 
\MT{ON}
While it seems on the surface that $f(y/2)$ would prove true to
cost \$25.00 or more, $y^2/x_n$ might indicate otherwise.
\MT
00002
00003
00001
Multicolumn mode can be used to format pages in up to five columns.  Multiple
columns are specified with the \CL control, which defines the number of
columns and the width of the gutters separating the columns.
The notation conventions used in the DSL control syntax and examples
in this manual are presented in the following table:
 
    Notation               Description
 
    Lowercase Letters      Lowercase letters (in italic font) indicate a
                           variable, to be replaced with a user-selected
                           value.  For example:
 
                           \IS{fid} could be entered as \IS{MyFile}.
 
    Uppercase Letters      Uppercase letters (in teletype font) indicate
                           a literal, to be entered as shown.  For
                           example:
 
                           \SPB{5}
 
                           must be entered exactly as shown.
 
    Special Characters     Special characters (such as \ or {) are
                           literals, to be entered as shown.
 
    Numerals               Numerals standing alone are literals, to be
                           entered as shown.  Numerals embedded in or
                           affixed to a string of uppercase letters are
                           also literals, to be entered as shown.
                           Numerals embedded in or affixed to a string of
                           lowercase letters are part of the variable
                           name to be replaced with a user-selected
                           value; for example, fid1.
 
    Braces ({})            Braces delimit the parameters of a DSL
                           control.  Braces can enclose variables or
                           literals which may be required or optional,
                           depending on the specific control.  The braces
                           themselves are required, unless otherwise
                           specified in the control description.
 
    OR Bar (|)             The OR bar separates elements in a list from
                           which one or more elements may be, or must be,
                           chosen.  For example:
 
                           \Ln{lhtitle|style}
 
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
                           \RM
 
                           means that controls and/or text could be
                           included between the the \IT and \RM controls.
CAP DSL has an on-line HELP facility.  CAP users can display syntax formats,
parameters, and descriptions of controls as well as descriptions of menu items
and related information.  For a list of HELP topics for DSL, enter the
following from the system command level (!):
 
HELP (DSL) TOPICS
The CAP formatting facilities can be viewed as a layered stack of
components, which work together to produce a formatted document. At the
bottom of the stack is the formatting program (TeX) that breaks the
document into pages.  At the top of the stack is the document that the
user wants to format.  The stack can be visualized as follows:
 
                                   Document
 
                                   DSL
 
                                   ADSL
 
                                   CapTeX
 
                                   TeX
 
A CAP document source file contains Document Structuring Language (DSL)
controls and text.  A DSL control is an instruction that defines a
structural element in the document, such as a new section, paragraph,
table, or figure, or specifies formatting information such as indentation
and spacing. The text is the actual textual information in the form of
sentences, lists, tabular data, etc.
 
The writer (the CAP user) creates the textual content of the document
and uses the DSL controls to structure the document.  The CAP administrator
uses the Administrative Document Structuring Language
(ADSL) to define the format styles to be associated with the DSL controls.
The CapTeX macro program contains the TeX definitions of
the DSL and ADSL controls. When the writer formats the document with CAP,
ADSL and CapTeX interpret the writer's DSL controls to create the
document in the administrator-defined format selected by the writer.
 
Thus the writer determines the contents of a document, while the
administrator determines the format or appearance of the document.
BR
A wide variety of formatting and style options are available to the
CAP user with DSL, as follows:
 
o   Odd and even page styles - different headings, footings, and
    layouts conditional on the facing of the page can be defined.
 
o   Heading styles - section, chapter, module, and paragraph headings
 
    can be defined to appear in various type styles and locations on the
    page, with or without page numbering and related headers and footers.
 
o   Named structures - most structural elements in a document (chapter,
 
    heading, paragraph, table, figure, index, etc.) can have multiple
    named variations. For example, a chapter structure can be specified as
 
    front matter, a section, an appendix, or an index; a table can be
    specified as being from 1 to 10 columns, etc.
 
o   Paragraph lists - items can be listed in various format styles.
    Numbered, lettered, and bulleted lists are automatically indented and
 
    spaced based on the particular style selected; additional DSL controls
    for indenting and spacing are not required.
 
o   Table definition - simple and complex table formats are available.
 
    Tables can be internally formatted, so that multiple-column tables can
    have formatted passages inside each column.
 
o   Page numbering styles - CAP allows Arabic page numbers as well
 
    as upper- and lower-case Roman page numbers, as a function of chapter
    style.
 
o   Running headers and footers - these are a function of the title
 
    page and chapter style, and are invoked automatically whenever a
    document is formatted.
 
o   Widow control - paragraphs tend to stay on one page.  The TeX formatter
    automatically "walks copy" to ensure an attractive, logical
    appearance.
 
o   Keep-together blocks - passages which should not be split over
 
    two pages can be flagged and moved to the next available full page,
    if necessary.
 
o   Footnote generation - footnotes are defined next to the passage
    to which they refer.  During formatting, they are automatically
 
    numbered and placed on the current page.
 
o   Hyphenation - the TeX formatter automatically applies an
    algorithmic formula to determine where a word should be broken. An
 
    exception dictionary, user global exceptions, and discretionary
    hyphenation are available.
 
o   Extended character handling - proportional spacing, multiple
    fonts, and foreign language characters are available.
 
o   Mathematical typesetting - documents can include complex
 
    mathematical formulas, either inside a line or set apart as equations.
 
o   True horizontal justification - lines are automatically stretched
    to fit the right margin.
 
o   True vertical justification - pages are automatically stretched to
 
    fit the entire page.
Next to the text itself, the paragraph is the most basic structure in a DSL
document.  A paragraph is any segment of text that is delimited by a blank
line or by a DSL control that causes a paragraph break, such as a structural
or formatting control.  Some DSL controls, such as \BRL (line break), \SPH
(horizontal space), \LT (literal mode), and font controls affect the text
and/or its spacing within a paragraph, but do not break the paragraph.  As
with other structures, DSL generally tries to keep paragraphs together on the
same page.
 
Paragraph formatting, including leading indentation, is determined by the
paragraph style set by the administrator.
PI
PL
Lists of items can be created with DSL in a variety of administrator-defined
styles, such as numbered, lettered, bulleted, or beginning with a word or
phrase.  The writer needs only to select a particular listing style and
identify the list items; indentation and spacing are automatically set within
the predefined style.  No additional controls are required.
 
The \PL control is used to create a list of items in a particular style.  The
\PI control is used to indicate items in the list.  For example:
 
\PL{ARABIC}
  \PI This is the first list item.
  \PI This is the second list item.
  \PI This is the third list item.
  \PI This is the fourth list item.
\PL
 
When formatted, the list appears as:
 1. This is the first list item.
 2. This is the second list item.
 3. This is the third list item.
 4. This is the fourth list item.
 
Note that paragraph lists can be nested, as long as each \PL control has a
matching \PL (without the paragraph style parameter) to close it.
Syntax:
\PI{piname}
 
The piname parameter is optional, depending on the plstyle parameter selected
on the related PL control.
Parameters:
 
piname  specifies a label to be included at the beginning of the paragraph
    item.
Description:
PI designates an item in a paragraph list.  The way that the formatter reacts
to PI depends on the paragraph listing style set in the previous PL control.
See the PL control description for more information.
Administration:
None.
Defaults:
None.
Examples:
 
\PL{ARABIC}
\PI First I want to go to the museum, where I can look at the strange
    and curious monsters.
 
    Then I want to go home, where I can watch situation comedies on the
    television.
\PI Now I am done with this document.
\PL
 
When formatted, the above passage appears as:
 1. First I want to go to the museum, where I can look at the strange and
    curious monsters.
    Then I want to go home, where I can watch situation comedies on the
    television.
 2. Now I am done with this document.
 
If the paragraph listing style ARABIC is changed to BULLETS in the example
above, the passage prints as follows:
 
o   First I want to go to the museum, where I can look at the strange and
    curious monsters.
 
    Then I want to go home, where I can watch situation comedies on the
    television.
o   Now I am done with this document.
 
Nested PL controls allow for complex outline structures:
 
\PL{ROMAN}
 \PI This is a description of a machine.
 \PL{CAPITALS}
  \PI This is the description of the first part.
  \PI This is the description of the second part.
 \PL
 \PI This is a generalized description.
\PL
This is another.
 
When formatted, the above appears as:
 
I.  This is a description of a machine.
 
    A.  This is the description of the first part.
    B.  This is the description of the second part.
II.  This is a generalized description.
 
This is another.
 
Note that the final PL control above reset the margin and ended the paragraph
list.
00003
00004
00002
00005
00001
Syntax:
 
\PL{plstyle}
   .
 data
   .
\PL
 
The plstyle parameter is required.
Parameters:
 
plstyle  is a paragraph listing style.  These styles are defined by the
    administrator.  If omitted, paragraph list processing is returned to the
    administrator-defined default.
Description:
PL determines the listing structure to be used when a PI control is
encountered in the source file.
 
Indentation levels are controlled by the nesting level of the PL controls.
 
Note that PL controls must be nested properly - each PL must have a matching
PL to close it.  Failure to do this produces an error message.  However, PL
processing is cancelled whenever a TP, CH, Ln, TB, GR, FG, or HH control is
encountered.
Administration:
The administrator can create different named paragraph styles as needed to
support a given environment.  The administrator controls the following:
 1. Space before and after the paragraph list.
 2. Indentation of list items.
 3. Space between list items.
 4. Style and placement of labels for list items.
Defaults:
The system-supplied plstyle defaults are as follows.
 
DEFAULT  no indentation, no special handling.  Synonym:  STANDARD.
 
ROMAN  indent paragraph but not first line, number with I., II., etc.
    Synonym:  RO.
 
CAPITALS  indent paragraph but not first line, number with A., B., etc.
    Synonym:  CA.
 
ARABIC  indent paragraph but not first line, number with 1., 2., etc.
    Synonym:  AR.
 
NUMBERLIST  same as ARABIC, except that there are no spaces between the
    paragraph items.  Synonym:  NL.
 
ORDINALS  indent paragraph but not first line, number with a., b., etc.
    Synonym:  OR.
 
SUBARABIC  indent paragraph but not first line, number with 1), 2), etc.
    Synonym:  SA.
 
SUBORDINALS  indent paragraph but not first line, number with a), b), etc.
    Synonym:  SO.
 
BULLETS  indent paragraph but not first line, mark with bullet
    (o) characters.  Synonym:  BU.
 
BULLETLIST  same as BULLETS, except that there are no spaces between the
    paragraph items.  Synonym:  BL.
 
DASHES  same as BULLETLIST, except that paragraph items are marked with a
    double dash (--) instead of bullets.  Synonym:  DS.
 
DARTS  same as BULLETLIST, except that paragraph items are marked with a
    single dash and a greater than sign (->) instead of bullets.
    Synonym:  DR.
 
DESCRIBE  indent paragraph but not first line, mark with the contents of
    the PI control, which appear in boldface.  Synonym:  DE.
 
DESCRIBE_ITALICS  same as DESCRIBE, except that the contents of the PI
    control are printed in italics.  Synonym:  DI.
 
WIDEDESCRIBE  same as DESCRIBE, except that the indentation is doubled.
    Synonym:  WI.
 
SYNTAX  same as DESCRIBE, except that the text following the PI control is
    printed in teletype.  Synonym:  SY.
 
ITEM  no indentation, put the contents of the PI control on its own line,
    printed in boldface.  Synonym:  IT.
 
Note that the piname parameter (including braces) is required on the PI
control for paragraph list styles that use an expression as a label, such as
DESCRIBE above.  The piname parameter is not required for styles that use a
number or a letter as a label, such as ARABIC above.
Examples:
 
\PL{DE}
\PI{First Step.} Prepare the outline.
\PI{Second Step.} Write the draft.
\PI{Third Step.} Review the draft.
\PI{Fourth Step.} Revise the draft.
\PL
 
See the description of the PI control for additional paragraph list examples.
00003
00004
00002
00005
00001
RF
Additional CAP information is presented in the following manuals:
 
CAP ADSL Reference, Order No. HA28
CP-6 CAP User Guide, Order No. HA29
CP-6 CAP Administrator Guide, Order No. HA30
Syntax:
\RF{rftype|label}
 
The rftype and label parameters are required.
Parameters:
 
rftype  specifies the type of cross-reference information to be retrieved, as
    follows:
 
    P   retrieves a page number associated with a label.
 
    N   retrieves the number of a chapter, level head (specification
        number), figure, table, or graphic associated with a label.
 
    H   retrieves a heading associated with a label.  A heading can be a
        chapter title; level heading; or figure, table, or graphic title.
 
    This parameter does not need to be enclosed inside the braces.
label  is the label parameter on the corresponding LA control.  label is a
    symbolic name for a position in a document source file.  This parameter
    must be enclosed in braces.
Description:
RF is used to reference a position marked by the LA control inside a document.
RF retrieves a page number, structure number, or heading associated with a
label specified by LA.
 
The RF control can be entered anywhere in the source file.
 
For example, assume that the writer specifies a label after a level heading.
When this same label is referenced in the RF control (RFH in this case), the
level heading title appears in the formatted document text at the point at
which RF was entered in the source file.  Similarly, a label specified in text
that formats on a particular page would produce a reference to that page
number when used with the RFP control at another place in the source file.
References to other structure numbers and titles work in a like manner.
 
Note the following regarding the use of RF and LA:
 1. Labels entered before the first chapter or level heading (if any) in a
    document cannot be referenced by chapter or heading title (RFH) or chapter
    or specification number (RFN), but can be referenced by page number (RFP).
 2. Labels entered after a chapter title but before the first level heading
    can be referenced by the chapter title and number.
 3. Labels entered after the first level heading can be referenced by the
    level heading title and specification number, if any.
 4. Page number references (RFP) always refer to the page on which the word
    preceding the label appears, not where the level heading or chapter title
    appears, unless the LA control is entered close to the Ln or CH control.
 
Both backward references (LA before RF) and forward references (RF before LA)
can be made.  Forward references require the use of a document style that can
make two or more passes during formatting of the source file, since the labels
are held on the first pass and matched with the references on the second pass.
 
See the LA and Ln control descriptions for additional information.
Administration:
The administrator defines what is to be printed if a reference is made to an
undefined label.  The system-supplied default is to print ??  in this case.
Examples:
 
\CH{The Details|3} \LA{chapter-ref}
  .
  .
  .
\L3{Detailed Description}
\LA{header-ref}
 
This is a detailed description containing more information.\LA{details}
 
Assuming the level heading and related text above appeared on page 3 of the
chapter, the following use of RF
 
If you require more information, see the \RFH{header-ref} subsection in
Chapter~\RFN{chapter-ref}, on page~\RFP{details}.
 
would produce the following references when formatted:
 
If you require more information, see the Detailed Description subsection in
Chapter 3, on page 3-3.
 
Note that the tie character or tilde (~) is used above so that the page and
structure numbers will not be separated from the introducing text.
 
In the following example, both a figure number and figure title are
referenced:
 
\FG{My Figure|3} \LA{last.figure}
Figure text.
Figure text.
Figure text.
\FG
 
(any amount of text could be here)
 
The concept of figure text is illustrated in Figure~\RFN{last.figure},
\RFH{last.figure}.
 
Assuming the figure was in Chapter 3, the above sentence appears as follows
when formatted:
 
The concept of figure text is illustrated in Figure 3-3, My Figure.
00003
00002
00004
00001
FF
TR
The following example shows how a table is entered:
 
\TB{My Table|*|COL|3}
\TH{Column 1 \TC Column 2 \TC Column 3}
This is some data. \TC This is some more. \TC This is some more. \TE
This is some data. \TC This is some data. \TC This is some more
                                              and some more and
                                              some more and a
                                              little bit more.
\TB
My Table      is the writer-defined title.
*      specifies that the table is not numbered.
COL      is the administrator-defined table style.
3      is the number of columns.
are column headings.
TC and TE      are table controls that delimit the contents of each cell (TC)
and the end of a row of cells (TE).
 
When formatted, the table appears as follows:
 
  Column 1                Column 2                  Column 3
 
  This is some data.      This is some more.        This is some more.
 
  This is some data.      This is some data.        This is some more and
                                                    some more and some more
                                                    and a little bit more.
00002
00004
00003
00001
00006
Syntax:
 
\SB{sbname}
(data for subset 1)
\SB{sbname}
(data for subset 2)
   .
\SB{}
(data for any other subset)
\SB
Parameters:
 
sbname  specifies a subset name.  Subset names can consist of any alphanumeric
    characters, as well as normal punctuation characters such as commas,
    periods, and semicolons.  Spaces can be used, but only if fill mode is on
    (FIN). Characters that are part of DSL syntax, such as \, |, {}, and $,
    cannot be used.  Underscores (_) also cannot be used.
Description:
SB defines subset areas that are included in a document for a particular
audience, subject, or purpose.  The subset capability allows a single document
to be modified for several purposes, such as differing levels of detail for
various audiences or differing functions used to accomplish the same
individual task.
 
Multiple subsets can be included in a single document, and specified for that
document during formatting.  Multiple subsets are useful when a document
contains different kinds of audience-specific data.
 
An area marked with SB is only included in a formatted document if the
formatting job recognizes the subset name.
 
Subsets (sbname) can be specified by the user through an option on the CAP
Formatting Options menu.  Multiple subsets are specified by separating the
subset names with commas.  Specifying subsets through this menu is described
in the CAP HELP facility.
 
If ALL is selected for sbname (even if other subsets are also selected), all
of the subsets and their related data are printed, in an administrator-defined
format.
 
Otherwise, the data for all subsets specified for the formatting job are
printed.  If no match is found between the subsets in the source file and
those specified for the job, or if no subset is specified, the data for the
\SB{} subset, if any, is printed.
 
Subset names are case-sensitive and must be specified during formatting in
exactly the same way as they are entered in the source file; ALL must be
specified in capital letters.
Note:
The \SB will not eliminate any spaces within the subset text definition.
Examples:
 
GLARP is a useful imaginary program. It runs on the
\SB{CP6} CP-6 \SB{GCOS} GCOS-7 \SB operating system.
\SB{CP6}CP-6\SB{GCOS}GCOS-7\SB operating system.
 
GLARP supports the FRED, JOE, and HARVEY options.
\SB{HELP}
For information on a specific option, enter:
 
HELP (GLARP) option
\SB{}
These options are described below.
\SB
 
If the CP6 subset is specified at formatting, the above passage appears as:
 
GLARP is a useful imaginary program.  It runs on the CP-6 operating system.
GLARP supports the FRED, JOE, and HARVEY options.  These options are described
below.
 
If GCOS,HELP are the subsets specified at formatting, the above passage
appears as:
 
GLARP is a useful imaginary program.  It runs on the GCOS-7 operating system.
GLARP supports the FRED, JOE, and HARVEY options.  For information on a
specific option, enter:
 
HELP (GLARP) option
 
If the ALL subset is specified at formatting, all of the subsets appear as
follows:
 
GLARP is a useful imaginary program.  It runs on the [CP6:  CP-6] [GCOS:
GCOS-7] operating system.
 
GLARP supports the FRED, JOE, and HARVEY options.  [HELP: For information on a
specific option, enter:
 
HELP (GLARP) option] [:  These options are described below.]
00002
00004
00003
00001
CH
FF
IS
Syntax:
\SP{sptype|value}
 
All parameters are optional.
Parameters:
 
sptype  specifies the type of space to be generated, as follows:
 
    B   means space downwards and break the current paragraph.  This is
        the default if sptype is not specified.
 
    F   means space downwards and don't break the current paragraph.
 
    H   means space to the right, horizontally.
 
    This parameter does not need to be enclosed inside the braces.
value  is a dimension that specifies the distance to space.  This parameter
    must be enclosed inside the braces.  If a numeric value only (without a
    unit of measurement) is spcified, distance is calculated in units of
    Average Character Height (ACH) for downwards movement and Average
    Character Width (ACW) for horizontal movement.  Inches, metric units,
    points, and picas can also be specified.  The default is 1 ACW or 1 ACH,
    depending on sptype.
Description:
SP inserts either horizontal (to the right) or vertical (downwards) space.
 
SP uses the concepts of Average Character Width and Average Character Height
to calculate distances.  An ACW is the width of the average character in the
current font.  An ACH is the height of the average character in the current
font.
 
Note that the amount of space specified by the SPB and SPF controls is added
to the amount of interparagraph spacing set by the administrator.
 
Consecutive SP controls produce an amount of space equal to the largest single
distance specified.  For example, SPB{2} SPB{4} SPB{5} are equivalent to
SPB{5}.
 
Specifying an SPB (or SP) between two lines produces a paragraph break.
Specifying SPB{0} produces a single blank line.
Example:
 
One of these gibberings poses the question:
\SPB
"What is love?"
\SPF
and answers it with:
\SPB{2}
"Five feet of\SPH{2.5in}heaven in a pony tail."
 
When formatted, the above appears as follows:
 
One of these gibberings poses the question:
 
"What is love?"
 
and answers it with:
 
"Five feet of                         heaven in a pony tail."
00002
00003
00001
DSL does not normally use space characters for positioning text strings on a
page.  Instead, DSL treats space characters as delimiters, to indicate where
text ends and begins.
 
Space characters are used by DSL as character or word delimiters rather than
for horizontal positioning.  Multiple occurrences of spaces are compressed to
a single space when formatted.
 
For example, TeX interprets
 
My  name  is                         Godot.
 
identically to
 
My name is Godot.
 
Both of the above print as:
My name is Godot.
 
Note that the above is true only if fill mode (wordwrap) is on.  The \FIN
control turns fill mode on, and is the system-supplied default.  The \FIF
control turns fill mode off, causing the spacing of each output line to be the
same as the spacing at input.  However, character transformations are still
made, and other DSL controls are interpreted normally.
 
The \LT{ON} control turns everything off.  This is called literal mode because
all the input is treated literally; that is, as it appears in the source file.
Multiple spaces appear as entered, as do multiple blank lines (described in
the next subsection).  During literal mode, no DSL controls are honored nor
character transformations made until an \LT control (with no ON parameter) is
encountered.  Then processing returns to whatever was active before the
\LT{ON} control was issued.
 
Even during fill mode, required spaces can be inserted into a document by
preceding each space with the backslash character (\ ).
 
For example:
 
Break \ \ \ \ \ \ break
 
prints as:
 
Break       break
 
The \SP control can also be used to insert a required amount of horizontal
space (\SPH).
 
Words can be tied together using the tilde character (~).  The tilde prints as
a blank, but the words thus tied together will not be separated between two
output lines.  For example, entering Section~2 will always keep "Section" and
"2" together on the same line.  The tilde should not be used to tie long
strings of words together, however, as this will prevent TeX from breaking the
line with the correct hyphenation.
SP
SP
TeX allows the printing of foreign language ligatures (diphthongs) and special
letters, with the following control words:
 
            Character                          Enter     Prints As
 
            French ligature OE                 \oe, \OE  oe, OE
 
            Latin and Scandinavian ligature AE \ae, \AE  ae, AE
 
            Scandinavian A-with-circle         \aa, \AA  a, A
 
            Scandinavian O-with-slash          \o, \O    ?, ?
 
            Polish suppressed-L                \l, \LL    l, L
 
            German "ess-zet" or sharp S        \ss       ?
 
See Fonts earlier in this section for usage examples of some of these control
words.  Note the use of braces (instead of spaces) to delimit the control
words in those examples.
 
TeX also allows the printing of nonmathematical symbols such as the following:
 
                   Symbol                   Enter Prints As
 
                   Dagger (obelisk)         \dag  *
 
                   Double dagger (diesis)   \ddag z
 
                   Section number sign      \S    x
 
                   Paragraph sign (pilcrow) \P    {
The following additional TeX control sequences are useful in creating a CAP
source file:
 
o   \- ("discretionary hyphen")
o   \/ ("italic correction")
o   \TeX
o   \copyright
 
The "discretionary hyphen", \-, is used to define hyphenation points for a
single occurrence of a word, as described under Hyphenation earlier in this
section.
 
The "italic correction", \/, is used to maintain an equal amount of space
between italicized or slanted text and normal (default) text.  Consider the
following example, without the italic correction:
 
These words (\IT{are italicized}) but these words \SL{are slanted}! These
other words are normal.
This prints as:
 
These words (are italicized) but these words are slanted!  These other words
are normal.
 
With the italic correction, the example looks like this:  These words (\IT{are
italicized}\/) but these words \SL{are slanted}\/!
These other words are normal.
 
This prints as:
 
These words (are italicized) but these words are slanted!  These other words
are normal.
 
The \TeX control sequence is used to print the TeX logo.  Remember to insert a
space preceded by a backslash (\TeX\ ) if a space between TeX and the
following character is desired.
 
The \copyright control sequence is used to print the copyright symbol, (c).
For example:
 
\copyright\ Bull HN Information Systems Inc.
which prints as:
 
(c) Bull HN Information Systems Inc.
SP
SP
FF
Syntax:
\ST{area}
Parameters:
 
area  specifies the area of the text to be struck through.
Description:
ST causes areas of the text to be struck through.
 
The ST control is currently not fully implemented, in that strikethrough text
areas that are longer than the width of the page will not wordwrap in fill
mode.  Wordwrap will occur, however, if each word of the strikethrough area is
individually enclosed in an ST control.
 
An alternative to using underline is to use a font other than normal (such as
italics) to represent the strikethrough text.
Example:
 
\FIF
This is a test of the \ST{strikethrough} function.
\IT{This is a test of the \ST{strikethrough} function.}
\FIN
 
The following is an example of how to handle a strikethrough area longer than
the width of the page:
 
This is a test of the \ST{strikethrough} function.  \ST{The}
\ST{strikethrough} \ST{text} \ST{extends} \ST{past} \ST{the} \ST{width}
\ST{of} \ST{the} \ST{page}.
00002
00003
00001
ST
DSL performs document formatting based on structures.  A structure is a
logical, useful division of a document, such as a chapter, section (the text
from one level head to the next), table, figure, or paragraph.  Structures can
contain lower-level structures within them, such as sections within a chapter.
The lowest-level structure is the text itself.
 
DSL structural controls are used to logically separate one portion of a
document from another.  Structural controls include \TP (title page), \CH
(chapter), \Ln (level head), and \PL (paragraph list).  Structural controls
are differentiated from formatting controls, which manipulate the position and
placement of text on the page.  Formatting controls include \FI (fill mode, or
wordwrap), \SP (spacing), \IN (indentation), \AL (alignment), and \CL
(multiple columns).
 
DSL tries to keep structures on a single page.  A structure enclosed inside a
keep-together (\KT) area will never be broken.  The \BRX control ties two
structures together so that DSL will not tend to break between them.
PAGE_FORMATTING
Subset areas can be defined in a document source file for a particular
audience, subject, or purpose by using the \SB control.  The subset capability
allows a single document to be modified for multiple needs, such as different
levels of detail for various audiences or different command syntax for
different systems that perform similar functions.
SB
DS
CONTROL_SUMMARY
SPECIAL_CHARACTERS
This subsection presents an overview of DSL table terminology, creation, and
controls, and provides an example of table entry and formatted output.
TB
TC
TE
TX
The following DSL controls are used to create tables:
TB      Table Build.  Defines the table title and calls the predefined table
style.
TH      Table Heading.  Defines the column headings for the table.
TC      Table Cell.  Marks the end of a table cell.
TJ      Table Join.  Joins several cells into a single cell to permit spanning
of columns within the table.
TE      Table Cell End.  Marks the end of a row of table cells.
TX      Table Cell Exit.  Marks the end of a row of table cells but does not
insert the normal horizontal rule between rows (as defined by the
administrator).  This control effectively allows the user to break a row
containing a large cell or cells to permit a page break.
TR      Table Rule.  Produces a horizontal rule across the table.
TS      Table Space.  Inserts vertical space between table rows.
00001
00003
00005
00002
00004
00007
00008
00006
TH
TJ
TOC
A table of contents is automatically created during formatting when the \TOC
control is included in the document source file.  The table of contents
includes all of the chapter titles; level heads; and table, figure, and
graphic titles in the document.
 
The \TOC control should be included in the source file after the preface or
similar front matter material, so that the table of contents pages will be
numbered in the same page numbering style as the rest of the front matter,
usually lowercase Roman.
 
The terms that go in a document's index are specified throughout the source
file with the \IX control.  During formatting, these terms (and the level
heads, if specified by the administrator) are automatically collated and
sorted to produce the index when the \IDX control is included in the source
file.
 
The \IDX control should be included at the end of the source file (or end of
the last source file if there is more than one).  To have the index begin in a
new section called "Index" with pages numbered as i-1, i-2, etc., the \CH
control using the system-supplied INDEX style should precede the \IDX control.
 
The \TOC, \IDX, \IX, and \CH controls are described in detail in Section 3.
TR
TS
The following terms are used to describe table creation with DSL:
table      an independent block of a formatted document, separate from the
text; a table is different from a figure in that a table contains cells.
style      an administrator-defined table structure which the writer calls to
obtain a table of a given appearance, to best suit the particular data to go
in the table.  Table styles that are page-related and that are content-related
are available, as described under the TB control in Section 3.
cell      an individual area inside a table where words or numbers are
positioned.
row      a set of cells laid horizontally across the page.  A row always
appears on a single page; it is never split between pages.  (See, however, the
TX control description in Section 3.)
rule      a line inside a table; rules generally separate the cells of a
table.  However, not all table styles use rules.
table control      a DSL control that delineates the parts of a table (cells
and rules).  The table controls are TB, TH, TC, TJ, TE, TX, TR, and TS.
non table control      a DSL control that determines how data will appear
within a cell of the table.  In general, any DSL control can be included in a
table cell; however, structural controls (like CH) are obviously inappropriate
for table use.
00003
00007
00004
00005
00002
00001
00006
Syntax:
 
\TB{tbtitle|tbnum|tbstyle|tbcols|tbwidth}
   .
 data
   .
\TB
 
The braces are required on the introducing TB control.
Parameters:
 
tbtitle  is the title of the table.  If omitted, no title is printed.
tbnum  is the current table number.  If omitted, the current value of tbnum is
    incremented by 1.  If * is specified, no table number is assigned and the
    table is not entered into the table of contents.
tbstyle  is an administrator-defined table style.  If no style is specified,
    the DEFAULT style is used.
tbcols  specifies the number of columns in the table.  This parameter is
    required.
tbwidth  specifies the width of the table in inches, metric units, points, or
    picas.  This parameter can be used only with large table styles with
    variable-size columns (described below).  Otherwise, it is ignored.
Description:
TB defines a table, which is constructed according to the rules defined in the
specified style.  If the table is larger than the remainder of the current
page, the title and table number are repeated on each page.
 
There are two basic types of table styles defined by the administrator:  large
tables and small tables.
 
Large table styles permit multiple-line, paragraphed text within table cells;
large tables can continue over many pages in a document.  Large tables can be
defined by the administrator as having either variable- or fixed-size columns.
When a large table with variable columns (such as the MATRIX style described
below) is formatted, the available page width is divided evenly into the
number of columns specified in the tbcols parameter.  When a large table with
fixed columns (such as the OPT style described below) is formatted, the column
width is whatever the administrator specified in the table style definition.
The administrator can also define large table styles that have both variable
and fixed columns in a single table.
 
The administrator can define small tables to permit paragraphed or single-line
text within table cells; the system-supplied default table styles (described
below) permit single-line cell entries only.  Small tables are normally used
for data that can fit on a single page.  When a small table is formatted, the
width of the table columns adjusts to the width of their contents, so the
overall width of the table depends on the width of the data in its widest
column.
 
There is no difference in the way large and small table styles are specified
by the writer on the TB control.  The writer chooses the name of a large or
small style from the list of table styles and their specifications supplied by
the administrator.
 
The writer should choose a large or small table style that suits the data.  If
a small table style is chosen and data exceed the page width, then a large
table style should be used.
 
See also the descriptions of the TC, TE, TH, TJ, TS, and TX controls.
Administration:
The administration of tables is complex, as it involves the interaction of
columns, rules (lines), column headings, and pages.  The administrator
controls the following:
 
   Presence of vertical and horizontal rules and outer boxing.
   Number of table cells.
   Format of table cell contents.
   Style definition:  large tables (with variable or fixed columns, or both)
   or small tables.
   Ability of tables to float to the next available page.
   Presence, position, and format of table numbers and captions.
   Space around the table.
   Presence of table numbers and captions in the contents' list of tables.
Defaults:
 
The system-supplied tbstyle defaults are:
 
DEFAULT  is a small table which is boxed, ruled, numbered by chapter, and
    captioned.  This is the table style used if no style is specified on
    the TB control.
 
SIMPLE  is the same as the DEFAULT style, but without horizontal rules
    between rows and vertical rules between columns.
 
PLAIN  is a small table without boxing, rules, table numbers, or captions.
 
MATRIX  is a large table which is boxed, ruled, numbered by chapter, and
    captioned.  Synonym:  COL.
OPT  is a large table with two uneven columns used primarily for computer
    command options.  It is boxed, ruled, numbered by chapter, and
    captioned.
 
OPTN  is the same as the OPT style, but without table numbers or captions.
Examples:
The following figure shows three large and three small tables.  The second
large table uses the tbwidth parameter to limit the table width to 5 inches.
The third small table, in style PLAIN, does not print the table title and
number.
 
\TB{Large Table One||MATRIX|2}
\TH{Column 1 \TC Column 2}
This is some textual data.  This is some more textual data and this is
some more and some more.
\TC
This is some textual data.  This is some more textual data and this is
some more and some more.
\TE
This is some textual data.  This is some more textual data and this is
some more and some more.
\TC
This is some textual data.  This is some more textual data and this is
some more and some more.
\TB
 
\TB{Large Table Two||MATRIX|3|5in}
\TH{Column 1 \TC Column 2 \TC Column 3}
This is some textual data.  This is some more textual data and this is
some more and some more.
\TC
This is some textual data.  This is some more textual data and this is
some more and some more.
\TC
This is some textual data.  This is some more textual data and this is
some more and some more.
\TE
This is some textual data.  This is some more textual data and this is
some more and some more.
\TC
This is some textual data.  This is some more textual data and this is
some more and some more.
\TC
This is some textual data.  This is some more textual data and this is
some more and some more.
\TB
\TB{Large Table Three||OPT}
\TH{Command \TC Description}
COPY source over destination (options)
\TC
This is some textual data.  This is some more textual data and this is
some more and some more.  This is some textual data.  This is some more
textual data and this is some more and some more.
\TE
COPY source over destination (options)
\TC
This is some textual data.  This is some more textual data and this is
some more and some more.  This is some textual data.  This is some more
textual data and this is some more and some more.
\TB
 
\TB{Small Table One||DEFAULT|3}
\TH{Column 1 \TC Column 2 \TC Column 3}
This is test line 1. \TC This is test line 2. \TC This is test line 3.
\TE
This is test line 4. \TC This is test line 5. \TC This is test line 6.
\TE
This is test line 7. \TC This is test line 8. \TC This is test line 9.
\TB
 
\TB{Small Table Two||SIMPLE|3}
\TH{Column 1 \TC Column 2 \TC Column 3}
This is test line 1. \TC This is test line 2. \TC This is test line 3.
 
\TE
This is test line 4. \TC This is test line 5. \TC This is test line 6.
\TE
This is test line 7. \TC This is test line 8. \TC This is test line 9.
\TB
 
\TB{Small Table Three||PLAIN|3}
\TH{Column 1 \TC Column 2 \TC Column 3}
This is test line 1. \TC This is test line 2. \TC This is test line 3.
\TE
This is test line 4. \TC This is test line 5. \TC This is test line 6.
\TE
This is test line 7. \TC This is test line 8. \TC This is test line 9.
\TB
 
When formatted, the file in the above figure appears as follows:
 
  Column 1                             Column 2
 
  This is some textual data.  This is
  some more textual data and this is
  some more and some more.             This is some textual data.  This is
                                       some more textual data and this is
                                       some more and some more.
  This is some textual data.  This is
  some more textual data and this is
  some more and some more.             This is some textual data.  This is
                                       some more textual data and this is
                                       some more and some more.
 
                Column 1       Column 2        Column 3
 
                This is some
                textual data.
                This is some
                more textual
                data and this
                is some more
                and some more. This is some
                               textual data.
                               This is some
                               more textual
                               data and this
                               is some more
                               and some more.  This is some
                                               textual data.
                                               This is some
                                               more textual
                                               data and this
                                               is some more
                                               and some more.
                This is some
                textual data.
                This is some
                more textual
                data and this
                is some more
                and some more. This is some
                               textual data.
                               This is some
                               more textual
                               data and this
                               is some more
    COPY source over
    destination (options)  This is some textual data.  This is some more
                           textual data and this is some more and some
                           more.  This is some textual data.  This is
                           some more textual data and this is some more
                           and some more.
 
      Column 1              Column 2              Column 3
 
      This is test line 1.  This is test line 2.  This is test line 3.
 
      This is test line 4.  This is test line 5.  This is test line 6.
 
      This is test line 7.  This is test line 8.  This is test line 9.
 
     Column 1               Column 2               Column 3
 
     This is test line 1.   This is test line 2.   This is test line 3.
 
     This is test line 4.   This is test line 5.   This is test line 6.
 
     This is test line 7.   This is test line 8.   This is test line 9.
 
     Column 1               Column 2               Column 3
 
     This is test line 1.   This is test line 2.   This is test line 3.
 
     This is test line 4.   This is test line 5.   This is test line 6.
 
     This is test line 7.   This is test line 8.   This is test line 9.
00003
00004
00002
00005
00001
Syntax:
\TC
Description:
TC marks the end of the data for the current table cell and the beginning of
the data for the next column cell.
 
The contents of each cell are local to that cell; if the user changes fonts or
alignment, for example, the fonts or alignment return to what they were
previously when the cell is exited.  This also applies to formatting controls.
All applicable DSL controls function inside a table cell.  This includes line
and space formatting, fill mode, paragraph lists, etc.  If the \* (comment) or
IX (index entry) control is used, it should be placed before the TE or TX
control so that the comment or index entry is attached to the table cell
rather than between the rows.
 
Each cell is formatted in a box; thus the data cannot run over the edges, but
wrap inside the cell.
Table cells are never broken across pages.  However, the TX control allows two
table cells to appear as a single, larger cell; the two cells can then be
split between pages if necessary.
Examples:
See the TB, TH, and TX control descriptions for examples of TC.
00001
00002
Syntax:
\TE
Description:
TE marks the end of the data for the current row of table cells.  It should
not be used after the last row of cells in the table, as the closing TB
control also marks the end of the data and ends the table.
Examples:
See the TB control description for an example of TE.
00001
00002
As mentioned earlier in the Fonts subsection, DSL provides, via TeX, access to
many characters not normally included on computer terminal keyboards.  The DSL
user can enter these characters in a CAP source file by using TeX control
sequences (also called macros).  This subsection presents an overview of the
most common and useful TeX control sequences; all of the sequences and their
use are described in detail in The TeXbook.
 
TeX control sequences are introduced with the backslash (\) character.  There
are two types of TeX control sequences:  control words and control symbols.  A
control word is like a DSL control in that it consists of the \ followed by
one or more letters (although the letters are lower case); for example,
\copyright.  A control symbol consists of the \ followed by a single nonletter
character; for example, \-.
 
In a document source file, a control word should be followed by a blank space
or a nonletter (punctuation) character or should be enclosed in braces ({}) to
tell TeX where the control word ends.  The blank space, however, will not be
printed when the document is formatted.  To include the space, it should be
preceded with the backslash (\ ), as mentioned earlier in this section under
Spaces.  The backslash and following space are referred to as a "control
space" in TeX.
 
A control symbol, on the other hand, does not have to be followed by a blank
space or be otherwise delimited to tell TeX where it ends, as it always has
exactly one symbol after the introducing backslash.
 
For example:
 
                      Enter                     Prints As
 
                      \TeX book (or {\TeX}book) TeXbook
 
                      \TeX\ book                TeX book
 
                      r\'esum\'e                resume
Syntax:
\TH{heading1 \TC heading2 ...}
 
The number of heading parameters should match the number of columns specified
in the tbcols parameter on the TB control.
Parameters:
 
heading  specifies the text of a table column heading.
Description:
TH supplies the text for the column headings of a table.  TH can be specified
only immediately after the TB control and can be specified only once.
 
For small table styles (whose column width is content-dependent), the writer
can add space to stretch a column's width by inserting blank spaces around the
column heading.
Examples:
 
\TB{|*|DEFAULT|2}
\TH{Commands \TC Description}
 
The above example defines two column headings:  "Commands" in column 1 and
"Description" in column 2.
 
\TB{|*|MATRIX|3}
\TH{Administrator \TC Detailed \BRL Commands \TC Description}
This is some data. \TC This is some data. \TC This is some data. \TB
 
The above example defines three column headings, with multiple lines per
heading.  When formatted, it appears as:
 
  Administrator           Detailed
                          Commands                  Description
 
  This is some data.      This is some data.        This is some data.
 
\TB{|*|SIMPLE|3}
\TH{Administrator \TC ~~~~~Detailed Commands~~~~~ \TC Description}
This is some data. \TC This is some data. \TC This is some data. \TB
 
The above example uses the small table style SIMPLE. The second column is
widened by five spaces on each side, by inserting the tilde (~) character.
When formatted, it appears as:
 
       Administrator          Detailed Commands            Description
 
    This is some data.       This is some data.       This is some data.
00002
00003
00001
TP
Syntax:
\TJ{n}
Parameters:
 
n   specifies the number of table columns to be joined.  The braces are
    required if n is greater than 9.
Description:
TJ joins several cells into a single cell to permit spanning of columns within
a table.  TJ can be used to span any number of columns and can be entered in
any table cell.
Examples:
 
\TB{Table Cell Joining One||MATRIX|4}
\TH{Color \TC Temperature \TC Location \TC Observations}
Rodeo Red \TC Warm \TC Caribbean \TC Objective \TE
Cyan \TC \TJ2 Cool    Frozen Antarctic Wastelands \TC Subjective \TE
Riviera Blue \TC Cool \TC N.E. U.S. \TC Subjective \TE
\TJ3 Fidalgo Silver   Cold   Pacific Northwest \TC Objective \TE
Junipero Orange \TC Hot \TC S.E. U.S. \TC Subjective \TB
 
When formatted, the above appears as:
 
  Color             Temperature        Location            Observations
 
  Rodeo Red         Warm               Caribbean           Objective
 
  Cyan              Cool Frozen Antarctic Wastelands       Subjective
 
  Riviera Blue      Cool               N.E. U.S.           Subjective
 
  Fidalgo Silver Cold Pacific Northwest                    Objective
 
  Junipero Orange   Hot                S.E. U.S.           Subjective
 
In the following example, the first cell of the second row is too large for
the cell width.  TJ is used to join the cell into the adjacent cell, which
becomes a new row (via the TX) with an empty first cell.  \TB{Table Cell
Joining Two||OPT}
\TH{Command \TC Description}
COPY source over destination (options)
\TC
This is some textual data.  This is some more textual data and this is
some more and some more.  This is some textual data.  This is some more
textual data and this is some more and some more.
\TE
\TJ2 COPY source over destination (options) \TX
\TC
This is some textual data.  This is some more textual data and this is
some more and some more.  This is some textual data.  This is some more
textual data and this is some more and some more.
\TB
 
When formatted, it appears as:
 
    Command                Description
 
    COPY source over
    destination (options)  This is some textual data.  This is some more
                           textual data and this is some more and some
                           more.  This is some textual data.  This is
                           some more textual data and this is some more
                           and some more.
    COPY source over destination (options)
 
                           This is some textual data.  This is some more
                           textual data and this is some more and some
                           more.  This is some textual data.  This is
                           some more textual data and this is some more
                           and some more.
00002
00003
00001
Syntax:
\TOC
Description:
TOC includes a table of contents in a document.  Tables of content are
generated from Ln, CH, TB, FG, and GR controls.  The table of contents is
created as an auxiliary file during formatting, but does not appear in a
document unless the TOC control is encountered.  When TOC is encountered, the
document is reformatted with the table of contents included at the point
marked by the control.
 
Note that the inclusion of the TOC control can significantly increase the
amount of time that it takes to completely format a document; this is because
the formatter must make at least two passes through the document.
 
The administrator can create draft formats that print the table of contents at
the end of the document which can significantly reduce the amount of
reformatting time required to generate the printed document.
Example:
The following shows a complete document skeleton that includes a table of
contents and an index:
 
\CH{Preface|*|FRONT}
\TOC
\CH{Introduction|1|CHAPTER}
  (remainder of document)
 
\CH{|*|INDEX}
\IDX
 
Note that inserting the TOC control after the preface in the above example
causes the table of contents pages to be numbered in the same front matter
style (lowercase Roman numerals) as the preface.
00001
00002
Syntax:
\TP{tpone|tptwo|...|tpnine}
 
All parameters are optional, but the braces are mandatory.
Parameters:
 
tpone through tpnine  specify fields that are inserted onto the title page.
    The placement and meaning of these fields are defined by the
    administrator.
Description:
TP creates a title page.  Fields that are not specified are either omitted or
a default is inserted.
Administration:
The administrator is responsible for the contents and position of the tp
fields on the title page and whether or not they are used in the document
headers and footers.
 
See Section 4 for a description of how TP acts during the formatting of HELP
files.
Defaults:
The system-supplied defaults for the tp parameters are:
 
tpone  the title of the document.
tptwo  the author of the document.
tpthree  the manual number of the document.  In the default footings, tpthree
    appears on each page, opposite the page number.
tpfour  the publication date of the document.
tpfive  the holder of the copyright on the document.  This is printed with
    "Copyright (c) " on the title page.
tpsix-tpnine  not used in the default TP definition.
Example:
The following example identifies a book entitled Computer Approximations by J.
Hart, with the publication number MS3191, published in 1984, with the
copyright held by R. Krieger:
\TP{Computer Approximations|J. Hart|MS3191|1984|R. Krieger}
00003
00004
00002
00005
00001
Syntax:
\TR
Description:
TR draws a horizontal table rule between rows, in addition to those rules that
are part of an administrator-defined table style.
 
TR can be used at the beginning of a table (immediately after the TH control,
if one exists), immediately after a TE or TX control, or intermixed with TS or
other TR controls.
 
TR is useful for adding additional rules to highlight sections in, or at the
end of, a table.  Two or more consecutive TR controls can be used to produce a
thicker rule.
Example:
 
\TB{Table Rules||MATRIX|2}
\TH{First Column \TC Second Column}
First column data \TC Second column data \TE
First column data \TC Second column data \TE \TR
First column data \TC Second column data \TE
First column data \TC Second column data \TE \TR \TR
\TB
 
The above example highlights the rule below the second row and adds a thicker
rule at the end of the table.  When formatted, it appears as:
 
  First Column                         Second Column
 
  First column data                    Second column data
 
  First column data                    Second column data
------------------------------------------------------------------------------
  First column data                    Second column data
 
  First column data                    Second column data
------------------------------------------------------------------------------
------------------------------------------------------------------------------
00001
00002
Syntax:
\TS{n}
Parameters:
 
n   is a dimension that specifies the vertical distance to space.  This
    parameter must be enclosed inside the braces.  Distance is calculated in
    units of Average Character Height (ACH) if a numeric value only (without a
    unit of measurement) is specified; inches, metric units, points, and picas
    can also be specified.
Description:
TS creates space within a table while preserving the structure of vertical
rules on the page.
 
TS uses the concept of Average Character Height to calculate distances.  An
ACH is the height of the average character in the current font.
 
TS can be used at the beginning of a table (immediately after the TH control,
if one exists), immediately after a TE or TX control, or intermixed with TR or
other TS controls.
TS can also be used within a table cell (between TC and TE). In this case,
note that if TS is entered at the very beginning of the cell (immediately
after the TC), it adds the designated amount of space at the top of the row.
If TS is entered anywhere in the cell after that point, it adds the space at
the bottom of the row.  This applies to any of the cells in the row.
Example:
 
Consider the following table structure:
 
\TB{Sample Table Showing TS||MATRIX|2}
\TH{Column One \TC Column Two}
Data for column one. Data for column one. Data for column one.
\TC
Data for column two. Data for column two. Data for column two.
\TX
\TS{4}
More for column one. More for column one. More for column one.
\TC
More for column two. More for column two. More for column two.
\TB
 
When formatted, the table appears as follows:
 
  Column One                           Column Two
 
  Data for column one.  Data for column
  one.  Data for column one.           Data for column two.  Data for column
                                       two.  Data for column two.
  More for column one.  More for column
  one.  More for column one.           More for column two.  More for column
                                       two.  More for column two.
00002
00003
00001
FF
Syntax:
\TX
Description:
TX allows page breaking inside a row of table cells.  By using TX, a single
table cell can be separated into two cells, thus creating an additional row at
which the table can be split.  The two cells maintain the appearance of a
single cell when formatted.
 
Otherwise, TX is similar to TE, except that the normal rule between rows (if
defined by the administrator for the table style) is not inserted.  Any
spacing between rows (administrator-defined for the table style or specified
with TS) is still added, so two rows separated by TX may have more vertical
spacing around them than an equivalent single row of cells.
TX allows the writer to define a place where a table can logically break
inside a vertically large row of table cells.  This in turn can reduce the
overall white space in a document.
 
Table cell rows that are larger than a single page must be broken by at least
one TX control.
Examples:
 
Consider the following two table structures:
 
\TB{Sample Table Showing TE||MATRIX|2}
\TH{Column One \TC Column Two}
Data for column one. Data for column one. Data for column one.
More for column one. More for column one. More for column one.
\TC
Data for column two. Data for column two. Data for column two.
More for column two. More for column two. More for column two.
\TB
\TB{Sample Table Showing TX||MATRIX|2}
\TH{Column One \TC Column Two}
Data for column one. Data for column one. Data for column one.
\TC
Data for column two. Data for column two. Data for column two.
\TX
More for column one. More for column one. More for column one.
\TC
More for column two. More for column two. More for column two.
\TB
 
When formatted, the two tables appear as follows:
 
  Column One                           Column Two
 
  Data for column one.  Data for column
  one.  Data for column one.  More for
  column one.  More for column one.
  More for column one.                 Data for column two.  Data for column
                                       two.  Data for column two.  More for
                                       column two.  More for column two.
                                       More for column two.
 
  Column One                           Column Two
 
  Data for column one.  Data for column
  one.  Data for column one.           Data for column two.  Data for column
                                       two.  Data for column two.
  More for column one.  More for column
  one.  More for column one.           More for column two.  More for column
                                       two.  More for column two.
 
Note that both tables appear to have two table cells.  However, the second
table actually has four table cells.  The first row of cells contain the
"Data" sentences and the second row of cells contain the "More" sentences.  In
the second table, the page can be split between the two table rows.  The first
table cannot be split because there is only one table row.
00001
00002
Syntax:
\UL{area}
Parameters:
 
area  specifies the area of the text to be underlined.
Description:
UL causes areas of the text to be underlined.
 
The UL control is currently not fully implemented, in that underline text
areas that are longer than the width of the page will not wordwrap in fill
mode.  Wordwrap will occur, however, if each word of the underline area is
individually enclosed in a UL control.
 
An alternative to using underline is to use a font other than normal (such as
italics) to emphasize the text.
Example:
 
\FIF
This is a test of the \UL{underline} function.
\IT{This is a test of the \UL{underline} function.}
\FIN
 
The following is an example of how to handle an underline area longer than the
width of the page:
This is a test of the \UL{underline} function.  \UL{The} \UL{underline}
\UL{text} \UL{extends} \UL{past} \UL{the} \UL{width} \UL{of} \UL{the}
\UL{page}.
00002
00003
00001
UNL
UL
Syntax:
\UNL{distance}
 
The distance parameter is required.
Parameters:
 
distance  is a dimension that specifies the distance of the leftward
    undentation.  This parameter must be enclosed inside the braces.  Distance
    is calculated in units of Average Character Width (ACW) if a numeric value
    only (without a unit of measurement) is specified; inches, metric units,
    points, and picas can also be specified.
Description:
UNL moves the margin to the left, opposite to the INL control, but only for
the next line of printed output.
 
UNL uses the concept of Average Character Width to calculate distances.  An
ACW is the width of the average character in the current font.
Example:
 
This is some data that allows us to show the current margins for
comparison before and after the \TT{UNL} control has been issued,
thereby altering the margins in a rightward and leftward direction.
\INL{5}
\UNL{5}
This is some data that allows us to show the current margins for
comparison before and after the \TT{UNL} control has been issued,
thereby altering the margins in a rightward and leftward direction.
 
When formatted, the above appears as follows:
 
This is some data that allows us to show the current margins for comparison
before and after the UNL control has been issued, thereby altering the margins
in a rightward and leftward direction.
 
This is some data that allows us to show the current margins for comparison
     before and after the UNL control has been issued, thereby altering the
     margins in a rightward and leftward direction.
00002
00003
00001
The user interacts with CAP via a set of consistently structured
menus, submenus, and prompts for menu selections.  The default is
automatically displayed with each prompt. A HELP facility is
available to provide additional information at the menu prompt level.
 
All the DSL formatting controls have a consistent, similar syntax
structure, for ease of use. The controls can be placed anywhere on a
line in the document source file; there can be multiple controls per
line as well as multiple lines per control.
 
The CAP menus are described in the CP-6 CAP User Guide
(HA29); the DSL controls are described in Section 3 of this manual.
Syntax:
 
\VB{format|first line\BRL second line\BRL ...  last line}
Parameters:
 
format  specifies default formatting controls to be used for all entries in
    the next parameter.  The contents of format should be restricted to font
    or alignment controls.  If none is specified, the current font and size
    are maintained, and the contents are left-aligned.
first line...  specifies lines separated by BRL controls, which can contain
    text or other DSL controls, including VB or VT. Each line is formatted as
    a single line, and is not wrapped.  DSL paragraph format controls like IN
    are ignored, while explicit paragraph breaks are not permitted and are
    considered errors.  Alignment or font controls within each line can be
    used to override those specified in the format parameter.
Description:
VB creates a vertical list or stack of lines that is exactly as wide as the
widest line in the first line ...  last line parameter.  The resulting stack
can then be used like a single character in the text, and aligns along its
bottom entry in relation to adjacent text.  Several stacks can appear on the
same line and can be together or separated by other text.
 
The VB control can go anywhere in the source file, even in structures such as
tables and headings.  VB permits multiple line entries in places (such as
table styles whose width adjusts to the table column contents) where normally
only single line entries would be allowed.  VB also permits precise alignment
of stacked lines that would otherwise be impossible with certain fonts, such
as Roman.
 
The VB control is closely related to the VT control, and also to the HB
control, which provides a more restricted horizontal analog.
Examples:
 
The following could be the text of a heading to appear at the beginning of a
document:
 
Software Design Document \SPH{2.5in} \VB{|File Number: 1234\BRL Topic:
Publishing Systems\BRL Author: J. Jones\BRL Date: January 1989}
 
When formatted, the above appears as:
 
                                                  File Number:  1234
                                                  Topic:  Publishing Systems
                                                  Author:  J. Jones
Software Design Document                          Date:  January 1989
 
Note that the list stacks above the line, with the bottom entry, Date:, on the
same line as the adjacent text.
 
In the example below, the format parameter is used to right-align the list
items and print them in italics:
 
Software Design Document \SPH{2.5in} \VB{\ALR\IT|File Number: 1234\BRL
Topic: Publishing Systems\BRL Author: J. Jones\BRL Date: January 1989}
 
When formatted, the above appears as:
 
                                                          File Number:  1234
                                                  Topic:  Publishing Systems
                                                            Author:  J.Jones
Software Design Document                                 Date:  January 1989
 
The VB and VT controls can be used together to create a list that stacks both
above and below a line.  See the VT control description for an example.
00002
00003
00001
VB
VT
Syntax:
 
\VT{format|first line\BRL second line\BRL ...  last line}
Parameters:
 
format  specifies default formatting controls to be used for all entries in
    the next parameter.  The contents of format should be restricted to font
    or alignment controls.  If none is specified, the current font and size
    are maintained, and the contents are left-aligned.
first line...  specifies lines separated by BRL controls, which can contain
    text or other DSL controls, including VT or VB. Each line is formatted as
    a single line, and is not wrapped.  DSL paragraph format controls like IN
    are ignored, while explicit paragraph breaks are not permitted and are
    considered errors.  Alignment or font controls within each line can be
    used to override those specified in the format parameter.
Description:
VT creates a vertical list or stack of lines that is exactly as wide as the
widest line in the first line ...  last line parameter.  The resulting stack
can then be used like a single character in the text, and aligns along its top
entry in relation to adjacent text.  Several stacks can appear on the same
line and can be together or separated by other text.
 
The VT control can go anywhere in the source file, even in structures such as
tables and headings.  VT permits multiple line entries in places (such as
table styles whose width adjusts to the table column contents) where normally
only single line entries would be allowed.  VT also permits precise alignment
of stacked lines that would otherwise be impossible with certain fonts, such
as Roman.
 
The VT control is closely related to the VB control, and also to the HB
control, which provides a more restricted horizontal analog.
Examples:
 
The following could be the text of a heading to appear at the beginning of a
document:
 
Software Design Document \SPH{2.5in} \VT{|File Number: 1234\BRL Topic:
Publishing Systems\BRL Author: J. Jones\BRL Date: January 1989}
 
When formatted, the above appears as:
 
Software Design Document                          File Number:  1234
                                                  Topic:  Publishing Systems
                                                  Author:  J. Jones
                                                  Date:  January 1989
 
Note that the list stacks below the line, with the top entry, File Number:, on
the same line as the adjacent text.
 
In the example below, the format parameter is used to right-align the list
items and print them in italics:
 
Software Design Document \SPH{2.5in} \VT{\ALR\IT|File Number: 1234\BRL
Topic: Publishing Systems\BRL Author: J. Jones\BRL Date: January 1989}
 
When formatted, the above appears as:
 
Software Design Document                                  File Number:  1234
                                                  Topic:  Publishing Systems
                                                           Author:  J. Jones
                                                         Date:  January 1989
 
The VT and VB controls can be used together to create a list that stacks both
above and below a line, as the following shows:
 
The Documentation Group is responsible for: \SPH{3}
\VT{|\VB{|Release Bulletins\BRL Introductions\BRL User Guides}\BRL
     \VT{|References\BRL Summaries}}
 
When formatted, the above appears as:
 
                                                Release Bulletins
                                                Introductions
The Documentation Group is responsible for:     User Guides
                                                References
                                                Summaries
00002
00003
00001
TeX prints warning messages when it determines that some detail of formatting
has resulted in a formatted document that is less than perfect.  The two most
common warning messages are the following:
Overfull hbox      This means that TeX could not fit a word on the current
output page line.  In the printed document, a black box is printed in the
right margin to indicate the line that failed.
 
If the word is part of a formatted passage, it means that TeX could not find
an appropriate hyphenation point.  To fix this, use the \- macro
(discretionary hyphen) to indicate all possible hyphenation points for the
word in question, or use the \HY control to define hyphenation points for all
occurrences of the word.
 
If the error occurs in a table or figure, it means that there is not enough
room inside the box for whatever the user is trying to put into it.  Shorten
the input or provide break points (using \BRL, for example) so that TeX can
correctly lay the input into the box.
Underfull vbox      This generally means that TeX was forced to generate a
page with a large amount of white space inside it.  This message can usually
be ignored.
00001
00002
