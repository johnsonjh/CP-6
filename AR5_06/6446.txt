TOLTS  (Total On-Line Test  System) is an  online test system which runs
concurrently with the operating system,  and makes available to CP-6 the
standard  set  of  Test  and  Diagnostic  programs which are used on all
Honeywell mainframes.  Properly used, TOLTS keeps it up longer.
 
For additional information on the HELP facility type
    ???HELP HELP
For additional information on TOLTS type
    ???HELP TOPICS
For a list of subtopics for one of the TOLTS subexecutives:
    ???HELP <subexecutive name> SUBTOPICS
          where <subexecutive name> ::= COLTS |
                                        MOLTS |
                                        POLTS 
 
TOLTS
TOLTS is the Total On-Line Test System
 ****************************************************************
 *                                                              *
 *   COPYRIGHT, (C) 1987, Honeywell Bull, Inc.                  *
 *                                                              *
 ****************************************************************
Syntax:
   [TEST] Cfffmmmm[ooo] |         MLCP/MLC-16, HDLC, or MDC adapter test
   [TEST] CfffmmmmM[oo] |         MLCP/MLC-16 Central test
   [TEST] CfffmmmmV[oo] |         Multiple Device Controller device test
   [TEST] Cfff0000      |         FEP Coupler test
   [TEST] Cxfffmmmm[oo] |         communicate with running test
   [TEST] CLSTAL        |         COLTS List All request
   [TEST] CW                      Wrap-up COLTS
 
Parameters:
   fff - one, two, or three digit FEP number
   mmmm - megabus address is the Level 6 megabus address of the
          line or MLCP/MLC-16 to be tested and must always
          be four digits long
   o - option character
       Note that options are not required, but if entered, the
       length of the COLTS command may not exceed 11 characters.
       type HELP (TOLTS) COLTS OPTIONS for a list of options
   x - communication character
       E = end running test
       O = modify options for a running test
 
