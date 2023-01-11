---
id: Introduction
created_date: 27/10/2022
updated_date: 27/10/2022
type: note
---

#  Introduction
- **🏷️Tags** :  #10-2022 #command #password #linux #windows #CheatSheet #permission #credentials 


| **Windows** | **Linux** |
| ------------- | ----------- |
| unattend.xml  | shadow       |
 |sysprep.inf|shadow.bak|
|SAM|password|


There are many tools and methods to utilize for login brute-forcing, like:

-   `Ncrack`
-   `wfuzz`
-   `medusa`
-   `patator`
-   `hydra`
-   and others.

# Hydra supported request : 
```shell-session
GabrielQK@htb[/htb]$ hydra -h | grep "Supported services" | tr ":" "\n" | tr " " "\n" | column -e

Supported			        ldap3[-{cram|digest}md5][s]	rsh
services			        memcached					rtsp
				            mongodb						s7-300
adam6500			        mssql						sip
asterisk			        mysql						smb
cisco				        nntp						smtp[s]
cisco-enable		        oracle-listener				smtp-enum
cvs				            oracle-sid					snmp
firebird			        pcanywhere					socks5
ftp[s]				        pcnfs						ssh
http[s]-{head|get|post}		pop3[s]						sshkey
http[s]-{get|post}-form		postgres					svn
http-proxy		        	radmin2						teamspeak
http-proxy-urlenum		    rdp				  		    telnet[s]
icq				            redis						vmauthd
imap[s]		        		rexec						vnc
irc				            rlogin						xmpp
ldap2[s]		        	rpcap
```

we can remove any passwords that do not meet these conditions from our wordlist. Some tools would convert password policies to `Hashcat` or `John` rules, but `hydra` does not support rules for filtering passwords. So, we will simply use the following commands to do that for us:

Code: bash

```bash
sed -ri '/^.{,7}$/d' william.txt            # remove shorter than 8
sed -ri '/[!-/:-@\[-`\{-~]+/!d' william.txt # remove no special chars
sed -ri '/[0-9]+/!d' william.txt            # remove no numbers
```


## Questions/Thoughts


## 🔗 Links
