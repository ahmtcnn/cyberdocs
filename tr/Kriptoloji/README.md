# Kriptoloji
# 1. AES (Advanced Encryption Standarts)(Gelişmiş Şifreleme Standartları)
## 1.1 AES Algoritmasının Tarihçesi:
* 1997 yılına kadar veri şifreleme standardı olarak DES Algoritması kullanılıyordu. Gelişen teknoloji ile birlikte DES Algoritmasının 64 bitlik anahtar uzayı güvenilirliğini yitirmeye başladı. Bu sebeple NIST (Ulusal Standartlar ve Teknoloji Enstitüsü) 1997 yılında yeni bir yarışma düzenlemiştir. 1998 yılında ilk turu gerçekleştirilen yarışmaya 15 farklı proje başvurmuştur, 1999 yılındaki ikinci tura ise sadece 5 proje kalmıştır. Toplamda 4 yıl süren değerlendirmeler sonucunda 2000 yılında Joan Daemen ve Vincent Rijmen tarafından tasarlanan Rijndael Algoritması Advanced Encryption Standard (AES) ismiyle NIST tarafından kabul edilmiştir.

## 1.2 AES Algoritmasının Yapısı:
* AES simetrik bir şifreleme algoritmasıdır. Yani hem şifreleme hem de şifre çözme işlemleri için aynı anahtar kullanılır. AES için girdi ve çıktı matrisleri 128 bit olmak zorundadır. Ama anahtar 128, 192 ve 256 bit olabilir.

![Durum Matirisi](/../../_media/Kriptoloji/AES/aes1.PNG)

* Tablo 1 ile gösterilen durum matrisinde her bir hücre 8 bit yer kaplamaktadır, 16 hücre bulunduğu için toplam 128 bitlik bir veriye karşılık düşer. Şifrelenecek mesaj ve anahtar durum matrisleri şeklinde düşünülerek üzerlerinde gerekli işlemler yapılır.
AES algoritması Bayt Değiştirme, Satır Kaydırma, Sütun Karıştırma ve Tur Anahtarı ile Toplama gibi adımların tekrar etmesi şeklinde düşünülebilir.
128 bit AES şifrelemesi için 10, 192 bit için 12, 256 için ise 14 tur sonunda şifrelenmiş mesaja ulaşılır.

![AES](/../../_media/Kriptoloji/AES/aes2.PNG)

## 1.3 Bayt Değiştirme
* Bayt değiştirme işlemi durum matrisindeki baytların farklı baytlara dönüştürülmesi işlemidir. Bu dönüşüm daha önceden belli bir lookup table üzerinden yapılır. Örnek bir tablo aşağıda verilmiştir. Örneğin bayt değiştirme yapılacak olan değer 0x37 olsun, bayt değiştirme sonrası bu değer 0x9A (sbox’ın 0x37. değeri) değerine dönüşür.

![SBox](/../../_media/Kriptoloji/AES/aes3.PNG)

![Bayt değiştirme öncesi ve sonrası durum matrisi](/../../_media/Kriptoloji/AES/aes4.PNG)

## 1.4 Satır Kaydırma

* Satır kaydırma işlemi bayt değiştirme işleminden sonra oluşan yeni durum üzerine uygulanır. Durum matrisindeki satırların belli değerde sola kaydırılması anlamına gelir.

![Satır Kaydırma](/../../_media/Kriptoloji/AES/aes5.PNG)

![Satır Kaydırma Önce ve Sonrası](/../../_media/Kriptoloji/AES/aes6.PNG)

## 1.5 Sütun Karıştırma
* Sütun karıştırma işlemi satır karıştırma adımında oluşan durum matrisinin her sütunun ayrı ayrı belli bir matris ile çarpılması ve ortaya çıkan matrisin yeni sütun olarak kullanılmasıdır.

![Sütun Karıştırma İşlemi](/../../_media/Kriptoloji/AES/aes7.PNG)

* Eğer çıkan sonuç 8 bit'ten büyük olursa, çıkan sonucun indirgenmesi gerekir. Örneğin;
* 0xd4 * 0x02 = 11010100 * 00000010 = (x7+x6+x4+x2)* (x) = x8+x7+x5+x3
* Görüldüğü gibi burada bulunan değer en az 9 bit ile ifade edilebilir. Bu nedenle sonucun 8. dereceden indirgenemez bir polinom(m(x)) ile modu alınmalıdır. Bu polinomun böleni tektir ve sadece kendisidir
* m(x)=x8+x4+x3+x+1= 100011011
* Mod işlemi recursive olarak m(x) fonksiyonunun modu alınacak sayının en yüksek dereceli basamağına kadar kaydırılması ve exorlanması ile gerçekleştirilir. Recursive işlemlerin son bulacağı şart ise çıkan sonucun 8 bit ile ifade edilebildiği noktadır.
0xd4* 0x02 =x8+x7+x5+x3= 110101000

