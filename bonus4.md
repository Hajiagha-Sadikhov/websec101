## İki Faktörlü Kimlik Doğrulama (2FA) Nedir?

2FA, bir kullanıcıyı doğrulamak için iki bağımsız bilgi veya varlık gerektiren bir güvenlik mekanizmasıdır. Bu iki faktör şu unsurlardan oluşur:

- **Bildiğiniz bir şey:** Şifre veya PIN.
- **Sahip olduğunuz bir şey:** Telefon, donanım anahtarı veya uygulama.
- **Siz olan bir şey:** Parmak izi, yüz tanıma veya diğer biyometrik veriler.

Örneğin, bir kullanıcı şifresini girdikten sonra telefonuna gelen bir kodla doğrulama yapar. Bu sayede, şifre tek başına çalınsa bile hesaba erişim sağlamak mümkün olmaz.

## İki Faktörlü Kimlik Doğrulama (2FA) ve Doğrulama Mekanizmalarını Atlama Yöntemleri

Günümüzde dijital güvenlik, yalnızca güçlü şifreler kullanmanın ötesine geçmiştir. Özellikle kritik hesaplar ve hizmetler için İki Faktörlü Kimlik Doğrulama (2FA), ek bir güvenlik katmanı sağlayarak kullanıcı hesaplarının daha güvenli olmasını sağlar. Ancak, kötü amaçlı kişiler bu mekanizmaları atlamak için çeşitli yöntemler geliştirmiştir. Bu yazıda, 2FA’nın ne olduğunu, türlerini, saldırı yöntemlerini ve bu saldırılara karşı alınabilecek önlemleri derinlemesine ele alacağız.

### İki Faktörlü Kimlik Doğrulama (2FA) Nedir?

2FA, bir kullanıcıyı doğrulamak için iki bağımsız bilgi veya varlık gerektiren bir güvenlik mekanizmasıdır. Bu iki faktör şu unsurlardan oluşur:

- **Bildiğiniz bir şey:** Şifre veya PIN.
- **Sahip olduğunuz bir şey:** Telefon, donanım anahtarı veya uygulama.
- **Siz olan bir şey:** Parmak izi, yüz tanıma veya diğer biyometrik veriler.

Örneğin, bir kullanıcı şifresini girdikten sonra telefonuna gelen bir kodla doğrulama yapar. Bu sayede, şifre tek başına çalınsa bile hesaba erişim sağlamak mümkün olmaz.

### 2FA Türleri

#### SMS Tabanlı 2FA

Kullanıcının telefonuna kısa mesaj olarak bir doğrulama kodu gönderilir.

- **Avantajları:** Kolayca uygulanabilir, kullanıcı dostudur.
- **Dezavantajları:** SIM swap saldırılarına ve SMS’in güvenli olmayan doğasına karşı savunmasızdır.

#### TOTP (Time-Based One-Time Password)

Google Authenticator, Authy veya benzeri uygulamalarla üretilen, zamana bağlı geçici kodları içerir.

- **Avantajları:** SMS'e göre daha güvenlidir.
- **Dezavantajları:** Uygulamanın kaybolması durumunda erişim sorunları yaşanabilir.

#### Push Bildirimleri

Mobil cihazlara gelen bir bildirim aracılığıyla doğrulama yapılır.

- **Avantajları:** Kod girme gerekliliğini ortadan kaldırır.
- **Dezavantajları:** Uygulamalara güvenli erişim sağlanmazsa riskli olabilir.

#### Donanım Anahtarları

YubiKey gibi fiziksel cihazlarla doğrulama yapılır.

- **Avantajları:** Fiziksel erişim gerektirdiği için çok güvenlidir.
- **Dezavantajları:** Kaybolduğunda erişim sorunları yaratır.

### İki Faktörlü Kimlik Doğrulamanın Atlatma yöntemleri

## [ ] Hatalı İki Faktörlü Doğrulama Mantığı 

