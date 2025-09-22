This section is about ducks that never cluck but quack instead.
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
 
This section tells you how to build a CAP file in such a way that
on-line HELP can be extracted from the same source file
that generates a printable manual.
All cold ducks eat snow-flakes every day.  For more information about
duck food, see  HELP topics:
DUCK_FOOD DIET_DUCK_FOOD WEIGHTGAIN_DUCK_FOOD
 
The HELP source file may be helpful if you need to analyze or debug your
on-line HELP
file.  If you are satisfied with your HELP messages, this file may
be deleted with no effect on your on-line HELP file.
Once your file is HELP-coded, display the Master Menu and
format your file.  Formatting a file for HELP is very similar
to formatting a document, except for the format name and the device
name, both of which are "HELP".
Your screen should look like:
 
CAP Function: 2
  Files to format: DUCK_E00
Key SE     1     0      29 09:43 FEB 06 '89  DUCK_E00
*
  Format name (DEFAULT): HELP
  Device name (LP@UPSTAIRS): HELP
  Help SI file to create (*:CAP:HSI): :DUCK:HSI
  Help subject to create: DUCK
 
At the Help SI file to create (*:CAP:HSI): prompt you must
provide a filename for storing the HELP source information.  Type
:DUCK:HSI.
Help subject to create: prompts for a simple
help subject, which is used to create a file that fits CAP's naming
convention.
This is the file you access for HELP topics and subtopics.
If you provided the subject DUCK, CAP names
your HELP file HELP:DUCK: and stores this file in
your account.
Your screen should look like the following:
 
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
 
Notice item 10. SUBSET has been given the value of HELP
by CAP.
 
At the Batch, Online, Save, Cancel, or menu option: prompt
type B or BATCH.  Your screen then looks like the following:
 
Batch, Online, Save, Cancel, or menu option: B
69157 .LHTEST running 0:00/29:59
---- Batch job for Formatting of DUCK_E00 to HELP:DUCK:. submitted.
 
Check your job report to make sure that your job ran successfully and
if you have any warnings or errors messages to be concerned about.
Dizzy ducks bump in to trees and other ducks.
Lone ducks doesn't like ducks.
LONE DUCK FOOD      is available at my local pet store.
LONE DUCK SHOES      are tailor-made for each duck.
LAME      This lame duck lost his leg in the Battle of the Lagoon.
 
Dirty Duck doesn't like water.
 1. One-legged ducks walk funny.
 2. My duck has a wooden leg.
00003
00001
00002
00003
ONLINE_HELP_FACILITY
This file (:DUCK:HSI) is one of the two HELP-related files that you have now
created
This file contains only the HELP source information
for DUCK HELP file.  The abstract message is coded as *A*,
the topics are coded as *K*, and the subtopics are coded as *B*.
The following is a copy of the HELP source file:
CAP has an on-line HELP facility.  CAP users can display syntax formats,
parameters, and descriptions of controls as well as descriptions of menu items
and related information.  For a list of HELP topics for CAP from the system
command level (!), enter the following at the terminal:
 
HELP (CAP) TOPICS
Additional CAP information is presented in the following manuals:
 
CAP DSL Reference, Order No. HA27
CAP ADSL Reference, Order No. HA28
CP-6 CAP Administrator Guide, Order No. HA30
