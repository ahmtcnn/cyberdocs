# Linux Sistemler

# 1. Linux Sistemlerde Hak Yükseltme

## 1.1 Temel olarak nelere bakılmalı?

* Bilgi Toplama
	- İşletim sistemi sürümleri kontrol edilmeli
	- Kernel sürümü kontrol edilmeli
	- Yüklü paketler, programlar ve servisler kontrol edilmeli. Eski sürümlerden kaynaklı zafiyetler barındırıyor olabilir.
* Yama eksiklikleri
* Yapılandırma eksiklikleri
	- /root/ klasörüne yazma izni
	- Bütün kullanıcı dizinlerine yazma izni
	- Çalıştırılabilir dosya hakları
	- root olarak koşan servisler
	- Uygulama (servis) yapılandırma eksiklikleri
* Basit/varsayılan parola kullanımı
* Açık metin parola kullanımı

## 1.2 Bilgi Toplama

* Dağıtım türü nedir, versiyonu nedir?
	- cat /etc/issue
	- cat /etc/*-release
	- cat /etc/lsb-release
	- cat /etc/redhat-release

* Kernel versiyonu nedir?
	- cat /proc/version
	- uname -a
	- uname -mrs
	- rpm -q kernel
	- dmesg | grep linux
	- ls /boot | grep vmlinuz-

* Çevresel değişkenlerden öğrenilebilecekler
	- cat /etc/profile
	- cat /etc/bashrc
	- cat ~/.bash_profile
	- cat ~/.bashrc
	- cat ~/.bash_logout

* Hangi servisler çalışıyor? Hangi servisler hangi kullanıcı ayrıcalıklarına sahip?
	- ps aux
	- ps -ef
	- top
	- cat /etc/services

* Hangi servisler root kullancısı ile çalışıyor? Hangi versiyona sahipler, şuan çalışıyorlar mı?
	- ls -alh/usr/bin
	- ls -alh/sbin/
	- dpkg -l
	- rpm -qa 
	- ls -alh /var/cache/apt/archiveso
	- ls -alh /var/cache/yum/

* Biz kimiz, sistemde kim oturum açtı, kim ne yapabilir?
	- id
	- who
	- last
	- cat /etc/passwd | cut -d: -f1 #kullanıcıları listele
	- grep -v -E "^#" /etc/passwd/ | awk -F: '$3 == 0 { print $1}' #Süperkullanıcıları listele
	- awk -F: '($3 == "0") {print}' /etc/passwd #Süperkullanıcıları listele
	- cat /etc/sudoers
	- sudo -l

* Hangi hassas dosyalar bulunabilir?
	- cat /etc/passwd
	- cat /etc/group
	- cat /etc/shadow
	- ls -alh /var/mail/
	- ls -alh /var/mail/
	- cat /var/apache2/config.inc
	- cat /var/lib/mysql/mysql/user.MYD
	- cat /root/anaconda-ks.cfg


* Hangi yazılım dilleri kurulu, yüklü?
	- find / -name perl*
	- find / -name python*
	- find / -name gcc*
	- find / -name cc*

* Nasıl dosya yükleyebilirim?
	- find / -name wget
	- find / -name nc*
	- find / -name netcat*
	- find / -name tftp*
	- find / -name ftp*

## 1.2 Yapılandırma Eksiklikleri

* /root/ klasörüne yazma izni
* Bütün kullanıcı dizinlerine yazma izni
* Çalıştırılabilir dosya hakları
* root olarak koşan servisler
* Uygulama(servis) yapılandırma eksiklikleri
* Hizmet ayarlarından herhangi biri yanlış yapılandırıldı mı? Zafiyetli eklentiler var mı?
	- cat /etc/syslog.conf
	- cat /etc/chttp.conf
	- cat /etc/lighttpd.conf
	- cat /etc/cups/cupsd.conf
	- cat /etc/inetd.conf
	- cat /etc/apache2/apache2.conf
	- cat /etc/httpd/conf/httpd.conf
	- cat /opt/lampp/etc/httpd.conf
	- ls -aRl /etc/ | awk '$1 ~ /^.*r.*/

* Hangi işlerin planlandığı ?
	- crontab -l
	- ls -alh /var/spool/cron
	- ls -al /etc/ | grep cron
	- ls -al /etc/cron-
	- cat /etc/at.allow
	- cat /etc/at.deny
	- cat /etc/cron.allow
	- cat /etc/cron.deny
	- cat /etc/crontab
	- cat /etc/anacrontab
	- cat /var/spool/cron/crontabs/root

