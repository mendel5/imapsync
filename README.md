# imapsync-how-to
How to install and use imapsync on Linux Mint for free (no purchase)

## Intro

Official links:
- https://imapsync.lamiral.info/
- https://github.com/imapsync/imapsync
- https://github.com/imapsync/imapsync/blob/master/INSTALL.d/INSTALL.Ubuntu.txt
- https://github.com/imapsync/imapsync/blob/master/FAQ.d/FAQ.Security.txt

## Installation

Operating system: Linux Mint 20.1 Cinnamon

Press `Ctrl` + `Alt` + `T` to open a terminal.

Execute the following commands:

```
sudo apt update

sudo apt upgrade

sudo apt install git make gcc

sudo apt install libauthen-ntlm-perl libclass-load-perl libcrypt-ssleay-perl libdata-uniqid-perl libdigest-hmac-perl libdist-checkconflicts-perl libencode-imaputf7-perl libfile-copy-recursive-perl libfile-tail-perl libio-compress-perl libio-socket-inet6-perl libio-socket-ssl-perl libio-tee-perl libmail-imapclient-perl libmodule-scandeps-perl libnet-dbus-perl libnet-ssleay-perl libpar-packer-perl libreadonly-perl libregexp-common-perl libsys-meminfo-perl libterm-readkey-perl libtest-fatal-perl libtest-mock-guard-perl libtest-mockobject-perl libtest-pod-perl libtest-requires-perl libtest-simple-perl libunicode-string-perl liburi-perl libtest-nowarnings-perl libtest-deep-perl libtest-warn-perl make cpanminus libcrypt-openssl-rsa-perl libjson-webtoken-perl libpackage-stash-xs-perl

cd ~/Downloads/

git clone https://github.com/imapsync/imapsync

cd imapsync/

sudo make install

./imapsync

./imapsync --testslive --releasecheck

```

Next steps:
- http://imapsync.lamiral.info/#doc

## Usage

All parameters explained:

```
./imapsync # Call the executable in the current directory
--dry # Perform a dry run, meaning that the commands are shown but not actually executed
--host1 'test1.lamiral.info' # Domain of the source IMAP account (host1)
--port1 993 # Port of the source IMAP domain (host1)
--user1 'source-user@source-domain.com' # Username of the source IMAP account (host1)
--password1 'secret1' # Password of the source IMAP account (host1)
--host2 'test2.lamiral.info' # Domain of the target IMAP account (host2)
--port2 993 # Port of the target IMAP domain (host2)
--user2 'target-user@target-domain.com' # Username of the target IMAP account (host2)
--password2 'secret2' # Password for the target IMAP account (host2)
--ssl1 # Force the usage of SSL/TLS (?) for the connection to host1, please refer to the section 'Encryption' below
--sslargs1 SSL_verify_mode=1 # Checks whether the SSL/TLS certificate of host1 is valid (if 1)
--sslargs1 SSL_version=TLSv1_2 # Set the encryption protocol (SSL/TLS) to host1 (source) to a specific version, in this case TLS1.2
--ssl2 # Force the usage of SSL/TLS (?) for the connection to host2, please refer to the section 'Encryption' below
--sslargs2 SSL_verify_mode=1 # Checks whether the SSL/TLS certificate of host2 is valid (if 1)
--sslargs2 SSL_version=TLSv1_2 # Set the encryption protocol (SSL/TLS) to host2 (target) to a specific version, in this case TLS1.2

--addheader # imapsync creates a message header for e-mails that lack a message header
--expunge1 # Expunge messages on host1 just before syncing a folder
--subscribeall # Subscribe to the folders transferred to host2 even if they are not subscribed on host1

--delete2 # Delete all emails on host2 (target)
--delete2folders # Delete all folders on host2 (target)

--debugssl 4 # Degree of verbosity of the ssl debug statements, available from 0 (off) to 4 (maximum), standard is 1

# Note: the line breaks and comments have to be removed. The whole command has to be on a single line.
```

## Encryption

