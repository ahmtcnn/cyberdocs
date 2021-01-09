# Mobil Uygulama Güvenliği
Mobil uygulama güvenliği, saldırganın mobil uygulamayı kullanarak saldırı yapabileceği, kulllanıcılara ve backend sitemlere karşı güvenlik tehditleri oluştrabileceği durumların incelenmesidir. Bu incelemeler aşağıda belirtilen noktaları içerebilir;
- Uygulamanın hangi bilgileri depoladığı, hangi bilgilere eriştiği ve veri iletişimini nasıl yaptığı,
- Uygulama üzerinden şifrelenmiş verilerin decrypt edilebilirliği,
- Uygulamanın decompile edilebilmesi ve kodların incelenmesi,
- Elde edilebilien kodlar üzerinden dinamik testlerin gerçekleştirilmesi.

[Mobile Owasp Top 10 (2016)](https://owasp.org/www-project-mobile-top-10/) yayınına göre aşağıdeki maddeler incelenebilir:
- M1: Improper Platform Usage
    - Bu zafiyetler bildiğimiz Web Owasp 10 için geçerli olan zafiyetlerin mobil taraftan tetiklenmesini ifade eder. Herhangi bir api ile iletişimi olan bir mobil uygulama, bu zafiyetleri içerebilir. Örneğin mobil uygulama içerisinden, kontrolü sağlanmayan bir input değeri için XSS zafiyeti tespit edilebilir. 

- M2: Insecure Data Storage
    - Saldırganlar telefonu ele geçirdiğinde bilgisayar yardımı ve araçlar ile içerisindeki dosyalara ulaşabilir. Bu durumda uygulamaların kişisel bilgileri kaydetmesi bu bilgilerin çalınabilmesine olanak sağlar. 

- M3: Insecure Communication
    - Kullanıcıların network trafiğinin şifreli iletilmesi, araya girebilecek saldırganların oturum bilgileri veya parola bilgilerini çalmasını engeller. Phising ve MITM saldırılarını engellemek üzere SSL bağlantısı kullanılmalı ve zayıf SSL bağlantılarından kaçınılmalıdır.

- M4: Insecure Authentication
    -
- M5: Insufficient Cryptography
- M6: Insecure Authorization
- M7: Client Code Quality
- M8: Code Tampering
- M9: Reverse Engineering
- M10: Extraneous Functionality


Bu durumda mobil uygulama güvenliği testleri iki başlık altında incelenebilir.

# 1. Statik Analiz

# 2. Dinamik Analiz


# 3. Kaynakça
- https://www.synopsys.com/glossary/what-is-mobile-application-security.html
- https://owasp.org/www-project-mobile-top-10/
