The STATS processor is used to display or write to disk host CP-6 performance 
and resource-utilization data.  The STATS data written to disk is the 
performance log file (usually :SNAPS in the current account).  STATS also 
provides the capability of generating summaries, graphical representations, 
and analyses of this data.  In addition, STATS is used to display summary 
statistics about FEP performance and resource utilization. 
To obtain more HELP information, see 
HELP (STATS) TOPICS              Displays available topics. 
HELP (STATS) COMMANDS            Displays a list of STATS 
                                 commands. 
HELP (STATS) COMMAND_SUMMARY     Displays a list of STATS 
                                 commands by category. 
HELP (STATS) STATS_ITEMS         Displays a list of STATS 
                                 items and their definitions. 
HELP (STATS) command PARAM       Displays parameters associated 
                                 with a particular command. 
HELP (STATS) command DESCRIPTION Displays description associated 
                                 with a particular command. 
?                                Displays next level of HELP 
                                 messages. 
??                               Displays all levels of HELP 
                                 messages. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
DO
Format: 
          {   [({LOG|LINEAR}[, n-m])]      [({LOG|LINEAR}[, n-m])]   } 
ANA[LYZE] {exp[(n-m                )] [,exp[(n-m                )]...} 
          {ALL                                                       } 
Parameters: 
exp    is a combination of constants, STATS items, parentheses and operators, 
which produces an arithmetic result.  For STATS items, type HELP (STATS) 
STATS_ITEMS.  For rules governing STAT expressions, type 
HELP(STATS)STATS_EXPRESSIONS.  Up to 20 expressions (with their optional scale 
specifications) may be given in each ANALYZE command. 
ALL    elicits compilation and output of statistics and plots on each of the 
STATS items. 
LO[G]|LI[NEAR]    specifies whether a linear or logarithmetic scale is to be 
used in displaying the values of a STATS expression.  The default is whatever 
is appropriate to the leftmost item in the expression. 
n-m    are decimal values specifying upper and/or lower limits of the values 
to be displayed. 
Description: 
The ANALYZE command is used to compile and output certain elementary 
statistics and distribution plots for data extracted from a STATS performance 
log file.  Intervals are extracted from the file based on the criteria 
specified by the TIME and SELECT commands (if such are used), and statistical 
and distribution data is computed based on these intervals. 
00002
00001
For a list of FEP ASYNC handler definitions, enter:  ? or ??.  To access 
individual definitions, type: 
HELP (STATS) ASYNC_HANDLER_DISPLAY definition 
where definition is any of the following: 
HANDLER_TO_LINE, OTHER_STATISTICS 
  Statistics                   
  Category                   Description 
Handler-to-line and line-to-handler statistics are provided for: 
Interrupts/minute          The number of interrupts registered per 
                           minute. 
% interrupt service time   The percentage of time spent processing 
                           interrupts.  This value plus the percentage 
                           of scheduled (non-interrupt) CPU value 
                           provided in the VDH statistics (see 
                           VDH_DISPLAY) is the total percentage of execution 
                           and service time for this handler (see 
                           FEP_MONITOR_DISPLAY). 
Buffer utilization, bytes  The number of bytes currently being used for 
                           async data transfers. 
Other statistics provided include: 
Context utilization,       The number of bytes currently being used in 
bytes                      handler memory for async contexts. 
Small output buffer,       The number of buffer requests per minute. 
Large output buffer,       (The size of the small and large output 
  gets/min                 buffers are set via the NETCON SET command 
                           handler parameters OTPBFRBYTSIZSML and 
                           OTPBFRBYTSIZBIG, respectively.) 
Small output buffer,       The number of times the buffer was filled 
Large output buffer,       with data from the CQ before the terminal 
  full/min                 was ready to accept the data. 
Line speeds                The distribution of async terminals by line 
                           speed. 
00001
00002
Format: 
{BAR[GRAPH]} exp[({LO[G]|LI[NEAR]}[, n-m])] 
{GRA[PH]   }    [(n-m)                    ] 
Parameters: 
exp    is a combination of constants, STATS items, parentheses and operators, 
which produces an arithmetic result.  For STATS items, type HELP (STATS) 
STATS_ITEMS.  For rules governing STAT expressions, type HELP (STATS) 
STATS_EXPRESSIONS. 
LO[G]|LI[NEAR]    see ANALYZE command. 
n-m    see ANALYZE command. 
Description: 
The BARGRAPH (or GRAPH) command may be used to extract data from a STATS 
performance log file and produce a bargraph displaying the value of a STATS 
expression.  Intervals will be selected from the file based on the criteria 
specified by the TIME and SELECT commands (if such were used), and for each 
interval selected, STATS will display the time at which the interval ended, 
the value of the specified expression, and a graphic representation of the 
expression's value relative to the range of values used to graph the 
expression. 
00002
00001
For a list of FEP BISYNC handler definitions, enter:  ? or ??.  To access 
individual definitions, type: 
HELP (STATS) BISYNC_HANDLER_DISPLAY definition 
where definition is any of the following: 
3270, RBT, POLLED_VIP 
  Bisync    Statistics                   
  Device    Category                   Description 
3270      Active sessions            The number of 3270 devices being 
                                     serviced by the bisync handler. 
          Handler-to-line and line-to-handler statistics are provided 
          for: 
          Characters/minute          The total number of characters per 
                                     minute. 
          Interrupts/minute          The number of interrupts registered 
                                     per minute. 
          % interrupt service time   The percentage of time spent 
                                     processing interrupts.  This value 
                                     plus the percentage of scheduled 
                                     (non-interrupt) CPU value provided 
                                     in the VDH statistics (see 
                                     VDH_DISPLAY) is the total 
                                     percentage of execution and service 
                                     time for this handler (see 
                                     FEP_MONITOR_DISPLAY). 
          Buffer utilization, bytes  The number of bytes currently being 
                                     used for bisync data transfers. 
          Other statistics provided include: 
          Context utilization,       The number of bytes currently being 
          bytes                      used in handler memory for bisync 
                                     contexts. 
          Output buffers             Buffer distribution by (byte) size. 
          # of transactions/minute   The number of input blocks from the 
                                     line per minute. 
          # of general poll loops/   The number of times per minute all 
          minute                     controllers are polled. 
          # of general polls         The number of times per minute 
          followed by output/minute  there was output data to send after 
                                     general polling. 
          # of general polls         The number of times per minute a 
          followed by nothing to     clock was started because there 
          do/min                     was no output to send after general 
                                     polling. 
          # of select sequences      The number of times the specific 
          sent/minute                controllers are polled per minute. 
RBT       Active streams             The number of active RBT streams 
                                     being serviced by the bisync 
                                     handler. 
          Handler-to-line and line-to-handler statistics are provided 
          for: 
          Characters/minute          The total number of characters per 
                                     minute. 
          Data blocks/minute         The total number of data blocks 
                                     transferred per minute. 
          Characters/block           The average block size: 
                                     (characters/min)/(data blocks/min). 
          Interrupts/minute          The number of interrupts registered 
                                     per minute. 
          % interrupt service time   The percentage of time spent 
                                     processing interrupts.  This value 
                                     plus the percentage of scheduled 
                                     (non-interrupt) CPU value provided 
                                     in the VDH statistics (see 
                                     VDH_DISPLAY) is the total 
                                     percentage of execution and service 
                                     time for this handler (see 
                                     FEP_MONITOR_DISPLAY). 
          Buffer utilization, bytes  The number of bytes currently being 
                                     used for bisync data transfers. 
          Other statistics provided include: 
          Context utilization,       The number of bytes currently being 
          bytes                      used in handler memory for bisync 
                                     contexts. 
          # of transactions/minute   The number of input blocks from the 
                                     line per minute. 
POLLED    Active sessions            The number of polled VIP devices 
VIP                                  being serviced by the bisync 
                                     handler. 
          Handler-to-line and line-to-handler statistics are provided 
          for: 
          Characters/minute          The total number of characters per 
                                     minute. 
          Interrupts/minute          The number of interrupts registered 
                                     per minute. 
          % interrupt service time   The percentage of time spent 
                                     processing interrupts.  This value 
                                     plus the percentage of scheduled 
                                     (non-interrupt) CPU value provided 
                                     in the VDH statistics (see 
                                     VDH_DISPLAY) is the total 
                                     percentage of execution and service 
                                     time for this handler (see 
                                     FEP_MONITOR_DISPLAY). 
          Buffer utilization, bytes  The number of bytes currently being 
                                     used for bisync data transfers. 
          Other statistics provided include: 
          Context utilization,       The number of bytes currently being 
          bytes                      used in handler memory for bisync 
                                     contexts. 
          Output buffers             Buffer distribution by (byte) size. 
          # of transactions/minute   The number of input blocks from the 
                                     line per minute. 
          # of general poll loops/   The number of times per minute all 
          minute                     controllers are polled. 
          # of general polls         The number of times per minute 
          followed by output/minute  there was output data to send after 
                                     general polling. 
          # of general polls         The number of times per minute a 
          followed by nothing to     clock was started because there 
          do/min                     was no output to send after general 
                                     polling. 
          # of select sequences      The number of times the specific 
          sent/minute                controllers are polled per minute. 
00001
00003
00002
DEVICE_OR_CHANNEL_DISPLAY
    A list of STATS commands and their definitions can be accessed by typing a 
    ? or a ??.  To obtain definitions of individual commands, type 
    HELP (STATS) COMMANDS command 
    where command is any of the following: 
    ANALYZE, BARGRAPH, DATE, DIRECTORY, DISPLAY, DO, END, ENTER, ERASE, FILE, 
    GLOM, GO, HELP HISTOGRAM, INITIATE, INTERVAL, LOG, MESSAGE, OUTPUT, PLOT, 
    PRINT, QUIT, REPLAY, RESET, SCATTERGRAM, SELECT, SNAPSHOT, SPAN, START, 
    STATISTICS, STATUS, STOP, SUMMARIZE, TERMINATE, TIME, X. 
  Command        Description 
  ANALYZE 
                 Displays specified statistics and distribution information 
                 from the performance log file. 
  BARGRAPH 
                 Displays a bargraph. 
  {DIRECTORY|DIR} 
                 Changes the default account and packset. 
  DISPLAY 
                 Sets flags indicating what displays are to be produced.  (The 
                 set of displays so denoted may be elicited by a SNAP, GO, 
                 REPLAY, or GLOM command.) 
  {DO|!} 
                 Enables IBEX command execution. 
  {END|EXIT|QUIT} 
                 Terminates STATS processing. 
  ENTER 
                 Invokes a CP-6 ADAPT dialog from within this processor. 
  ERASE 
                 Deletes accumulated output for logical devices. 
  FILE 
                 Specifies the identity of the performance log file.  (The 
                 SNAP or GO commands will cause records to be written to this 
                 file.) 
  GLOM 
                 Produces displays of performance data (PMDAT) and FEP data 
                 for a pre-specified time span. 
  GO 
                 Starts the sequence of displays and/or log file writes, as 
                 specified by the DISPLAY, LOG, FILE, and INTERVAL commands. 
  HELP 
                 Requests information concerning a command or concept. 
  HISTOGRAM 
                 Specifies which histograms are to be produced by a DISPLAY 
                 command specifying the HISTOGRAMS display. 
  INTERVAL 
                 Specifies how often performance snapshots are to be taken. 
                 (The GO commands will cause snapshots to be taken at the 
                 interval so specified.) 
  LOG 
                 Sets flags indicating what data is to be written to the 
                 performance log file.  (A write-to-log of the data so denoted 
                 may be elicited by a SNAP or GO command.) 
  MESSAGE 
                 Sends a specified message text to the central system console. 
  OUTPUT 
                 Directs processor output to a destination. 
  {PLOT|SCATTERGRAM} 
                 Plots one set of data from the performance log file against 
                 another. 
  PRINT 
                 Directs that output accumulated for logical devices be sent 
                 to destinations immediately. 
  REPLAY 
                 Reads performance data from the performance log file and 
                 produces a sequence of displays. 
  RESET 
                 Resets DISPLAY, LOG, INTERVAL, FILE, and/or TIME flags 
                 parameters to their default values. 
  SELECT 
                 Specifies the criteria which a logged snapshot must meet in 
                 order to be included in REPLAY, STATISTICS, ANALYZE, BARGRAPH 
                 or PLOT processing. 
  SNAPSHOT 
                 Initiates an immediate, one-time set of displays and/or 
                 log-file writes, as specified by the DISPLAY, LOG, and FILE 
                 commands. 
  {START|INITIATE} 
                 Starts up the Monitor Usage Evaluator (MOUSE). 
  STATISTICS 
                 Displays specified statistics from the performance log file. 
  STATUS 
                 Requests printout of the current values of the parameters 
                 associated with the DISPLAY, LOG, INTERVAL, FILE, TIME, and 
                 SELECT commands. 
  {STOP|TERMINATE} 
                 Deactivates the Monitor Usage Evaluator (MOUSE). 
  SUMMARIZE 
                 Specifies the content of the one-line summary display invoked 
                 by a DISPLAY command specifying the SUMMARY display. 
  {TIME|DATE|SPAN} 
                 Identifies portions of a performance log file. 
00005
00001
00002
00029
00003
00004
00005
00006
00007
00008
00006
00009
00010
00011
00012
00013
00024
00014
00015
00016
00017
00018
00019
00006
00020
00021
00018
00022
00023
00029
00024
00025
00026
00027
00028
00027
00029
00006
    The STATS commands are listed by function below.  The declaration commands 
    describe the characteristics of the desired displays or log writes or 
    sequences thereof, but do not of themselves initiate any production of 
    displays or log writes. 
    Declaration commands:  FILE, DATE, DISPLAY, HISTOGRAM, INTERVAL, LOG, 
    RESET, SELECT, SPAN, SUMMARIZE, TIME. 
    Display and/or Write Performance Log commands:  GO, SNAPSHOT 
    Display Performance Log commands:  GLOM, REPLAY 
    Declaration and Display Performance Log commands:  ANALYZE, BARGRAPH, 
    PLOT, SCATTERGRAM, STATISTICS. 
    Control Commands:  START, STOP, STATUS, MESSAGE, HELP, END, QUIT, EXIT, 
    DIRECTORY, DO, ERASE, OUTPUT, PRINT. 
For a list of FEP common handler definitions, enter:  ? or ??.  To access 
individual definitions, type: 
HELP (STATS) FEP_HANDLER_DISPLAY definition 
where definition is any of the following: 
BUFFER_MANAGEMENT, FREE_BUFFER_DISTRIBUTION 
  Statistics                                  
  Category            Statistics            Description 
Buffer Management   These statistics include the following memory pool 
                    and clock service data (available through the 
                    KV$BPC structure): 
                    Words total           The total number of words in 
                                          buffer space memory. 
                    In use                The total number of buffer 
                                          space memory words currently 
                                          in use. 
                    Peak in use           The most buffer space memory 
                                          used at one time. 
                    # of get calls/       The number of buffer requests 
                    minute, % time        per minute and the time taken 
                                          by the buffer requests. 
                    # of release calls/   The number of buffer release 
                    minute, % time        requests per minute and the 
                                          time taken by the buffer 
                                          release calls. 
                    # of get failures     The number of buffer requests 
                    with enough free/     that failed because the 
                                          available buffer space was 
                                          not in large enough pieces. 
                    # of fragmentations/  The number of memory 
                    minute                fragmentations per minute. 
                    # of re-combinations/ The number of times memory 
                    minute                recombined per minute. 
                    # of buddy searches/  The number of buddy space 
                    minute                searches per minute. 
                    Clock context block   A count of the clock buffers. 
                                          This value is the number of 
                                          clocks (timers) running in 
                                          the handler. 
                    Service calls/min     Number of clock service calls 
                                          (i.e., set clock, start timer 
                                          and stop timer) per minute. 
                    Expirations/min       Number of clock time outs per 
                                          minute. 
     Note:  If the BISYNC handler supports both RBT and 3270 devices, 
            RBT and 3270 share the same buffer management data. 
Free Buffer    The distribution of handler buffers by buffer size.  The 
Distribution   first row contains the buffer size for the columnar 
               data.  Each column represents the buffer size doubled. 
               There are always two rows of statistics, as follows: 
               follows: 
               Row         Description 
               # free      A count of the number of available buffers, 
                           by buffer size. 
               peak free   The largest number of buffers ever 
                           available, by buffer size. 
00001
00002
    For a list of CPU display definitions, enter: ??. 
  Display Entry     Definition 
  % mode execution 
                    The percentage of CPU time spent executing user code in 
                    each mode.  The mode is specified as either batch, online, 
                    ghost, or TP.  This percentage is directly chargeable to 
                    users in the form of CPU execution time. 
  % mode service 
                    The percentage of CPU time spent executing monitor code to 
                    satisfy user monitor service requests.  The mode is 
                    specified as batch, online, ghost, or TP.  This percentage 
                    is directly chargeable to users in the form of CPU service 
                    time. 
  % monitor execution 
                    The percentage of CPU time spent executing monitor code 
                    for internal monitor functions (e.g., scheduling, 
                    interrupt handling, etc.).  This percentage of the CPU 
                    time is the monitor overhead. 
  % I/O wait 
                    The percentage of CPU time spent idle waiting for I/O 
                    operations to complete.  If the system did not have to go 
                    into an idle state waiting for I/O to complete, this 
                    percentage will be zero. 
  % resource wait 
                    The percentage of CPU time spent idle waiting for an 
                    internal monitor resource to become available.  If the 
                    system did not have to go into an idle state waiting for 
                    an internal monitor resource to become available, this 
                    percentage will be zero. 
  % I/O resource wait 
                    The percentage of CPU time spent idle waiting for I/O to 
                    complete or for an internal monitor resource to become 
                    available.  If the system did not have to go into an idle 
                    state waiting for an I/O to complete or an internal 
                    monitor resource to become available, this percentage will 
                    be zero. 
  % true idle 
                    The percentage of CPU time that was spent idle with 
                    nothing to do. 
  ETMF 
                    Execution time multiplication factor.  This factor is 
                    multiplied times the required CPU time to give an estimate 
                    of how much elapsed time will be required to execute a 
                    task.  For example, if a task requires 2 CPU minutes and 
                    the ETMF is 3, then the task will require approximately 6 
                    minutes of elapsed time to complete. 
  90% response time 
                    The time in milliseconds between the receipt of an 
                    activation character (normally a carriage return) by the 
                    host and the start of processing for 90% of the activation 
                    characters received.  The 90% response time is calculated 
                    only for online users.  Note that this is not the response 
                    time from last character entered to first character 
                    received, and does not include delays in the FEP. 
  I/O load factor 
                    This factor is the measure of the I/O load on the system. 
                    This factor is the probability that an I/O request will be 
                    queued rather than executed immediately.  This number is 
                    the average of the I/O load factors of all devices active 
                    during the interval. 
  # of mode users 
                    The number of users on the system for each mode.  The mode 
                    is specified as batch, online, ghost or TP.  For a GO or 
                    REPLAY command, the number in the snap column is the 
                    number of users on the system in the respective mode at 
                    the end of the interval.  The number in the all column is 
                    the average number of users on the system in the 
                    respective mode since the last system boot or recovery. 
                    For a GLOM command, each column is the average number of 
                    users on the system in the respective mode during the 
                    interval specified in each column. 
  I/Os per minute 
                    The number of I/O connects per minute to all IOM-connected 
                    controllers and system consoles.  Each connect may contain 
                    several I/O commands for the controller. 
  Schedules per minute 
                    The number of passes per minute through the system 
                    scheduler.  The number of schedules per minute is 
                    influenced by the number of I/Os per minute, the number of 
                    interactions per minute, and tuning parameters. 
  Interactions per min 
                    The number of activation characters (e.g., carriage 
                    return, line feed, etc.) received by the host per minute. 
  Events per minute 
                    The number of scheduler events that occurred per minute. 
  PMMEs per minute 
                    The number of monitor service requests per minute.  Every 
                    monitor service request is a Privileged Master Mode Entry 
                    (PMME) CLIMB instruction. 
  Avg. usec per PMME 
                    The average number of microseconds required to complete 
                    the monitor service request. 
  Minutes in interval 
                    The number of minutes in the interval.  The all column 
                    contains the number of minutes since the last system boot 
                    or recovery.  The snap column contains the number of 
                    minutes in the interval of the INT or GLOM command. 
00011
00017
00008
00015
00014
00010
00012
00006
00004
00018
00001
00003
00016
00009
00005
00013
00002
00007
TIME
DEVICE_OR_CHANNEL_DISPLAY
For a list of DEVICE or CHANNEL display definitions, enter: ??. 
  Heading     Definition 
  # of connects 
              The number of connects to the controller, device, or channel.  A 
              connect is performed at the beginning of an input/output 
              request.  A connect may contain more than one input/output 
              operation. 
  Connects per min. 
              The number of connects per minute to the controller, device, or 
              channel; that is the number of connects divided by the number of 
              minutes in the interval. 
  % idle 
              The percentage of time the controller, device, or channel is 
              idle.  Idle means no input/output is in progress and no 
              input/output is waiting.  For controllers this value is always 
              100%. 
  % Wait 
              The percentage of time the controller, device, or channel is 
              waiting.  Waiting means no input/output is in progress, and one 
              or more input/output requests are waiting but cannot be started 
              because no IOM channel or controller slot is available.  For 
              controllers and channels, this value is always 0%. 
  % busy 
              The percentage of time the controller, device, or channel is 
              busy.  Busy means input/output is in progress and no other 
              input/output request is waiting.  For controllers, this value is 
              always 0%. 
  % backlog 
              The percentage of time the controller, device, or channel 
              input/output is backlogged.  Backlog means one input/output is 
              in progress and one or more input/output requests are waiting. 
              For controllers and channels, this value is always 0%. 
  Load factor 
              The percentage of time an input/output request for a controller, 
              device, or channel will be queued instead of initiated 
              immediately.  This percentage is calculated as LOAD FACTOR = 
              100% * ( wait + backlog ) / ( 100 - idle ).  For controllers and 
              channels, this value is always 0%. 
00006
00005
00001
00002
00003
00007
00004
DISPLAY
Format: 
{DIR|DIRECTORY} [fid|R[ESET]] 
Parameters: 
fid    specifies the new default account fid, and may consist of an account or 
a packset name and an account. 
RESET    specifies that the default account is to be reset to the running 
account. 
Description: 
DIRECTORY changes the default account and packset.  The default account and 
packset are the account and associated packset that are selected if an account 
is not supplied as part of a disk file fid specification.  Initially, the 
default account is the logon or running account and the packset name is nil. 
When used without parameters, DIRECTORY displays the current directory 
pointer. 
Examples: 
#DIRECTORY .SYSLIB 
This command directs that subsequent fids that do not include an account are 
to default to the .SYSLIB account and the packset associated with that 
account. 
#DIRECTORY DP#UTIL.Y 
This command specifies that subsequent fids that do not include an account are 
to default to the Y account on the packset named UTIL. 
#DIRECTORY RESET 
This command re-establishes the running account and its associated packset as 
the default. 
00002
00003
00001
Format: 
Form 1: 
DI[SPLAY] displayname[, displayname] ... 
Form 2: 
ALS[O] DI[SPLAY] displayname[, displayname] ... 
Form 3: 
DON[T] DI[SPLAY] displayname[, displayname] ... 
Parameters: 
displayname    is any of the display names that can be displayed by typing a ? 
or ?? after this message.  To display a particular display name, type HELP 
(STATS) DISPLAY_NAMES 
Description: 
The DISPLAY command sets flags indicating what data reports are to be produced 
by SNAP, GO, REPLAY, and GLOM processing.  The DISPLAY form of the command, 
Form 1, clears all previous flags and sets those specified by the list of 
displaynames.  Form 2, the ALSO DISPLAY form, sets the indicated flags without 
clearing those set by previous DISPLAY commands.  Form 3, DONT DISPLAY, resets 
the indicated flags without affecting any others. 
00002
00001
For a list of valid display names and their definitions, enter:  ? or ??. 
To access individual display name definitions, type: 
HELP (STATS) DISPLAY displayname 
where valid display names are ALL, CHANNELS, CPU, DEVICES, EVERYTHING, FAULTS, 
FEP, FEP_EXTENDED, FEP_SUMMARY, HISTOGRAMS, IO, MOUSE, NONE, NOTHING, PMDAT, 
PROCESSORS, RESOURCES, SCPU, SUMMARY. 
CPU is the default. 
  Display Name   Description 
  {ALL|ANY[THING]|EVE[RYTHING]} 
                 All STATS display items. 
  CHA[NNELS] 
                 Displays activity figures for all host IOM channels. 
  CPU 
                 Displays an overview of the performance of the CP-6 system. 
                 Data displayed include a breakdown of CPU time spent by user 
                 type, number of users (total and by user type), Execution 
                 Time Multiplication Factor, 90  response time, I/O load 
                 factor, and several miscellaneous scheduling counters.  CPU 
                 is the default. 
  DEV[ICES] 
                 Displays activity figures for all host-resident I/O devices. 
  FAULTS 
                 Displays information gathered by the system hardware fault 
                 handler. 
  FEP[{[E]X[TENDED]|S[UMMARY]}] [feplist] [fepstats [FOR fephand]] 
                 EXTENDED    displays extended VDH information.  In addition 
                 to the information displayed in a FEP n display, a FEPX n 
                 display includes VDH structure usage, function count, and 
                 event count data. 
                 SUMMARY    displays summary information of the selected FEP 
                 statistics types for the specified FEP(s) and handler(s).  If 
                 feplist is omitted, displays summary information for all 
                 FEPs. 
                 feplist    is a list of FEP node numbers separated by one or 
                 more spaces.  If a feplist is not specified, all FEPs are 
                 selected. 
                 fepstats    is a list of FEP statistics types separated by 
                 one or more spaces.  Valid values are: 
                     Value       Description 
                     ALL         Means all of the following fepstats 
                                 types. 
                     3270        3270-type statistics. 
                     ASYNC       Asyncrhonous-type statistics. 
                     FEI         FEP interface-type statistics. 
                     HDLC        HDLC-type statistics. 
                     MONITOR     LCP6-type statistics. 
                     PLDVIP      Polled VIP-type statistics. 
                     RBT         Remote batch terminal type statistics. 
                     URP         Unit record type statistics. 
                     VDH         Virtual device handler type statistics. 
                     X25         X.25 type statistics. 
                     X29         X.29 type statistics. 
                     If fepstats is not specified, ALL is assumed. 
                 fephand    is a list of FEP handlers/entities separated by 
                 one or more spaces.  Valid values are: 
                     Value       Description: 
                     'handler'   A handler name (1-8 characters) enclosed 
                                 in quotes.  Only one 'handler' may be 
                                 specified per FEP. 
                     ALL         Specifies all of the following 
                                 handlers/entities. 
                     3270        Specifies the 3270 entity within 
                                 BISYNC. 
                     ASYNC       Specifies the ASYNC handler. 
                     BISYNC      Specifies the BISYNC handler. 
                     or BSC 
                     COUPLER     Specifies the COUPLER handler. 
                     HDLCX25     Specifies the HDLCX25 handler. 
                     MONITOR     Specifies the LCP-6 monitor. 
                     or LCP6 
                     NODEADMN    Specifies the NODEADMN handler. 
                     PLDVIP      Specifies the Polled VIP entity within 
                                 BISYNC. 
                     RBT         Specifies the RBT entity within BISYNC. 
                     UNITREC     Specifies the UNITREC handler. 
                     If a fephand value is not specified, ALL is assumed. 
                     Note:  It is the user's responsibility to ensure that 
                     fepstat and fephand selection combinations are 
                     meaningful. 
  HIS[TOGRAMS] 
                 Displays histograms concerning certain systemwide activities 
                 and parameters (speed of interactive response, memory size of 
                 CP-6 users, etc.). 
  {IO|I/O} 
                 Displays both the DEVICES and CHANNELS data. 
  MOU[SE] 
                 Displays information gathered by the Monitor Usage Evaluator 
                 (MOUSE); provides an analysis of the usage and performance of 
                 all CP-6 monitor services utilized since the START MOUSE 
                 command was issued. 
  {NON[E]|NOT[HING]} 
                 No STATS display items. 
  PM[DAT] 
                 All of the STATS standard displays.  They are standard in the 
                 sense that they do not require starting a special purpose 
                 performance monitor to gather the information to be 
                 displayed. 
  PROCE[SSORS] 
                 Displays usage figures (number of users and amount of CPU 
                 time used) for CP-6 shared processors. 
  RES[OURCES] 
                 Displays usage figures for CP-6 central resources (pages of 
                 memory, IOQ packets, CFU table entries, etc.). 
  SCP[U] 
                 Displays CPU-specific information for each central processor 
                 in a multi-CPU system. 
  SUM[MARY] 
                 Displays a one-line summary of the system parameters 
                 specified via the SUMMARIZE command. 
00001
00001
00002
00003
00004
00001
00005
00006
00006
00006
00007
00008
00009
00010
00010
00011
00012
00013
00014
00015
Format: 
{DO|!} IBEX-command 
Parameters: 
IBEX-command    any legal IBEX command.  (See the CP-6 Programmer Reference 
Manual (CE40).) 
Description: 
The DO command allows the user to execute an IBEX command without exiting the 
current processor. 
Note:  The ! (exclamation point) may be used instead of the word DO.  It 
should be noted however that if the ! is used in an XEQ file, it will 
terminate the current processor session unless preceded by at least one blank, 
or by a double ! (!!). 
Examples: 
#DO DI 
means display the current system status 
#!LDEV LP09 TITLE='report title',PAGE=100,COPIES=3 
means set up a title and page number for a report destination 
00002
00003
00001
Format: 
{E[ND]|[E]X[IT]|Q[UIT]} 
Description: 
The END (or QUIT or EXIT) command is used to terminate STATS. 
00001
Format: 
ENTER [script_fid] [,frame_name] [initial_input] 
Parameters: 
script_fid    is the file identifier for the script to be executed. 
frame_name    is the first frame of the script to execute. 
initial_input    supplies responses to the initial prompts for the dialog. 
Description: 
The ENTER command invokes a CP-6 ADAPT dialog that permits use of precompiled, 
menu-driven user interfaces called compiled scripts.  script_fid identifies 
the file containing the compiled script for the dialog.  See the CP-6 ADAPT 
Reference Manual (HA12) for more information on using ADAPT dialogs. 
00002
00001
Format: 
ERASE [ALL|ldevlist] 
Parameters: 
ALL    specifies that the accumulated output for all logical devices is to be 
deleted.  This is the default. 
ldevlist    specifies that the accumulated output for the specified logical 
device or devices is to be deleted.  The list is entered in the format 
ldevname[,ldevname]... 
ldevname is a logical device name established through the LDEV command. 
Description: 
ERASE deletes the accumulated output for logical devices. 
Examples: 
#ERASE ALL 
deletes all output accumulated for all logical devices defined for the session 
or job. 
00002
00003
00001
The FAULT display definitions are:    
  Fault        Category       Description 
Command      Memory         Caused by an illegal request by a processor; 
                            e.g., an attempt to execute a privileged 
                            instruction or a privileged option, or to 
                            access working space zero. 
                            Source:  User program error. 
Connect      Instruction    Occurs if input-output interrupt occurs and 
             generated      a master CPU needs to communicate with a 
                            slave CPU. 
                            Source:  Processor (IOM or CPU) issues a 
                            connect request. 
Derail       Instruction    Caused by execution of a Derail instruction 
             generated      in the user program. 
                            Source:  DELTA uses Derail for breakpoints. 
Divide       Program        Occurs if division cannot be carried out 
check        generated      (i.e., the divisor is 0). 
                            Source:  User program error. 
Dynamic      Virtual        Caused by an attempt to execute a CLIMB 
linking      memory         instruction through a dynamic linking 
             generated      descriptor. 
                            Source:  This fault should not occur. 
                            If it does, contact your Bull CP-6 
                            representative. 
Execute      Hardware       Occurs when the EXECUTE switch on the 
             generated      processor maintenance panel is depressed. 
                            Source: Operator. 
Fault-tag    Instruction    Caused by execution of an instruction that 
             generated      has a fault tag address identifier. 
                            Source:  User program error. 
IPR          Instruction    Caused by an illegal address (for 
(Illegal     generated      instructions using the address field to 
Procedure)                  specify a register), an illegal modifier (or 
                            modifier sequence), or an illegal 
                            instruction sequence. 
                            Source: User program error 
Lockup       Program        Occurs if interrupts are inhibited by the 
             generated      program for more than the lock up time. 
                            Source:  The user program. 
Memory       Memory         Occurs when an attempt is made to execute a 
(Store)                     privileged instruction that addresses a 
                            location outside the segment boundary; 
                            execution of the instruction accesses an 
                            empty segment. 
                            Source:  User program error. 
Missing      Virtual        Occurs when a virtual address is referenced 
page         memory         for which a real memory page has not been 
             generated      mapped in. 
                            Source:  User program error or virtual 
                            segment. 
Missing      Virtual        Caused by an attempt to access memory using 
segment      memory         an improperly set segment descriptor. 
             generated      Source: This fault should not occur.  If 
                            it does, contact your Bull CP-6 
                            representative. 
Missing      Virtual        Occurs during virtual to real memory mapping 
WS           memory         when the word obtained from the working 
             generated      space (WS) page table directory cannot be 
                            read. 
                            Source: This fault should not occur.  If 
                            it does, contact your Bull CP-6 
                            representative. 
MME          Instruction    Caused by execution of a Master Mode Entry 
             generated      (MME) instruction in the user program. 
                            Source:  User program, normally TOLTS. 
Op not       Hardware       Occurs if the processor fails to generate 
complete     generated      a memory operation within an appropriate 
                            amount of time, when the system controller 
                            terminates a double/precision cycle, or when 
                            returning to an interrupted multiword 
                            instruction if incorrect data is loaded. 
                            Source: Hardware error. 
             Program        Occurs if a system controller is not 
             generated      attached to the processor for the address 
                            specified, or if the SCU ports are disabled 
                            via program control while the program is 
                            being executed. 
                            Source: Hardware error. 
Overflow     Program        Caused by an arithmetic overflow, exponent 
             generated      overflow, or exponent underflow. 
                            Source: User program. 
Parity       Hardware       Caused by detection of a parity error. 
             generated      Source: Hardware error. 
Safe-store   Virtual        Occurs if the safe store stack is full 
             memory         or has less than two complete frames 
             generated      remaining. 
                            Source: Operating system error. 
Security 1   Virtual        Occurs if an attempt is made to modify 
             memory         or fetch instructions  or operands 
             generated      illegally. 
                            Source: User program error. 
Security 2   Virtual        Caused by an attempt to access a segment 
             memory         that the user is not allowed to access. 
             generated      Source:  User program error. 
Shutdown     Hardware       Occurs when an impending power failure 
             generated      is detected. 
                            Source: Hardware error. 
Startup      Hardware       Occurs when power restoration is 
             generated      detected. 
                            Source: Hardware error. 
Timer        Hardware       Occurs when the timer count set by the 
runout       generated      Scheduler reaches -1. 
                            Source: Hardware fault. 
For a list of FEP FEI coupler definitions, enter:  ? or ??.  To access 
individual definitions, type: 
HELP (STATS) FEI_COUPLER_DISPLAY definition 
where definition is HOST_INTERFACE 
  Statistic                     Description 
The following to host and from host front end interface statistics are 
provided for the coupler: 
Interrupts/minute             The number of interrupts registered per 
                              minute. 
% Interrupt service time      The percentage of time spent processing 
                              interrupts.  This value plus the 
                              percentage of scheduled (non-interrupt) 
                              CPU value provided in the VDH statistics 
                              (see VDH_DISPLAY) is the total 
                              percentage of execution and service time 
                              for the coupler (see FEP_MONITOR_DISPLAY). 
Circular buffer messages/min  The number of messages between the host 
                              and FEP going through the circular queue 
                              (CQ) per minute. 
Circular buffer bytes/min     The total number of bytes contained in the 
                              messages per minute. 
Dcw aborts/minute             The number of Data control word (Dcw) 
                              aborts occurring because the I/O list was 
                              interrupted. 
% Scheduled execution time    Execution time spent as a result of CPU 
                              processing from the CQ as opposed to 
                              interrupt processing.  The percent of FEP 
                              being used by the coupler is % Scheduled 
                              execution time minus the percent of 
                              interrupt level execution). 
