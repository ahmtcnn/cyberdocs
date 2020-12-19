# Denial Of Service Attacks (DoS) - Hizmet Reddi Saldırıları
* Hizmet reddi saldırıları, uygulma veya sunuculara aşırı istek ve yük bindirerek kaynak tüketimini artırarak cevap veremez hale getirmektir. Herhangi bir sunucu, uygulama, port, iot cihazı vb. akla gelebilecek her türlü hizmet sağlayan bir ürüne Hizmet Reddi saldırıları gerçekleştirilebilir. Günümüzde en yaygın kullanım alanı web uygulamaları ve sunuculardır. Farklı katmanlarda protokollerin çalışma prensibine göre farklı yaklaşımlarla gerçekleştirilebilir.

# 1. Syn Flood Saldırısı
* Syn flood saldırıları, TCP handshake mekanizmasının sömürülmesi ilkesine dayanır. Normalde bir TCP bağlantısı aşağıdaki gibi gerçekleşir:
    - İstemci sunucuya bağlanmak için SYN paketi yollar. 
    - Sunucu bu pakete karşılık SYN+ACK paketi ile cevap verir ve bu bağlantı ile ilgili Transimision Control Block (TCB) denilen bir veri yapısı **oluşturur.** Bu yapılar SYN Backlog denilen alanda saklanır. TCP Backlog da sunucu üzerinde hafıza (memory) içerisinde tutulur, alanı kısıtlıdır.
    - İstemci SYN-ACK paketine karşılık ACK paketi yollar ve three way handshake tamamlanır artık veri alışverişi başlayabilir ve TCP Backlog içerisinde var olan bu bağlantıya ait node silinebilir.

    ![SYN Image](../../_media/syn.png)


* Syn flood saldırılarında gerçekleşen senaryoya bakacak olursak:
    - İstemci sunucuya bağlanmak için kaynak ip adresi değiştirilmiş (spoofed) SYN paketi yollar. 
    - Sunucu bu pakete karşılık SYN+ACK paketi ile cevap verir ve bu bağlantı ile ilgili Transimision Control Block (TCB) denilen bir veri yapısı **oluşturur.**
    - Sunucunun yolladığı SYN-ACK paketi istemciye ulaşmaz çünkü kaynak ip adresi değiştirilmiştir. Ancak sunucu bu bağlantıya ait ACK paketini bekler. Bu durumda bağlantı half-open  durumda yani yarı açık durumda kalır.
    - İstemci sürekli olarak bu isteği farklı kaynak ip adresleri ile devam ettirerek sunucunun TCP Backlog alanını doldurur. Bu durumda sunucu artık gelen istekleri reddeder ve sunucuya erişim kesilir.

## 1.1 SYN Flood Araçları

*  [hping3](https://github.com/antirez/hping)
*  [nping](https://github.com/nmap/nmap/tree/master/nping)
*  [scapy](https://github.com/secdev/scapy) (python kütüphanesi)
    - [örnek araç](https://github.com/EmreOvunc/Python-SYN-Flood-Attack-Tool.git)

## 1.2 SYN Flood Engelleme/Önlemler
   
- **Filtreleme**:  Router a bir paket geldiğinde, o paketin kaynağını doğrulamak üzere erişmeye çalışır. Eğer o kaynağa erişemiyorsa bunun bir saldırı olma ihtimali yüksek demektir. Bu durumdaki paketlerin kaynak ip adresi engellenerek saldırı engellenmeye çalışılabilir. Ancak efektif bir yöntem değildir. Spoof edilen kaynak ip adresleri erişilebilir de olabilir. 

- **Backlog size** : Eğer sunucunun Backlog alanı hızlı bir şekilde doluyorsa Backlog size genişletilebilir. Bu durumda çok daha fazla bağlantı kaydedilebilir hale gelir ve Backlog alanın dolması biraz daha uzun sürer. Ancak bu çözüm tek başına etkili olmaz. Daha yüksek trafik ile saldırı sonucunda başarısız olunabilir.
- **SYN-RECEIVED Time** : Sunucu SYN-RECEIVED durumunda varsayılan olarak belirli bir süre bekler. (Eğer SYN-ACK gelmezse Backlog içerisinde) Bu süre azaltılarak spoof edilen ip lerin Backlog alanını işgal etmesi daha kısa zamana indirgenebilir ve yeni bağlantılar için kısa zamanda yer ayrılabilir. Ancak bu durumda gerçek kullanıcıların bağlantıları etkilenebilir. Ağ hızında yavaşlık olması durumunda gerçek bir kullanıcı bu ayardan etkilenerek bağlantı kuramayabilir.
- **Recycling half-opened PCBs**: Backlog alanı dolduğu zaman yeni bir bağlantı alınması için hafızada tutulan SYN-RECEIVED durumundaki bir bağlantının time-out olması gerekir. Bu yöntemde ise diğer bağlantıların timeout olması beklenmeden, eğer Backlog full ise en eski Half-open durumundaki connection bırakılarak yenisi alınır. Eğer saldırı hızı yüksek ise veya Backlog alanı küçük ise bu yöntem başarısız olabilir.
- **SYN Cache** : SYN Cache, gelen paketlerin kaydının tamamen RECEIVED SYN Transimision Control Block (TCB) ile değilde daha küçük bir bilgi ile kaydedilmesini sağlar. Tüm bağlantı sağlanana kadar TCB oluşturulmaz. Gelen SYN paketinden gizli bir bit seçilir, ip adresi ve port numarası ile hashlenir. Bu hash, SYN Cache tekniğinde oluşturulan, half-open bağlantılar için kullanılan tabloya kaydedilir. Her hash bilgisi için belli bir alan vardır ve bu alan dolduğunda en eski hash kaydı silinir. Eğer bu hash bilgilerine ait herhangi birinin bağlantısı tamamlanırsa (3 way handshake) bu bağlantı bilgisi artık Full TCB alanına taşınabilir. 
- **SYN Cookies**: 
    






# Referanslar
- https://www.imperva.com/learn/ddos/syn-flood/  
- https://tr.wikipedia.org/wiki/SYN_sald%C4%B1r%C4%B1s%C4%B1  
- https://www.cloudflare.com/learning/ddos/syn-flood-ddos-attack/
- https://www.ionos.com/digitalguide/server/security/syn-flood/
- https://web.cs.hacettepe.edu.tr/~abc/teaching/bil656/presentations/SerhatTurkmen.pdf
- https://www.net.in.tum.de/fileadmin/TUM/NET/NET-2019-06-1/NET-2019-06-1_14.pdf
- https://sites.google.com/site/sireeshajakku/networking/tcp/syn-attach-mitigation
- https://tools.ietf.org/html/rfc4987#section-3.4   
- https://www.youtube.com/watch?v=ymttSrEo0R0