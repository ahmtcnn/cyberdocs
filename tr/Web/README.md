# Web Uygulama Güvenliği

* Bu bölümde Web uygulaması enumeration araçları, ipuçları ve taktikler, istismar türleri anlatılmaya çalışılmıştır.

# Enumeration & Bilgi Toplama

### Web Sunucu Tip & Versiyon Tespit Etme

* Web sunucu bilgileri ve sürüm bilgileri belirlenerek web uygulamalarına yönelik saldırılar için yol haritası belirlenebilir. Sürümün neden olduğu güvenlik açıklarını hızlı bir şekilde tespit edebilmemiz için sunucu adı, sürüm bilgisinin öğrenilmesi gerekmektedir.

    - Web sunucusundan dönen **başlık bilgilerine** bakılabilir (**whatweb aracı**, **curl**, **tarayıcı incelemesi** vb. araçlar kullanılabilir.)
    - **Wappalyzer** aracı kullanılabilir. (chrome, mozilla eklentisi)
    - Web sunucusu portuna  **nmap** ile tarama yapılabilir.

### Kullanılan Web Teknolojileri

* Web sunucularında, hazır sistemlerde, frameworklerde veya güncellenmemiş sistemlerde çalışan uygulamalarda çeşitli kritik güvenlik açıkları oluşabilir. Bu açıdan hangi teknolojilerin kullanıldığını öğrenmek oldukça faydalı olabilir.

    - **Whatcms** aracı kullanılabilir. (online)
    - **Nikto** aracı kullanılabilir.
    - **Retirejs** aracı kullanılabilir. (güncel olmayan/zafiyetli js dosyalarını tespit etmek)
    - **Wappalyzer** tarayıcı eklentisi kullanılabilir.
    - Wordpress uygulamalarını taramak için **Wpscan** aracı kullanılabilir.
    - Joomla siteler için **Joomscan** aracı kullanılabilir.

### WAF Tespit Etme

* Web uygulaması bir web uygulaması güvenlik duvarının arkasında bulunuyorsa, bazı taramalar false pozitif sonuçlar verebilir, düzgün çalışmayabilir ve bu nedenle sağlıklı olmayabilir. Bu nedenle, bir güvenlik duvarının varlığı tespit edilirse, enumeration ve istismar aşamalarında farklı teknikler kullanılabilir.

    - **wafw00f** aracı kullanılabilir
    - Web sunucusu **header bilgileri** görüntülenebilir. (waf veya sunucu adı başlıklarda olabilir)
    - **Whatwaf** aracı kullanılabilir.
    - **Nmap**, ile banner grabbing yapılabilir.


### Ip History Araştırması
* Web uygulamaları doğrudan bulut hizmeti sağlayıcılarında barındırılmıyorsa,  WAF kullanımı için dns yönlendirmesiyle etkin olacaktır. Bu nedenle, istekler reverse proxy ile, WAF aracılığıyla gerçek sunucuya iletilir. Bu durumdaki yanlış yapılandırılmış sunuculara gerçek IP adresi kullanılarak erişilebilir. Bu noktada WAF baypas edilebilir. Gerçek ip adresi doğrudan veya dns host yapılandırma dosyalarıyla kullanılabilir. 

    - **https://securitytrails.com** web sitesi ip verilerini araştırma için kullanılabilir.
    - **https://www.virustotal.com/gui/** web sitesi araştırma için kullanılabilir.
    - **https://viewdns.info/iphistory/** web sitesi araştırma için kullanılabilir.