Fep okay functions/minute     The number of times the host queries the 
                              FEP after the host comes back on-line. 
Output functions/minute       A count of data messages per minute coming 
                              from the host. 
Nop functions/minute          The number of times the CQ has wrapped. 
Time functions/minute         A count of time functions sent by the host 
                              to the FEP. 
00001
ASYNC_HANDLER_DISPLAY
BISYNC_HANDLER_DISPLAY
FEI_COUPLER_DISPLAY
HDLCX25_HANDLER_DISPLAY
COMMON_HANDLER_DISPLAY
HDLCX25_HANDLER_DISPLAY
For a list of FEP LCP-6 display definitions, enter:  ? or ??.  To access 
individual definitions, type: 
HELP (STATS) LCP6_MONITOR_DISPLAY definition 
where definition is any of the following: 
GENERAL, MEMORY_POOL, USER_CLASS, READ_WRITE_STATISTICS, BOBCAT_CONTEXT, 
FETCHES 
  Statistics                                
  Category            Statistics          Description 
General             % User exec         The percentage of LCP-6 time 
                                        spent in execution of user 
                                        code in the FEP for each type 
                                        of user:  time sharing (Ts), 
                                        comgroup (Cg), handler (Hn) 
                                        and ghost (Gh).  This 
                                        percentage is directly 
                                        chargeable to users in the form 
                                        of LCP-6 execution time. 
                    % User serv         Specifies the percentage of 
                                        LCP-6 time spent executing 
                                        monitor code to satisfy user 
                                        monitor service requests in 
                                        the FEP for each type of user 
                                        (Ts, Cg, Hn, and Gh).  This 
                                        percentage is directly 
                                        chargeable to users in the 
                                        form of LCP-6 service time. 
                    % Monitor           Specifies the percentage of 
                    execution time      LCP-6 time spent executing 
                                        monitor code for internal 
                                        monitor functions (e.g., 
                                        scheduling, interrupt 
                                        handling, etc.).  This 
                                        percentage of LCP-6 time is 
                                        the monitor overhead. 
                    % idle              The percentage of LCP-6 time 
                                        that was spent idle with 
                                        nothing to do. 
                    % Total Scheduled   The total LCP-6 executing and 
                    Time                idle time for all users. 
                                        (Always approximates 100.00.) 
