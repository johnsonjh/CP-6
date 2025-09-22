The ROUTECON processor is used to define the network addresses used by all
CP-6 OSI applications.
ROUTECON runs on the host CP-6 system as a batch or on-line job.  ROUTECON
accepts commands, updates the :ROUTE file, displays routing information, and
updates the routing tables on the host and the FEPs.
The DCBs used by ROUTECON are:
    M$SI for ROUTECON command input
    M$LO for user messages
Use of ROUTECON requires the FMSEC, MFEP and SPCLMM privileges as well as the
NETCON processor privilege.
ROUTECON builds and maintains the :ROUTE file.  The :ROUTE file contains all
the OSI routing information for the CP-6 network.  This information is used by
SLUG on the host and NODEADMN on the FEP to maintain the OSI Routing Tables.
  **************************************************************
  *   Copyright (c) Honeywell Bull Inc., 1988
  **************************************************************
  Command      Purpose
DEFINE       Defines a NSAP.
DELETE       Deletes an existing NSAP.
DISPLAY      Displays all currently known NSAPs.
END          Exits the ROUTECON Processor.
COMMANDS
Format:
DEFINE nsap_id   TYPE=nsap_type, FEP=fep_node, HOST=host_node,
                   LNSAP=lnsap_id, NW_TYPE=nw_type,
                   NSAP=nsap, X25=nw_addr
Description:
This command is used to define the OSI routing information for each remote OSI
endpoint and to define the relationship between the physical addresses used by
X.25 and the NSAP addresses used by the OSI layers.  This command is also used
to define your own local NSAP address.
The set of options used for any single DEFINE command depends on whether the
command defines your local system or a remote endpoint.
Options valid for both local and remote:
   nsap_id
   TYPE=nsap_type
   FEP=fep_node
   NSAP=nsap
Options valid only if local definition:
   HOST=host_node
Options valid only if remote definition:
   NW_TYPE=nw_type
   X25=nw_addr
   LNSAP=nsap_id
Examples:
DEF LOC84 TYPE=LNSAP, FEP=5, NSAP=514C363641
DEF RMT84 TYPE=RNSAP, FEP=5, LNSAP=LOC84
           NSAP=517A657573, X25=3106000888
DEF LOC80 TYPE=LNSAP, FEP=5, NSAP=3106000777
DEF RMT80 TYPE=RNSAP, FEP=5, LNSAP=LOC80
           NSAP=3106000999, X25=3106000999, NW=X25_80
00001
00002
Format:
DELETE nsap_id
Description:
This command removes the specified nsap_id from the routing tables on each
node in the CP-6 network.
Example:
DELETE LOC80
DELETE RMT80
00001
00002
Format:
DISPLAY [nsap_id]
Description:
This command displays the current setting for the specified nsap_id.  If
nsap_id is not specified, the current settings for all nsap_ids is displayed.
Example:
!ROUTECON
-ROUTECON A00 HERE
*DISP LOC84
nsap id     : LOC84
nsap type   : local
host node   :  0
fep node    :  5
nsap  :  bytes :   5 addr: .514C363641
*DISP RMT84
nsap id     : RMT84
nsap type   : remote
network type: x25_84
fep node    :  5
nsap  :  bytes :   5 addr: .5171657573
lnsap :  bytes :   5 addr: .514C363641
x.25  :  digits:  10 addr: .3106000888
*DISP LOC80
nsap id     : LOC80
nsap type   : local
host node   :  0
fep node    :  5
nsap  :  bytes :   5 addr: .3106000777
*DISP RMT80
nsap id     : RMT80
nsap type   : remote
network type: x25_80
fep node    :  5
nsap  :  bytes :   5 addr: .3106000999
lnsap :  bytes :   5 addr: .3106000777
x.25  :  digits:  10 addr: .3106000999
*END
00001
00002
Format:
END
Description:
The END command, and its synonyms QUIT and X, are used to terminate ROUTECON
and return control to IBEX.
00001
D
  DEFINE Command -
      HELP DEFINE
  DELETE Command -
      HELP DELETE
  DISPLAY Command -
      HELP DISPLAY
  DNIC (Data Network Identification Code) -
      HELP CP_6_OSI_CONFIGURATION
E
  END Command -
      HELP END
N
  NSAP address -
      HELP CP_6_OSI_CONFIGURATION
P
  PSN (Packet Switching Network) -
      HELP CP_6_OSI_CONFIGURATION
R
  ROUTECON Options -
      HELP OPTIONS
  ROUTECON Processor -
      HELP ROUTECON_PROCESSOR
X
  X.121 address -
      HELP CP_6_OSI_CONFIGURATION
  X.25 address -
      HELP CP_6_OSI_CONFIGURATION
00001
00002
00003
00004
00005
HELP_INDEX
The options have the following meaning:
  Option          Meaning
  nsap_id
                  Provides a convenient way to refer to this NSAP definition.
                  The nsap_id is installation defined and consists of up to 8
                  characters.  Only alphanumeric characters, ":" and "$" may
                  be used.
                  Note that the nsap_id is not used outside of the ROUTECON
                  processor in any way; it simply provides a way to specify
                  the LNSAP option value and the DELETE and DISPLAY parameter
                  without entering the hexadecimal digits used to specify NSAP
                  values.
                  This option must be specified; there is no default.
  TYPE=nsap_type
                  nsap_type must specify LNSAP if this is a Local NSAP or must
                  specify RNSAP if this is a Remote NSAP.
                  This option must be specified; there is no default.
  FEP=fep_node
                  Specifies the node number of the FEP where the communication
                  line to the remote network connects.  This must be a local
                  FEP; routing through a remote FEP is not supported.
                  This option must be specified; there is no default.
  HOST=host_node
                  Specifies the node number of the host on which the OSI
                  application resides.  The default is the node number of the
                  host where ROUTECON is being executed.  Valid only if
                  TYPE=LNSAP.
  LNSAP=lnsap_id
                  Specifies the Local NSAP nsap_id.  This is used to locate
                  the NSAP to be supplied to the remote endpoint when
                  initiating an OSI connection.  The lnsap_id must have
                  previously been defined as the nsap_id on another DEFINE
                  command.
                  This option must be specified if TYPE=RNSAP.  There is no
                  default.
  NW_TYPE=nw_type
                  Specifies the type of network that is used to reach this
                  remote endpoint.  Valid options are X25_80 and X25_84; the
                  default is X25_84.  Valid only if TYPE=RNSAP.
                  The CP-6 implementation of X.25 utilizes the 1984 protocols,
                  but can accept inbound connections from those
                  implementations that use use only the 1980 protocols.  When
                  NW_TYPE=X25_80 is specified for a remote endpoint, the CP-6
                  system uses the 1980 X.25 protocol when initiating an
                  outbound connection.
  NSAP=nsap
                  Specifies the Network Service Access Point, as defined by
                  ISI 8348/DAD2, or as defined by the private X.25 network
                  naming authority, or the X.25 address as defined for an 1980
                  X.25 network.
                  nsap consists of a sequence of up to 40 hexadecimal digits,
                  and must consist of an even number of digits.
                  This option must be specified; there is no default.
  X25=nw_addr
                  Specifies the remote X.25 address, including any subaddress,
                  if any.  The addr consists of a sequence of up to 19
                  binary-coded decimal digits.
                  This option must be specified if TYPE=RNSAP.  There is no
                  default.
00003
00004
00005
00007
00001
00006
00002
00008