### Port Tarama
* Web uygulamasının çalıştığı portu tarayarak, banner grabbing yöntemi ile bilgi toplanabilir. Web uygulamasının işaret ettiği ip adresinin farklı portları açık olabilir. Web sunucusu bağlantı noktasını ve bilinen diğer bağlantı noktalarını birlikte incelemek faydalıdır. Farklı açık portlar, sunucu hakkında bilgi edinmemize yol açabilir.

    - **nmap**.
        -**- sS** ile Nmap, SYN taraması anlamına gelir. Bu seçenekler, bağlantı noktası durumu için daha doğru sonuçlar elde etmek için kullanılmalıdır.
        - ** - sV ** parametresi sürüm tespiti için kullanılır.
        - **-h** parametresi ile onlarca seçenek gözden geçirilebilir. (**https://nmap.org/book/man-briefoptions.html**)
    

### Dizin Taraması
* Ne kadar fazla içerik, fonksiyon kullanıcı etkileşimi varsa test edilecek ve zafiyet oluşturabilecek unsurlar o kadar fazla olabilir. Bu durumda tüm olası sayfaları bulmak, test sayfaları veya  açık bırakılmış içerikleri test edebilmek için dizin taramaları yapmak gerekir. Web uygulamalarının erişilebilir sayfaları, güvenlik açıklarını tarayabileceğimiz ve arayabileceğimiz içeriklerdir. Yapılandırma dosyalarına, şifresiz yönetim arayüzlerine ve site arşiv dosyalarına sunucuda erişilebiliyorsa, ciddi bilgi ifşası ve güvenlik açıklarına neden olabilir.

    - Crawlerlar, erişilebilir tüm sayfaları bağlantılardan çıkartmak için kullanılabilir. (**Burp Suite** aracı kullanılabilir)
    - Dizin bruteforce araçları kullanılabilir. (**Dirsearch**, **wfuzz**, **gobuster**, taramalar kullanılan wordlist kadar etkilidir.)
    - **robots.txt** dosyaları incelenebilir.
    - Platforma özel sayfalar kontrol edilebilir. Örneğin wordpress kullanılıyorsa, WP upload ve yapılandırma sayfalarını vb. taranabilir.


### Subdomain Taraması
* Hedef web sitesine ait birden fazla subdomain olabilir. Bu subdomainler aynı sunucuda host ediliyor veya abi endpointleri oluşturuyor olabilir. Tıpkı dizin taramaları gibi hedefe ait diğer subdomainleri kontrol etmek bilgi toplama/saldırı yüzeyini artırır. 
    
    - [Sublist3r](https://github.com/aboul3la/Sublist3r) aracı kullanılabilir. (DNS ve bruteforce tekniklerini kullanır.)
    - [Virustotal](https://www.virustotal.com/gui/) web uygulaması kullanılabilir.
    - [DNS Dumpster](https://dnsdumpster.com/) web aracı kullanılabilir.
    - [Amass](https://github.com/OWASP/Amass) aracı kullanılabilir.
    - Birçok aracın birleştirilerek sunulduğu [nmmapper](https://www.nmmapper.com/sys/tools/subdomainfinder/) kullanılabilir.
    - Herhangi kişisel yazılmış wordlist bazlı tarama aracı kullanılabilir. (Githubda onlarca araç bulunabilir.)

### Google Dorks
* Hedef web uygulamasında yayın yapılan dizinler ve dosyalar bilgi ifşasına yol açabilir. Bruteforce ve crawler yapmanın yanı sıra, google dorklarını kullanarak belirli format, isim, yazı içeren sayfalara hedef adresini kapsayacak şekilde aramalar yapılabilir. 

    - [Google Dorks](https://www.exploit-db.com/google-hacking-database)
    - [pentest-tools](https://pentest-tools.com/information-gathering/google-hacking#) web uygulamasında bazı bilindik google dorkları hazır olarak verilmiş. Örnek olarak kullanılabilir.

### Internal Ip/Path Disclosure (HTML Source Code Analysis)
* Hedef Web uygulamarında kaynak kodlarda unutulmuş veya geliştirme ortamında kullanılan sunucu ip adresleri kalmış olabilir. Bunun dışında bazı web sunucuları, HTTP/1.0 ile yapılan isteklere header bilgisi içerisinde domain adı değilde local ip adresleri ile cevap verebilir. Bu durum yerel ip adres bilgisi ifşası olarak değerlendirilebilir. Yerel ip adresleri kurum dışından bilinmezler. Bu durum saldırganın ağ katmanı saldırılarını gerçekleştirmesine yardımcı olabilir.

    - Web sayfaları kaynak kodları incelenebilir, tool yardımı ile regular expression kuralları uygulanarak ip yapıları filtrelenebilir. (Hazır tarama araçları bu şekilde çalışır)
    - SSL yoksa telnet ile bağlantı kurularak (telnet somesite.com 80) ```HEAD / HTTP/1.0``` ile istek yollanabilir.
    - SSL varsa openssl s_client -crlf -connect example.com:443 ile bağlantı kurularak aynı istek yollanabilir.

### Shodan Search
* Web uygulamaları için arama yapabilceğimiz arama motorları nasıl varsa, ( Google, Yandex vb.) internete bağlı tüm cihazlar içinde arama yapabileceğimiz (web uygulamaları dahil her şey) biz arama motoru vardır. Shodan. Hangi ip adresleri IIS sunucusu koşuyor, nerede ssh bağlantıları açık, rdp portu açık olan cihazlar, cisco kullanan cihazlar vb. bir çok aramanın yapılacağı bir arama motoru. Konu web olduğu için, shodan'ı bir web uygulamasının hangi portlarında hangi servislerin koştuğunun indexleri hakkında shodandan bilgi alabiliriz. Direkt olarak web uygulaması kullanılabilir. Veya indirerek shodan cli kullanılabilir.

    -   [Shodan](https://www.shodan.io/)

### Web Archive Search
* Wayback machine web uygulamalarının arşivini tutan, belirli zaman aralıklarıyla snapshot ını alan bir platform. Bir web uygulamasının önceki sürümleri incelenerek farklı fonksyionlarıni farklı dizinlerin varlığı tespit edilebilir farklı bilgiler toplanabilir. 

- [Web Archive](https://web.archive.org/)

### DNS Records
* Web uygulamasını işaret eden ip adreslerini, mail gateway, name server gibi bilgiler hakkında bilgi almak için dns sorguları kullanılabilir.
    - **Dig** aracı kullanılabilir.
    - **Nslookup** kullanılabilir.
    - **Fierce** aracı kullanılabilir.
    - **dnsenum** aracı kullanılabilir.
    - **https://dnsspy.io**/, **https://intodns.com/**, **https://www.digwebinterface.com/**, **https://dnsdumpster.com/** gibi web uygulamaları kullanıabilir.

# Exploitation 

### XSS
* XSS (Cross Site Scripting) Siteler arası betik çalıştırma zafiyeti, saldırganların hedef kullanıcı üzerinde, hedef kullanıcı tarafında javascript kodları çalıştırılmasını sağlayan bir zafiyettir. Saldırgan hedef kullanıcıya client tarafında js kodu çalıştırarak ne gibi zararlar verebilir? :
    - Alert basılabilir :)
    - Js çalıştırılması sonucu cookie bilgilerine erişilebilir. Bu bilgilere erişen js kodu ile birlikte herhangi bir yere bir istek gönderilebilir ve elde edilebilir.
    - Kullanıcının cookie bilgisini çalmadan, direkt kullanıcı tarafından yapılması istenilen istekler hedef sunucuya gönderilebilir.
    - Onkeypress eventi ile açılan sayfa üzerinde keylogger gibi bilgi toplanabilir istenilen adrese bu bilgiler gönderilebilir.
    - Daha anlatılamayan hayal gücüne veya web uygulaması içeriğine göre bir çok farklı senaryo bu zafiyet exploit edilebilir.
XSS çok popüler olduğundan dolayı burada aranacak şeyin payloadlar veya payload kaynakları olabileceği düşünüşmüştür.
    - [Porswigger XSS](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet) adresi kullnılarak hangi element ile hangi eventler tetiklenebilir ve örnekleri incelenebilir.
    - [Payload List](https://github.com/payloadbox/xss-payload-list) ilham alınabilir.
    - [İhtiyaca göre Payload list](https://github.com/ihebski/XSS-Payloads) kullanıabilir.
    - [Yetkili abiler](https://owasp.org/www-community/xss-filter-evasion-cheatsheet) incelenebilir.
    

### SQL Injection

### File Upload

### File Inclusion

### Command Injection

### Brute Force

### DNS Zone Transfer

### CSRF

### Host Header Injection

### SSL Encrytptions Vulnerabilities


### Kaynakça

https://portswigger.net/kb/issues/00600300_private-ip-addresses-disclosed
https://help.shodan.io/the-basics/what-is-shodan