Memory Pool         The unit of measurement for these statistics is the 
                    256-word page. 
                    IO pages in use     The total number of I/O pages 
                                        currently being used. 
                    Fragmented IO       Number of released I/O pages 
                    pages not in use    that could not be released 
                                        into non-I/O space. 
                    Fprg-Sfile pages    Total pages for front end 
                    total               programs and shared processors. 
                    Maximum pages       The total number of pages in the 
                    available to any    system minus those dedicated to 
                    user                use by the monitor and handlers. 
                    Current pages       The number of unused user 
                    available to any    pages.  This number is the 
                    user                difference between the number 
                                        of maximum pages available and 
                                        the number of pages used. 
User class          Statistics describe handler and LCP-6 monitor page 
                    use. 
                    Comgroup connected  For each user class used, the 
                      FPRG              total number within the class 
                    Ghost               and the maximum number of pages 
                    Handler             used within each class. 
                    Timesharing FPRG 
                    LCP-6 Monitor       The total number of pages 
                                        required by the LCP-6 monitor. 
                    TOTAL               Total number of physical pages 
                                        of memory in the FEP. 
Read-Write          These statistics measure the traffic between the 
Statistics By       host and FEP (HO), FEP programs and terminals (UC), 
Resource            programs that log on independently (LG) and the 
                    handlers and the node administrator (NA). 