* Kullanıcı ne yapıyor? Açık metin olarak parola var mı? 
	- cat ~/.bash_history
	- cat ~/.nano_history
	- cat ~/.atftp_history
	- cat ~/.mysql_history
	- cat ~/.php_history

* Hangi kullanıcı bilgilerine ulaşılabilir?
	- cat ~/.bashrc
	- cat ~/.profile
	- cat /var/mail/root
	- cat /var/spool/mail/root

* Private-Key bilgileri bulunabilir mi?
	- cat ~/.ssh/authorized_keys
	- cat ~/.ssh/identify.pub
	- cat ~/.ssh/identify
	- cat ~/.ssh/id_rsa.pub
	- cat ~/.ssh/id_rsa
	- cat ~/.ssh/id_dsa.pub
	- cat ~/.ssh/id_dsa
	- cat /etc/ssh/ssh_config
	- cat /etc/ssh/sshd_config
	- cat /etc/ssh/ssh_host_dsa_key.pub
	- cat /etc/ssh/ssh_host_dsa_key
	- cat /etc/ssh/ssh_host_rsa_key.pub
	- cat /etc/ssh/ssh_host_rsa_key
	- cat /etc/ssh/ssh_host_key.pub
	- cat /etc/ssh/ssh_host_key

* /etc/ dizinine hangi yapılandırma dosyaları yazılabilir? 
	- ls -aRl /etc/ | awk '$1 ~ /^.*w.*/' 2>/dev/null #Herhangi biri
	- ls -aRl /etc/ | awk '$1 ~ /^..w/' 2>/dev/null #Owner(Sahip)
	- ls -aRl /etc/ | awk '$1 ~ /^.....w/' 2>/dev/null #Grup
	- ls -aRl /etc/ | awk '$1 ~ /^.*w.*/' 2>/dev/null #Diğer
	- ls -aRl /etc/ | awk '$1 ~ /w.$/' 2>/dev/null #Herhangi biri
	- find /etc/ -readable -type f 2>/dev/null #Herhangi biri
	- find /etc/ -readable -type f -maxdepth 1 2>/dev/null # Herhangi biri

* /var/ dizininde neler bulabiliriz ?
	- ls -alh /var/log
	- ls -alh /var/mail
	- ls -alh /var/spool
	- ls -alh /var/spool/lpd
	- ls -alh /var/lib/pgsql
	- ls -alh /var/lib/mysql
	- cat /var/lib/dhcp3/dhclient.leases

* Web servislerinde gizlenmiş ayar(.config) dosyaları var mı? Veritabanı bilgisine sahip bir ayar(.config) dosyası var mı?
	- ls -alhR /var/www/
	- ls -alhR /srv/www/htdocs/
	- ls -alhR /usr/local/www/apache22/data/
	- ls -alhR /opt/lampp/htdocs/
	- ls -alhR /var/www/html/

* Nerede yazma ve çalıştırma işlemleri yapılabilir? Birkaç ortak yer (/tmp, /var/tmp, /dev/shm)
	- find / -writable -type d 2>/dev/null #yazabilme işlemleri
	- find / -perm -222 -type d 2>/dev/null #yazabilme işlemleri
	- find / -perm -o w -type d 2>/dev/null #yazabilme işlemleri
	- find / -perm -o x -type d 2>/dev/null #çalıştırabilme işlemleri
	- find / \(-perm -o w -perm -o x \) -type d 2>/dev/null #yazabilme ve çalıştırabilme işlemleri

## 1.3 Açık Metin Parola Kullanımı
* Dosyalar
* Herhangi bir dosyada düz metin kullanıcı adı veya parola var mı?
	- grep -i user [filename]
	- grep -i pass [filename]
	- grep -C 5 "password" [filename]
	- find . -name "*.php" -print0 | xargs -O grep -i -n "var $password"
* Scriptlerde, veritabanlarında, config dosyalarında yada loglarda parolalar var mı?
	- cat /var/apache2/config.inc
	- cat /var/lib/mysql/mysql/user.MYD
	- cat /root/anaconda-ks.cfg

## 1.4 Araçlar
	- unix-privesc-check
	- linuxprivchecker.py