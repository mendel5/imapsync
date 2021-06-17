# imapsync-how-to
How to install imapsync on Linux Mint for free (no purchase)

Links:
- https://imapsync.lamiral.info/
- https://github.com/imapsync/imapsync
- https://github.com/imapsync/imapsync/blob/master/INSTALL.d/INSTALL.Ubuntu.txt

## How to

OS: Linux Mint 20.1 Cinnamon

Press `Ctrl` + `Alt` + `T` to open a Terminal.

Execute the following commands:

```
sudo apt update

sudo apt upgrade

sudo apt install git make gcc

sudo apt install libauthen-ntlm-perl libclass-load-perl libcrypt-ssleay-perl libdata-uniqid-perl libdigest-hmac-perl libdist-checkconflicts-perl libencode-imaputf7-perl libfile-copy-recursive-perl libfile-tail-perl libio-compress-perl libio-socket-inet6-perl libio-socket-ssl-perl libio-tee-perl libmail-imapclient-perl libmodule-scandeps-perl libnet-dbus-perl libnet-ssleay-perl libpar-packer-perl libreadonly-perl libregexp-common-perl libsys-meminfo-perl libterm-readkey-perl libtest-fatal-perl libtest-mock-guard-perl libtest-mockobject-perl libtest-pod-perl libtest-requires-perl libtest-simple-perl libunicode-string-perl liburi-perl libtest-nowarnings-perl libtest-deep-perl libtest-warn-perl make cpanminus

sudo cpanm Mail::IMAPClient

cd ~/Downloads/

git clone https://github.com/imapsync/imapsync

cd imapsync/

./imapsync

./imapsync --testslive --releasecheck

sudo cp imapsync /usr/bin/

imapsync --testslive --releasecheck

imapsync

```

Next steps:
- http://imapsync.lamiral.info/#doc

## Other

Links:
- https://blog.wydler.eu/2020/02/05/imapsync-installieren-und-nutzen/ - 2020 DE
- https://marketmix.com/de/imapsync-emailkonten-auf-neuen-server-umziehen/ - 2016 DE
- https://www.haybach.com/imapsync/doc/GOOD_PRACTICES.html - 2018 EN
- https://tecadmin.net/use-imapsync-on-ubuntu/ - 2021 EN
- https://www.systutorials.com/docs/linux/man/1-imapsync/
- https://github.com/imapsync/imapsync/blob/master/INSTALL.d/INSTALL.Debian.txt
