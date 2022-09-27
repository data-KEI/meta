### Stunnel 클라이언트 구성
- Stunnel 설치: sudo apt install stunnel
~~~
$ sudo apt install stunnel
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Note, selecting 'stunnel4' instead of 'stunnel'
Suggested packages:
  logcheck-database
The following NEW packages will be installed:
  stunnel4
0 upgraded, 1 newly installed, 0 to remove and 13 not upgraded.
Need to get 215 kB of archives.
After this operation, 569 kB of additional disk space will be used.
Get:1 http://archive.ubuntu.com/ubuntu jammy/universe amd64 stunnel4 amd64 3:5.63-1build1 [215 kB]
Fetched 215 kB in 2s (99.2 kB/s)
Selecting previously unselected package stunnel4.
(Reading database ... 143652 files and directories currently installed.)
Preparing to unpack .../stunnel4_3%3a5.63-1build1_amd64.deb ...
Unpacking stunnel4 (3:5.63-1build1) ...
Setting up stunnel4 (3:5.63-1build1) ...
Creating group stunnel4 with gid 998.
Creating user stunnel4 (stunnel service system account) with uid 998 and gid 998.
Created symlink /etc/systemd/system/multi-user.target.wants/stunnel.target → /lib/systemd/system/stunnel.target.
Processing triggers for man-db (2.10.2-1) ...
Scanning processes...
Scanning processor microcode...
Scanning linux images...

Running kernel seems to be up-to-date.

The processor microcode seems to be up-to-date.

No services need to be restarted.

No containers need to be restarted.

No user sessions are running outdated binaries.

No VM guests are running outdated hypervisor (qemu) binaries on this host.
~~~
- 인증서 다운로드
~~~
$ sudo scp -P 764 user@IP:/etc/stunnel/stunnel.pem  /etc/stunnel/stunnel.pem
user@IP's password:
stunnel.pem                                                                   100% 3001     2.4MB/s   00:00
~~~
- Stunnel 설정: vi /etc/stunnel/stunnel.conf
~~~
output  = /var/log/stunnel4/stunnel.log
cert    = /etc/stunnel/stunnel.pem
key     = /etc/stunnel/stunnel.pem
pid     = /var/run/stunnel4/stunnel.pid
#client  = yes

[openvpn]
client = yes
accept = 1234
~~~
### OpenVPN 구성
- OpenVPN 설치: sudo apt install openvpn
~~~
$ sudo apt install openvpn
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  libpkcs11-helper1
Suggested packages:
  resolvconf openvpn-systemd-resolved easy-rsa
The following NEW packages will be installed:
  libpkcs11-helper1 openvpn
0 upgraded, 2 newly installed, 0 to remove and 13 not upgraded.
Need to get 662 kB of archives.
After this operation, 1,825 kB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libpkcs11-helper1 amd64 1.28-1ubuntu0.22.04.1 [50.3 kB]
Get:2 http://archive.ubuntu.com/ubuntu jammy/main amd64 openvpn amd64 2.5.5-1ubuntu3 [611 kB]
Fetched 662 kB in 2s (266 kB/s)
Preconfiguring packages ...
Selecting previously unselected package libpkcs11-helper1:amd64.
(Reading database ... 143693 files and directories currently installed.)
Preparing to unpack .../libpkcs11-helper1_1.28-1ubuntu0.22.04.1_amd64.deb ...
Unpacking libpkcs11-helper1:amd64 (1.28-1ubuntu0.22.04.1) ...
Selecting previously unselected package openvpn.
Preparing to unpack .../openvpn_2.5.5-1ubuntu3_amd64.deb ...
Unpacking openvpn (2.5.5-1ubuntu3) ...
Setting up libpkcs11-helper1:amd64 (1.28-1ubuntu0.22.04.1) ...
Setting up openvpn (2.5.5-1ubuntu3) ...
Created symlink /etc/systemd/system/multi-user.target.wants/openvpn.service → /lib/systemd/system/openvpn.service.
Processing triggers for man-db (2.10.2-1) ...
Processing triggers for libc-bin (2.35-0ubuntu3.1) ...
Scanning processes...
Scanning processor microcode...
Scanning linux images...

Running kernel seems to be up-to-date.

The processor microcode seems to be up-to-date.

No services need to be restarted.

No containers need to be restarted.

No user sessions are running outdated binaries.

No VM guests are running outdated hypervisor (qemu) binaries on this host
~~~
- OpenVPN 구성: vi /etc/openvpn/VPNconfig.conf
~~~
dev tun
tls-client
remote localhost 1234
pull
proto tcp-client
script-security 2
comp-lzo
reneg-sec 0
cipher SEED-CBC
auth SHA512
auth-user-pass /etc/openvpn/auth
<ca>
......
</ca>
~~~