Bazen iki faktörlü kimlik doğrulamadaki hatalı mantık, bir kullanıcının ilk giriş adımını tamamladıktan sonra, web sitesinin aynı kullanıcının ikinci adımı tamamladığını yeterince doğrulamaması anlamına gelir. Örneğin, kullanıcı ilk adımda normal kimlik bilgileriyle aşağıdaki gibi giriş yapar:

```http
POST /login-steps/first HTTP/1.1
Host: vulnerable-website.com
...
username=carlos&password=qwerty
```
Kullanıcı, ardından hesabıyla ilişkili bir çerez atanarak giriş işleminin ikinci adımına yönlendirilir:

```
HTTP/1.1 200 OK
Set-Cookie: account=carlos
```

```
GET /login-steps/second HTTP/1.1
Cookie: account=carlos
```

Doğrulama kodunu gönderirken, istek bu çerezi kullanarak kullanıcının hangi hesaba erişmeye çalıştığını belirler:
```
POST /login-steps/second HTTP/1.1
Host: vulnerable-website.com
Cookie: account=carlos
...
verification-code=123456

Bu durumda, bir saldırgan kendi kimlik bilgileriyle giriş yapabilir, ancak doğrulama kodunu gönderirken hesap çerezinin değerini herhangi bir rastgele kullanıcı adına değiştirebilir:

```
POST /login-steps/second HTTP/1.1
Host: vulnerable-website.com
Cookie: account=victim-user
...
verification-code=123456

## 2FA Devre Dışı Bırakma Özelliğinde Clickjacking  
Uygulamanın bir kullanıcının 2FA'yı devre dışı bırakmasına izin verdiği sayfayı iframe ile deneyin.  
Eğer iframe başarılı olursa, mağduru tuzağınıza düşürmek için sosyal mühendislik saldırısı gerçekleştirmeye çalışın.

## Yanıt Manipülasyonu  
2FA isteğinin yanıtını kontrol edin.  
Yanıtta "Success" değerini gözlemliyorsanız, bunu "Success" olarak değiştirin ve 2FA'nın atlatılıp atlatılmadığını kontrol edin.

## Durum Kodu Manipülasyonu  
Yanıt durum kodu 4XX (örneğin, 401, 402 vb.) ise, yanıt durum kodunu "200 OK" olarak değiştirin ve 2FA'nın atlatılıp atlatılmadığını kontrol edin.

## 2FA Kodu Yeniden Kullanılabilirliği  
Bir 2FA kodu isteyin ve kullanın.  
Şimdi, 2FA kodunu yeniden kullanmayı deneyin; eğer başarıyla kullanılıyorsa bu bir sorundur.  
Ayrıca, birden fazla 2FA kodu istemeyi deneyin ve yeni bir kod istendiğinde önceki istenen kodların süresinin dolup dolmadığını kontrol edin.  
Daha sonra, önceki kullanılan kodu uzun bir süre (örneğin, 1 gün veya daha fazla) sonra yeniden kullanmayı deneyin. Bu, 6 haneli bir 2FA kodunu kırmak ve tahmin etmek için yeterli bir süre olabilir.

## 2FA Devre Dışı Bırakma Özelliğinde CSRF  
Kullanıcının 2FA devre dışı bırakma işlemini CSRF yoluyla manipüle etmeye çalışın.

## Yedek Kod Suistimali  
Yedek kodları devre dışı bırakmak ve sıfırlamak için yanıt/durum kodu manipülasyonu, kaba kuvvet gibi 2FA'da kullanılan teknikleri uygulayın.

## 2FA Etkinleştirme Önceki Oturumu Süresiz Kılmıyor  
Uygulamaya iki farklı tarayıcıda giriş yapın ve birinci oturumdan 2FA'yı etkinleştirin.  
Diğer oturumu kullanın; eğer bu oturum süresiz kalıyorsa, yetersiz oturum süresi dolma sorununu gösterebilir.  
Bu durumda, bir saldırgan 2FA'dan önce aktif bir oturumu ele geçirirse, 2FA olmadan tüm işlemleri gerçekleştirme olasılığı vardır.

