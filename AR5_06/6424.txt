CP-6 NFS is a Network File System server.  NFS allows users on another machine
with client NFS (typically UNIX or a PC) to access the CP-6 filesystem, or part
of it, as if it were resident on their machine.
The Network File System consists of three processors:
o   NFSD, which is the Network File System server processor;
o   NFSA, which is a processor that allows you to create an authorization file
    suitable for use by the NFSD system ghost; and
o   NFSU, which is a processor that allows you to set NFS parameters, display
    NFS execution information, and build the NFS system authorization file.
For help, type the following:
 
HELP (NFS) NFSA          - for information on the NFSA processor
HELP (NFS) NFSD          - for information on the NFSD processor
HELP (NFS) NFSU          - for information on the NFSU processor
HELP (NFS) LIMITATIONS   - for a list of limitations of CP-6 NFS
HELP (NFS) FUNCTIONS     - for a list of supported standard-NFS
                           functions
B[UILD] [ F[ROM] fid1 ] [ O[VER] fid2 ]
    fid1 defaults to etc:user_equiv.:SYS fid2 defaults to :nfssec.:SYS
    This command rebuilds the security file used by NFSD by invoking NFSA.
    NFSD should be restarted in order to get the latest security information.
D[ISPLAY] { D[S] | F[ILES] | H[OSTS] | U[SERS] }
    DS (default) displays the contents of the common data segment (DS8).  FILES
    dumps the FCTXs (current files CP-6 NFS is using/knows about).  HOSTS dumps
    the HCTXs (current hosts which are using CP-6 NFS).  USERS dumps the UCTXs
    (current users that are using CP-6 NFS).
o   Supported NFS Functions
    -   Get attributes
    -   Set attributes (only on NFS created files)
    -   Lookup (verify that file exists)
    -   Read from file
    -   Write to file
    -   Create file
    -   Remove file (delete)
    -   Rename file
    -   Read directory
    -   Mount Functions (Mount, Unmount, Unmount all, Dump)
o   Unsupported NFS Functions
    -   Read symbolic link
    -   Write to cache
    -   Create link to file
    -   Create symbolic link
    -   Create directory
    -   Remove directory
    -   Mount function (Export database)
o   CP-6 NFS A02 operates in server mode only.  There is no client mode.
o   CP-6 NFS version A02 will connect only to a single XPS or DPX FEP (the
    default UNIX FEP defined in etc:routes) connected to the CP-6 host.  The
    presence of a second XPS or DPX FEP will confuse NFS unless etc:routes is
    suitably configured.  The CP-6 TCP/IP Reference Manual (HA26) describes how
    to configure the etc:routes file.
o   The nfsd daemon on a DPX FEP must be disabled, so that the DPX FEP can be
    used as a CP-6 NFS front-end.
o   CP-6 NFS version A02 can create only two types of files: "text" files and
    "binary" files.  The criteria to establish which file type to use is set on
    the first write to that file; if the first write buffer (to a maximum of
    256 characters) contains only printable ASCII, CR, LF, HT, VT, FF, and BS,
    and the write position is at the beginning of the file, then the file is
    assumed to be text;  otherwise, it is assumed to be binary.
o   CP-6 NFS version A02 will not write into the middle of a "text" file;
    instead, upon a write, it will truncate the file at the point of the write.
    The only file formats supported as "text" files for writing are consec and
    UR files.
o   CP-6 NFS version A02 will create and update binary mode files only in the
    format already defined by the CP-6 C library.
o   UNIX file names containing the character "." (period) will appear on CP-6
    containing the substituted character "$" (dollar sign).  Any file already
    in a CP-6 directory containing the character "$" will appear to the NFS
    user as if it contained a ".".
o   Packsets cannot be listed when the entire system is mounted.  Thus any
    commands using "gwd" (An internal UNIX call to Get the Working Directory)
    inside of an NFS "entire system" mounted directory may not work (e.g.,
    "emacs" and "pwd").
o   CP-6 NFS version A02 may incorrectly return the file length when first
    looking at a non-NFS file.  The length is correctly determined when the
    file is completely read, and then further attempts to read the length
    result in the correct value.