Regarding security with encryption in transit:
- imapsync offers two parameters for encryption in transit, `--ssl` and `--tls` (with a suffix of `1` or `2` for the host). It's not totally clear which of these commands does what in terms of encryption.
- In IMAP transfers, there are two encryption options, `SSL/TLS` and `STARTTLS`. Encryption with `SSL/TLS` is preferred because it is more secure than `STARTTLS` (see links below).
- As far as the author knows, `--ssl` in imapsync refers to IMAP's `SSL/TLS` and imapsync's `--tls` refers to IMAP's `STARTTLS`.
- Therefore imapsync's `--ssl` parameter is to be preferred over imapsync's `--tls` parameter.
- This is confusing because the TLS encryption protocol is the successor of the SSL encryption protocol and the modern TLS is generally preferred over the older SSL. But since in this case imapsync's parameters seem to refer to the IMAP terms and not the enryption protocol terms, there is a different meaning.

## Other

Links:
- https://blog.wydler.eu/2020/02/05/imapsync-installieren-und-nutzen/ - 2020 DE
- https://marketmix.com/de/imapsync-emailkonten-auf-neuen-server-umziehen/ - 2016 DE
- https://www.haybach.com/imapsync/doc/GOOD_PRACTICES.html - 2018 EN
- https://tecadmin.net/use-imapsync-on-ubuntu/ - 2021 EN
- https://www.systutorials.com/docs/linux/man/1-imapsync/
- https://github.com/imapsync/imapsync/blob/master/INSTALL.d/INSTALL.Debian.txt
- https://wiki.zimbra.com/wiki/Guide_to_imapsync
- https://pagure.io/imapsync
- https://serverfault.com/questions/523804/is-starttls-less-safe-than-tls-ssl
- https://mailtrap.io/blog/starttls-ssl-tls/
- https://www.fastmail.help/hc/en-us/articles/360058753834-SSL-TLS-and-STARTTLS
- https://www.privacy-handbuch.de/handbuch_31c.htm

## imapsync help output

