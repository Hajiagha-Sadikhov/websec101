### Ek Adım: API Güvenliği – Modern İletişimin Kalkanı

Artık web güvenliği yolculuğunda ciddi bir mesafe kat ettin. Son olarak, modern uygulamaların bel kemiğini oluşturan **API güvenliğine** eğilelim. Mobil uygulamalar, tek sayfa uygulamaları (SPA), IoT cihazları, mikro servis mimarileri—hepsi API’ler üzerinden konuşuyor. Bu yüzden API güvenliği, genel güvenlik stratejinin kritik bir parçası.

---

### API Güvenliğinin Önemi

Klasik web uygulamalarında sunucu, HTML’i oluşturup istemciye gönderirken, modern yapılarda çoğunlukla istemci (örn. mobil uygulama) minimal bir frontend ile API’lere istek atar ve JSON, XML gibi ham verileri alarak kendi arayüzünde işler. Bu mimari esneklik sağlarken, saldırganlar için de yeni yüzeyler oluşturur.

**Kritik Nokta:** Bir API’yi hedef alan saldırgan, genelde arkadaki veri tabanına ve diğer servis bileşenlerine daha direkt bir yol bulmaya çalışır. Kimlik doğrulama, yetkilendirme, veri doğrulama, hız sınırlama (rate limiting) gibi konular burada öne çıkar.

---

### API Güvenlik Zafiyetleri

**1. Broken Object Level Authorization (BOLA):**  
En sık rastlanan sorunlardan biri. Kullanıcı kimliği doğrulansa bile ilgili kaynağa erişme yetkisi yoksa engellenmesi gerekir. Eksik yetkilendirme kontrolü, bir kullanıcının başkasına ait kayıtlara erişmesine neden olabilir.

**2. Broken User Authentication:**  
API uçları bazen mobil veya farklı istemcilerden erişildiği için kimlik doğrulama zayıflıkları kritik hale gelir. Doğrulama token’larının çalınması, süresiz geçerli oturumlar ya da eksik 2FA gibi konular büyük risk taşır.

**3. Excessive Data Exposure:**  
API’ler bazen istemcinin ihtiyacından fazla veri döner. Saldırganlar bu fazla veriyi (örn. hassas kullanıcı bilgilerini) görebilir. “Backend for Frontend” (BFF) gibi modellerle, sadece gerekli veriyi dönen bir katman tasarlamak şarttır.

**4. Rate Limiting Eksikliği (DoS/DDoS Saldırıları):**  
Saldırgan binlerce isteği hızlıca API’ye fırlatarak sistemi yavaşlatabilir veya çökertmeye çalışabilir. Rate limiting ve throttling mekanizmaları bu tür saldırıları önler.

**5. Injection ve Input Validation Eksiklikleri:**  
SQLi, XSS, Command Injection gibi klasik sorunlar API’lerde de geçerlidir. Kullanıcıdan gelen her veriyi mutlaka filtrele, doğrula ve gerekirse sanitize et.

---

### En İyi Uygulamalar

**1. Kimlik Doğrulama ve Yetkilendirme Standartları:**  
- **OAuth 2.0, OpenID Connect:** Üçüncü taraf uygulamalar için güvenli yetki devri.  
- **JWT (JSON Web Tokens):** Kullanıcı kimliğinin kanıtlanması için hafif ve güvenli bir yöntem.  
- Token ömürlerini kısıtla, refresh token mekanizmalarını doğru uygula.

**2. Input Validation ve Output Encoding:**  
- API’ye gelen her veriyi şüpheyle karşıla.  
- JSON şemasına göre veri doğrulaması (validation) yap.  
- Gerekliyse output encoding uygula.

**3. Rate Limiting, Throttling, WAF Entegrasyonları:**  
- API Gateway veya load balancer üzerinden gelen istek sayısını sınırla.  
- Ani istek patlamalarına karşı alarm mekanizmaları kur.  
- WAF kurallarıyla şüpheli istekleri engelle.

**4. Güvenli İletişim (HTTPS) ve Şifreleme:**  
- Tüm veri alışverişini TLS üzerinden yap.  
- Hassas verileri sunucu tarafında ya da veritabanında şifrele.

**5. İzleme, Loglama ve Anomali Tespiti:**  
- API çağrılarını logla, kim neye ne zaman erişiyor bil.  
- Anormal istek pattern’larını tespit eden araçlar kullan.

---

### Örnek Araçlar ve Platformlar

- **[OWASP API Security Top 10](https://owasp.org/www-project-api-security/):** API güvenlik risklerinin en güncel listesi.  
- **API Gateway Çözümleri (AWS API Gateway, Kong, Apigee):** Kimlik doğrulama, rate limiting, logging ve izleme gibi özellikler sunarlar.  
- **[API Security Testing Tools](https://apisec.ai/), [42Crunch](https://42crunch.com/):** Otomatik API güvenlik testleri, OpenAPI/Swagger dokümanlarını tarama.

Ayrıca, bug bounty platformlarında API odaklı programlar da vardır. Buralarda API güvenlik pratiklerini gerçek dünyada deneyerek becerilerini keskinleştirebilirsin.

---

### Kapanış

API güvenliği, modern uygulamaların kırılgan noktasını oluşturuyor. Mobil, web veya mikro servis tabanlı mimarilerde, API’ler hem birleştirici hem de potansiyel birer açık kapıdır. Bu nedenle kimlik doğrulamadan veri doğrulamaya, rate limiting’den log analizine kadar her aşamada güvenlik önlemlerini tasarımın bir parçası yapmalısın.

Artık elinde, web güvenliği, bulut güvenliği, DevSecOps ve API güvenliği ile ilgili geniş bir bakış açısı var. Bu bilgilerle, ister bir bug bounty avcısı ister bir güvenlik mühendisi ol, sistemi daha güvenli hale getirecek araçlara ve yaklaşımlara sahipsin.

Unutma, öğrenme devam eden bir süreç. Yeni teknolojiler, yeni saldırılar, yeni savunma yöntemleri ortaya çıktıkça sen de kendini güncelle. Yolun açık olsun!