Description:
COLTS  (Communications  On  Line  Test  System) provides testing for the
various hardware components of the CP-6 L6 Front End Processors (FEP's).
Testing  is accomplished by  transfer of test  data from the  host to L6
COLTS, a T&D  module in the FEP.  L6 COLTS  performs the particular test
function requested  and sends the results back  to the host, where error
checking and reporting is done.  The method of communicating between the
host and L6 is via CP-6 DCB's (Data Control Blocks).
 
COLTS Test Procedure:
The  user  is  required  to  utilize  CP-6  NETCON  to partition out any
MLCP/MLC-16 lines to be tested, prior to the start of testing.  The user
should also  assume that the FEP  to be tested has  been booted with the
appropriate run unit and configuration file.
 
The procedure for conducting COLTS testing is:
    - the user logs on to  a properly authorized account, i.e., one with
      TND and MFEP host privileges,  TND and MSYS FEP privileges, access
      to TANDD_DECK_FILE_ID.:FED, and authorized to run FPRGs.
    - NETCON  must  then  be  used  to deconfigure any MLCP/MLC-16 lines
      which are to be tested.
    - T&D is invoked by entering "TOLTS" (IBEX level).
    - When TOLTS responds with a ??? prompt, the user enters the desired
      COLTS command.
    - COLTS  will  then  proceed  to  execute  according  to the command
      entered. The  user may interrupt execution at  any time by hitting
      the  terminal <BREAK>  key which  will cause  the ??? prompt to be
      output, giving  the user control and allowing  more commands to be
      entered.
    - When testing is concluded, usable  lines should be returned to the
      system via NETCON.
 
A test request causes testing to be initiated on the requested hardware,
provided that it is  available for testing, i.e., previously partitioned
via  NETCON. If a  test request cannot  be honored, the  user will be so
informed.
 
COLTS Restrictions:
COLTS testing can occur concurrently  with user activity in both the FEP
and the host.  A COLTS user has the ability to  run up to eight tests at
once, either on the same FEP or on several different FEP's. However, two
COLTS users may not simultaneously test components on the same FEP - the
first user  to initiate testing of  a given FEP is  the exclusive tester
for that FEP until he finishes with it.
 
MLCP and MLC-16 Line Tests:
An  MLCP  or  MLC-16  line  test  can  be  invoked on any line which has
previously been partitioned via NETCON. The test checks the send/receive
channel pair for the line  indicated by the megabus address specified in
the test request. One MLCP/MLC-16  daughter board contains two lines (an
even-odd  pair), and  each line  in turn  consists of a receive/transmit
channel pair, as summarized in the sample MLCP configuration shown below
(assume the MLCP is based at megabus address 2C00)
 
Address 2C00 = line 0 (channels 0+1)   **first daughter board**
        2C80 = line 1 (channels 2+3)   **first daughter board**
        2D00 = line 2 (channels 4+5)   **second daughter board**
        2D80 = line 3 (channels 6+7)   **second daughter board**
        2E00 = line 4 (channels 8+9)   **third daughter board**
        2E80 = line 5 (channels 10+11) **third daughter board**
        2F00 = line 6 (channels 12+13) **fourth daughter board**
        2F80 = line 7 (channels 14+15) **fourth daughter board**
 
For  async  and  sync  lines,  if  the  line  selected for testing is an
odd-numbered  line,  then  the  next-lowest  numbered  line must also be
partitioned out via NETCON, i.e.,  to test line 0(2,4,6), partition only
line  0(2,4,6);  to  test   line  1(3,5,7),  deallocate  the  line  pair
0&1(2&3,4&5,6&7). a sample test request would be:
   [TEST] C22480       (fep #2, line 1 of MLCP at 2400)
 
Examples:
Examples- Assume that an FEP is configured  as FEP 2 and that an MLCP is
configured on the FEP at the megabus address (hex) of 2C00.
 
Any of  the following test requests  would start a test  on line zero of
that MLCP:
   [TEST] C22C00
   [TEST] C022C00
   [TEST] C0022C00
 
Note that the  megabus address is the required 4 digits,  but 1, 2, or 3
digits  is legal for  FEP number.  For  broadband synchronous, HDLC, and
broadband  HDLC there is  only one line  per daughter board.  This means
that there is no even-odd pair to worry about partitioning.
 
MLCP/MLC-16 Central Tests:
The MLCP and MLC-16 central logic  tests check all of the RAM and mother
board logic of  the selected MLCP/MLC-16. In order to  use the test, all
lines  on the  desired MLCP/MLC-16  must be  partitioned out via NETCON.
For an MLCP,  the megabus address specified in the  test request must be
an async line  address of that MLCP on the  L6 megabus. The test request
for  the central  logic test  must contain  an "M" following the megabus
address  in  order  to  distinguish  the  test  request from a line test
request:
   [TEST] C22400M
 
FEP Coupler Tests:
The  coupler exerciser  is not  a diagnostic;  it merely sends blocks of
test  data to the  L6 which are  then sent back  to the test program and
checked  for errors. Each  pass of the  coupler exerciser sends 100 test
messages  (10  tests  of  10  messages  each).  The coupler exerciser is
invoked  by a  standard COLTS  test request  using a  megabus address of
zero:
   [TEST] C30000       (tests coupler to fep #3)
 
Note: No NETCON action is required to run this test.
COLTS Option Requests:
A COLTS option  input is used to direct COLTS  options to a test program
which has previously been started  by a test request command. The option
input format is
   [TEST] COfffmmmmoo
 
The FEP and  megabus address fields used should match  those used in the
original  test  request.  The  string  "COf.....o" may not exceed eleven
characters.
 
COLTS user options allow the  user to exercise various levels of control
over the execution  of his test programs. Options are  invoked on a test
program basis, that is, a particular  option may be either on or off for
each program under  the user's control. Options are turned  on or off in
one of three ways:
   1. by appending option characters to the initial test request;
   2. by using the option input command for a test program; or
   3. by  inputting option  data in  response to  a test  program "ENTER
      OPTIONS" request.
 
Methods  (1) and  (2) are  easiest for  short option strings; for longer
strings, use  the "O" option to  get to the "ENTER  OPTIONS" level, then
input the option string.
Option Characters:
B - Bypass  error  message  output.  Bypass  overrides  a  Pass or Cycle
    message  unless Halt  is set;  Halt forces  these messages  out over
    Bypass.
H - Halt  for  input  of  options  following  error  messages,  Test End
    messages, Pass End messages, and Cycle End messages.
I - Inform user of each normal test end. If H is also set, then an Enter
    Options: is appended to the End Test Message. If the next segment is
    being called, if an End Pass  message is being output, or if a cycle
    ends; the End Test message is overridden.
L - Loop on current test (cannot loop on test 0)
M - Specifies central test instead of  subchannel test. Can be used only
    on initial  TEST call and must be  the first character following the
    megabus address. Not used for page communications requests.
N - negate the  following option character (valid preceding  B, H, I, L,
    P, R, or T only)
O - go to Enter Options: following complete processing of the options on
    the test request string.
P - Issue an  End Pass message any  time a back jump  is detected by the
    next test  sequencing. If H is  also set, then an  Enter Options: is
    appended to the End Pass  message. The error tallies for the current
    pass are reset  when End Pass is reported or  when P is being turned
    ON.
R - Issue and End Cycle message  any time a normal test page termination
    would occur and cycle back to the first test in the current sequence
    again. If H is also set,  then an Enter Options:  is appended to the
    End Cycle  message. The error tallies for  both the current pass and
    current  cycle  are  reset  when  End  Cycle  is reported. The error
    tallies for the cycle are reset whenever R is being turned ON.
S - unconditionally Skip to the next test
T - If turn ON (no preceding  N), then unconditionally jump to the first
    occurrence of the test in the current sequence; the test number must
    follow and must  be non-zero, and can consist of  one, two, or three
    digits.  For segmented  test pages,  a value  outside of the current
    segment causes  a jump to the  corresponding segment without further
    processing of  the current option string. If  turn OFF (NTxxx), then
    then test number must be in  the current sequence and not the forced
    termination test number.
V - Specifies device  test instead of subchannel test.  Can be used only
    on initial  TEST call and must be  the first character following the
    megabus address. Not used for page communications requests.
 
Control Mnemonics:
The  following control mnemonics  (.OPTIONS) will be  processed if input
for the Enter Options: request.
 .GO - return to the test page where interrupted
       if S or Txxx, or .RSEQ or .SEQT, has been specified,
       the next sequencing is done.
 .OPT - an Enter Options: message is output
 .RSEQ - resequence tests to their initial (at page call) order
 .SEQT - sequence tests in a special order
 .TAL - A message with a tally of errors is output. P or R must
        be set and the message will include information for
        the current pass or cycle or both depending on the state
        of P or R or both. The error tallies are reset for the
        pass or cycle or both when reported.
 .TEST E - the test page is force terminated
 .TEST W - the test page is wrapped up
 .TYP - subsequent error messages will be printed
 .WAIT - the test page is put in a wait condition
 
COLTS LSTAL Command:
The  COLTS  LSTAL  command  will  cause  COLTS  to  issue a user message
displaying  the current status  of all of  the user's test programs that
have  not terminated,  i.e., test  in execution,  test waiting  for idle
line, test in abeyance, test in WAIT mode, etc. The LSTAL command is
   [TEST] CLSTAL
COLTS Test Termination:
COLTS  termination commands are  available either to  end one particular
test program  or to terminate all COLTS  testing. The command format for
ending all testing is
   [TEST] CW
 
This form  causes all active test programs  to abort and should normally
only be utilized in emergencies or under software error conditions.  The
normal method of terminating testing is to issue a terminate command for
each active test program, in the form
   [TEST] CEfffmmmm
 
where FEP number and megabus address are the values used in the original
test request. As the test program ends, a termination message is sent to
the user.
 
Help is provided for the following COLTS subtopics:
   SYNTAX
   PARAMETERS
   DESCRIPTION
   TESTING
   RESTRICTIONS
   MLCP
   CENTRAL
   COUPLER
   OPTION_REQUESTS
   CLSTAL
   TERMINATION
 
00007
00011
00008
00002
00008
00011
00005
00007
00005
00007
00005
00010
00009
00001
00004
00013
00012
00003
TOLTS Commands:
 
Tolts commands are of 3 types:
 
   1. Test Requests
 
      [TEST] { <COLTS request> |
               <MOLTS request> |
               <POLTS request> 
 
   2. Help Requests
 
      HE/LP [(processor)] [TOPICS] [keyword1] [- keyword2]
      ?     more help please
      ??    all available help please
 
   3. Termination Requests
 
      E/ND
      X/IT
      Q/UIT
 
   4. Message Requests (communication with the Operator)
 
      MSG <message text[?]>
 
   5. Debug Test Requests (used by developers only)
 
      DEBUG [TEST] { <COLTS request> |
                     <MOLTS request> |
                     <POLTS request> 
Syntax:
D/EBUG [TEST] <test request> [<debug options>]
 
Parameters:
   TEST - optional
   <test request> - { <COLTS request> |
                      <MOLTS request> |
                      <POLTS request> 
   <debug options> = <set of options separated by commas>
                     AT, SOG, SOI, SAS, SM
 
Options:
   A/ND T/OLTS - used only if  the user wishes to set breakpoints in the
      TOLTS  Executive (CP-6  code) as  well as  the test  page.  Due to
      SCHEMA  requirement, may only  be used for  TOLTS run units on the
      LADC B machine.
        shortest abbreviation: AT
   S/TOPPING  O/N  G/ELBARS  -  used  only  when the user wishes to halt
      execution  of the test  page each time  GELBAR mode is re-invoked.
      May be used for any TOLTS run unit.
        shortest abbreviation: SOG
   S/TOPPING O/N I/O - used when the user wishes to stop before any test
      i/o's  are issued;  the 11  word entry  for the  i/o is  dumped in
      octal.  Due to SCHEMA requirement,  may only be used for TOLTS run
      units on the LADC B machine.
        shortest abbreviation: SOI
   S/TOPPING  A/T S/UBEXEC -  used when the  user wishes to  stop at the
      beginning of the TOLTS Subexecutive (CCLT CMLT CPLT CSLT).  May be
      used for any TOLTS run unit.
        shortest abbreviation: SAS
   S/CREAMING M/MES  - used to obtain  a list of MME's  performed by the
      TOLTS Subexecutive.   Due to SCHEMA requirement,  may only be used
      for TOLTS run units on the LADC B machine.
        shortest abbreviation: SM
 
Description:
Under normal circumstances, the DEBUG  test request is only to be issued
by developers at LADC since  DEBUG test requests are used in conjunction
with the  CP-6 Universal debugger, DELTA.  When  a DEBUG test request is
entered, TOLTS programmatically  adds symbolic definitions and execution
control breakpoints to DELTA. These symbols and breakpoints make it easy
for a  test page developer to  step through and debug  a test page as it
executes.  The various debug  options provide for even more capabilities
in this area. The options may be spelled out fully so new users of TOLTS
debug  can  be  confident  of  what  they  are  doing;  however,  once a
familiarity  with  the  system  is  established,  the  abbreviations are
suggested since they are more convenient.
 
Note: The POLTS Subexecutive may  only be debugged using the TOLTS DEBUG
request  since  POLTS  test  pages  are  executed  by  interpreting  TDL
instructions.
 
Examples:
 
   A Few Valid Command Forms:
 
      ???DEBUG TEST P01219 AND TOLTS, STOPPING ON GELBARS
      ???DEBUG TEST P01219 AT, SOG
      ???DEBUG P01219 AT, SOG, SOI, SAS, SM
      ???DEBUG P01219 AT, SOI
      ???DEBUG P01219 STOPPING ON IO, SCREAMING MMES
 
   Any combination of options may be entered as long as they are
   separated by commas.
   Also note that the word 'TEST' is optional.
 
Sample Session:
*----------------------------------------------------------------------*
|  !TOLTS                         "invoke TOLTS                        |
|  TOLTS Executive Version E02 900327 on 04/06/90                      |
|  ***Deckfile: TANDD_DECK_FILE_ID.:FED (IFAD Release: IFADD6)         |
|  ???DEBUG MMT012001t1 SAS,AT    "enter DEBUG request                 |
|  MOLTS Subexecutive CMLT (MOLTCM) loaded at .130000                  |
|  99 A_BRK@ B_PATCHI+.1634       "stopped at Subexecutive             |
|  >TRAP MME,EVENT                                                     |
|  >AT TOP$POLTS+.1657            "any DELTA command may be entered    |
|  >G                                                                  |
|  ***MOLTS EXEXUTIVE Version 900327 890724 on 900406 AT 07.9          |
|  01 A_BRK@ TOP$POLTS:5337 [IF]                                       |
|  >DI TOP$TCP.TEST_TYPE(TCX)     " Display this variable              |
|  TOP$TCP.TEST_TYPE(TCX) = 'MTR'                                      |
|  >]                             " STEP IN DELTA                      |
|  TOP$POLTS:5339 [ASSIGNMENT]>DI MTARF$->MTAR_DATA.WR_FLAG#           |
|  MTARF$->MTAR_DATA.WR_FLAG# = '000'B                                 |
|     .                           " more  debug options                |
|     .                           "e.g., DUA, M, LET, etc.             |
|  >G                                                                  |
|  MOLTS test page FTR1 (FMTXXA) loaded at .164000                     |
|  **0 (MMT01201  ) START FMTXXA-FTR1 , TTLDAT 890425                  |
|  FTR1 entering GELBAR mode at GELBAR address .001141                 |
|  99 A_BRK@ FTR1+.1141                                                |
|  >                                                                   |
|   <CTRL>BREAK                                                        |
|   ???TEST MEMT0012001    "Terminate MOLTS test early                 |
|  **0(MMT012001  ) FORCED TERM 1   "MOLTS message                     |
|  TEST E REQUEST RECEIVED                                             |
|  ***MOLTS EXECUTIVE VERSION 900327 OFF 900406 AT  8.3                |
|  ???Q      "or END                                                   |
|  TOLTS Version E02 off 04/06/90 at  8.32                             |
*----------------------------------------------------------------------*
 
 
00003
00004
00002
00001
00005
00005
DEER:
DEER  is the CP-6  DEckfile Editor Routine.  A deckfile is  a CP-6 keyed
file  that is  the basis  for running  the Total On-Line Testing System.
When TOLTS is in execution, test  modules are read from the deckfile and
placed into core for execution.  DEER facilitates the management of CP-6
deckfiles and the modules contained therein.
 
Type HELP (DEER) TOPICS for a list of DEER topics.
 
DPS8000:
The DPS8000 computer supports the same MOLTS and POLTS tests as did  the 
DPS/8 series. However, an additional set of commands have been developed 
to  perform  MOLTS testing in behalf of the SP/MCA  (Service  Processor/ 
Maintenance  Channel Adaptor). These commands allow the user to  test  a 
specified IPC, CPU, or SCU in an online environment.  Further detail  on 
this is provided in the MOLTS/RPMS portion of this help file.
 
DPS90:
On a DPS90 machine the following  types of diagnostics will be run under
MSOS (Maintenance System Operating Supervisor) instead of TOLTS:
 
   Functional Tests (POLTS type tests)
      Disk
      Tape
      Unit Record Devices
   ITRs (MOLTS MPC tests)
   MDRs (MOLTS MDR tests)
 
Check  your   MSOS  documentation  for  further   information  on  these
diagnostics.
 
 
Syntax:
E/ND | Q/UIT | X
 
Parameters:
   None.
 
Description:
The END command terminates TOLTS in a normal fashion.
 
Examples:
   ???E
   ???QUIT
   ???X
 
All of the above terminate TOLTS.
 
00002
00003
00001
FEPCON has been replaced by NETCON.
 
Hardware:
TOLTS and its subexecutives support the full spectrum of CP-6  hardware. 
Please  refer  to  the  System  Support  Reference  Manual  (under  TIGR 
commands) for a complete list of supported hardware.
 
 
  COLTS: MLCP (communications processor, mother board)
         MLC-16 (communications processor, mother board)
         Daughter boards
  MOLTS: MSP0600-0603 disk MPC ITR's
         MSP0800 disk PPU (DAU) ITR's
         MTP0601 tape MPC ITR's
         MTP0610 GCR tape MPC ITR's
         URP0600-0602 unit record MPC ITR's
         MTU0600 tape drive MDR's
         MTU0610 GCR tape drive MDR's
         MSU0451 disk drive MDR's
         MSU0509 disk drive MDR's
         MSU0509 disk drive MTAR/FTAR's
         MSU3380/3382 disk MTAR/FTAR's 
         MSU3381/3383 disk MTAR/FTAR's 
         MSU3380/3382 disk MFC's 
         MSU3380/3382 disk MDC's 
         MSU8082/8092 disk MDS's 
         MSU8082/8092 disk MTAR/FTAR's 
         MSU8082/8092 disk TMD's 
  POLTS: CRU0501 card reader
         CRU1050 card reader
         MSU0402 disk drives
         MSU0451 disk drives
         MSU0501 disk drives
         MTU0400 tape drives
         MTU0500 tape drives
         MTU0600 tape drives
         MTU0610 tape drives
         MTU0630 tape drives
         PCU0120 card punch
         PCU0121 card punch
         PRU0901 line printer
         PRU0903/1203 line printers
         PRU1200/1600 line printer, 132 columns
  TURTLE: Terminal test of all CP-6 supported terminals
 
Syntax:
H/ELP [(processor)] [TOPICS] [keyword1] [- keyword2]
 
Parameters:
processor  - specifies  a program  or processor  that has  an associated
     helpfile  in  the  form HELP:processor:[.[account][.password].  The
     default  is  the  processor  currently  under control, in this case
     TOLTS.
TOPICS - specifies that only  a list of available topics (message names)
     is  required.  The  range of  topics is  determined by  keyword1 or
     keyword2.
keyword1 - specifies the name of the message to be printed.
keyword2 - if  a range is specified (by including  a dash "-"), keyword2
     is  the upper  limit of  the range.   If a  range is not specified,
     keyword2 is a submessage, or category within a message.
 
Description:
HELP prints information.
 
HELP  messages have  levels.  Once  the initial  level has been printed,
typing a question mark prints the next level, usually containing greater
detail.  Typing two question marks prints the entire message.
 
Examples:
???HELP COLTS
means print the a short description of the COLTS subsystem.
 
???HELP TOPIC
means print the names of all available TOLTS HELP messages.
 
???HELP MLCP_LINE_TESTS EXAMPLES
means print a list of the print some examples of the MLCP line test
requests.
 
00002
00003
00001
Integrated Firmware And Diagnostics:
In order  to run T&D, a  customer must have a  Deckfile installed on his
system  by a  Customer Service  Representative (CSR).   This Deckfile is
distributed  to   the  field  via  an   IFAD  (Integrated  Firmware  and
Diagnostics)  tape via the  normal CSD FCO  channels from Phoenix.  (The
IFAD  tape is the  successor to the  old firmware tape  which used to be
distributed  to  the   field.)   Honeywell  customers  with  maintenance
contracts  will receive  an IFAD  tape which  will contain  MPC firmware
along with  Test and Diagnostic programs.   Other customers will receive
only a firmware tape.
 
The CSR  will build a Deckfile, called  TANDD_DECK_FILE_ID from the IFAD
tape using  a utility program called DEER.   The default account for the
Deckfile is :FED.
 
See  HELP  for  the  DEER  build  function for information regarding the
installation of a deckfile.
   !HELP (DEER) BUILD DESCRIPTION
 
MSG
Syntax:
   [TEST] MDCicccdd[oo] |         Removable Disk Confidence Test
   [TEST] MDRicccdd[oo] |         Microcoded Device Routine
   [TEST] MFCicccdd[oo] |         MOLTS FIPS Comprehensive
   [TEST] MLSTAL        |         MOLTS List All request
   [TEST] MMTicccdd[oo] |         Media Test And Recertification
   [TEST] MPCiccc[oooo] |         Isolation Test Routine
   [TEST] MTCicccdd[oo] |         Tape Compatibility Test
   [TEST] MTGicccdd[oo] |         Tape Shotgun Test
   [TEST] MW            |         Wrap-up MOLTS
   [TEST] RPMi          |         Initiate SP/MCA maintenance session
   [TEST] MDS           |         Modular Disk Subsystem test
   [TEST] TMD                     Self-test part of MDS disks
 
 
   [TEST] MxDCicccdd[o] |         communicate with Disk Confidence test
   [TEST] MxDRicccdd[o] |         communicate with MDR test
   [TEST] MxFCicccdd[o] |         communicate with MFC test
   [TEST] MxMTicccdd[o] |         communicate with MTAR/FTAR test
   [TEST] MxPCiccc[ooo] |         communicate with ITR test
   [TEST] MxTCicccdd[o] |         communicate with Tape Compatibility test
   [TEST] MxTGicccdd[o] |         communicate with Tape Shotgun test
   [TEST] MxDSicccdd[o]           communicate with MDS disk test
 
 
Parameters:
   i - single digit IOM number (single digit IMX number for RPM)
   ccc - two or three digit channel number in decimal
   dd - two digit device number in decimal
   o - option character
       type HELP (TOLTS) MOLTS OPTIONS for a list of options
   x - communication character
       Note that options are not required, but if entered, the
       length of the MOLTS command may not exceed 11 characters.
       E = end the running test normally
       O = modify options for a running test
 
Description:
MOLTS  (Mainframe On-Line  Test System)  provides diagnostic  testing of
both  MPCs  (Microprogrammed   Peripheral  Controllers)  and  peripheral
devices  themselves.   Diagnostic  testing  means  an attempt at failure
diagnosis down to  the replaceable part.  Thus MOLTS is  one of the most
sophisticated test  and diagnostic tools available  on CP-6.  It greatly
aids in failure resolution and repair.
 
MOLTS Test Procedure:
All MOLTS  tests run concurrent with the  operating system and all other
user activity.   The following is the procedure  which is generally used
for running MOLTS:
 
a.  Logon on a properly authorized account.  (Proper authorization
    means (1) TND privilege and (2) access to files in :FED and :SYS.)
b.  Have the system's operator use SYSCON to set the TDOK bit for
    the device to be tested. (Some components of the system may also
    have to be partitioned also.)
    Type HELP (TOLTS) MOLTS PARTITIONING for additional help.
c.  Invoke TOLTS by entering !TOLTS
d.  TOLTS will respond with a ??? prompt, at which point it is ready
    for the initial test request.  From this point on, the human
    interface dialog is the same as it is for all online test
    systems.
e.  TOLTS will automatically ask the operator permission to run
    MOLTS at the operator console.  The operator may respond and
    either allow testing or not.  The console dialog:
 
         sysid: REQUEST DIAG KEYIN
         !DIAG sysid  [operator giving permission]
         !NODIAG sysid  [operator denying permission]
 
f.  MOLTS begins running and continues to a termination.
    Communication can be established with MOLTS at any time by
    hitting the "break" key.
g.  On completion, the operator should reset the TDOK bit for the
    device via SYSCON.
 
MOLTS Partitioning Tips:
If the T&D user has been  granted the SYSCON privilege, he may partition
components  of   the  system.  Otherwise,  and  in   most  cases  it  is
recommended, the system operator should  be contacted to have him do any
needed partitioning.
 
For MOLTS Tests:
 
MDC tests -   partition the disk from the system
MDR tests -   for disks, no partitioning is necessary
              only the T&D cylinders of the disk are accessed
         -    for unit record and tape devices, partitioning
              is required
MFC tests -   for disks and tape devices, partitioning is
              required
MMT tests -   if only MTAR/FTAR read tests are to be performed,
              no partitioning is necessary
          -   to perform MTAR/FTAR write tests, partitioning is
              required
MPC tests -   if the devices associated with the MPC are set up
              in a crossbarred configuration, the MPC need not
              be partitioned
          -   for non-crossbarred configurations, all devices
              associated with the MPC must be partitioned with
              the MPC NOT being partitioned
MTC tests -   partition the tape handler from the system
MTG tests -   partition the tape handler from the system
MDS tests -   partition the disk from the system
TMD tests -   partition the disk/controller from the system
 
 
Isolation Test Routines (ITR's)
The MPC tests are called ITR's (Isolation Test Routines).  The ITR's are
MPC  overlays which are  downline loaded into  the MPC Control Store and
test  the  MPC  internally.   If  there  is  a failure detected, the ITR
physically HALTS the MPC with  an error signature available at the MPC's
maintenance panel.   This signature has been generated  as a result of a
simulation technique and is used  in conjunction with a fault dictionary
to come  up with a list  of the most probable  integrated circuits which
failed.  The Field Engineer then can replace the chip.
 
If  there is  no failure  detected, the  ITR results  in a reboot of MPC
firmware.
 
In  the CP-6  environment, the  MPC is  made accessible  to the T&D user
either  by setting the  TDOK bit in  SYSCON or by  the operator giving a
DIAG keyin.
 
For the case of Mass Store MPCs (disk), a dual controller is required in
most cases.
 
MOLTS FIPS Comprehensive (MFC's)
The MFC  tests are a comprehensive  set of tests for  FIPS disk and tape
devices.  A scratch tape, or disk  pack must be available on the device.
The program does not provide  fault isolation of device failures, but is
a  functional  test  providing  error  messages  on error as a result of
commands, command sequences, illegal commands, or data errors.
With the disk, no data will be destroyed; writing is done only on the
T&D cylinders.
 
 
MOLTS Disk Confidence Tests (MDC's)
MDC  is a removable  disk device and  media reverification program which  
consists of  five separately executable worst-case  pattern write tests, 
and  any  data read tests. The tests use standard T&D dialogue  to  
exercise several  removable  disk devices(451,500/501,FIPs). MDC can be  
used  to distinguish  between  device and pack failures.  No attempt is  
made  to diagnose   a problem down to an optimum  replaceable  unit  
(ORU),   but extensive  status translation is provided for error 
detection  messages. The controller -- error detection mechanism,  is 
disabled  to permit  an unbiased   view  of disk errors and gives the 
user up to  three  command retries on error detection.
 
 
Reads and Writes:
The program's read tests do  not compromise customer or system disk pack
security since a non-data transfer DCW is used (i.e., a read disk method
that  discards data  before any  point in  time where  it can  be seen).
Typically,  write tests are  on a scratch  disk pack and  result in data
destruction of the pack.
 
Execution:
Tests 1 and  2 (Sequential Read and Write) have  a finite execution time
whereas Tests 3, 4, and 5 (Random Write, Read, and Write-Read) run until
terminated by  the user. The program writes  and reads the entire usable
disk  surface,  not  just  the  T&D  cylinder.  In  addition,  status is
translated into easy-to-use language on error messages.
 
MOLTS MDS Disk Comprehensive/Confidence Tests (MDS's):
The MDS test is a comprhensive set of tests for disks which are part  of 
the  Modular Disk Subsystem design. The test performs tests  similar  to 
those performed by the MFC disk comprhensive set of tests. There is  one 
important distinction which needs to be made, however. That is, the  MDS 
test is  usually run as a comprehensive test and will not  destroy  user 
data  (T1-T26). However, there exists an optional test (T27) which  does 
run  as a confidence test and will destroy user data. This is  the  only 
T&D test of its kind, therefore great caution must be used. We therefore 
recommend that the disk be partitioned prior to running MDS tests.
 
MDS CM/Drive Self-tests:
The  purpose  of this test is to verify MDS CM-3  controller  and  drive 
diagnostics on the Modular Disk Subsystem (MDS). The test is invoked  by 
the user entering TEST TMDICCCDD and the user will be prompted to  enter 
a  'C' or 'D' to test the CM or drive. Partitioning of the CM and  drive 
is required before running the test.
 
  
Microcoded Device Routines (MDR's):
The peripheral tests are called MDR's (Microprogrammed Device Routines).
These are  a combination of a  test driver resident in  the host and MPC
overlays which are downline loaded into the MPC.  In order to run MDR's,
the  device must  be made  accessible by  setting the  TDOK bit  for the
device using  SYSCON, or receiving a DIAG  keyin from the operator.  The
test  driver then  downline loads  a long  series of  MPC overlays which
execute,  testing  a  different  part  of  the  device  each time one is
executed.   This overlay  technique allows  much better fault resolution
than is available at the system level in the host.
 
Note that system  I/O can continue to the other  devices on the MPC, and
in the case of a disk, to the disk itself.
 
MOLTS LiST ALl (MLSTAL):
The  MOLTS  LSTAL  command  will  cause  MOLTS  to  issue a user message
displaying  the current status  of all of  the user's test programs that
have  not terminated,  i.e., test  in execution,  test waiting  for idle
time, test in abeyance, test in WAIT mode, etc...
 
MTAR/FTAR - Media Test and Recertification Tests (MMT's):
MOLTS  also provides media  testing and reallocation  capability for the 
disk  devices  in  the  form  of  the MTAR/FTAR program. This   requires 
extensive   user dialogue-  the reader  is referred  to  the   MTAR/FTAR 
program documentation  for more  detailed information.   Note,  however,  
that by calling  in  MTAR/FTAR  test  4,  the  user  can  have access to 
online  usage  documentation  contained  within  the  MTAR/FTAR  program 
itself.
 
Restrictions:
MTAR/FTAR   test  5  (Emergency Permfile  Track Repair)   and  MTAR/FTAR  
test  6  (Disk Reformat) will not operate on a disk pack which  has  not 
been scratched.
 
Note,   The  Emergency  Track  Repair  facility  of  MTAR/FTAR  is   not 
implemented in CP-6.
 
 
MOLTS Tape Confidence (MTC's):
The  MOLTS Tape  Compatibility test  has been  used with good success in
testing  device quality and  can be used  on any magnetic tape subsystem
using  MPC controllers.  MTC  reads and writes  predictable random data,
random  size, records.   On the  read pass,  the program regenerates the
data so that  a data compare can take place.  All errors are reported as
they  occur.  At  the completion  of each  pass (a  pass being a read or
write), a message is output which requests the next type of pass.
 
Operation:
A work  tape must be mounted  on the handler to  be tested.  The handler
should  be placed in  READY status. The  MTC test is  then entered using
TOLTS.
 
MOLTS Tape Shotgun (MTG's):
The  MOLTS  Tape  Shotgun  test  may  be  operated  on any magnetic tape
subsystem  using MPC  controllers. The  test is  designed to  stress the
device to its extremes. It is  a good test of the tape handler's ability
to  read, write,  start-stop, and  position tape.  MTG will perform most
commands in a random pattern and length.
 
Operation:
A work  tape must be mounted  on the handler to  be tested.  The handler
should  be placed in  READY status. The  MTG test is  then entered using
TOLTS. After the program loads, it  will output a warning message and go
into  wait mode to  allow options to  be entered. To  exit wait mode and
enter options, the [TEST] MOTGiccdd request should be used.
 
Service Processor (RPM's)
[TEST]  RPMi,  where  i  is  the  IMX  number, is used to initiate MOLTS
testing in the form of an SP/MCA (Service Processor/ Maintenance Channel
Adaptor) Maintenance session.                                           
This  procedure  allows  the user to issue  MCA  and  Service  Processor 
commands  to a specified IPC, SCU, or CPU in an online environment.  The 
commands  are  separated into two categories (those to IMX  targets  and 
those to the CPU/SCU) as outlined below.
 
COMMANDS TO IMX TARGETS:
TEST IPC x DIAG - Run NFT's and Self Tests if available on IPC x
TEST IPC x NFT  - Run NFT's only on IPC x
TEST IPC x DPM  - Run Diagnostic Procedure Modules
TEST IPC x SELF - Runs extended Self Tests
TEST IPC x QRY  - Microprocessor Maintenance Panel functions
RESET IPC x     - Reset selected IPC
LOAD IPC x      - Load firmware in IPC
RMCA            - Restart test page, initialize and reset MCA channel
STOP            - Terminate the test page
QUIT            - Terminate the session
 
COMMANDS TO THE CPU/SCU:
The  user  also  has  online access to the  Service  Processor  (SP)  to 
exercise the CPU and SCU via the term "SP". You cannot test SCU 0 if  it 
is "low order". 
 
SP RESET CPU (0-3)          CPU is reset and self tested
SP RESET SCU (1-3)          SCU is reset and self tested
SP LOAD CPU (0-3)           Firmware loaded in CPU
SP LOAD SCU (1-3)           Firmware loaded in SCU
SP RLOAD CPU (0-3)          Reset & Load CPU
SP RLOAD SCU (1-3)          Reset & Load SCU
SP TEST CSP (0-3) SCL       SP Shift Control Logic tests
SP TEST CPU (0-3) SPT       CPU Shift Path tests
SP TEST SCU (1-3) SPT       SCU Shift Path tests
SP TEST CPU (0-3) NFT       CPU NFT tests
SP TEST SCU (1-3) NFT       SCU NFT tests
SP TEST CPU (0-3) DPM       CPU DPM tests
SP TEST SCU (1-3) DPM       SCU DPM tests
SP TEST CPU (0-3) DISPLAY   CPU Display
SP TEST SCU (1-3) MPM       SCU Maintenance Panel Module
 
Note - Before testing a CPU it must be stopped with the STOP CPU keyin.
       Before testing a SCU it must first be released via SYSCON.
 
 
Option Characters:
B - Bypass  error  message  output.  Bypass  overrides  a  Pass or Cycle
    message  unless Halt  is set;  Halt forces  these messages  out over
    Bypass.
E - Output Transient  Error message. If a numeric  digit (or two digits)
    follows, the value is used  to override the test page standard value
    for the number of retries to  be made. The control of retry count is
    independent of the turn ON or OFF capability of E or NE.
H - Halt  for  input  of  options  following  error  messages,  Test End
    messages, Pass End messages, and Cycle End messages.
I - Inform user of each normal test end. If H is also set, then an Enter
    Options: is appended to the End Test Message. If the next segment is
    being called, if an End Pass  message is being output, or if a cycle
    ends; the End Test message is overridden.
L - Loop on current test (cannot loop on test 0)
N - negate the  following option character (valid preceding  B, E, H, I,
    L, P, R, or T only)
O - go to Enter Options: following complete processing of the options on
    the test request string.
P - Issue an  End Pass message any  time a back jump  is detected by the
    next test  sequencing. If H is  also set, then an  Enter Options: is
    appended to the End Pass  message. The error tallies for the current
    pass are reset  when End Pass is reported or  when P is being turned
    ON.
R - Issue and End Cycle message  any time a normal test page termination
    would occur and cycle back to the first test in the current sequence
    again. If H is also set,  then an Enter Options:  is appended to the
    End Cycle  message. The error tallies for  both the current pass and
    current  cycle  are  reset  when  End  Cycle  is reported. The error
    tallies for the cycle are reset whenever R is being turned ON.
S - unconditionally Skip to the next test
T - If turn ON (no preceding  N), then unconditionally jump to the first
    occurrence of the test in the current sequence; the test number must
    follow and must  be non-zero, and can consist of  one, two, or three
    digits.  For segmented  test pages,  a value  outside of the current
    segment causes  a jump to the  corresponding segment without further
    processing of  the current option string. If  turn OFF (NTxxx), then
    then test number must be in  the current sequence and not the forced
    termination test number.
 
Control Mnemonics:
The  following control  mnemonics (.OPTIONS)  will be  processed only if
input for the Enter Options: request:
 .GO - return to the test page where interrupted
       if S or Txxx, or .RSEQ or .SEQT, has been specified,
       the next sequencing is done.
 .OPT - an Enter Options: message is output
 .RSEQ - resequence tests to their initial (at page call) order
 .SEQT - sequence tests in a special order
 .TAL - A message with a tally of errors is output. P or R must
        be set and the message will include information for
        the current pass or cycle or both depending on the state
        of P or R or both. The error tallies are reset for the
        pass or cycle or both when reported.
 .TEST E - the test page is force terminated
 .TEST W - the test page is wrapped up
 .TYP - subsequent error messages will be printed
 .WAIT - the test page is put in a wait condition
 
Help is provided for the following MOLTS subtopics:
   SYNTAX
   PARAMETERS
   DESCRIPTION
   TESTING
   PARTITIONING
   ITRS
   MDCS
   MDRS
   MFCS
   MLSTAL
   MMTS
   MTCS
   MTGS
   RPMS
   MDS
   TMD
   OPTION
 
 
00006
00002
00007
00006
00021
00021
00005
00005
00013
00007
00012
00010
00010
00011
00014
00006
00012
00013
00014
00005
00016
00018
00023
00001
00004
00015
00020
00022
00022
00024
00016
00018
00003
00011
Syntax:
   MSG <message text[?]>
 
   MSG - must be entered exactly
         no abbreviations or other forms to avoid confusion
         with MOLTS test requests
   <message text> - text to be sent to the operator's console
   ? - if the message text ends in a question mark, TOLTS
       waits for a reply to the message and prints the reply
 
Description:
The  MSG command of  TOLTS allows a  TOLTS user to  communicate with the
system operator. Text may be sent to the operator's console that does or
does  not require  a reply.  This command  should prove  very helpful to
TOLTS users located at remote sites such as LADC or the TAC center.
 
   ???MSG PLEASE MOUNT FT#MYTAPE
   ???MSG IS THE TAPE MOUNTED?
 
The first example merely sends the text to the console. The second sends
the text and will receive and print the operator's reply.
 
00002
00003
00001
NETCON:
NETCON must be used to partition MLCP/MLC-16 lines prior to testing, and
to return  the lines again when testing  is completed.  Attempts to test
lines  which have  not been  partitioned will  result in a "RESOURCE NOT
AVAILABLE" message from COLTS.
 
Usage:
NETCON is invoked  at the IBEX level prior to  invoking TOLTS, and again
when  TOLTS has exitted.  The NETCON processor  privilege is required to
use NETCON (or have the system operator do it for you).
 
Use the following dialogue to partition lines for testing:
!NETCON
*SELECT NODE = n
*PARTITION a TO b
*END
 
where n is the desired FEP, i.e., 1,2,3, etc. and a TO b is the range of
channels to be partitioned, for example, .2400 TO .25C0.
 
Use the following dialogue to enable lines after testing:
 
!NETCON
*SELECT NODE = n
*RETURN a TO b
*END
 
Partition:
Remember that (a)NETCON deals in  channels (2 per line), and (b) testing
an  odd-numbered line  requires that  both the  odd and  next lower even
line's channels  (4 in all) be partitioned.   The following table shows,
for an  MLCP based at megabus address  .2400, what channel ranges should
be partitioned to test each line.
 
To test:          Partition:
line 0            .2400 to .2440     channels 0&1
line 1            .2400 to .24C0     channels 0-3, lines 0&1
line 2            .2500 to .2540     channels 4&5
line 3            .2500 to .25C0     channels 4-7, lines 2&3
line 4            .2600 to .2640     channels 8&9
line 5            .2600 to .26C0     channels 8-11, lines 4&5
line 6            .2700 to .2740     channels 12&13
line 7            .2700 to .27C0     channels 12-15, lines 6&7
 
Note  that due  to these  allocation requirements,  it's not possible to
simultaneously  test both  lines of  an even-odd  pair, i.e.,  there's a
maximum of 4 tests allowed per MLCP and one test per even-odd line pair.
To partition  the entire MLCP in the  example above, the correct channel
range input would be .2400 to .27C0 (8 lines, 16 channels).
 
NETCON may also be used to display system configuration data:
!NETCON
*DISPLAY STATUS
(status of all FEP's will be output)
*SELECT NODE = n
*DISPLAY CHANTBL CHAN = a TO b
(table of data for channels a to b will be output)
(to specify all channels use DISPLAY CHANTBL FULL)
*END
One further hint: prior to using NETCON, use (or have the
operator use) SPY to list those lines which are currently
active.
 
00003
00002
00002
00001
Notation Conventions used for describing TOLTS Command Syntax:
 
CAPITAL LETTERS - Capital letters must be entered as shown for input
 
lowercase letters - Lowercase letters identify an element that must be
                    replaced with a user selected value.
 
Brackets [] - An element inside brackets in optional.
 
Braces {} - Elements placed inside a pair of braces identify a
            required choice. These are always used with the OR
            bar (|).
 
 
Owner:
Kirk Dixon, LADC Phoenix
(Also Gordon Guenthner)
 
 
Syntax:
   [TEST] Piccdd[ooooo] |         initial POLTS request
   [TEST] Pxiccdd[oooo] |         communicate with POLTS test
   [TEST] PLSTAL        |         POLTS List All request
   [TEST] PW                      wrap-up POLTS with a dump
 
Parameters:
   i - single digit IOM number
   ccc - two or three digit channel number in decimal
   dd - two digit device number in decimal
   o - option character
       type HELP (TOLTS) POLTS OPTIONS for a list of options
   x - communication character
       Note that options are not required, but if entered, the
       length of the POLTS command may not exceed 11 characters.
       E = end the running test normally
       O = modify options for a running test
 
Description:
POLTS (Peripheral On-Line Test  System) provides a comprehensive, system
level test of peripherals in a CP-6 environment.  Peripherals are tested
from  the  host  using  standard  I/O  commands  and sequences through a
special testing  interface built into the  CP-6 operating system.  POLTS
tests  offer no  explicit diagnostic  information, but provide extensive
information about test failures, i.e.,  what test and command were being
executed,  expected and  received statuses,  data patterns  in error and
other pertinent data.
 
POLTS  test failure information  is intended to  help the Field Engineer
troubleshoot  a  peripheral   problem.   MOLTS  tests  provide  explicit
diagnostic  information  about  peripheral  failures,  and do actual ORU
callout and recommend troubleshooting procedures.
 
POLTS Test Procedure:
All POLTS  tests run concurrent with the  operating system and all other
user  activity (which  obviously must  not be  directed to  the affected
peripheral).  The following is the procedure which is generally used for
running POLTS on a peripheral:
 
a.  Logon on a properly authorized account.  (Proper authorization
    means (1) TND privilege and (2) access to files in :FED and :SYS.)
b.  Have the system's operator use SYSCON to set the TDOK bit for
    the device to be tested.
c.  Invoke TOLTS by entering !TOLTS
d.  TOLTS will respond with a ??? prompt, at which point it is ready
    for the initial test request.  From this point on, the human
    interface dialog is the same as it is for all online test
    systems.
e.  TOLTS will automatically ask the operator permission to run
    POLTS at the operator console.  The operator may respond and
    either allow testing or not.  The console dialog:
 
         sysid: REQUEST DIAG KEYIN
         !DIAG sysid  [operator giving permission]
         !NODIAG sysid  [operator denying permission]
 
f.  POLTS begins running and continues to a termination.
    Communication can be established with POLTS at any time by
    hitting the "break" key.
g.  On completion, the operator should reset the TDOK bit for the
    device via SYSCON.
h.  POLTS tests do not run on FIPS devices.
 
 
POLTS Partitioning Tips:
a.  DISKS -- no need to partition any shared disks;  CP-6 allows
    POLTS testing concurrent with user activity on same drive.
b.  TAPES -- partition with SYSCON before mounting the test tape
    so CP-6 will not AVR it or set the "protect" bit.
c.  LINE PRINTER -- "LOCK" it from the operator console before using
    using SYSCON to gracefully remove it from the system.
d.  CARD PUNCH -- "LOCK" it also before using SYSCON.
e.  CARD READER -- partition it first before loading the test deck and
    putting it in ready so CP-6 will ignore the special interrupt
    generated when the reader is put in "READY".
POLTS LiST ALl (PLSTAL):
The  POLTS  LSTAL  command  will  cause  POLTS  to  issue a user message
displaying  the current status  of all of  the user's test programs that
have  not terminated,  i.e., test  in execution,  test waiting  for idle
time, test in abeyance, test in WAIT mode, etc...
 
 
Option Characters:
B - Bypass  error  message  output.  Bypass  overrides  a  Pass or Cycle
    message  unless Halt  is set;  Halt forces  these messages  out over
    Bypass.
E - Output Transient  Error message. If a numeric  digit (or two digits)
    follows, the value is used  to override the test page standard value
    for the number of retries to  be made. The control of retry count is
    independent of the turn ON or OFF capability of E or NE.
H - Halt  for  input  of  options  following  error  messages,  Test End
    messages, Pass End messages, and Cycle End messages.
I - Inform user of each normal test end. If H is also set, then an Enter
    Options: is appended to the End Test Message. If the next segment is
    being called, if an End Pass  message is being output, or if a cycle
    ends; the End Test message is overridden.
L - Loop on current test (cannot loop on test 0)
N - negate the  following option character (valid preceding  B, E, H, I,
    L, P, R, or T only)
O - go to Enter Options: following complete processing of the options on
    the test request string.
P - Issue an  End Pass message any  time a back jump  is detected by the
    next test  sequencing. If H is  also set, then an  Enter Options: is
    appended to the End Pass  message. The error tallies for the current
    pass are reset  when End Pass is reported or  when P is being turned
    ON.
R - Issue and End Cycle message  any time a normal test page termination
    would occur and cycle back to the first test in the current sequence
    again. If H is also set,  then an Enter Options:  is appended to the
    End Cycle  message. The error tallies for  both the current pass and
    current  cycle  are  reset  when  End  Cycle  is reported. The error
    tallies for the cycle are reset whenever R is being turned ON.
S - unconditionally Skip to the next test
T - If turn ON (no preceding  N), then unconditionally jump to the first
    occurrence of the test in the current sequence; the test number must
    follow and must  be non-zero, and can consist of  one, two, or three
    digits.  For segmented  test pages,  a value  outside of the current
    segment causes  a jump to the  corresponding segment without further
    processing of  the current option string. If  turn OFF (NTxxx), then
    then test number must be in  the current sequence and not the forced
    termination test number.
X - Enables  the extended status  portion of the  standard error message
    for   MPC   test   pages.   This   option  is  initially  forced  ON
    automatically.  The user should  utilize the NX option characters if
    no   extended  status   message  is   desired.  The   message  could
    subsequently be enabled by utilizing the X option character.
 
Control Mnemonics:
The  following control  mnemonics (.OPTIONS)  will be  processed only if
input for the Enter Options: request:
 .GO - return to the test page where interrupted
       if S or Txxx, or .RSEQ or .SEQT, has been specified,
       the next sequencing is done.
 .MAN - places test in manual mode
 .OPT - an Enter Options: message is output
 .RSEQ - resequence tests to their initial (at page call) order
 .SEQT - sequence tests in a special order
 .SEQxx - accept a TDL (T&D Language) instruction to replace
          the instruction on line xx
 .SEQAxx - accept test page data values to replace data
           values on line XX
 .TAL - A message with a tally of errors is output. P or R must
        be set and the message will include information for
        the current pass or cycle or both depending on the state
        of P or R or both. The error tallies are reset for the
        pass or cycle or both when reported.
 .TEST E - the test page is force terminated
 .TEST W - the test page is wrapped up
 .TYP - subsequent error messages will be printed
 .WAIT - the test page is put in a wait condition
 
Help is provided for the following POLTS subtopics:
   SYNTAX
   PARAMETERS
   DESCRIPTION
   TESTING
   PARTITIONING
   PLSTAL
   OPTIONS
 
 
00002
00006
00007
00001
00005
00006
00008
00004
END
Restrictions:
Here is  some additional information on TOLTS  and its idiosyncracies in
the CP-6 environment:
   1. TOLTS can only run one subexecutive at a time.
   2. There  is  no  dedicated  printer  capability,  i.e., .PRT or .PR2
      options.
   3. TURTLE (TOLTS  User Requested Terminal Line  Exerciser) is not run
      under the TOLTS system.  It is available only by calling it at the
      IBEX level (!TURTLE).
   4. There is  no Partial On-Line (POL)  testing capability. Hence test
      requests of the form, TEST Bfmmmm, are invalid.
   5. TOLTS  is only compatible  with deckfiles that  were created using
      DEER (DEckfile Editor Routine).
 
DPS90
Subsystems:
TOLTS supports the following major test subsystems:
      COLTS - Communications On-Line Test System
              * MLCP, MLC-16, HDLC tests
              * MLCP, MLC-16 Central tests (M option)
              * FEP Coupler tests (0000 address)
              * Device tests (V option)
      MOLTS - Mainframe On-Line Test System
              * MPC tests (Micro-Programmed Controller)
              * ITR's (Isolation Test Routines)
              * MDR tests (Micro-coded Device Routines)
              * MTAR/FTAR tests (Media Test And Recertification)
              * MTC test (MOLTS Tape Compatibility)
              * MTG test (MOLTS Tape Shotgun)
              * MDC tests (MOLTS Disk Confidence)
              * RPM (Initiates the SP maintenance session)
              * MDS test (Modular Disk Subsystem)
              * TMD test (self tests, Modular Disk Subsystems)
      POLTS - Peripheral On-Line Test System
              * POLTS tests
 
Terminal Conventions:
   1. All CP-6 terminal conventions apply, including full duplex.
   2. <BREAK>  is used to  initiate communications with  a subexec while
      the subexec is in execution.
.pa
 
 
   3. TOLTS may be run from a system console using a console ghost.
      To use it in this manner, one will need to prefix each T&D 
      command with 'G:' (e.g., G:TOLTS). Also, the 'B:' command 
      used to provide a BREAK command to the console ghost.
 
 
TURTLE
TOLTS User Requested Terminal Line Exerciser:
TURTLE  is  the  terminal  test  or  "TOLTS User Requested Terminal Line
Exerciser".   This program  is independent  of TOLTS.   It is  the first
level of  testing and will report  the errors as they  occur.  There are
eight  tests and  the program  flows sequentially  from one  test to the
next.  The user may exit TURTLE by hitting <break>.
 
TURTLE is invoked at the IBEX level by typing:
   !TURTLE
 
TOLTS Usage:
TOLTS is a separately priced software product.  The TOLTS program is not
capable of testing any hardware without the installation of an IFAD tape
using DEER.
 
For additional information type
    ???HELP IFAD
 
END