## 2FA Referans Kontrolü Atlatma  
2FA'dan sonra gelen sayfaya veya uygulamanın diğer herhangi bir kimlik doğrulama yapılmış sayfasına doğrudan gidin.  
Eğer başarılı olmazsa, referans başlığını 2FA sayfasının URL'si ile değiştirin. Bu, isteğin 2FA koşulu yerine getirildikten sonra geldiği izlenimini yaratabilir.

## 2FA Kodu Sızıntısı  
2FA kodunu tetikleyen istekte (örneğin, OTP gönderme işlevi), isteği yakalayın.  
Bu isteğin yanıtını kontrol edin ve 2FA kodunun sızıp sızmadığını analiz edin.

## JS Dosyası Analizi  
2FA kodu isteğini tetiklerken, yanıt içinde referans verilen tüm JS dosyalarını analiz edin.  
2FA kodunu atlatmanıza yardımcı olabilecek herhangi bir bilgi içeren bir JS dosyası olup olmadığını kontrol edin.

## Kaba Kuvvet Korumasının Eksikliği  
2FA kodu isteyin ve bu isteği yakalayın.  
Bu isteği 100-200 kez tekrarlayın; eğer bir sınırlama yoksa, bu bir oran sınırı sorunudur.  
2FA kodu doğrulama sayfasında, geçerli 2FA kodu için kaba kuvvet denemesi yapın.

## Şifre Sıfırlama/E-posta Değiştirme - 2FA Devre Dışı Bırakma  
Mağdur kullanıcının e-posta değişikliği veya şifre sıfırlama işlemini gerçekleştirmenizin mümkün olduğunu varsayalım ya da mağduru bunu yapmaya zorlayın.  
Eğer e-posta değiştirildiğinde veya şifre sıfırlandığında 2FA devre dışı bırakılıyorsa, bu bir güvenlik sorunudur.

## 2FA Kodu Bütünlüğü Doğrulama Eksikliği  
Saldırgan hesabından bir 2FA kodu isteyin.  
Bu geçerli 2FA kodunu mağdurun 2FA isteğinde kullanın ve 2FA korumasını atlatıp atlatamayacağını kontrol edin.


## 2FA Atlatma Senaryoları  

### Doğrudan İstek  
2FA sayfasını atlayıp kimlik doğrulaması yapılmış sayfalara doğrudan giderek atlatma yapabilirsiniz.  
Referrer başlığını değiştirerek, 2FA engellemelerini geçip geçemediğini kontrol edin.

### Token Yeniden Kullanımı  
Hesabınızda daha önce kullanılan bir token’ı kimlik doğrulaması için yeniden kullanmayı deneyin.

### Kullanılmayan Jetonların Paylaşılması  
Hesabınızdan bir jeton alın ve bu jetonu başka bir hesapta kullanarak 2FA’yı atlatmayı deneyin.

### Sızdırılmış Jeton  
Web uygulamalarından sızan jetonların 2FA’yı bypass etmek için kullanılıp kullanılamadığını kontrol edin.

### Oturum İzni  
Aynı oturumu kullanarak 2FA’yı geçmeyi deneyin. Kendi hesabınızla 2FA’yı tamamlayın, ancak mağdurun hesabında bu işlemi atlatmayı hedefleyin.

### Şifre Sıfırlama Fonksiyonu  
Şifre sıfırlama bağlantılarını yeniden kullanarak 2FA’yı bypass etmeye çalışın.

### Oran Sınırlaması Olmaması  
Oran sınırlaması yoksa kaba kuvvet yöntemi ile 2FA’yı aşmayı deneyin.

### Akış Hızı Sınırlaması Var Ama Hız Sınırı Yok  
Sınır koyulmuşsa, sabırlı şekilde 2FA kodlarını zorlayarak geçebilirsiniz.