o   The CP-6 NFS RENAME function (ex. unix 'mv' command) cannot move files from
    one CP-6 mounted directory to a different CP-6 mounted directory.
o   While CP-6 NFS currently does interpret "." and ".." entries in paths, it
    does not report these entries via the "ls" command.
o   CP-6 NFS will not allow you to remove files unless you have write
    permission to them or are the owner.
The processor NFSA creates an authorization file suitable for use by the NFSD
system ghost.  NFSA also can be invoked via the BUILD command in NFSU.
For help, type the following:
 
HELP (NFS) NFSA USAGE    - for NFSA syntax
HELP (NFS) NFSA FORMAT   - for the format of a UNIX user entry
HELP (NFS) NFSA EXAMPLE  - for a sample NFSA mapping and security file
HELP (NFS) NFSA NOTES    - for notes on NFSA implementation
HELP (NFS) NFSA VERIFYING_USERS  -  for information on user
                           access to the CP-6 file system.
Typically, NFSA would be  invoked as follows:
  !NFSA etc:user_equiv.:SYS OVER :nfssec.:SYS
The input text file (typically etc:user_equiv.:SYS) contains a list of UNIX
users with their corresponding CP-6 user, NFS mount access and NFS privileges.
The security file (typically :nfssec.:SYS) is a file suitable for use by the
NFSD system ghost.  NFSD can be directed to use a different security file by
setting the F$NFSSEC DCB before invoking NFSD.
The format of a UNIX user entry is as follows:
 
UNIX[ID]=( uidops ), HOST=hostop , CP6[ID]=( cp6idops ), NFS=( nfsops )
 
  uidops (UNIX users to be recognized by CP-6 NFS) :
 
    NA[ME] [ = ] unixid
 
              User's name (first field in etc/passwd).  This is not
              used by CP-6 NFS, but it used by LPD.X
 
    GID [ = ] { n | ? }
 
              User's group identifier (fourth field in etc/passwd).
              "n" ranges from -2 To 65533  and "?" means that any
              positive GID is accepted.  This restriction on the "?" is
              enforced to increase security because UNIX assigns negative
              GIDs to unsafe users. In particular GID -2 (65534 on
              machines that use 16bit GIDs) is normally assigned to
              'nogroup' for anonymous or untrusted logins.
 
    UID [ = ] { n | ? }
 
              User's user identifier (third field in etc/passwd).
              "n" ranges from -2 to 65533 and "?" means that any
              positive UID is accepted.  This restriction on the "?" is
              enforced to increase security because UNIX assigns negative
              UIDs to unsafe users. In particular UID -2 (65534 on
              machines that use 16bit UIDs) is normally assigned to
              'nobody' for anonymous or untrusted logins.
 
  hostop (NFS clients the above users can use CP-6 NFS from) :
 
    [ ( ] ? [ ) ]
 
              The users are allowed to use CP-6 NFS from any UNIX
              client.
 
    ( host, host, ... )
 
              The users are defined on, and allowed to use CP-6
              NFS, from any of the UNIX clients listed.
 
    host
 
              The users are defined on, and allowed to use CP-6
              NFS, from the UNIX client listed.
 
  cp6idops (CP-6 users corresponding to UNIX users) :
 
    AC[CT] [ = ] account
 
              CP-6 logon account with which to access the CP-6 file system.
              This definition limits users' access as if they
              were logged in directly to CP-6, via the builtin CP-6
              file and account security.
 
    NA[ME] [ = ] name
 
              CP-6 logon name with which to access the CP-6 file system.
 
  nfsops :
 
    S[ECCHK] { [ [ = ] Y[ES] ] | [ = ] N[O] }
 
              Recheck file access on most commands.  This command
              does not do much with CP-6 NFS A02, but is intended
              to facilitate the easy addition of "export" lists.
              Default is NO if option is not specified.
 
    FMB[LK] { [ [ = ] Y[ES] ] | [ = ] N[O] }
 
              Set FMBLK privilege.  If set, this allows the listing of
              accounts at the PAD or MAD level, and for the "gwd"
              routine to work at the account level if the MAD or PAD
              is mounted.  Default is NO if option is not specified.
 
    N[XTA] { [ [ = ] Y[ES] ] | [ = ] N[O] }
 
              Same as FMBLK option.
 
    FMS[EC] { [ [ = ] Y[ES] ] | [ = ] N[O] }
 
              Set FMSEC privilege.  This setting does not require the
              CP-6 user (from cp6idops) to have FMSEC privileges.
              Default is NO if option is not specified.
 
    FMR[EAD] { [ [ = ] Y[ES] ] | [ = ] N[O] }
 
              Set FMSEC privilege.  This setting does not require the
              CP-6 user (from cp6idops) to have FMSEC privileges.
              Default is NO if option is not specified.
 
    M[OUNT] { [ [ = ] Y[ES] ] | [ = ] N[O] }
 
              Allow this user to do mounts via CP-6 NFS, if set.
              Default is NO if option is not specified.
 
    R[EJECT] { [ [ = ] Y[ES] ] | [ = ] N[O] }
 
              Reject any NFS commands for this user, if set.  Default
              is NO if option is not specified.
 
    T[OPLVL] [ = ] { A[LL] | M[AD] | P[AD] | N[ONE] }
 
              Limits how much the users can mount, also limits how
              far parent ("..") access can go.  Default is MAD.
 