Bobcat Context      These statistics measure currently used (Current) 
                    and most ever used (Peak) usage for the following 
                    Bobcat tables, maximum values for which are 
                    established as boot parameters via the NETCON SET 
                    command: 
                    Display Name   Description 
                    User           The number of User Table entries. 
                                   NETCON boot parameter:  MUIS. 
                    SSN            The number of entries in the 
                                   Application Protocol Engine SeSsioN 
                                   Table, which defines the context 
                                   blocks used for FPRG DCBs.  NETCON 
                                   boot parameter:  APESSN. 
                    LDCT           The number of Logical Device Control 
                                   Table entries, which defines the 
                                   number of end points terminating in 
                                   the FEP.  NETCON boot parameter: 
                                   LDCT. 
                    IOP            The number of Input/Output Parameter 
                                   Table entries, which define the I/O 
                                   blocks available in the FEP.  NETCON 
                                   boot parameter:  IOP. 
Fetches from host   These statistics report program initiation. 
Fetches from Sfile  "Fetches from host" reports the number of programs 
  Table             sent from the host.  "Fetches from Sfile Table" 
                    reports the number of shared programs initiated 
                    without having to read them from the host.  The sum 
                    of these two statistics is the total number of 
                    programs started since the FEP was booted. 
00005
00006
00001
00002
00004
00003
FEP_LCP6_MONITOR_DISPLAY
For a list of FEP summary definitions, enter:  ? or ??.  To access individual 
definitions, type: 
HELP (STATS) FEP_SUMMARY_DISPLAY definition 
where definition is any of the following: 
ASYNC, RBT, URP, 3270, HDLC, PERCENT_BUSY, MEMORY_PAGES 
  Statistics                    Description 
Async terminals               Total number of async terminals active on 
                              the FEP. 
Async bytes output/min        Total number of characters sent to the 
                              async terminals per minute. 
Async bytes input/min         Total number of characters sent from the 
                              async terminal per minute. 
RBT devices                   Total number of RBT terminals active on 
                              the FEP. 
RBT bytes output/min          Total number of characters sent to the RBT 
                              terminals per minute. 
RBT bytes input/min           Total number of characters sent from the 
                              RBT terminals per minute. 
urp devices                   Total number of unit record devices active 
                              on the FEP. 
urp bytes output/min          Total number of characters sent to the 
                              unit record devices per minute. 
3270 terminals                Total number of 3270 devices active on the 
                              FEP. 
3270 bytes output/min         Total number of characters sent to the 
                              3270 devices per minute. 
HDLC connections              Total number of active HDLC lines on the 
                              FEP. 