### Kodu Yeniden Gönder ve Limitleri Sıfırla  
Kodu yeniden gönderdiğinizde, oran sınırlaması sıfırlanırsa, bunu kullanarak 2FA’yı aşın.

### İstemci Tarafı Oran Sınırlaması Aşma  
Tarayıcı tarafındaki limitleri geçmek için belirli bir yöntem kullanın.

### Kullanıcının Hesabında Oran Sınırlaması Eksikliği  
Hesap içindeki işlemleri korumak için oran sınırlaması olmayabilir.

### SMS ile Kodu Yeniden Gönderirken Oran Sınırlaması Eksikliği  
SMS kodu yeniden gönderildiğinde oran sınırlamasının olmaması ile manipülasyon yapın.

### Sonsuz OTP Yeniden Üretimi  
OTP’yi sürekli üretip aynı token’larla 2FA’yı aşmayı deneyin.

### Tahmin Edilebilir Cookie  
Tahmin edilebilir bir cookie ile “beni hatırla” fonksiyonunu kullanarak kimlik doğrulamasını atlatın.

### IP Adresi  
IP adresini manipüle ederek, mağdurun kimlik doğrulamasını atlatmaya çalışın.

### Alt Alan Adları  
Test alt alan adlarını kullanarak 2FA’yı atlayabilecek eski sürümler veya zayıf uç noktalar bulun.

### API'ler  
2FA API uç noktalarını test ederek atlatma açığı bulabilirsiniz.

### Önceki Oturumlar  
2FA etkinleştirildiğinde önceki oturumların sonlandırıldığından emin olun.

### Yedek Kodlara Yetersiz Erişim Kontrolü  
Yedek kodlara izinsiz erişim ile 2FA’yı atlatmaya çalışın.

### Bilgi Sızması  
2FA sayfasında sızdırılan bilgiler ile güvenlik açığı araştırın.

### Null veya 000000 ile 2FA'yı Atlatma  
2FA sayfasındaki varsayılan null veya sabit kodlarla atlatma yapın.

### E-postayı Doğrulamadan 2FA'yı Etkinleştirme  
E-posta doğrulamasını atlayarak 2FA’yı etkinleştirmeye çalışın.

### 2FA'yı Devre Dışı Bırakırken Şifre Kontrolü Yok  
Şifre doğrulama olmadan 2FA’yı devre dışı bırakmayı deneyin.

### MFA Modu, Cihaz Güvenilirliği Süresi Dolmadığında Mağdurun Cihazından MFA'yı Aşmak  
Güvenilir cihaz süresi dolmadan MFA’yı aşmak için cihaz bilgilerini manipüle edin.

### Boş Kod Göndererek 2FA'yı Aşma  
Yanlış OTP göndererek oturum açmayı deneyin.

### Kapanış
Bu teknikler ve senaryolar, 2FA (iki faktörlü kimlik doğrulama) sistemlerinin güvenlik açıklarını keşfetmeye yönelik potansiyel saldırı yöntemleridir. Bu tür testlerin yalnızca etik hacking çerçevesinde ve izinli ortamlarda gerçekleştirilmesi önemlidir. Amacımız, sistemlerin zayıf noktalarını keşfederek güvenliklerini artırmak ve potansiyel saldırılara karşı daha dayanıklı hale getirmektir.

Her zaman unutulmamalıdır ki, güvenlik testleri ve saldırılar yalnızca uygun izinlere sahip olduğunuz ortamlarda yapılmalıdır.

---

### Referanslar
1. [2FA Bypass Techniques - HackTricks Wiki](https://book.hacktricks.wiki/en/pentesting-web/2fa-bypass.html)
2. [TOP MFA Bugs - HackerOne Reports](https://github.com/reddelexc/hackerone-reports/blob/master/tops_by_bug_type/TOPMFA.md)
