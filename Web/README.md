# Getting Started

# Enumeration & Information Gathering

### Web Server Type & Version Detection

    Web sunucu bilgisi ve versiyon bilgilerini tespit ederek web uygulamalarına yönelik yapılacak saldırılar için yol haritası belirlenebilir. Özellikle versiyondan kaynaklı zafiyetleri hızlıca tespit etmemiz için sunucu adı ve versiyon bilgisini öğrenmek gerekir. Peki web sunucu bilgisini nasıl öğrenebiliriz.
    - Web sunucudan dönen başlık bilgilerine bakarak ( whatweb aracı, curl, browser üzerinden görüntüleme vb araçlar kullanılabilir.)
    - Wappalyzer tool kullanılabilir. (chrome, mozilla eklentisi)
    - nmap ile ilgili web sunucu portuna tarama yapılabilir. (-sSVC parameteresi tavsiye edilir.)
    - nmap ile os detection yapılarak tahmin yürütülebilir.

### Web Technologies in Use

    Web sunucular üzerinde çalışan uygulamalarda, hazır sistemlerde veya frameworklerde güncellenmemiş sistemlerde çeşitli kritik zafiyetler meydana gelebilir. Bu açıdan hangi teknolojiler kullanılıyo öğrenmek oldukça işe yarayabilir. Peki uygulama üzerinde çalışan, kullanılan teknolojileri nasıl öğrenebiliriz?
    - whatcms aracı kullanılabilir. (online)
    - nikto aracı kullanılabilir.
    - retirejs eklentisi kullanılabilir. (güncel olmayan js dosyalarını tespit edebilmek adına)
    - wappalyzer kullanılabilir
    - Wordpress uygulamalarını taramak için wpscan kullanılabilir.
    - Joomla siteler için joomscan kullanılabilir.
### Firewall Detection

### Ip History Search

### Port scan

### Directory Search

### Subdomain Search

### Google Dorks

### Internal Ip/Path Disclosure (HTML Source Code Analysis)

### Shodan Search
!> **Time** is money, my friend!
### Web Archive Search

# Exploitation 

### XSS

### SQL Injection

### File Upload

### File Inclusion

### Command Injection

### Brute Force

### DNS Zone Transfer

### CSRF

### Host Header Injection

### SSL Encrytptions Vulnerabilities