# imapsync-how-to
How to use imapsync

How to install and use imapsync on Ubuntu 20.04 for free (no purchase)

Main:
- https://imapsync.lamiral.info/
- https://github.com/imapsync/imapsync
- https://github.com/imapsync/imapsync/blob/master/INSTALL.d/INSTALL.Ubuntu.txt
- https://www.systutorials.com/docs/linux/man/1-imapsync/


Advice:
- https://blog.wydler.eu/2020/02/05/imapsync-installieren-und-nutzen/ - 2020 DE
- https://marketmix.com/de/imapsync-emailkonten-auf-neuen-server-umziehen/ - 2016 DE
- https://www.haybach.com/imapsync/doc/GOOD_PRACTICES.html - 2018 EN
- https://tecadmin.net/use-imapsync-on-ubuntu/ - 2021 EN


## How to 1

OS: Ubuntu 20.04.2 LTS


```
sudo apt update
sudo apt -y upgrade
sudo apt install -y git make gcc
sudo apt install -y apt-file cpanminus libc6-dev libssl-dev
sudo apt install -y libperl-dev zlib1g-dev libnet-ssleay-perl
sudo apt-get install -y libperl-dev libssl-dev makepasswd rcs perl-doc libio-tee-perl git libmail-imapclient-perl libdigest-md5-file-perl libterm-readkey-perl libfile-copy-recursive-perl build-essential make automake libunicode-string-perl
// sudo mount -o remount,exec /tmp
cpanm App::cpanminus Authen::NTLM CGI Compress::Zlib Crypt::OpenSSL::RSA Data::Dumper Data::Uniqid Dist::CheckConflicts Encode Encode::IMAPUTF7 File::Copy::Recursive File::Tail IO::Socket::INET IO::Socket::INET6 IO::Socket::SSL IO::Tee JSON JSON::WebToken LWP::UserAgent Mail::IMAPClient Module::ScanDeps PAR::Packer Pod::Usage Readonly Regexp::Common Sys::MemInfo Term::ReadKey Test::MockObject Test::More Test::Pod Unicode::String
// mount -o remount,noexec /tmp
cd /usr/local/src
sudo git clone https://github.com/imapsync/imapsync.git
cd imapsync
sudo make install
```


## How to 2

OS: Linux Mint 20.1 Cinnamon

```
sudo apt update

sudo apt upgrade

sudo apt install libauthen-ntlm-perl libclass-load-perl libcrypt-ssleay-perl libdata-uniqid-perl libdigest-hmac-perl libdist-checkconflicts-perl libencode-imaputf7-perl libfile-copy-recursive-perl libfile-tail-perl libio-compress-perl libio-socket-inet6-perl libio-socket-ssl-perl libio-tee-perl libmail-imapclient-perl libmodule-scandeps-perl libnet-dbus-perl libnet-ssleay-perl libpar-packer-perl libreadonly-perl libregexp-common-perl libsys-meminfo-perl libterm-readkey-perl libtest-fatal-perl libtest-mock-guard-perl libtest-mockobject-perl libtest-pod-perl libtest-requires-perl libtest-simple-perl libunicode-string-perl liburi-perl libtest-nowarnings-perl libtest-deep-perl libtest-warn-perl make cpanminus

sudo cpanm Mail::IMAPClient

-----

cd ~/Downloads

git clone https://github.com/imapsync/imapsync


--
git clone ?
--

cd 
tar xzvf  imapsync-1.xxx.tgz

cd imapsync-1.xxx

./imapsync

./imapsync --testslive

cp imapsync /usr/bin/

```