In order for UNIX users to be able to access the CP-6 filesystem through CP-6
NFS, NFS must verify that they are authorized for access (via the NFS security
information).  CP-6 NFS recognizes UNIX users as a HOST,GID,UID combination.
The following table lists the order in which CP-6 NFS looks for the presence of
a user in the security information:
                 UID    GID    HOST
                 ------------------
                 uid    gid    host
                 uid     ?     host
                  ?     gid    host
                  ?      ?     host
                 uid    gid     ?
                 uid     ?      ?
                  ?     gid     ?
                  ?      ?      ?
NFSA must be used every time etc:user_equiv is updated.  There is no automatic
conversion.  Also note that NFSD needs to be restarted to force it to pick up
the newest security information.
A sample NFSA mapping and security file follows:
UNIXID=(name=userid1,gid=100,uid=25 ),;
      HOST=(unix1,unix2),;
      CP6ID=(ACCT=:SYSTAC,NAME=TESTMAN),;
      NFS=(TOPLVL=ALL,SECCHK=YES,FMSEC=YES)
 
UNIXID=(name=mickeym,gid=?,uid=?),;
      HOST=xpsnumbr1,;
      CP6ID=(ACCT=MICKEY,NAME=999MOUSE),;
      NFS=(TOPLVL=ALL,SECCHK=YES,NXTA=YES,FMREAD=YES)
 
UNIXID=(name=everyoneelse,gid=?,uid=?),;
      HOST=?,;
      CP6ID=(ACCT=DONALD,NAME=999DUCK),;
      NFS=(TOPLVL=NONE,SECCHK)
 
UNIXID (name=system1,gid=512,uid=1024),;
      HOST=?,;
      CP6ID (ACCT=SYSTEM,NAME=MANAGER),;
      NFS(TOPLVL=ALL,SECCHK=no,FMSEC)
 
UNIXID(name=root,gid=?,uid=0),;
      HOST=xpsnumbr1,;
      CP6ID(ACCT=ZZZWALT,NAME=999DISNEY),;
      NFS(TOPLVL=ALL,MOUNT)
 
UNIXID=(name=goofy,gid=100,uid=999),;
      HOST=?,;
      CP6(NAME=GOOFY,ACCT=ZZZGOOFY),;
      NFS(REJECT)
 
UNIXID=(name=efudd,gid=110,uid=900),;
      HOST=(xpsnumbr1, xpsnumbr2),;
      CP6(NAME=ELMER,ACCT=ZZZELMER),;
      NFS(TOPLVL=ALL,MOUNT,NXTA)
00005
00002
00004
00001
00003
The NFSD processor is the Network File System server processor.  The server
allows users on another machine with client NFS (typically UNIX or a PC) to
access the CP-6 filesystem, or part of it, as if it were resident on their
machine.
For help, type the following:
 