HDLC output bytes/min         Total number of characters sent to HDLC 
                              lines. 
HDLC input bytes/min          Total number of characters received over 
                              HDLC lines. 
% FEP busy                    (% Total Scheduled Time)-(% idle) 
                              (See FEP_MONITOR_DISPLAY.) 
Memory pages available        The number of pages of memory available 
                              in the FEP for general use.  This memory 
                              can be used to load SFILE tables, start 
                              an FPRG, connect a CG device, etc.  A 
                              value of zero means the FEP is out of 
                              memory.  In this case either the FEP 
                              configuration must be changed or memory 
                              must be added to the FEP. 
00004
00014
00015
00013
00001
00003
00001
00002
00016
00005
00004
00005
00006
00017
00007
00006
00002
00009
00007
00008
00003
00010
00011
00012
UNITREC_HANDLER_DISPLAY
VDH_DISPLAY
Format: 
FIL[E] fid 
Parameters: 
fid    specifies a standard CP-6 file identifier (which must specify a disk 
file). 
Description: 
The FILE command is used to specify the identity of the file into which STATS 
is to write any performance log entries specified by the LOG command.  If no 
file id is entered, the file :SNAPS, found in the current file management 
account, is assumed. 
00002
00001
Format: 
GLOM 
Description: 
The GLOM command reads the snapshot records corresponding to the start and end 
of the selected time span, and takes the difference between the accumulated 
counts in the two records.  The display produced includes performance data 
(PMDAT) and FEP data from the log file (it excludes MOUSE data).  The 
performance file used is that specified by the FILE command.  The time 
interval used is that specified by the TIME command; if no TIME command has 
been issued, the first and last snapshots in the file will be used.  The 
displays produced are those specified in the DISPLAY command. 
STATS cannot produce any displays for a time interval during which the system 
was restarted (via an automatic recovery or by a manual tape or disk boot 
sequence); if the user attempts to GLOM such an interval, STATS will reject 
the request and will inform the user of the time at which the system was 
restarted.  The user may then separately GLOM the intervals prior to and 
following the recovery. 
00001
Format: 
   [ONCE     ] 
GO [FOREVER  ] 
   [n[ TIMES]] 
Parameters: 
n    specifies a one-to-seven character integer. 
Description: 
The GO command is used to start the sequence of performance displays and/or 
log-file writes specified by the DISPLAY, LOG, FILE, and INTERVAL commands. 
When told to GO, STATS will do the following: 
1.  Fetch an initial copy of the necessary performance monitoring data; 
2.  Write the initial data to the performance log file if the corresponding 
    LOG flag is set; 
3.  Sleep for the number of minutes indicated by the INTERVAL command; 
4.  Fetch a new copy of the performance data; 
5.  Write the new data to the log file if the LOG flag is set; 
6.  Produce whatever displays were specified by the DISPLAY command; 
7.  Repeat steps 3-6 until the specified number of displays has been produced. 
00002
00001
BARGRAPH
For a list of FEP HDLCX25 handler definitions, enter:  ? or ??.  To access 
individual definitions, type: 
HELP (STATS) HDLCX25_HANDLER_DISPLAY definition 
where definition is any of the following: 
HDLC, X29, X25 
  Type of        Statistics                   
  Statistics     Category                   Description 
HDLC           Lines                      A count of the number of 
                                          active HDLC lines serviced by 
                                          the handler. 
               FEP-to-line and Line-to-FEP statistics are provided for: 
               Interrupts/minute          The number of interrupts 
                                          registered per minute. 
               % Interrupt level          The percentage of time spent 
               execution                  processing interrupts.  This 
                                          value plus the percentage of 
                                          scheduled (non-interrupt) CPU 
                                          value provided in the VDH 
                                          statistics (see VDH_DISPLAY) 
                                          is the total percentage of 
                                          execution and service time for 
                                          this handler (see 
                                     FEP_MONITOR_DISPLAY). 
               Frames/minute              The total number of frames per 
                                          minute. 
               Frame bytes/minute         The total number of bytes in 
                                          the frames. 
               Bytes/frame                The average frame size: 
                                          (frames/minute)/ 
                                          (frame bytes/minute). 
               Frame level rejects/       The count is incremented each 
               minute                     time an out-of-sequence frame 
                                          is sent. 
               In addition, the following statistics are included: 
               Frame level timeouts/      The count is incremented if a 
               minute                     frame was not acknowledged 
                                          within the allowed period of 
                                          time (set via the SUPER LINK 
                                          profile option TIMEOUT) and/or 
                                          if there is no activity on the 
                                          link for the link assurance 
                                          period (TIMEOUT + 1). 
               Frame level resets         The number of times the 
                                          connect sequence is 
                                          re-initiated. 
               Frame connects/minute      The number of times the other 
                                          end recovers from a 
                                          disconnect. 
               Frame disconnects/minute   The number of times 
                                          communication terminates 
                                          because the other end is not 
                                          answering. 
X.29           Buffer utilization, bytes  The number of bytes currently 
                                          being used for X29 data 
                                          transfers. 
               Context utilization,       The number of bytes currently 
               bytes                      being used in handler memory 
                                          for X29 contexts. 
               Small output buffer,       The number of buffer requests 
               Large output buffer,       per minute. 
                 gets/min 
               Small output buffers,      The number of times the buffer 
               Large output buffers,      was filled with data from the 
                 full/min                 CQ before the device was ready 
                                          to accept it. 
               Line speeds                The distribution of X29 
                                          connections by line speed. 
               X.29 circuits              The total number of X29 
                                          circuits. 
                    NOTE:  X29 line speed distribution is not currently 
                           accurate.  However, the total number of X29 
                           circuits reported is reliable. 
X.25           Circuits                   The number of circuits on the 
                                          X.25 line. 
               FEP-to-line and Line-to-FEP statistics are provided for: 
               Packets/minute             A count of all packets:  data 
                                          and control. 
               Bytes/minute               The total number of bytes 
                                          transmitted per minute. 
               Bytes/packet               The average packet size: 
                                          (packets/minute)/ 
                                          (bytes/minute). 
               Call packets/minute        The number of call (only) 
                                          packets per minute. 
               Clear packets/minute       The number of clear (only) 
                                          packets per minute. 
               Data packets/minute        The number of data (only) 
                                          packets per minute. 
               Data bytes/minute          The number of bytes 
                                          transmitted in data packets 
                                          per minute. 
               Data bytes/packet          The average data packet size: 
                                          (data packets/minute)/ 
                                          (data bytes/packet) 
               Non-continued packets/min  The number of non-continued 
                                          packets. 
               Flow packets/minute        The number of flow control (RR 
                                          and RNR) packets. 
               Packet level restarts/     The number of times restart 
               minute                     handshakes are performed 
                                          before initiating any other 
                                          activity. 
               Other statistics provided include: 
               Packet level resets/minute The number of times virtual 
                                          circuits are re-initialized. 
               Packet window full/minute  The number of times data 
                                          output is blocked because the 
                                          packet window is full. 
               Packet blocked by frame/   The number of times packet 
               minute                     data output is blocked because 
                                          the frame level is not 
                                          servicing the request. 
               I/O buffer gets/minute     The number of times I/O buffer 
                                          requests are satisfied by the 
                                          HDLCX25 internal I/O buffer 
                                          manager. 
               I/O buddy space gets/      The number of times the 
               minute                     HDLCX25 internal I/O buffer 
                                          manager cannot satisfy the 
                                          request and passes it on to 
                                          the Buddy space manager. 
00001
00003
00002
Format: 
HELP [(processor)] [TOPICS] [keyword1] [-] [keyword2] 
Note:  The elements 
    [(processor)] 
    [TOPICS] 
    [keyword1] [-] [keyword2] 
can be entered in any sequence. 
Parameters: 
For IBEX HELP, type:  !HELP HELP PARAMETERS 
Description: 
For IBEX HELP, type:  !HELP HELP DESCRIPTION 
Examples: 
For IBEX HELP, type:  !HELP HELP EXAMPLES 
00002
00003
00001
A 
  ANALYZE Command - 
      HELP ANALYZE 
B 
  BARGRAPH Command - 
      HELP BARGRAPH 
D 
  DIRECTORY Command - 
      HELP DIRECTORY 
  DISPLAY Command - 
      HELP DISPLAY 
  DISPLAY Command (STATS) - 
      HELP DISPLAY FORMAT: 
  DO Command - 
      HELP DO 
E 
  END Command - 
      HELP END 
  ENTER Command - 
      HELP ENTER 
  ERASE Command - 
      HELP ERASE 
F 
  FILE Command - 
      HELP FILE 
  File Created by STATS - 
      HELP RELATED_FILES 
G 
  GLOM Command - 
      HELP GLOM 
  GO Command - 
      HELP GO 
H 
  HELP Command - 
      HELP HELP 
  HISTOGRAM Command - 
      HELP HISTOGRAM 
I 
  INTERVAL Command - 
      HELP INTERVAL 
  Invoking STATS - 
      HELP INVOKING_STATS 
L 
  LOG Command - 
      HELP LOG 
M 
  MESSAGE Command - 
      HELP MESSAGE 
  Monitor Usage Evaluator (MOUSE) - 
      HELP PRIVILEGES 
O 
  OUTPUT Command - 
      HELP OUTPUT 
P 
  PLOT|SCATTERGRAM Command - 
      HELP PLOT 
  PRINT Command - 
      HELP PRINT 
  Privileges for Use of STATS - 
      HELP PRIVILEGES 
R 
  REPLAY Command - 
      HELP REPLAY 
  RESET Command - 
      HELP RESET 
  RESET Command (STATS) - 
      HELP RESET FORMAT: 
S 
  SELECT Command - 
      HELP SELECT 
  SELECT Command (STATS) - 
      HELP SELECT FORMAT: 
  :SNAPS file - 
      HELP RELATED_FILES 
  SNAPSHOT Command - 
      HELP SNAPSHOT 
  START|INITIATE Command - 
      HELP START 
  STATISTICS Command - 
      HELP STATISTICS 
  STATS Command Summary - 
      HELP COMMAND_SUMMARY 
  STATS Expressions - 
      HELP STATS_EXPRESSIONS 
  STATUS Command - 
      HELP STATUS 
  STATUS Command (STATS) - 
      HELP STATUS FORMAT: 
  STOP|TERMINATE Command - 
      HELP STOP 
  SUMMARIZE Command - 
      HELP SUMMARIZE 
T 
  TIME|DATE|SPAN Command - 
      HELP TIME 
00001
00002
00003
00004
00005
00006
00007
00008
00009
00010
00011
00012
00013
00014
HELP_INDEX
Format: 
            {ALL                                       } 