![Mod işlemi](/../../_media/Kriptoloji/AES/aes8.PNG)

* Bu örnekte mod işlemi tek iterasyonda tamamlandı ancak bazı örneklerde bu durum birkaç iterasyon sürebilir, ayrıca yeni sütundaki her bir bayt için ayrı ayrı 4 çarpma ve toplama işlemi olduğu için en kötü durumda her çarpmadan sonra mod işlemi uygulamak maliyeti artırmaktadır.
Maliyeti düşürmek için mümkün tüm durumlar daha önceden hesaplanıp bir lookup table üzerinde tutulur. 

## 1.6 Tur Anahtarı ile Toplama
* Her turun sonunda bulunan mesaj o anki tur anahtarı ile toplanır. Her turda farklı bir anahtar kullanıldığı için tur sayısı kadar yeni anahtar gereklidir. Aşağıda 10 turluk bir AES 128 algoritmasında gerekli anahtar tablosunun bir kısmı gösterilmiştir.

![Genişletilmiş Örnek Anahtar Tablosu](/../../_media/Kriptoloji/AES/aes9.PNG)

* 4. sütun 2. anahtarın başlangıç noktasını ifade eder. 128 bitlik AES Algoritması için 11 adet farklı anahtara ihtiyaç vardır. Bunlardan ilki(belirlenen anahtar) en başta mesaj ile toplanır. Geriye kalan anahtarlar ilk anahtar yardımıyla üretilir ve her tur sonunda oluşan mesaj üzerine eklenir. 

## 1.7 Anahtarın üretilmesi

* AES algoritması anahtarı alır ve bir dizi işlemden geçirdikten sonra döngü sayısı kadar anahtar üretir.Bu sebeple her turda farklı anahtar döngüye katılır.128 bit uzunluk için 10 döngü oluştuğu varsayılırsa 10 farklı anahtardan söz edilebilir. Akabinde şifre çözülürken ilk anahtar, 10.döngüdeki tur anahtarı olur.

![İşlemler Döngüsü](/../../_media/Kriptoloji/AES/aes10.PNG)

* Yeni anahtarın oluşturulmasındaki temel işlem bir önceki sütun ile 4 önceki sütunun toplanmasıdır. İstisnai olarak,  4'ün katı olan her sütunda toplamadan önce bir işlem dizisi (T işlemi) uygulanır.Bu işlem; öteleme, s kutusundan geçirme ve Rc(x) vektörü ile toplama işlemidir. Rc(x) vektörü aşağıda verilmiştir. Örneğin, yeni oluşturulacak anahtarın ilk sütunu için konuşursak, bir önceki sütun,önceki anahtarın son sütunudur. 4 önceki sütun ise eski anahtarın ilk sütunudur. T işlemi evrelerinde 1 önceki sütun önce yukarı 1 ötelenir, sonra s kutusundan değişim yapılır ve Rc vektörünün ilgili indisiyle toplanır. T işlemi tamamlanınca da 4 önceki sütun ile toplanarak yeni anahtarın ilk sütunu olarak anahtar durum matrisine yazılır.

![RC Tablosu](/../../_media/Kriptoloji/AES/aes11.PNG)

## 1.8 Deşifreleme

* Deşifreleme işlemi yapılan işlemleri ters sıralama ile yapılmasıdır. Ters Bayt Değiştirme, Ters Satır Kaydırma, Ters Sütun Karıştırma ve Tur Anahtarıyla Toplama adımlarını içerir. Ancak Tur Anahtarıyla Toplama adımı genişletilmiş anahtarın içerisindeki son anahtardan başlayarak geriye doğru ilerler. Yani şifreleme için kullandığımız son anahtar deşifreleme için kullandığımız ilk anahtar olur.

* Ters bayt değiştirme işlemi için bayt değiştirme işleminde olduğu gibi bir lookup table’dan faydalanılır. Bu tablodaki veriler bayt değiştirme tablosundaki verilerin tersleridir. Örneğin 0x00 değerinin bayt değiştirme tablosundaki karşılığı 0x63 iken, 0x63 değerinin ters bayt değiştirme adımındaki değeri 0x00’dır. Aşağıda örnek bir ters bayt değiştirme tablosu görülmektedir.

![Ters SBox Tablosu](/../../_media/Kriptoloji/AES/aes12.PNG)

* Ters satır kaydırma adımında, satır kaydırma adımında yapılan işlemler sağa kaydırılarak tekrarlanır.

![Ters SBox Tablosu](/../../_media/Kriptoloji/AES/aes13.PNG)

## 1.9 Ters Kaydırma İşlemi
* Ters sütun karıştırma adımında ise yine sütun karıştırma adımına benzer işlemler yapılır ancak bu kez aşağıdaki matris kullanılır.

![Ters Sütun Karıştırma](/../../_media/Kriptoloji/AES/aes14.PNG)