HELP (NFS) NFSD INVOKING     - for how to invoke the NFSD process
HELP (NFS) NFSD MOUNTING     - for mounting options and syntax
HELP (NFS) NFSD SECURITY     - for NFSD security issues
NFSD is most conveniently run as a ghost, from an account with access to at
least two CL resources.  If NFSD is not being run from :SYS, the running
account must also provide JIT privilege.
To start NFSD, place the run unit in :SYS and start it using GOOSE, as shown in
the example below.
!GOOSE
START account,uname,password USING !NFSD
END
If you want NFSD running all the time, you should put an entry into the
GOOSE_EGG file, as shown in the example below.
!GOOSE
U
AP
START account,uname,password AT STARTUP+3 USING !NFSD
END
END
If desired, NFSD can be run through a non-default UNIX FEP by setting the
F$ROUTES DCB to the appropriate FEP routing table (defaults to etc:routes.:SYS)
before NFSD is started.  However, only one UNIX FEP can be run through NFSD;
this means that only one copy of NFSD can be running at any one time.  The CP-6
TCP/IP A02 SRB describes how to setup FEP routing tables.
CP-6 NFS security relies mainly on the mapping of UNIX users to CP-6 users and
the defined file access permissions for those CP-6 users.  NFS users are
limited to what they can access only by what is mounted, and what their mapped
CP-6 names and additional privileges can access.  This makes the UNIX-to-CP6
user mapping file a very critical part of NFS security.
The other security issue is the accessibility of certain accounts and packsets.
With CP-6 NFS, there is no way to exclude certain packsets or accounts from
being accessed through NFS except for the built-in CP-6 security.  The access
to the file system is controlled only via the mounting level allowed for each
UNIX host, and what the UNIX host mounts.
Exclusion of a packset from NFS access can be accomplished if the system
administrator controls NFS from both the CP-6 side and UNIX sides.  Instead of
mounting the entire system, the administrator could mount only those packsets,
for which access is allowed, individually in their own UNIX directories.
Future versions of CP-6 NFS may implement "exporting"; this would allow access
control of the CP-6 file system at the packset and account level.  The system
administrator could easily "lock" or "open" accounts and packsets that CP-6 NFS
can access from the CP-6 side only.
This section describes the differences in the supported NFS file manipulation
functions and the corresponding CP-6 file management operations.  Also
described are the UNIX file attributes that must be set for each of the
file-manipulation functions to operate.  This section documents side-effects
which are not documented in the specifications for NFS, and do not map directly
to the corresponding CP-6 file management functions.
Contained in a UNIX file is the creator of the file (UID and GID of the user -
see "Implementing User Authorization With NFSA" section for more information on
UID and GID) and file permission access bits for the owner (user UID matches
creation UID of the file), group (user GID matches creation GID of the file),
and other (everyone else).  This information is used to determine what any user
can do with the file -- read, write and execute.  The permissions refered to in
the remainder of this section refer to the UNIX permissions, and in no way
override the inherent CP-6 file management access permissions.
The NFS file manipulation functions are the following:
REMOVE:   equivalent to DELETE on CP-6.  The user must either own or have write
          permission to the file.
RENAME:   this only works if both the source and target files are in the same
          directory.  If the target file exists, it is deleted before the
          rename occurs.  The user must either own or have write permission to
          the source file and, if the target file exists, the user must have
          permission to remove it.
CREATE:   if the file to be created already exists, then that file will be
          used.  If create specifies that the file is to be truncated, then all
          records in the file will be deleted, otherwise, the file will be left
          intact.  The user must have write permission to the file.  If a file
          is created without write permission, no writes are allowed to it,
          even though UNIX allows initial writes.
SETATTR:  works only for NFS-created files, and works as expected.  The user
          must own the file.
READ:     works as expected with the appropriate CP-6 record to UNIX record
          translation.  The user must have read permission to the file.
WRITE:    works as expected with the approprate UNIX record to CP-6 record
          translation.  The user must have write permission to the file.
To mount a CP-6 file system via your UNIX FEP, type the following on your
client NFS machine:
  /etc/mount unix-fep-name:CP6-file-system /unix-account
