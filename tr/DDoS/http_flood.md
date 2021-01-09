#  HTTP Flood Saldırısı
HTTP Flood saldırıları web sunucuya tamamen normal istekler yaparak, yoğun trafik sonucu kaynakların tüketilmesini hedefleyen saldırılarıdır. GET ve POST methodları kullanılabilir. Burada amaç kaynak tüketimi olduğu için web uygulaması üzerinde biraz bilgi toplama aşaması DDoS saldırısını başarıya iletebilir. Web uygulamalarının bazı fonksiyonları çok kaynak tüketmeden hızlıca cevap verebilirken bazıları işlem yaparak, sorgu yaparak kaynak tüketimi yaparlar. Bu durumda bu fonksiyon veya sayfalara karşı HTTP Flood saldırını başlatmak verimi artırabilir saldırı sonucunu değiştirebilir. 

## HTTP Flood Araçları

- [GoldenEye](https://github.com/jseidl/GoldenEye) araci  kullanılabilir.
- [HTTPFlood](https://github.com/Leeon123/golang-httpflood) aracı kullanılabilir.
- [stressthem](https://www.stressthem.to/) web uygulaması kullanıabilir (NOT FREE)
- [HULK](https://github.com/grafov/hulk) aracı kullanılabilir.


#  HTTP Flood Önleme/Önlemler
- HTTP Flood saldırıları normal insan trafiği gibi görünebileği için direkt ve sert önlemler almak normal trafik akışını da etkilecektir. Bu durumda web uygulamaları üzerinde güvenlik sorular vb. challengelar kullanılabilir. Anti DDoS mekanizmaları kullanarak ip reputation check, (zararlı bilinen iplerin blocklanması), trafik profiling vb. teknikler kullanılabilir.