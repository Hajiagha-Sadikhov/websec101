### Ek Adım: Token Tabanlı Kimlik Doğrulama ve Güvenlik

Artık güvenliğin pek çok boyutunu inceledik. Şimdi biraz da **token tabanlı kimlik doğrulama** konusuna bakalım. Token’lar, API’lere ve diğer kaynaklara erişimi denetlemek için son derece yaygın bir yöntem haline geldi. Özellikle mikro servisler, mobil uygulamalar, SPA’ler ve sunucusuz (serverless) mimarilerde token tabanlı doğrulama, geleneksel "session cookie" tabanlı yöntemlerin yerini alıyor.

---

### Token Nedir?

Kısaca ifade etmek gerekirse **token**, kullanıcının kimliğini ya da yetkilerini temsil eden bir “jeton” gibidir. Bu jetonu sunarak API’lere veya kaynaklara erişirsin. En önemli fark, session cookie’lerinde olduğu gibi sunucu tarafında durum (state) tutma zorunluluğunun olmamasıdır.

- **Stateless Doğrulama:**  
  Sunucu tarafında kullanıcıya ait bir session kaydı tutulmaz. Token içindeki bilgileri okuyarak (örneğin JWT ile) her istekte kullanıcının kimliğini ve yetkilerini doğrulayabilirsin.

---

### Yaygın Token Türleri

**1. JSON Web Token (JWT):**  
Header, Payload ve Signature kısımlarından oluşan bir yapıdır. Base64URL ile encode edilir. JWT, payload kısmında kullanıcı ID, yetkiler, token süresi gibi bilgileri taşır ve imza (signature) kısmı ile değiştirilemez olması sağlanır.

**2. OAuth 2.0 Access ve Refresh Token’ları:**  
- **Access Token:** Kısa ömürlüdür. API erişim izni sağlar.  
- **Refresh Token:** Access token süresi bittiğinde yeni bir access token almak için kullanılır. Uzun ömürlüdür ama çok kritik bilgileri içermediğinden yine risk kontrollüdür.

**3. HMAC ve Signed Token’lar:**  
JWT haricinde, özel formatta hazırlanmış ve imzalanmış token’lar da kullanılabilir.

---

### Token Kullanımında Dikkat Edilmesi Gerekenler

**1. Gizlilik ve Saklama Yeri:**  
Token’lar hassas bilgidir. Onları tarayıcıda `localStorage`’da saklamak XSS olduğunda risk yaratabilir.  
- Öneri: Token’ı HttpOnly cookie olarak gönder ki JavaScript ile okunamasın.  
- Eğer localStorage kullanılacaksa, XSS’i minimuma indirmek için CSP, input validation gibi önlemler al.

**2. Ömür Süresi ve Yenileme Mekanizması:**  
Access token’ları kısa ömürlü tut. 5-15 dakikalık bir süre normaldir. Süre bittiğinde Refresh Token kullanarak yenile. Bu sayede çalınsa bile etkisi az sürer.

**3. İmza Doğrulaması ve Anahtar Yönetimi:**  
JWT imzasını doğrulamak için güvendiğin bir ortak anahtar (public key) sistemi kur. Private key’i güvende tut. Anahtar rotasyonu yaparak periyodik olarak imza anahtarlarını değiştir.

**4. Scope ve Yetkilendirme:**  
Token’ın içinde kullanıcının hangi kaynaklara erişebileceği tanımlanmalı. Çok geniş yetkiler vermek yerine, her token’ın kapsamını (scope) minimal tut.

**5. Token İptali (Revocation):**  
Bir token çalındığında veya kullanıcının erişimini iptal etmek istediğinde bunu yapabilmelisin. Blacklist mekanizması, token revocation endpoint’leri veya kısa süreli token’lar bu sorunu hafifletir.

---

### Pratik Öneriler

- **OpenID Connect / OAuth 2.0** gibi standartları incele. Bu protokoller, token yönetimi, kimlik doğrulama ve yetkilendirme için iyi bir altyapı sağlar.  
- CI/CD pipeline’ında token validasyon testleri veya JWT imza doğrulama testleri ekleyebilirsin.  
- Token’ı taşıyan isteklerde her zaman HTTPS kullan.  
- Token içeriğinin (özellikle JWT payload’unun) hassas bilgileri barındırmadığından emin ol. Payload, Base64URL encode edilmiştir ama gizli değildir, kolayca okunabilir.

---

### Kapanış

Token tabanlı kimlik doğrulama, modern mimarilerin kalbinde yer alıyor. Doğru uygulandığında, ölçeklenebilir ve dağıtık ortamlarda kimlik ve erişim yönetimi konusuna pratik bir çözüm sunar. Ancak dikkatsizce uygulanırsa, token hırsızlığı, kimlik taklidi ve çeşitli güvenlik açıklarına davetiye çıkarır.

Artık bu ek adımla beraber token kullanımının inceliklerini de öğrendin. Edindiğin bu bilgilerle, hangi mimariyi seçersen seç, güvenliği en baştan sağlam bir zemine oturtma şansın var. Unutma, güvenlikte detaylar fark yaratır!
