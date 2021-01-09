# Bilgi Toplama

# 1. Pasif Bilgi Toplama

* Google Hacking
	- https://pentest-tools.com/information-gathering/google-hacking
	- https://www.exploit-db.com/google-hacking-database/

* theHarvester
	- Kullanımı:
		-d: Aranacak domain
		-b: Veri kaynağı: google, googleCSE, bing, bingapi, pgp, linkedin, google-profiles, jigsaw, twitter, googleplus, all
		-f: HTML veya XML dosyası olarak kaydetme
		-l: Arama sonucu limiti
	- Örnek tarama:
		theharvester -d bilgi.edu.tr -l 500 -b google -h sonuc.html

* Sosyal medya
	- linkedin.com
	- facebook.com
	- twitter.com
	- instagram.com

* Whois Sorguları
	- whois IP
		Alan adı tescil edilen şirket
		Domain süresi tarihleri
		DNS sunucular
		İletişim bilgileri
		Web sitesi istatistikleri
		E-mail
		DNS kayıtları
		Mail Sunucusu
	- Domain Tools
		http://whois.domaintools.com/
	- Cqcounter
		http://cqcounter.com/whois/ 
	- Robtex
		https://www.robtex.com/ 
	- Reverse IP Lookup
		https://www.yougetsignal.com/tools/web-sites-on-web-server/ 

* Dosya Metadataları
	- Foca
		https://www.elevenpaths.com/labstools/foca/
		Proje yarat
		Arama yap
		Dosyaları indir
		Metadataları extract et
		Metadataları analiz et
	- Metagoofil

* Veri Sızıntıları
	- Have I Been Pwned
		https://haveibeenpwned.com/
	- DeepWeb
	- Pastebin

* Arama Motorları
	- Alt alan adlarının tespit edilmesi
	- Kullanılan dosya tiplerinin tespit edilmesi
	- Zafiyet içeren bir versiyona özel arama
	- Alan adı hedefli aramalar
	- Email toplamak
	- Özel karakterler ile arama
	- Bing IP den diğer siteler
	- Namaserver daki diğer alan adları
	- Robots.txt
		Engellenen arama motorları
		Engellenen erişim dizinleri
		Erişime izin verilen dizinler
		Site map adresi

* Reverse DNS Lookup
	- NS Server ve TTL değerleri
	- NS Sunucu IP’leri
	- Recursive İsteklerin durumu
	- NS sunucu sayısı
	- NS sunucu networklerinin farklı olması durumu
	- SOA kaydı
	- MX Sunucuları ve IP adresleri
	- PTR kaydı
	- DNS sunucu ve yapılandırma eksiklikleri

* Tools
	- Fierce
	- TheHarvester
	- Maltego
	- Foca 
	- Oometaextractor
	- Metagoofil
	- Meta extractor
	- Dmitry
	- Social Mapper

# 2. Aktif Bilgi Toplama

* DNS Sorguları
* Port Taramaları
	- NMAP
* SMB bilgi toplama
* SMTP bilgi toplama
* SNMP bilgi toplama
* Aktif sistemleri tespiti
* Kullanılan portların tespiti
* Kullanılan OS bilgisi
* Kullanılan servis bilgisi
* Kullanulan uygulamaların tespiti
* Kullanılan Firewall, WAF vb cihaz bilgisi
* Brute force ile dizinlerin tespiti
* DNS istekleri ile subdomainlerin tespiti
* Zone transferi ile dns kayıtlarının elde edilmesi
* Ağ haritasının tespiti

# 3. Siber İstihbarat(CTI) Siteleri 

* Shodan
	- https://www.shodan.io/ 
* Censys
	- https://censys.io/ 
* Virustotal
	- https://www.virustotal.com/ 
* Netcraft
	- http://searchdns.netcraft.com/ 
* AlienVault
	- https://otx.alienvault.com 
* Spiderfoot
	- http://www.spiderfoot.net/ 
* Built With
	- https://builtwith.com/  
* Certificate Search: Pasif olarak subdomain listesi görüntülenebilir.
	- https://crt.sh/
* Archive Org: Web sitelerinin tüm yıllarda ki hallerini cache'sinde tutar ve incelememize izin verir.
	- https://archive.org/
* IntelligenceX
	- https://intelx.io/