where:
  "unix-fep-name" is the name of your UNIX front-end.
  "unix-account" is the UNIX account where the file system is mounted.
  "CP6-file-system" is the name of the CP-6 file system to mount.
    This is the portion of the CP-6 file system which is to be
    accessable from NFS, and the depth of the hierarchy therein.
    You can specify:
      "."           - MAD      (all accounts in the MAD)
      "DP#psn"      - PAD      (all accounts in the given packset)
      "DP#psn.acct" - PAD.ACCT (a fully specified account)
      ".acct"       - MAD-ACCT (an account in the MAD)
      "/"           - ALL      (all packsets on your CP-6 system)
For example, if you have a UNIX front-end called "dolly", and you want to mount
the MAD on a directory called /nfs-mnt, type the following:
  /etc/mount dolly:. /nfs-mnt
The only UNIX users allowed to perform mounts are those listed in the
etc:user_equiv file with the NFSOPS option MOUNT.  For these users, the
following are the implications of the TOPLVL option:
  NONE - can't mount anything
  MAD -  can mount the MAD, PAD, or PAD.ACCT or MAD-ACCT
  PAD -  can mount PAD, or PAD.ACCT
  ALL -  can mount everything, the MAD, PAD, or PAD.ACCT or MAD-ACCT
To unmount a directory, type the following:
  /etc/umount /unix-account
00003
00001
00004
00002
The NFSU program allows for the setting of NFS parameters, displaying of NFS
execution information, and building of a system authorization file.
You may be asked to run this program and report certain values if you request
tuning support for your site.
NFSU has the following commands: BUILD, DISPLAY, RESTART, SET, and STATS.
For HELP on a command type the following:
HELP (NFS) command_name
RESTART
    not implemented.
      { DS[SIZE]             }
      { DC[BS]               }
      { B[UFFERS]            } SE[T] { O[PEN] [ T[IMEOUT] ] } = n
      { Q[UICK] [ G[RANS] ]  }
      { S[LOW] [ G[RANS] ]   }
      { T[RANSIZE]           }
    DSSIZE
      The maximum number of context blocks in the common data segment that can
      be active before garbage collection is invoked.  Acceptable values are
      between 20 and 2000; the default is 1950.
    DCBS
      The maximum number of files used, and cached, before garbage collection
      is invoked.  Acceptable values are between 20 and 120; the default is
      120.
    BUFFERS
      The maximum number of file buffers to be used before garbage collection
      is invoked.  Acceptable values are between 20 and 255; the default is
      255.
    OPEN TIMEOUT
      The maximum time, in seconds,  which a file being "held" by CP-6 will
      remain open (and busy to other CP-6 processes) since the last activity
      occured on it.  Acceptable values are 1 to 4000; the default is 30.
    QUICK GRANS
      The maximum size of a quick file that will be pre-read in order to
      determine its actual file length.  The default is 50.
      A quick file is a file which can be read in an optimized manner (blocked
      mode) in order to determine its file length, thus generally requiring one
      read per file granule.  Quick files are uncompressed keyed, consec, and
      UR files.  All other files are considered slow files, and require at
      least one read per record.
      When a file does not exist in the NFS cache, its file attributes must be
      determined.  One of the attributes of a file is its length.  The QUICK
      GRANS and SLOW GRANS parameters allow a threshold at which a file can be
      preread in order to determine the file's actual character length (which
      is not stored in a CP-6 file).  If the file is not preread, the file
      length will most likely be incorrect, and will be corrected only when the
      file is processed to the end; therefore, initial attempts to use the file
      may result in incorrect behavior on the NFS client.
    SLOW GRANS
      The maximum size of a slow file that will be pre-read in order to
      determine its actual file length.  See the description under QUICK GRANS
      for more information.  The default is 10.
    TRANSIZE
      The udp transfer size in bytes, generally the data size of the data part
      of READ and WRITE requests.  Acceptable values are 512 to 8192; the
      default is 4096.
ST[ATS]
    A full screen display containing the running information on NFS.  The
    display is updated every 3 seconds, and requires a minimum 18x80 window
    size.  <BREAK> exits from the display.