```
./imapsync --help

Name:

 imapsync - Email IMAP tool for syncing, copying, migrating and archiving
 email mailboxes between two imap servers, one way, and without duplicates.

Version:

 This documentation refers to Imapsync $Revision: 1.977 $

Usage:

  To synchronize the source imap account
    "test1" on server "test1.lamiral.info" with password "secret1"
  to the destination imap account
    "test2" on server "test2.lamiral.info" with password "secret2"
  do:

   imapsync \
    --host1 test1.lamiral.info --user1 test1 --password1 secret1 \
    --host2 test2.lamiral.info --user2 test2 --password2 secret2

Options:

  usage: imapsync [options]

 The standard options are the six values forming the credentials. Three
 values on each side are needed in order to log in into the IMAP servers.
 These six values are a host, a username, and a password, two times.

 Conventions used in the following descriptions of the options:

  str means string
  int means integer
  reg means regular expression
  cmd means command

  --dry               : Makes imapsync doing nothing for real, just print what
                        would be done without --dry.

Options/credentials:

  --host1        str  : Source or "from" imap server.
  --port1        int  : Port to connect on host1.
                        Optional since default ports are the
                        well known ports imap/143 or imaps/993.
  --user1        str  : User to login on host1.
  --password1    str  : Password for the user1.

  --host2        str  : "destination" imap server.
  --port2        int  : Port to connect on host2. Optional
  --user2        str  : User to login on host2.
  --password2    str  : Password for the user2.

  --showpasswords     : Shows passwords on output instead of "MASKED".
                        Useful to restart a complete run by just reading
                        the command line used in the log,
                        or to debug passwords.
                        It's not a secure practice at all.

  --passfile1    str  : Password file for the user1. It must contain the
                        password on the first line. This option avoids showing
                        the password on the command line like --password1 does.
  --passfile2    str  : Password file for the user2.

 You can also pass the passwords in the environment variables
 IMAPSYNC_PASSWORD1 and IMAPSYNC_PASSWORD2

Options/encryption:

  --nossl1            : Do not use a SSL connection on host1.
  --ssl1              : Use a SSL connection on host1. On by default if possible.

  --nossl2            : Do not use a SSL connection on host2.
  --ssl2              : Use a SSL connection on host2. On by default if possible.

  --notls1            : Do not use a TLS connection on host1.
  --tls1              : Use a TLS connection on host1. On by default if possible.

  --notls2            : Do not use a TLS connection on host2.
  --tls2              : Use a TLS connection on host2. On by default if possible.

  --debugssl     int  : SSL debug mode from 0 to 4.

  --sslargs1     str  : Pass any ssl parameter for host1 ssl or tls connection. Example:
                        --sslargs1 SSL_verify_mode=1 --sslargs1 SSL_version=SSLv3
                        See all possibilities in the new() method of IO::Socket::SSL
                        http://search.cpan.org/perldoc?IO::Socket::SSL#Description_Of_Methods
  --sslargs2     str  : Pass any ssl parameter for host2 ssl or tls connection.
                        See --sslargs1

  --timeout1     int  : Connection timeout in seconds for host1.
                        Default is 120 and 0 means no timeout at all.
  --timeout2     int  : Connection timeout in seconds for host2.
                        Default is 120 and 0 means no timeout at all.

Options/authentication:

  --authmech1    str  : Auth mechanism to use with host1:
                        PLAIN, LOGIN, CRAM-MD5 etc. Use UPPERCASE.
  --authmech2    str  : Auth mechanism to use with host2. See --authmech1

  --authuser1    str  : User to auth with on host1 (admin user).
                        Avoid using --authmech1 SOMETHING with --authuser1.
  --authuser2    str  : User to auth with on host2 (admin user).
  --proxyauth1        : Use proxyauth on host1. Requires --authuser1.
                        Required by Sun/iPlanet/Netscape IMAP servers to
                        be able to use an administrative user.
  --proxyauth2        : Use proxyauth on host2. Requires --authuser2.

  --authmd51          : Use MD5 authentication for host1.
  --authmd52          : Use MD5 authentication for host2.
  --domain1      str  : Domain on host1 (NTLM authentication).
  --domain2      str  : Domain on host2 (NTLM authentication).

Options/folders:

  --folder       str  : Sync this folder.
  --folder       str  : and this one, etc.
  --folderrec    str  : Sync this folder recursively.
  --folderrec    str  : and this one, etc.

  --folderfirst  str  : Sync this folder first. Ex. --folderfirst "INBOX"
  --folderfirst  str  : then this one, etc.
  --folderlast   str  : Sync this folder last. --folderlast "[Gmail]/All Mail"
  --folderlast   str  : then this one, etc.

  --nomixfolders      : Do not merge folders when host1 is case-sensitive
                        while host2 is not (like Exchange). Only the first
                        similar folder is synced (example: with folders
                        "Sent", "SENT" and "sent"
                        on host1 only "Sent" will be synced to host2).

  --skipemptyfolders  : Empty host1 folders are not created on host2.

  --include      reg  : Sync folders matching this regular expression
  --include      reg  : or this one, etc.
                        If both --include --exclude options are used, then
                        include is done before.
  --exclude      reg  : Skips folders matching this regular expression
                        Several folders to avoid:
                         --exclude 'fold1|fold2|f3' skips fold1, fold2 and f3.
  --exclude      reg  : or this one, etc.

  --automap           : guesses folders mapping, for folders well known as
                        "Sent", "Junk", "Drafts", "All", "Archive", "Flagged".

  --f1f2    str1=str2 : Force folder str1 to be synced to str2,
                        --f1f2 overrides --automap and --regextrans2.

  --subfolder2   str  : Syncs the whole host1 folders hierarchy under the
                        host2 folder named str.
                        It does it internally by adding three
                        --regextrans2 options before all others.
                        Add --debug to see what's really going on.

  --subfolder1   str  : Syncs the host1 folders hierarchy which is under folder
                        str to the root hierarchy of host2.
                        It's the couterpart of a sync done by --subfolder2
                        when doing it in the reverse order.
                        Backup/Restore scenario:
                        Use --subfolder2 str for a backup to the folder str
                        on host2. Then use --subfolder1 str for restoring
                        from the folder str, after inverting
                        host1/host2 user1/user2 values.


  --subscribed        : Transfers subscribed folders.
  --subscribe         : Subscribe to the folders transferred on the
                        host2 that are subscribed on host1. On by default.
  --subscribeall      : Subscribe to the folders transferred on the
                        host2 even if they are not subscribed on host1.

  --prefix1      str  : Remove prefix str to all destination folders,
                        usually "INBOX." or "INBOX/" or an empty string "".
                        imapsync guesses the prefix if host1 imap server
                        does not have NAMESPACE capability. So this option
                        should not be used most of the time.
  --prefix2      str  : Add prefix to all host2 folders. See --prefix1

  --sep1         str  : Host1 separator. This option should not be used
                        most of the time.
                        Imapsync gets the separator from the server itself,
                        by using NAMESPACE, or it tries to guess it
                        from the folders listing (it counts
                        characters / . \\ \ in folder names and choose the
                        more frequent, or finally / if nothing is found.
  --sep2         str  : Host2 separator. See --sep1

  --regextrans2  reg  : Apply the whole regex to each destination folders.
  --regextrans2  reg  : and this one. etc.
                        When you play with the --regextrans2 option, first
                        add also the safe options --dry --justfolders
                        Then, when happy, remove --dry for a run, then 
                        remove --justfolders for the next ones.
                        Have in mind that --regextrans2 is applied after
                        the automatic prefix and separator inversion.
                        For examples see:
                        https://imapsync.lamiral.info/FAQ.d/FAQ.Folders_Mapping.txt

Options/folders sizes:

  --nofoldersizes     : Do not calculate the size of each folder at the
                        beginning of the sync. Default is to calculate them.
  --nofoldersizesatend: Do not calculate the size of each folder at the
                        end of the sync. Default is to calculate them.
  --justfoldersizes   : Exit after having printed the initial folder sizes.

Options/tmp:

  --tmpdir       str  : Where to store temporary files and subdirectories.
                        Will be created if it doesn't exist.
                        Default is system specific, Unix is /tmp but
                        /tmp is often too small and deleted at reboot.
                        --tmpdir /var/tmp should be better.
  --pidfile      str  : The file where imapsync pid is written,
                        it can be dirname/filename.
                        Default name is imapsync.pid in tmpdir.
  --pidfilelocking    : Abort if pidfile already exists. Useful to avoid
                        concurrent transfers on the same mailbox.

Options/log:

  --nolog             : Turn off logging on file
  --logfile      str  : Change the default log filename (can be dirname/filename).
  --logdir       str  : Change the default log directory. Default is LOG_imapsync/

 The default logfile name is for example

  LOG_imapsync/2019_12_22_23_57_59_532_user1_user2.txt

 where:

  2019_12_22_23_57_59_532 is nearly the date of the start
  YYYY_MM_DD_HH_MM_SS_mmm 
  year_month_day_hour_minute_seconde_millisecond

 and user1 user2 are the --user1 --user2 values.

Options/messages:

  --skipmess     reg  : Skips messages matching the regex.
                        Example: 'm/[\x80-ff]/' # to avoid 8bits messages.
                        --skipmess is applied before --regexmess
  --skipmess     reg  : or this one, etc.

  --skipcrossduplicates : Avoid copying messages that are already copied
                          in another folder,  good from Gmail to X when
                          X is not also Gmail.
                          Activated with --gmail1 unless --noskipcrossduplicates

  --debugcrossduplicates : Prints which messages (UIDs) are skipped with
                           --skipcrossduplicates (and in what other folders
                           they are).

  --pipemess     cmd  : Apply this cmd command to each message content
                        before the copy.
  --pipemess     cmd  : and this one, etc.
                        With several --pipemess, the output of each cmd
                        command (STDOUT) is given to the input (STDIN)
                        of the next command.
                        For example,
                        --pipemess cmd1 --pipemess cmd2 --pipemess cmd3
                        is like a Unix pipe:
                        "cat message | cmd1 | cmd2 | cmd3"

  --disarmreadreceipts : Disarms read receipts (host2 Exchange issue)

  --regexmess    reg  : Apply the whole regex to each message before transfer.
                        Example: 's/\000/ /g' # to replace null by space.
  --regexmess    reg  : and this one, etc.

Options/labels:

 Gmail present labels as folders in imap. Imapsync can accelerate the sync
 by syncing X-GM-LABELS, it will avoid to transfer messages when they are
 already on host2.

  --synclabels        : Syncs also Gmail labels when a message is copied to host2.
                        Activated by default with --gmail1 --gmail2 unless
                        --nosynclabels is added.
                       
  --resynclabels      : Resyncs Gmail labels when a message is already on host2.
                        Activated by default with --gmail1 --gmail2 unless
                        --noresynclabels is added.

 For Gmail syncs, see also:
 https://imapsync.lamiral.info/FAQ.d/FAQ.Gmail.txt

Options/flags:

  If you encounter flag problems see also:
  https://imapsync.lamiral.info/FAQ.d/FAQ.Flags.txt

  --regexflag    reg  : Apply the whole regex to each flags list.
                        Example: 's/"Junk"//g' # to remove "Junk" flag.
  --regexflag    reg  : then this one, etc.

  --resyncflags       : Resync flags for already transferred messages.
                        On by default.
  --noresyncflags     : Do not resync flags for already transferred messages.
                        May be useful when a user has already started to play
                        with its host2 account.

Options/deletions:

  --delete1           : Deletes messages on host1 server after a successful
                        transfer. Option --delete1 has the following behavior:
                        it marks messages as deleted with the IMAP flag
                        \Deleted, then messages are really deleted with an
                        EXPUNGE IMAP command. If expunging after each message
                        slows down too much the sync then use
                        --noexpungeaftereach to speed up, expunging will then be
                        done only twice per folder, one at the beginning and
                        one at the end of a folder sync.

  --expunge1          : Expunge messages on host1 just before syncing a folder.
                        Expunge is done per folder.
                        Expunge aims is to really delete messages marked deleted.
                        An expunge is also done after each message copied
                        if option --delete1 is set (unless --noexpungeaftereach).

  --noexpunge1        : Do not expunge messages on host1.

  --delete1emptyfolders : Deletes empty folders on host1, INBOX excepted.
                          Useful with --delete1 since what remains on host1
                          is only what failed to be synced.

  --delete2           : Delete messages in host2 that are not in
                        host1 server. Useful for backup or pre-sync.
                        --delete2 implies --uidexpunge2

  --delete2duplicates : Delete messages in host2 that are duplicates.
                        Works only without --useuid since duplicates are
                        detected with an header part of each message.

  --delete2folders    : Delete folders in host2 that are not in host1 server.
                        For safety, first try it like this (it is safe):
                        --delete2folders --dry --justfolders --nofoldersizes
                        and see what folders will be deleted.

  --delete2foldersonly   reg : Delete only folders matching the regex reg.
                               Example: --delete2foldersonly "/^Junk$|^INBOX.Junk$/"
                               This option activates --delete2folders

  --delete2foldersbutnot reg : Do not delete folders matching the regex rex.
                               Example: --delete2foldersbutnot "/Tasks$|Contacts$|Foo$/"
                               This option activates --delete2folders

  --noexpunge2        : Do not expunge messages on host2.
  --nouidexpunge2     : Do not uidexpunge messages on the host2 account
                        that are not on the host1 account.

Options/dates:

  If you encounter problems with dates, see also:
  https://imapsync.lamiral.info/FAQ.d/FAQ.Dates.txt

  --syncinternaldates : Sets the internal dates on host2 same as host1.
                        Turned on by default. Internal date is the date
                        a message arrived on a host (Unix mtime).
  --idatefromheader   : Sets the internal dates on host2 same as the
                        ones in "Date:" headers.

Options/message selection:

  --maxsize      int  : Skip messages larger  (or equal) than  int  bytes
  --minsize      int  : Skip messages smaller (or equal) than  int  bytes
  --maxage       int  : Skip messages older than  int days.
                        final stats (skipped) don't count older messages
                        see also --minage
  --minage       int  : Skip messages newer than  int  days.
                        final stats (skipped) don't count newer messages
                        You can do (+ zone are the messages selected):
                        past|----maxage+++++++++++++++>now
                        past|+++++++++++++++minage---->now
                        past|----maxage+++++minage---->now (intersection)
                        past|++++minage-----maxage++++>now (union)

  --search       str  : Selects only messages returned by this IMAP SEARCH
                        command. Applied on both sides.
                        For a complete set of what can be search see
                        https://imapsync.lamiral.info/FAQ.d/FAQ.Messages_Selection.txt

  --search1      str  : Same as --search but for selecting host1 messages only.
  --search2      str  : Same as --search but for selecting host2 messages only.
                        So --search CRIT equals --search1 CRIT --search2 CRIT

  --maxlinelength int : skip messages with a line length longer than  int  bytes.
                        RFC 2822 says it must be no more than 1000 bytes but
                        real life servers and email clients do more.


  --useheader    str  : Use this header to compare messages on both sides.
                        Ex: Message-ID or Subject or Date.
  --useheader    str    and this one, etc.

  --usecache          : Use cache to speed up next syncs. Not set by default.
  --nousecache        : Do not use cache. Caveat: --useuid --nousecache creates
                        duplicates on multiple runs.
  --useuid            : Use UIDs instead of headers as a criterion to recognize
                        messages. Option --usecache is then implied unless
                        --nousecache is used.

Options/miscellaneous:

  --syncacls          : Synchronizes acls (Access Control Lists).
                        Acls in IMAP are not standardized, be careful
                        since one acl code on one side may signify something
                        else on the other one.
  --nosyncacls        : Does not synchronize acls. This is the default.

  --addheader         : When a message has no headers to be identified,
                        --addheader adds a "Message-Id" header,
                        like "Message-Id: 12345@imapsync", where 12345
                        is the imap UID of the message on the host1 folder.

Options/debugging:

  --debug             : Debug mode.
  --debugfolders      : Debug mode for the folders part only.
  --debugcontent      : Debug content of the messages transferred. Huge output.
  --debugflags        : Debug mode for flags.
  --debugimap1        : IMAP debug mode for host1. Very verbose.
  --debugimap2        : IMAP debug mode for host2. Very verbose.
  --debugimap         : IMAP debug mode for host1 and host2. Twice very verbose.
  --debugmemory       : Debug mode showing memory consumption after each copy.

  --errorsmax     int : Exit when int number of errors is reached. Default is 50.

  --tests             : Run local non-regression tests. Exit code 0 means all ok.
  --testslive         : Run a live test with test1.lamiral.info imap server.
                        Useful to check the basics. Needs internet connection.
  --testslive6        : Run a live test with ks2ipv6.lamiral.info imap server.
                        Useful to check the ipv6 connectivity. Needs internet.

Options/specific:

   --gmail1           : sets --host1 to Gmail and other options. See FAQ.Gmail.txt
   --gmail2           : sets --host2 to Gmail and other options. See FAQ.Gmail.txt

   --office1          : sets --host1 to Office365 and other options. See FAQ.Exchange.txt
   --office2          : sets --host2 to Office365 and other options. See FAQ.Exchange.txt

   --exchange1        : sets options for Exchange. See FAQ.Exchange.txt
   --exchange2        : sets options for Exchange. See FAQ.Exchange.txt

   --domino1          : sets options for Domino. See FAQ.Domino.txt
   --domino2          : sets options for Domino. See FAQ.Domino.txt

Options/behavior:

  --maxmessagespersecond int : limits the number of messages transferred per second.

  --maxbytespersecond int : limits the average transfer rate per second.
  --maxbytesafter     int : starts --maxbytespersecond limitation only after
                            --maxbytesafter amount of data transferred.

  --maxsleep      int : do not sleep more than int seconds.
                        On by default, 2 seconds max, like --maxsleep 2

  --abort             : terminates a previous call still running.
                        It uses the pidfile to know what process to abort.

  --exitwhenover int  : Stop syncing and exits when int total bytes
                        transferred is reached.

  --version           : Print only software version.
  --noreleasecheck    : Do not check for any new imapsync release.
  --releasecheck      : Check for new imapsync release.
                        it's an http request to
                        http://imapsync.lamiral.info/prj/imapsync/VERSION

  --noid              : Do not send/receive ID command to imap servers.

  --justconnect       : Just connect to both servers and print useful
                        information. Need only --host1 and --host2 options.
                        Obsolete since "imapsync --host1 imaphost" alone
                        implies --justconnect

  --justlogin         : Just login to both host1 and host2 with users
                        credentials, then exit.

  --justfolders       : Do only things about folders (ignore messages).

  --help              : print this help.

  Example: to synchronize imap account "test1" on "test1.lamiral.info"
                      to  imap account "test2" on "test2.lamiral.info"
                      with test1 password "secret1"
                      and  test2 password "secret2"

  imapsync \
     --host1 test1.lamiral.info --user1 test1 --password1 secret1 \
     --host2 test2.lamiral.info --user2 test2 --password2 secret2

Here is imapsync 1.977 on host imapsync-vm, a linux system with 3.2/5.7 free GiB of RAM
with Perl 5.30.0 and Mail::IMAPClient 3.43
$Id: imapsync,v 1.977 2019/12/23 20:18:02 gilles Exp gilles $
Check if a new imapsync release is available by adding --releasecheck
Homepage: https://imapsync.lamiral.info/
```
