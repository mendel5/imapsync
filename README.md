# imapsync-how-to
How to install and use imapsync on Linux Mint for free (no purchase)

Links:
- https://imapsync.lamiral.info/
- https://github.com/imapsync/imapsync
- https://github.com/imapsync/imapsync/blob/master/INSTALL.d/INSTALL.Ubuntu.txt

## Installation

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

## Usage
```
imapsync --dry --host1 'test1.lamiral.info' --user1 'test1' --password1 'secret1' --host2 'test2.lamiral.info' --user2 'test2' --password2 'secret2'

--sslargs1 SSL_version=TLSv1_2
--sslargs2 SSL_version=TLSv1_2

--delete2 --delete2folders

--debugssl 4

The autor should really test the guide with a clean install. the packages “ssl” and “libssl-dev” are missing

To recover:
sudo apt-get install gcc
sudo apt-get install libssl-dev
sudo cpanm Crypt::OpenSSL::Random –force
sudo cpanm Crypt::OpenSSL::RSA –force
sudo make clean
sudo make install

Paket: libcrypt-openssl-rsa-perl (0.31-1 und andere) 
libcrypt-openssl-rsa-perl

```

Todo: SSL / TLS
- https://imapsync.lamiral.info/FAQ.d/FAQ.Security.txt

## Other

Links:
- https://blog.wydler.eu/2020/02/05/imapsync-installieren-und-nutzen/ - 2020 DE
- https://marketmix.com/de/imapsync-emailkonten-auf-neuen-server-umziehen/ - 2016 DE
- https://www.haybach.com/imapsync/doc/GOOD_PRACTICES.html - 2018 EN
- https://tecadmin.net/use-imapsync-on-ubuntu/ - 2021 EN
- https://www.systutorials.com/docs/linux/man/1-imapsync/
- https://github.com/imapsync/imapsync/blob/master/INSTALL.d/INSTALL.Debian.txt
- https://wiki.zimbra.com/wiki/Guide_to_imapsync
