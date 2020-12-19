# Denial Of Service Attacks (DoS) - Hizmet Reddi Saldırıları
* Hizmet reddi saldırıları, uygulma veya sunuculara aşırı istek ve yük bindirerek kaynak tüketimini artırarak cevap veremez hale getirmektir. Herhangi bir sunucu, uygulama, port, iot cihazı vb. akla gelebilecek her türlü hizmet sağlayan bir ürüne Hizmet Reddi saldırıları gerçekleştirilebilir. Günümüzde en yaygın kullanım alanı web uygulamaları ve sunuculardır. Farklı katmanlarda protokollerin çalışma prensibine göre farklı yaklaşımlarla gerçekleştirilebilir.

# Syn Flood Saldırıları 
* Syn flood saldırıları, TCP handshake mekanizmasının sömürülmesi ilkesine dayanır. Normalde bir TCP bağlantısı aşağıdaki gibi gerçekleşir:
    - İstemci sunucuya bağlanmak için SYN paketi yollar. 
    - Sunucu bu pakete karşılık SYN+ACK paketi ile cevap verir ve bu bağlantı ile ilgili Transimision Control Block (TCB) denilen bir veri yapısı **oluşturur.** Bu yapılar SYN Backlog denilen alanda saklanır. TCP Backlog da sunucu üzerinde hafıza (memory) içerisinde tutulur, alanı kısıtlıdır.
    - İstemci SYN-ACK paketine karşılık ACK paketi yollar ve three way handshake tamamlanır artık veri alışverişi başlayabilir ve TCP Backlog içerisinde var olan bu bağlantıya ait node silinebilir.

* Syn flood saldırılarında gerçekleşen senaryoya bakacak olursak:
    - İstemci sunucuya bağlanmak için kaynak ip adresi değiştirilmiş (spoofed) SYN paketi yollar. 
    - Sunucu bu pakete karşılık SYN+ACK paketi ile cevap verir ve bu bağlantı ile ilgili Transimision Control Block (TCB) denilen bir veri yapısı **oluşturur.**
    - Sunucunun yolladığı SYN-ACK paketi istemciye ulaşmaz çünkü kaynak ip adresi değiştirilmiştir. Ancak sunucu bu bağlantıya ait ACK paketini bekler. Bu durumda bağlantı half-open  durumda yani yarı açık durumda kalır.
    - İstemci sürekli olarak bu isteği farklı kaynak ip adresleri ile devam ettirerek sunucunun TCP Backlog alanını doldurur. Bu durumda sunucu artık gelen istekleri reddeder ve sunucuya erişim kesilir.

## Araçlar

    - ### hping

# test3

## test5