# Mobil Uygulama Güvenliği
Mobil uygulama güvenliği, saldırganın mobil uygulamayı kullanarak saldırı yapabileceği, kulllanıcılara ve backend sitemlere karşı güvenlik tehditleri oluştrabileceği durumların incelenmesidir. Bu incelemeler aşağıda belirtilen noktaları içerebilir;
- Uygulamanın decompile edilebilmesi ve kodların incelenmesi,
- Uygulamanın hangi bilgileri depoladığı, hangi bilgilere eriştiği ve veri iletişimini nasıl yaptığı,
- Uygulama üzerinde şifrelenmiş verilerin  ve transfer edilen verilen decrypt edilebilirliği,
- Elde edilebilien kodlar üzerinden dinamik testlerin gerçekleştirilmesi.

[Mobile Owasp Top 10 (2016)](https://owasp.org/www-project-mobile-top-10/) yayını incelenerek daha detaylı bilgilere ulaşılabilir.

# 1. Android (apk) Analizi

## 1.1 APK dosyasının elde edilmesi/yüklenmesi ve bilgi toplama
- **Genymotion vb. emülatör'e veya fiziksel telefona apk uygulamasının yüklenmesi**

    - Genymotion üzerinde android bir cihaz oluşturulması/çalıştırılması
    - ilgili apk yı google playden, müşteriden veya [APKpure](https://apkpure.com/), [apkmirror](https://www.apkmirror.com/) [apk-dl](https://apk-dl.com/) sitelerinden veya [PlayStoreDownloader](https://github.com/ClaudiuGeorgiu/PlaystoreDownloader) aracı ile  elde ettikten sonra emülatöre/telefona indirilmesi.
    - apk dosyası elimizde ise [adb](https://www.xda-developers.com/install-adb-windows-macos-linux/) aracı ile (adb install example.apk) telefona indirilebilir. Genymotion emülatörün üzerine sürükle bırak yardımı ile yüklenebilir.
    - Eğer apk bir şekilde telefona yüklendi (örn:google play) ancak elimizde apk dosyası yok ise **"adb shell pm list packages -f"** komutu ile çalışan android cihaz üzerindeki tüm paketleri görüntüleyebiliriz. Örnek paket isimleri "com.package_name" gibi listelenecektir. (pipe, grep ile uygulama ismi filtrelenebilir.) Burada aradığımız uygulamanın paket adını bulduktan sonra **"adb shell pm path com.ornekpaketismi"** ile dosya dizinini tespit edebilir, **"adb pull /data/app/com.package_name..apk"** ile apk dosyasını bilgisayarımıza indirebiliriz.

- **APK Dosya analizi/tersine mühendislik**
    - Apk (Android Package Kit) dosyaları içerisinde uygulama ile ilgili dosyaları barındıran zip, rar benzeri bi paketlemedir.
    - [apktool](https://ibotpeaches.github.io/Apktool/) aracı ile **"apktool d örnek.apk"** komutunu kullanarak **AndroidManifest.xml**, bazı kaynak dosyaları ve assets bilgilerine ulaşılabilir. 
    - [dex2jar](https://github.com/pxb1988/dex2jar/releases/tag/2.0) aracı ile **"dex2jar örnek.apk"** komutu ile apk dosyalarını .jar dosyalarına çevirerek  [JD-Gui](http://java-decompiler.github.io/) aracını kullanarak açabiliriz. Veya apk uzantısını zip haline getirerek içerisindeki .dex uzantılı dosyalarını JD-Gui ile açabiliriz. Bu durumda android için yazılmış java kodlarını görmek mümkün olabilir.
    - [Jadx]
    - [MobSF](https://github.com/MobSF/Mobile-Security-Framework-MobSF) Framework ü kullanılarak otomatize statik analiz adımları sağlanabilir. MobSF bir çok statik analiz adımını otomatize olarak, kolay anlaşılabilir bir arayüz ile bizlere sunar.
    - [Androbug](https://github.com/AndroBugs/AndroBugs_Framework) aracı kullanılarak MobSF benzeri statik analiz adımlarını otomatize hale getirilebilir.
    - [staCoan](https://github.com/AndroBugs/AndroBugs_Framework) aracı kullanılarak yine apk dosyalarından java kodları elde edilmeye çalışabilir, araç aynı zamanda "key, url, password" vb. keywordlerin yerlerini tespit ederek kolaylıkla incelenmesine olanak tanır.
    - Uygulamanın açılması, kullanılması, veri alışverişi yapılması sonrasında dinamik olarak kaydedilen bilgileri manuel olarak test etmek gerekir. Bu durumda **"adb.exe shell"** komutu ile çalışan telefona/emülatöre bağlanarak "/data/data/paket_adı" yolu takip edilerek kaydedilen tüm string db ve cache bilgileri hassas bilgiler içerme olasılığına karşı incelenmelidir.

## 1.2 Network Analizi

- Burp Proxy ayarlanması
    - Burp sertifikasının export edilip adb ile cihaza yüklenmesi : **"adb push “C:\test.sertifika “/sdcard/”"**
    - Android cihaz üzerinde Settings > additional settings > privacy > certificates >install ile sertifikanın seçilerek yüklenmesi
    - wifi ayarlarından proxy eklenerek burp proxy ilgili ip ve portu işaret edilmesi
    - Burp tarafında **"all interface"** seçeneği ile ilgili portu dinlemek
- SSL pinning bypass edilmesi
    - 

# 2. IOS Analizi


# 3. Kaynakça
- https://www.synopsys.com/glossary/what-is-mobile-application-security.html
- https://owasp.org/www-project-mobile-top-10/
- https://mobexler.com/checklist.htm