HIS[TOGRAM] {histitem[(mode)] [, histitem[(mode)]] ... } 
            {histitem[/mode] [, histitem[/mode]] ...   } 
Parameters: 
ALL    specifies a listing of all histograms. 
histitem    is any of the options that can be displayed by typing ?? or by 
typing:  HELP (STATS) HISTOGRAM option.  Valid options are RESPONSE, 
USER_SIZE, INTERACTION, PMME_TIME. 
mode    indicates whether the user wishes to see data that applies to the 
entire time that the system has been up (since the last re-boot), or data that 
applies only to the most recent STATS monitoring interval, or both. 
Acceptable modes are A[LL], S[NAP], and B[OTH].  The default is BOTH. 
Description: 
The HISTOGRAM command is used to specify the identity of those histograms to 
be displayed during SNAP and GO processing.  When the HISTOGRAM command is 
issued, the HISTOGRAM display flag is turned on and all other display flags 
are turned off.  The DISPLAY command may be used to turn other display flags 
on, if desired. 
HELP (STATS) HISTOGRAM option 
where option may be any of the following:  INTERACTION, PMME_TIME, RESPONSE, 
USER_SIZE.  These options are displayed under these headings: 
  Option         Description 
  INT[ERACTI[ON|VE]][COM[PUTE]][TIME] 
                 Graphs the amount (in milliseconds) of compute time (user 
                 execution and service) used during each user interaction. 
  PMM[E][TIME] 
                 Graphs the amount of time (in microseconds) required to 
                 complete user service requests (PMMEs).  This data is 
                 available only when the MOUSE monitoring function is active. 
  RES[PONSE] 
                 Graphs the time (in milliseconds) required for interactive 
                 users to receive CPU service after hitting the RETURN key. 
  [USER][MEM[ORY]] SIZE 
                 Graphs the memory size (in 1024-word pages) of users of the 
                 CP-6 system. 
00002
00003
00003
00001
00004
00004
00005
00006
00006
00006
START
Format: 
INT[ERVAL][hours:]minutes 
Description: 
The INTERVAL command is used to specify the number of minutes between 
performance displays and/or performance log file entries.  An interval of zero 
minutes is meaningless and will cause the default interval of five minutes to 
be used. 
00001
    STATS can be run as a batch, ghost, or on-line job.  (Typically, it is run 
    as a ghost job to collect statistics for later analysis.)  It is invoked 
    by the command !STATS.  The DCBs used by STATS are: 
    o   M$SI for input 
    o   M$LO for display output 
    o   M$DO for diagnostic output 
    When run as an on-line job, STATS solicits commands with the # character. 
    Commands can be written on multiple lines, using the semicolon to indicate 
    line continuation. 
    The format for the !STATS command is: 
                 [{INTO}     ] 
    STATS [fid1] [{ON  } fid2] 
                 [{OVER}     ] 
fid1    specifies a standard CP-6 file identifier which must specify a command 
file. 
fid2    specifies a standard CP-6 file identifier which identifies the 
destination for STATS display output. 
Upon completion, STATS sets the STEP Condition Code (STEPCC) based on the 
condition encountered during STATS execution, as follows: 
    STEPCC     Condition 
    ------     --------- 
       0       No errors 
       1       Warning (e.g., command/syntax) errors 
       2       Serious (e.g., file busy) errors 
       3       Fatal errors (STATS does a M$ERR) 
The I/O cache granule types are:    CONSEC, DATA, ELSE, FD, FIT, GP, INDEX, 
MAD, PAD, REL and UL. 
  Granule Types     Description 
CONSEC            Consecutive files, which contain data records (only). 
DATA              Data granules, which contain keyed file data. 
ELSE              All other granules (including symbiont files and 
                  unit record files). 
FD                File Directories, each of which contains a list of 
                  all files in an account. 
FIT               File Information Table, containing access controls 
                  and other file specific information for all files. 
GP                Granule Pool, a list of free granules on the packset. 
INDEX             Index granules, which contain the record keys for 
                  keyed files. 
MAD               Master Account Directory, a global list of all 
                  accounts on the system. 
PAD               Packset Account Directories, each of which contains 
                  a list of all accounts in the packset. 
REL               Relative files, which contain fixed length data 
                  records (only). 
UL                Upper level index, which contains pointers to 
                  index granules. 
FEP_LCP6_MONITOR_DISPLAY
Format: 
Form 1: 
LOG logoption[, logoption] ... 
Form 2: 
{ALS[O]} LOG logoption[, logoption] ... 
{ADD   } 
Form 3: 
{DON[T]} LOG logoption[, logoption] ... 
{DRO[P]} 
Parameters: 
logoption    is any of the log options available by typing ?? or by typing: 
HELP (STATS) LOG logoption 
where logoptions are ALL, FEP, MOUSE, NONE, PMDAT.  The options are displayed 
under the following headings: 
  Option         Description 
  {ALL|ANY[THING]|EVE[RYTHING]} 
                 All LOG options. 
  FEP[n] 
                 Data gathered by the specified FEPs will be written to the 
                 log file if this option is specified.  If n is omitted, data 
                 gathered by all FEPs will be written to the log file. 
  MOU[SE] 
                 Data produced by the Monitor Usage Evaluator (MOUSE) will be 
                 written to the log file if this flag is set and if MOUSE has 
                 been activated by a START MOUSE command. 
  {NONE|NOT[HING]} 
                 No LOG options. 
  PM[DAT] 
                 All standard performance monitoring data will be written to 
                 the log file if this option is specified.  For details, see 
                 the PMDAT option of the DISPLAY command. 
Description: 
The LOG command sets flags indicating what performance monitoring data are to 
be written to the performance log file by SNAP and GO processing.  The LOG 
form of the command, Form 1, clears all previous flags and sets those 
indicated by the log options specified.  Form 2, the ALSO LOG form, sets the 
indicated flags without clearing those set by previous LOG commands.  Form 3, 
DONT LOG, resets the indicated flags without affecting any flags previously 
set. 
00002
00002
00007
00002
00003
00004
00005
00005
00001
00006
Format: 
M[ESSAGE] messagetext 
Parameters: 
messagetext    is the text to be sent. 
Description: 
The MESSAGE command is used to send a message to the central system console. 
It is provided primarily for use when STATS is being run as a system ghost 
job, to inform the operator that STATS has been successfully initiated. 
Usage Notes: 
The MESSAGE command may not be continued, but as many MESSAGE commands as 
necessary may be used.  Command commentary (characters contained in 
double-quotes) will be included in the message sent to the operator if it is 
present in the message text. 
00002
00001
00003
    The MOUSE (MOnitor USage Evaluator) feature provides a means of 
    determining the performance and efficiency of the various monitor services 
    (PMMEs) available to user programs and special system processors.  When 
    activated, the MOUSE routines intercept each service request at the 
    beginning and end of its execution, and maintain a table of data 
    concerning the number of uses of each type of service, and the amount of 
    CPU time and number of physical I/Os issued by each service.  Type HELP 
    (STATS) START for more information. 
Format: 
         [[OVER] LP[@location]] 
OUT[PUT] [[INTO] fid          ] [(option[,option]...[)]] 
         [[ON  ] ME           ] 
         [[TO  ]              ] 
Parameters: 
fid    any valid CP-6 file identifier. 
ON or TO    indicates to only honor the OUTPUT command if the file does not 
already exist. 
OVER    indicates to honor the OUTPUT command whether or not the file exists. 
INTO    indicates to merge the result of the OUTPUT command into the file if 
it exists, or to create a new one if it does not. 
LP    directs output to the default line printer; @location specifies a 
specific line printer. 
ME    returns the output destination to the user's terminal. 
option    is one of the following: 
    F[ORM]={formname|'formname'}    Applies to unit record files and unit 
    record devices and specifies the name of a form to be mounted on a unit 
    record device. formname is a 1-6 character string, which can be quoted. 
    The name must have been defined to the system by the system manager (via 
    the Form Definition File). The default is blank, which means the default 
    form for a unit record device and form 'STDLP' for unit record files. 
    I[XTNSIZE]=value    Specifies an initial disk storage allocation (in 
    blocks) for the output file.  value must be in the range of 1 through 
    134217727.  The default is 2. 
    O[RGANIZATION={C[ONSECUTIVE]|U[NIT]R[ECORD]}    Specifies the organization 
    of the output file as either CONSECUTIVE or UNIT RECORD.  If this option 
    is not specified, the output file is created as a UR file. 
    X[TNSIZE]=value    Use of this option causes an automatic M$EXTEND when 
    needed. value specifies a secondary disk storage allocation (in blocks) 
    for the output file, and must be in the range 1 through 32000.  The 
    default is 2. 
Description: 
The OUTPUT command is used to direct all processor output to a destination. 
OUTPUT with no options redirects output to the original output destination. 
Output can be directed to any valid file name (fid).  If none of ON, TO, OVER, 
or INTO is specified, ON will be assumed. 
00002
00001
Format: 
                             {AGAINST} 
{PLO[T]       } Y-exp[scale] {VERSUS } X-exp[scale] 
SCA[TTERGRAM]}               {VS     } 
                    {AGAINST} 
    [, Y-exp[scale] {VERSUS } X-exp[scale]] ... 
                    {VS     } 
Parameters: 
Y-exp    is a combination, appropriate to the Y axis, of constants, STATS 
items, parentheses and operators which produces an arithmetic result.  For 
STATS items, type HELP (STATS) STATS_ITEMS.  For rules governing STAT 
expressions, type HELP (STATS) STATS_EXPRESSIONS. 
X-exp    is the same as Y-exp except applies to the X axis. 
scale    is [{LOG|LINEAR}[, n-m]|[n-m]] where LOG|LINEAR and n-m are the same 
as in the ANALYZE command. 
Description: 
The PLOT (or SCATTERGRAM) command is used to generate one or more two-variable 
scattergram plots based on data derived from snapshot intervals in a STATS 
performance log file.  Intervals are selected from the file based on the 
criteria specified by the TIME and SELECT commands (if such are used), the 
expressions specified by the user are evaluated, and the points indicated by 
the expressions' values are recorded in an internal table.  The plots are 
actually printed when the end of the file is encountered; each PLOT command 
requires only one pass through the file and can produce up to ten plots. 
00002
00001
Format: 
PRINT [ALL|ldevlist] 
Parameters: 
ALL    specifies that the accumulated output for all logical devices is to be 
sent to destination(s) immediately.  This is the default. 
ldevlist    specifies that the accumulated output for the specified logical 
device or devices is to be sent to destination(s) immediately.  The list is 
entered in the format 
ldevname[,ldevname]... 
ldevname is a logical device name established through the LDEV command. 
Description: 
PRINT directs that output accumulated for logical devices be sent to 
destination(s) immediately. 
Examples: 
#PRINT LP01,LP02 
The above example causes the accumulated output associated with logical 
devices LP01 and LP02 to be sent immediately to the associated destinations. 
00002
00003
00001
    No special privilege is required for accessing the :SNAPS file; if a user 
    has appropriate file access to the account, the user can access the 
    contents of the :SNAPS file.  To retrieve data from the running system 
    (either host or FEP), the PM privilege is required.  To start or stop the 
    Monitor Usage Evaluator (MOUSE), the EXPM privilege is required. 
