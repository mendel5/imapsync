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

Command in one line:

```
--> put the whole command here
```

All parameters explained:

```
./imapsync # call the executable in the current directory
--dry # perform a dry run, meaning that the commands are shown but not actually executed
--host1 'test1.lamiral.info' # domain of the source IMAP account (host1)
--user1 'test1' # username of the source IMAP account (host1)
--password1 'secret1' # password of the source IMAP account (host1)
--host2 'test2.lamiral.info' # domain of the target IMAP account (host2)
--user2 'test2' # username of the target IMAP account (host2)
--password2 'secret2' # password for the target IMAP account (host2)

--sslargs1 SSL_verify_mode=1 # checks whether the SSL/TLS certificate of host1 is valid (if 1)
--sslargs1 SSL_version=TLSv1_2 # Set the encryption protocol (SSL/TLS) to host1 (source) to a specific version, in this case TLS1.2
--sslargs2 SSL_verify_mode=1 # checks whether the SSL/TLS certificate of host2 is valid (if 1)
--sslargs2 SSL_version=TLSv1_2 # Set the encryption protocol (SSL/TLS) to host2 (target) to a specific version, in this case TLS1.2

--debugssl 4 # degree of verbosity of the ssl debug statements, available from 0 (off) to 4 (maximum), standard is 1

--delete2 # delete all emails on host2 (target)
--delete2folders # delete all folders on host2 (target)

# Note: the line breaks have to be removed
```

Regarding security:
- imapsync offers two options for encryption in transit, `--ssl` and `--tls` (with a suffix of `1` or `2` for the host). It's not totally clear which of these commands does what in terms of encryption.
- In IMAP transfers, there are two encryption options, `SSL/TLS` and `STARTTLS`. `SSL/TLS` is more secure than `STARTTLS` (see links below).
- As far as the author knows, `--ssl` in imapsync refers to IMAP's `SSL/TLS` and imapsync's `--tls` refers to IMAP's `STARTTLS`.
- Therefore imapsync's `--ssl` parameter is to be preferred over imapsync's `--tls` parameter.
- This is confusing because the TLS encryption protocol is the successor of the SSL encryption protocol and the modern TLS is generally preferred over the older SSL. But since in this case imapsync's tags seem to refer to the IMAP terms and not the enryption protocol terms, there is a different meaning.

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