For a list of PROCESSOR display definitions, enter: ??. 
  Heading     Definition 
  Processor name 
              The processor name is taken from the name of the run unit.  The 
              account is not reported as part of the processor name.  If run 
              units with the same name are run from separate accounts, there 
              will be multiple entries with the same processor name. 
  Type 
              Specifies the type of the processor.  The type is one of the 
              following: 
              icp    Interactive command program.  This program executes in 
              the command processor domain. 
              idb    Interactive debugger.  This processor executes in the 
              debugger domain. 
              std    standard run unit.  This processor executes in the user 
              domain. 
  Users 
              Specifies the number of users of the processor.  For the GO or 
              REPLAY commands, this is the number of users of the processor 
              during the interval.  For the GLOM command, this is the average 
              number of users of the processor during the interval. 
  % exec 
              Specifies the percentage of CPU time spent in execution in the 
              processor for all users of the processor.  For the snap column, 
              this is the percentage of CPU execution time used by this 
              processor during the interval.  For the all column, this is the 
              average percentage of CPU execution time used by this processor 
              since the last system boot or recovery. 
  % serv 
              Specifies the percentage of CPU time spent in processing monitor 
              service requests for this processor for all users of the 
              processor.  For the snap column, this is the percentage of CPU 
              service time used by this processor during the interval.  For 
              the all column, this is the average percentage of CPU service 
              time used by this processor since the last system boot or 
              recovery. 
00004
00001
00005
00002
00003
END
RESET
    The STATS processor reads and writes files in a format internal to the 
    processor, and puts them in :SNAPS (unless the user renames the file). 
    Displays can be directed to files by the user in the invoking !STATS 
    command. 
Format: 
REP[LAY] 
Description: 
The REPLAY command is used to produce a sequence of sets of displays derived 
from the standard performance data (PMDAT), MOUSE data, or FEP performance 
data in the log file.  The performance file used is that specified in the FILE 
command.  The time interval used is that specified in the TIME or DATE 
command.  Any time-interval selection criteria that has been input via the 
SELECT command will be observed.  The displays produced are those specified in 
the DISPLAY command. 
00001
Format: 
R[ESET] [param[,param] ... ] 
Parameters: 
param    is any of the options that can be displayed by typing ?? or by 
typing: 
HELP (STATS) RESET option 
where option can be any of the following: 
DATE, DISPLAY, FILE, INTERVAL, LOG, SELECTION, SPAN, TIME.  These options are 
displayed under the headings: 
  Option     Description 
  DI[SPLAY] 
             Sets the DISPLAY flags back to DISPLAY CPU. 
  FIL[E] 
             Sets the FILE fid back to :SNAPS. 
  INT[ERVAL] 
             Sets the INTERVAL value back to five minutes. 
  LOG 
             Sets the LOG flags back to LOG NOTHING. 
  SEL[ECTION] 
             Sets the interval selection criteria back to SELECT ALL. 
  {TIM[E]|DAT[E]|SPA[N]} 
             Sets the TIME limits to include the entire performance log file. 
Description: 
The RESET command is used to reset any of certain STATS parameters to their 
default values.  If no options are specified, all of the above items are 
reset. 
00007
00008
00002
00003
00004
00005
00001
00006
00007
00007
For a list of RESOURCE memory display definitions, enter: ??. 
  Item      Definition 
  AARDVARK and RECOVERY 
            Pages required for the boot processor (AARDVARK) and the automatic 
            recovery processor (RECOVERY). 
  XDELTA and monitor debug schema 
            Pages required for the monitor debugger (XDELTA) and the debug 
            schema used to debug the monitor.  The size of the debug schema 
            area may change by specifying different values to the FUNCTIONAL 
            CODE GROUPS question at boot time. 
  Monitor procedure and static data 
            Pages required for the monitor executable procedure (i.e., 
            PROC: ...)  and static data (i.e., DCL ... STATIC). 
  Monitor context (JITs, HJITs, PPUT, page tables) 
            Pages required for the monitor context area, which includes the 
            monitor Job Information Table (JIT), Housekeeping JIT (HJIT), 
            physical page use table (PPUT), and page tables (PT). 
  Monitor dynamic data segments 
            Pages required for monitor dynamic segments, which includes CFUs, 
            LDCTs, ASAVE and ENQ. 
  TIGR-built tables 
            Pages required for tables built by TIGR at boot time.  This 
            includes the user table, I/O cache, device tables and autoshare 
            tables. 
  Communications WSQs 
            Pages used in communication with FEPs.  These pages are controlled 
            by the INQSZ and OUTQSZ parameters on the TIGR processor FEP 
            command. 
  Comgroup queue 
            An area for comgroup context.  The size of this area is controlled 
            by the CGCXTSZ and CGMAP parameters on the TIGR processor MON 
            command. 
  Total pages held back for monitor use 
            Pages reserved for CFUs, LDCTs, ASAVE, ENQ and stealable pages. 
            These pages are affected by the CFU, DEVMAX, ENQ, and STEALPGS 
            options on the TIGR processor MON command. 
  Resident system ghosts 
            Pages required for resident system ghosts.  These are ghost users 
            that perform part of the operating system's functions such as ELF, 
            PIG, SLUG, INSYM, and CUTSYM (and are referred to as the MING 
            ghosts). 
  Required processors (IBEX, DELTA, LOGON) 
            Pages required for the IBEX, DELTA, and LOGON processors.  These 
            processors must be present for the system to function. 
  All other special shared (resident) processors 
            Pages required for all processors, shared libraries, alternate 
            shared libraries, and debuggers.  These items are specified on the 
            SPROC options on the TIGR processor MON command. 
  Total dedicated memory 
            Total pages required by the monitor, its tables, ghosts, and 
            processors. 
  Available to users 
            Pages available to users.  This number is the difference between 
            the total pages in the system and the total dedicated memory. 
  Currently allocated to users 
            Pages that are currently actually allocated to users.  These pages 
            cannot be shared.  These pages plus the automatically shared run 
            unit pages in use, plus the shared data segments in use constitute 
            all user memory. 
  Automatically shared run units in use 
            Pages of procedure of automatically shared run units that are 
            currently being used by one or more users. 
  Shared data segments in use 
            Pages of shared data segments currently being used by one or more 
            users. 
  Free pages 
            Pages in the system not currently used for any purpose. 
  Automatically shared run units not in use 
            Pages of the procedure of automatically shared run units that are 
            not being used by any user.  The pages are candidates to be used 
            for other purposes if the free pages are exhausted. 
  I/O cache pages (Use Count=0) 
            I/O cache pages not currently being used. 
  Total pages currently available 
            Pages on the system that are currently available for use.  This 
            number is the sum of the free pages and pages for the 
            automatically shared run units not in use. 
  Suspected bad physical pages 
            Pages that have been marked as suspect by TOLTS. 
  Physical pages being tested 
            Pages that are currently being tested by TOLTS. 
  Confirmed bad physical pages 
            Pages that have been partitioned by SYSCON. 
  I/O cache pages 
            Total I/O cache pages, both used and unused. 
  Number of pages not accounted for 
            Pages that cannot be currently accounted for.  Because of the 
            dynamic page usage of CP-6, pages are constantly being assigned to 
            new functions or usages.  This number reflects the number of pages 
            that are currently in a status that STATS is unaware of. 
  Total physical pages in system 
            Total pages in the system.  This is the system memory size as 
            found by AARDVARK at the last system boot or recovery. 
00001
00012
00014
00008
00007
00024
00015
00013
00018
00020
00025
00004
00005
00003
00021
00009
00027
00026
00023
00011
00010
00019
00016
00017
00022
00006
00002
PLOT
Format: 
SELECT {ALL       } 
       {expression} 
Parameters: 
ALL    clears any previously specified selection criteria, so that all 
snapshot intervals in the file (within the range specified by the TIME 
command, if such was used) will be selected. 
expression    is a combination of constants, STATS items, parentheses and 
operators, which produces an arithmetic result.  For STATS items, type HELP 
(STATS) STATS_ITEMS.  For rules governing STAT expressions, type HELP (STATS) 
STATS_EXPRESSIONS. 
Description: 
The SELECT command may be used to specify certain criteria which snapshot 
intervals must meet to be included in the output of a REPLAY, STATISTICS, 
ANALYZE, GRAPH, or PLOT command. 
00002
00001
Format: 
SNA[PSHOT] 
Description: 
The SNAPSHOT command is used to produce, on a one-time basis, the displays and 
log writes specified by the previously-entered DISPLAY, LOG, and FILE 
commands.  The set of performance data (snapshot) obtained portrays the state 
of the system at a specific time point and its history from start-up to that 
point. 
00001
TIME
STATUS
Format: 
{STA[RT]   } MOUSE [FOR [SYSID] nnnnn] 
{INI[TIATE]} 
Parameters: 
FOR SYSID nnnnn    specifies that MOUSE record monitor usages only for the 
specified user. 
nnnnn    is a sysid for a user. 
Description: 
The START command is used to activate the MOnitor USage Evaluator (MOUSE). 
The MOUSE feature provides a means of determining the performance and 
efficiency of the various monitor services ("PMMEs") available to user 
programs and special system processors.  When activated, the MOUSE routines 
intercept each service request at the beginning and end of its execution, and 
maintain a table of data concerning the number of uses of each type of 
service, and the amount of CPU time and number of physical I/Os issued by each 
service. 
Usage Notes: 
1.  Use of this command requires that the user have extended performance 
    monitoring authorization. 
2.  The use of the MOUSE feature will cause an increase in the amount of CPU 
    time required to complete each monitor service request.  Depending on the 
    kinds of service requests issued, this can cause a decrease in service 
    throughput ranging anywhere from 5% to 40%, with an average decrease of 
    about 15%. 
3.  The ANLZ command SPY may be used to obtain sysid information.  Sysid 
    information is also displayed when an on-line user logs on and when a job 
    is batched on a terminal (if batched by an on-line user) or on the 
    operator's console (if batched from cards). 
00002
00001
00003
Format: 
STATI[STICS] {exp[, exp] ... } 
             {ALL            } 
Parameters: 
exp    is a combination of constants, STATS items, parentheses and operators, 
which produces an arithmetic result.  For STATS items, type HELP (STATS) 
STATS_ITEMS.  For rules governing STAT expressions, type HELP (STATS) 
STATS_EXPRESSIONS. 
ALL    elicits compilation and output of the statistics on each of the STATS 
items. 
Description: 
The STATISTICS command is used to compile and output certain elementary 
numerical statistics concerning data contained in a STATS performance log 
file.  Intervals are selected from the file based on the criteria specified by 
the TIME and SELECT commands (if such are used), and data is extracted from 
the intervals to generate statistics for up to twenty different variables or 
expressions.  Statistics available include maximum and minimum values, mean 
and standard deviation. 
00002
00001
A STATS expression is a combination of constants, STATS items, parentheses, 
and operators, which produces an arithmetic result.  The following rules apply 
to expressions: 
1.  All expressions must include at least one item from the STATS_ITEMS list 
    (i.e., expressions composed solely of constants are not permitted). 
2.  Operators are:  +, -, *, /, <, =, >, <=, <> (or ~=), >=, AND (or &), OR 
    (or |), and NOT (or ~). 
3.  Comparison operators (<, =, etc.) return a 1 if the comparison is true, 
    and a 0 if the comparison is false. 
4.  Logical operators (AND, OR, and NOT) treat zero values as FALSE and 
    non-zero values as TRUE.  They return zero for false and one for true. 
5.  Due to the parsing technique used (recursive descent), all operators have 
    the same precedence and are executed right to left unless a different 
    order of operation is specified via parentheses (as in APL). 
6.  Division by zero is handled specially.  A non-zero value divided by zero 
    will produce a very large number of the same sign as the original number. 
    Zero divided by zero will produce zero. 
The maximum complexity of an expression is limited by the size of the 
reverse-Polish notation stack used to represent it internally.  Some 
expressions (in the PLOT command, for example) are limited to roughly 15 
active elements (items, constants, and operators); others (in the SELECT 
command) are limited to 30 elements.  Parentheses are not considered active 
elements and do not take up stack space; therefore, when in doubt, use 
parentheses. 
A list of STATS items and their definitions can be accessed by typing a ? or 
??.  To obtain definitions of individual STATS items, type 
HELP (STATS) STATS_ITEMS item 
where item may be any of the following: 
BATCH, CPUS, DISK, EVENTS, ETMF, EXECUTION, GHOST, IDLE, INTERACTIONS, 
IO_AND_RESOURCE, IO_LOAD, IO_WAIT, MEMORY, MISC, MONITOR, ONLINE, PMMES, 
RESPONSE, RESOURCE, SCHEDULES, SERVICE, TAPE, TOTAL_IOS, TP, USERS. 
  Item Name      Description 
  {[90%] RESP[ONSE]|RT90} 
                 90% response time (in milliseconds) measured from receipt of 
                 input by host to startup of requested function. 
  [%] EXE[CUTION] 
                 Percent of time spent executing users' code. 
  [%] IDL[E] 
                 Percent of time spent idle with nothing happening. 
  [%] I/O {&|AND} RES[OURCE] [WAIT] 
                 Percent of time spent idle both with I/O in progress and with 
                 users awaiting necessary resources. 
  [%] I/O [WAIT] 
                 Percent of time spent idle with I/O in progress. 
  [%] MON[ITOR] 
                 Percent of time spent performing non-user tasks. 
  [%] RES[OURCE] [WAIT] 
                 Percent of time spent idle with users waiting for necessary 
                 resource. 
  [%] SER[VICE] 
                 Percent of time spent servicing users' monitor service calls 
                 (PMMEs). 
  BAT[CH] [USER] 
                 Number of batch users in system. 
  CPU[S] 
                 Number of CPUs currently running. 
  DISK [I/OS] 
                 Number of disk I/Os per minute. 
  ETMF 
                 Execution time multiplication factor. 
  EVE[NTS] 
                 Number of scheduler events occurring per minute. 
  GHO[ST] [USERS] 
                 Number of ghost users in system. 
  {INT[ERACTIONS]|INT[S]} 
                 Number of terminal interactions per minute. 
  [IO|I/O] LOAD 
                 Disk I/O load factor. 
  MEM[ORY] 
                 Number of pages of memory currently available. 
  {MISC|OTHER} [I/OS] 
                 Number of miscellaneous (unit record) I/Os per minute. 
  ONL[INE] [USERS] 
                 Number of interactive users in system. 
  PMM[ES] 
                 Number of monitor service calls (PMMEs) issued per minute. 
  {SCHED[ULES]|SCHED[S]} 
                 Number of passes through the system scheduler per minute. 
  TAPE [I/OS] 
                 Number of tape I/Os per minute. 
  [TOTAL] {IO[S]|I/O[S]} 
                 Total number of I/Os per minute. 
  TP [USERS] 
                 Number of transaction processing users in system. 
  USER[S] 
                 Total number of users in system. 
00009
00010
00011
00012
00013
00002
00014
00003
00015
00015
00023
00004
00016
00005
00017
00018
00006
00019
00018
00020
00007
00001
00021
00021
00008
00022
00023
00024
00025
Format: 
ST[ATUS] 
Description: 
The STATUS command produces a display of the current values of several of the 
parameters that the STATS user may set to control STATS' functioning. 
Displays of the following are produced: 
o   The DISPLAY flags, as set by the DISPLAY command 
o   The LOG flags, as set by the LOG command 
o   The interval length, as set by the INTERVAL command 
o   The file identification of the log file, as set by the FILE command 
o   The playback time span, as set by the TIME command 
o   The selection criteria, as set by the SELECT command 
00001
Format: 
{STO[P]     } MOUSE 
{TER[MINATE]} 
Description: 
The STOP command deactivates the monitor usage evaluator. 
Usage Notes: 
Use of this command requires that the user have extended performance monitor 
authorization. 
00001
00002
Format: 
SUM[MARIZE] item[, item] ... 
Parameters: 
item is a STATS item that can be displayed by typing HELP (STATS) STATS_ITEMS. 
From 1 to 20 items may be specified. 
Description: 
The SUMMARIZE command is used to select the data items to be displayed by 
STATS when the one-line SUMMARY display has been selected. 
00002
00001
FEP_SUMMARY_DISPLAY
STOP
Format: 
{DAT[E]} 
{TIM[E]} [[mm/dd/yy] [, hh:min] [-[mm/dd/yy] [, hh:min]]] 
{SPA[N]} [ALL                                           ] 
Parameters: 
hr, min, mm, dd and yy    are all decimal values with a maximum length of two 
digits specifying hours, minutes, months, days and years, respectively.  If 
the date portion is omitted, the current day is assumed; if the time portion 
is omitted, the value "00:00" will be assumed for the starting time and 
"23:59" will be assumed for the ending time. 
ALL    specifies the complete performance log file. 
Description: 
The TIME|DATE|SPAN command may be used to specify the beginning and ending 
limits of the portion of a performance log file that is to be played back via 
the REPLAY, STATISTICS, ANALYZE, GRAPH, GLOM and PLOT commands. 
Usage Notes: 
1.  From one to four of the above options may be entered. 
2.  Dates and times are interchangeable (for example, the beginning of the 
    range could be entered hh:min, mm/dd/yy). 
3.  The end of the range may be entered before the beginning of the range by 
    preceding the end with the necessary dash (-). 
4.  Altering the starting time does not affect the ending time; the reverse is 
    also true.  Specifying a date for the starting time does not cause that 
    date to be assumed if the ending time does not specify a date; the reverse 
    is also true. 
00002
00001
00003
For a list of FEP UNITREC handler definitions, enter:  ? or ??.  To access 
individual definitions, type: 
HELP (STATS) UNITREC_HANDLER_DISPLAY definition 
where definition is any of the following: 
HANDLER_TO_LINE, STATISTICS 
  Statistics                   
  Category                   Description 
Handler-to-line and line-to-handler statistics are provided for: 
Interrupts/minute          The number of interrupts registered per 
                           minute. 
% interrupt service time   The percentage of time spent processing 
                           interrupts.  This value plus the percentage 
                           of scheduled (non-interrupt) CPU value 
                           provided in the VDH statistics (see 
                           VDH_DISPLAY) is the total percentage of 
                           execution and service time for this handler 
                           (see FEP_MONITOR_DISPLAY). 
Buffer utilization, bytes  The number of bytes currently being used for 
                           data transfer to unit record devices serviced 
                           by this handler. 
Other statistics provided include: 
Context utilization,       The number of bytes currently being used in 
bytes                      handler memory for unit record contexts. 
Devices                    A count of the number of each type of unit 
                           record device connected to the handler: line 
                           printer (LP), card punch (CP), and card 
                           reader (CR). 
00001
00002
For a list of FEP VDH definitions, enter:  ? or ??.  To access individual 
definitions, type: 
HELP (STATS) VDH_DISPLAY definition 
where definition is any of the following: 
VDI_CONNECTIONS, SCHEDULED_CPU, VDH_STATISTICS, CIRCULAR_QUEUE BYTE_STATISTICS 
  Statistics                    Description 
VDI connections               The number of virtual device interfaces 
                              being serviced by the handler. 
% Scheduled (non-interrupt)   Execution time spent as a result of CPU 
CPU                           processing from circular queue (CQ) as 
                              opposed to interrupt processing.  The 
                              percent of FEP being used by the handler 
                              is % Scheduled (non-interrupt) CPU minus 
                              the percent of interrupt level execution. 
The following statistics are provided, if appropriate. 
User to VDH entry attempts    The number of times the handler-end wants 
                              to access VDH.  (User, for this statistic, 
                              is the handler.) 
User to VDH entry deferrals   The number of times VDH entry was refused. 
                              (User, for this statistic, is the 
                              handler.) 
Connect events                Number of new connections (logons) 
                              initiated by the handler. 
Circular queue data is reported in the user-to-handler and 
handler-to-user columns for the following data (note that, in these 
columns, user refers to the host-end connection): 
Total msgs/minute             Total msg statistics report application 
Total msg bytes/minute        layer protocol messages:  Virtual Device 
Total msg bytes/msg           Operator (VDO) functions. 
Session msgs/minute           Session msg statistics report messages of 
Session msg bytes/minute      any kind, including VDOs and session level 
Session msg bytes/msg         functions (e.g., connects, disconnects). 
Data msgs(records)/minute     Data msg statistics report data messages: 
Data msg total bytes/min      VDO data functions. 
Data msg total bytes/msg 
The following statistics are provided for the number of bytes VDH puts 
in the output buffers (in the Handler-to-line column) and for the 
number of bytes of input data received from the handler (line-to-handler 
column): 
     Data msg data bytes/minute 
     Data msg data bytes/msg 
In addition, the extended FEP display includes current buffer 
information by structure type, VDH function and event counts in both 
directions (i.e., user to VDH, and VDH to user), and VDO function 
counts in both directions. 
00005
00004
00002
00003
00001
END
