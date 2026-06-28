---
title: "RFC-0000: Problem Bildirimi"
status: "Çalışma Taslağı"
category: "Bilgilendirici"
project-codename: "ADP"
lang: "tr"
canonical: "docs/rfc-0000-problem-statement.md"
date: "2026-06-27"
author: "Aybars Mete Keleş"
---

# RFC-0000: Problem Bildirimi
## Web'de Otonom Agent'lar için Servis-Arayüz Keşfi

> **Çeviri notu.** Bu belge, RFC-0000'ın Türkçe çalışma çevirisidir. Bu belge setinin **kanonik (asıl) sürümü İngilizce'dir** ve `docs/rfc-0000-problem-statement.md` dosyasında bulunur. Herhangi bir tutarsızlık durumunda İngilizce sürüm esas alınır.

---

## Bu Belgenin Durumu

Bu belge bir IETF belgesi **değildir**. IETF, IRTF veya başka bir standart organının resmî yayını olarak sunulmamaktadır. Belge, IETF Internet-Draft yazım geleneğini ve titizliğini benimseyen, halka açık tartışma amacıyla yayımlanmış **bağımsız bir çalışma taslağıdır** (working draft).

Belgeye atanan "RFC-0000" numarası, RFC Editor tarafından verilmiş bir numara değildir. Bu, ilgili belge setini iç tutarlılıkla numaralandırmak için kullanılan **dahili bir proje tanımlayıcısıdır**. Aynı şekilde "ADP" adı da nihai bir isim değil, bir **proje kod adıdır** (codename); isim, problemin ve teknik çözümün olgunlaşmasından sonra verilecek son kararlardan biridir.

Bu belge bir çözüm önermez. Bu belgenin tek amacı, web üzerinde bugün standartlaşmamış belirli bir problemi netleştirmek ve okuyucunun "burada gerçekten çözülmesi gereken, ortak bir mekanizmaya kavuşmamış bir problem var" sonucuna kendi muhakemesiyle ulaşmasını sağlamaktır. Bu problemin önerilen çözümü, ayrı bir spesifikasyon belgesi olan RFC-0001'de tanımlanmaktadır.

Geri bildirim ve tartışma açıktır ve teşvik edilir.

---

## Özet

Web, otuz yılı aşkın süredir, kendisini tüketen istemci sınıflarına uyum sağlayarak gelişmiştir. Web, farklı makine tüketicilerinin ihtiyaçları ortaya çıktıkça, belirli problemler için küçük ve öngörülebilir keşif (discovery) konvansiyonları geliştirmiştir: bir tarayıcının bir siteyi nasıl gezeceği, bir kimlik istemcisinin bir sağlayıcının yapılandırmasını nereden öğreneceği, bir güvenlik araştırmacısının bir açığı kime bildireceği gibi sorular, web üzerine eklenen küçük, ortak konvansiyonlarla cevaplanmıştır.

Bugün web'in yeni bir tüketici sınıfı ortaya çıkmıştır: insan adına, gerçek zamanlı olarak görev yürüten **otonom agent'lar**. Bu istemciler yalnızca içerik okumakla kalmaz; servislerle etkileşime girer, işlem başlatır ve daha önce hiç entegre olmadıkları servislerle çalışmak durumunda kalır. Ne var ki bu istemci sınıfı için web henüz ortak bir keşif konvansiyonuna sahip değildir.

Bu belge, söz konusu boşluğu tanımlar. Yeni bir çözüm önermeden önce çözülmesi gereken problemi net biçimde ortaya koyar: bir otonom istemci, daha önce karşılaşmadığı bir servisle ilk kez karşılaştığında, o servisin hangi makine tüketilebilir arayüzlere sahip olduğunu ve bunların nerede bulunduğunu standart bir yöntemle belirleyemez. Belge bu problemi, web'in keşif tarihçesi ışığında inceler; mevcut mekanizmaların her birinin **farklı** bir problemi çözdüğünü tarafsız biçimde gösterir; problemi somut kullanım senaryolarıyla temellendirir; ve herhangi bir çözümün taşıması gereken nitelikleri sıralar. Çözümün kendisi bu belgenin konusu değildir.

---

## 1. Giriş

İnternet, var olduğu süre boyunca tek bir tür kullanıcıya hizmet eden durağan bir sistem olmamıştır. Tam tersine, web'in tarihi, kendisini tüketen istemcilerin doğasındaki değişime sürekli uyum sağlama tarihidir.

Bu uyum, çoğu zaman büyük ve iddialı sistemler tasarlanarak değil, küçük ve ortak konvansiyonlar üzerinde uzlaşılarak gerçekleşmiştir. Bir arama motoru tarayıcısının bir siteyi nasıl gezmesi gerektiği, bir kimlik istemcisinin bir sağlayıcının yapılandırmasını nereden öğreneceği, bir güvenlik araştırmacısının bir açığı kime bildireceği — bunların her biri, web'in üzerine eklenen küçük, öngörülebilir, makine tarafından okunabilir keşif konvansiyonlarıyla çözülmüştür. Bu konvansiyonların ortak özelliği, bir makinenin bir sistem hakkında ihtiyaç duyduğu temel bilgiye **tahmin etmeden, standart bir biçimde** ulaşabilmesini sağlamalarıdır.

Bu belge, web'in en yeni tüketici sınıfı olan otonom agent'ların, kendilerinden önceki istemci sınıflarının bazılarının sahip olduğu türden bir keşif konvansiyonundan bugün yoksun olduğunu öne sürmektedir. Sonuç olarak, bir agent yeni bir servisle karşılaştığında, web'in daha önce belirli sınıflar için çözdüğü bir problemi yeniden — ve bu kez her servis için ayrı ayrı, kırılgan yöntemlerle — çözmek zorunda kalmaktadır.

Bu belgenin amacı bir çözüm sunmak değildir. Amacı, bu problemin gerçek, somut ve standartlaşmamış olduğunu göstermektir. Belge boyunca herhangi bir mekanizma, format veya teknik tasarım önerilmeyecektir. Okuyucudan beklenen, belgenin sonunda problemi açıkça görmesi ve "evet, burada çözülmesi gereken ortak bir problem var" yargısına ulaşmasıdır. Bu probleme önerilen teknik çözüm, RFC-0001'in konusudur.

### 1.1. Belgenin Kapsamı

Bu belge yalnızca **keşif** (discovery) problemini ele alır. Bu belge:

- bir arayüz formatı tanımlamaz,
- bir iletişim protokolü tanımlamaz,
- bir kimlik doğrulama veya yetkilendirme modeli tanımlamaz,
- bir yetenek (capability) veya niyet (intent) modeli tanımlamaz,
- bir güven (trust) çerçevesi tanımlamaz.

Bu belge yalnızca tek bir soruyu inceler ve bu sorunun bugün standart bir cevabı olmadığını gösterir: **"Bir makine istemcisi, daha önce hiç karşılaşmadığı bir servisle ilk kez karşılaştığında, o servisin makine tüketilebilir arayüzlerini nereden bulmaya başlamalıdır?"**

### 1.2. Belgenin Hedef Kitlesi

Bu belge iki kitleye birden hitap edecek şekilde yazılmıştır. Birincisi, web standartları, protokol tasarımı ve dağıtık sistemler konusunda deneyimli teknik okuyuculardır. İkincisi ise konuya yeni giren, ancak problemin doğasını ve önemini anlamak isteyen okuyuculardır. Belge, terminolojiyi titizlikle kullanırken, her temel kavramı sıfırdan kuracak biçimde açıklamayı hedefler.

---

## 2. Web'deki Makine Tüketicilerinin Evrimi

Bu bölümün amacı, ele alınan problemin **yeni bir teknolojiden kaynaklanan istisnai bir durum** değil, web'in doğal evrimindeki bir sonraki adım olduğunu göstermektir. Bunu yapmak için, web'i tüketen istemci sınıflarının zaman içindeki gelişimini izleyeceğiz.

### 2.1. Birinci Sınıf: İnsan Okuyucu

Web ilk olarak insanlar için tasarlandı. Belgeler, insanların okuması için biçimlendirilmiş işaretleme dilinde (markup) yazıldı; tarayıcılar bu belgeleri insan gözüne sunmak için geliştirildi. Bu dönemde web'in birincil tüketicisi, ekranı okuyan, bağlantıları takip eden ve kararları kendi muhakemesiyle veren bir insandı.

Bu sınıf için "keşif", insanın bilişsel bir işlemiydi. İnsan, bir sayfaya bakar, anlamı kavrar, ilgili bağlantıya tıklardı. Sistemin makineye sunduğu özel bir keşif bilgisi gerekmiyordu; çünkü tüketici, anlamı çıkarabilen bir insandı.

### 2.2. İkinci Sınıf: Tarayıcı ve İndeksleyici

Web büyüdükçe, içeriğin ölçekte gezilmesi ve dizinlenmesi ihtiyacı doğdu. Arama motorları, web'i otomatik olarak dolaşan makineler — tarayıcılar (crawler) — geliştirdi. Bu, web'in ilk büyük **makine tüketicisi** sınıfıydı.

Tarayıcı, insandan farklıdır: anlamı insan gibi kavramaz, içeriği insan gibi yorumlamaz. Yalnızca büyük ölçekte gezer ve okur. Bu yeni istemci sınıfı, daha önce var olmayan bir ihtiyaç doğurdu: bir tarayıcının bir siteyi nasıl gezeceğini, hangi bölümlere girmemesi gerektiğini ve hangi içeriğin var olduğunu **öngörülebilir biçimde** bilmesi gerekiyordu.

Web bu ihtiyaca, büyük bir sistem tasarlayarak değil, küçük ve ortak konvansiyonlarla cevap verdi. Sitenin kökünde bulunan düz metin tabanlı bir dosya, tarayıcılara erişim kurallarını bildirdi; bir başka konvansiyon, sitenin içeriğinin makine tarafından okunabilir bir listesini sundu. Bunlar küçük, tahmin edilebilir ve herkese açık konvansiyonlardı. İşte bu, web'in bir makine tüketici sınıfının keşif ihtiyacını ortak bir konvansiyonla karşıladığı en belirgin örnektir.

### 2.3. Üçüncü Sınıf: Mobil Uygulama Çağı

Sonraki dönemde, web'in arkasındaki servisleri tüketen yeni bir istemci türü yaygınlaştı: mobil uygulamalar ve zengin istemci uygulamaları. Bu uygulamalar, kullanıcıya bir arayüz sunarken arka planda servislerle programatik olarak konuşuyordu.

Ne var ki bu dönemdeki etkileşim büyük ölçüde **noktadan noktaya** ve **önceden inşa edilmiş** entegrasyonlara dayanıyordu. Her uygulama, konuşacağı servisi geliştirme zamanında biliyor; o servisin arayüzünü geliştiriciler elle inceliyor; entegrasyon koda gömülerek bir kez yazılıyordu. Bu çağda **genel bir keşif konvansiyonu oluşmadı**; çünkü istemci, hangi servisle nasıl konuşacağını zaten önceden bilen bir geliştiricinin ürünüydü. Yine de bu dönem önemli bir geçişi başlattı: web artık yalnızca insanlara belge sunan değil, makinelere veri ve işlem sunan bir altyapıya dönüşüyordu.

### 2.4. Dördüncü Sınıf: Programatik API İstemcisi

Programatik tüketim olgunlaştıkça, makineden makineye etkileşim açık bir disiplin hâline geldi. Servisler, sundukları arayüzleri yapılandırılmış ve makine tarafından okunabilir biçimde tanımlayan açıklamalar yayımlamaya başladı. Bu açıklamalar, bir arayüzün hangi işlemleri sunduğunu, hangi parametreleri beklediğini ve hangi yanıtları döndürdüğünü tarif ediyordu.

Bu, makine tüketicileri açısından önemli bir ilerlemeydi. Ancak buradaki keşif hâlâ büyük ölçüde **insan aracılığıyla** gerçekleşiyordu. Tipik akış şöyleydi: bir geliştirici, bir servisin var olduğunu bir biçimde öğrenir; o servisin dokümantasyonunu insan olarak bulur; arayüz açıklamasını okur; ve entegrasyonu **tasarım zamanında, bir kez** yazardı. Açıklamanın kendisi makine tarafından okunabilir olsa da, "bu servisin hangi arayüzleri var ve nereden başlamalıyım?" sorusunun cevabı, çoğunlukla bir insanın bulduğu ve koda taşıdığı bir bilgiydi.

### 2.5. Beşinci Sınıf: Otonom Agent (Bugün)

Bugün web'in karşı karşıya olduğu yeni tüketici sınıfı, önceki sınıfların hepsinden niteliksel olarak farklıdır.

Otonom bir agent, bir insan adına hareket eden, ancak entegrasyonu tasarım zamanında bir geliştiricinin elle kurmadığı bir makine istemcisidir. Bir kullanıcı, agent'tan bir görevi yerine getirmesini ister; agent, bu görevi tamamlamak için, daha önce hiç entegre olmadığı servislerle **çalışma zamanında** karşılaşabilir, onları anlamak ve onlarla etkileşime girmek zorunda kalabilir. Bu, önceki sınıflardan kritik biçimde ayrılır:

- **Tarayıcıdan farklı olarak**, agent yalnızca okumaz; işlem başlatabilir, etkileşime girebilir.
- **Mobil uygulamadan farklı olarak**, agent'ın karşılaşacağı servis önceden bilinmeyebilir; entegrasyon koda gömülü değildir.
- **API istemcisinden farklı olarak**, keşif ve entegrasyon kararını bir geliştirici tasarım zamanında değil, agent'ın kendisi çalışma zamanında vermek durumundadır.

İşte bu, web'in evrimindeki yeni durumdur: tüketici artık bir kez entegrasyon yazan bir geliştirici değil, daha önce görmediği servislerle gerçek zamanlı ve otonom biçimde karşılaşan bir istemcidir.

### 2.6. Evrimden Çıkan Gözlem

Bu evrimden çıkan gözlem, her tüketici sınıfı için mutlaka bir keşif konvansiyonu oluştuğu **değildir**. Bazı sınıflar için — özellikle tarayıcı sınıfı için — belirli ve öngörülebilir konvansiyonlar gelişti; mobil dönemde ise keşif büyük ölçüde noktadan noktaya çözüldü ve genel bir konvansiyon oluşmadı. Buradaki asıl gözlem şudur: bir makine tüketicisi sınıfı belirgin ve yaygın bir keşif ihtiyacı doğurduğunda, web bu ihtiyacı zamanla küçük, ortak konvansiyonlarla karşılama eğilimi göstermiştir.

Otonom agent sınıfı ise bugün, böyle yaygın bir keşif ihtiyacı doğurmasına rağmen, bu ihtiyacı karşılayan ortak bir konvansiyondan yoksundur. Bu belgenin geri kalanı, bu yoksunluğun tam olarak neyi ifade ettiğini, neden bir problem oluşturduğunu ve neden mevcut mekanizmaların bu problemi çözmediğini inceleyecektir.

> **Bölüm Özeti.** Web, makine tüketicisi sınıfları belirgin keşif ihtiyaçları doğurdukça, belirli problemler için küçük ve öngörülebilir konvansiyonlar geliştirme eğiliminde olmuştur. Otonom agent sınıfı bugün böyle bir ihtiyacı doğurmakta, ancak onu karşılayan ortak bir konvansiyon henüz bulunmamaktadır.

---

## 3. Terminoloji

Bu bölüm, belge boyunca kullanılan temel terimleri tanımlar. Terimler hem Türkçe hem de yaygın İngilizce karşılıklarıyla verilmiştir.

Büyük harfle yazılan anahtar kelimeler — "MUST", "MUST NOT", "SHOULD", "SHOULD NOT", "MAY" — RFC 2119 ve RFC 8174'te tanımlanan anlamlarıyla, yalnızca bu büyük harfli biçimde göründüklerinde kullanılır. Bu belge bir spesifikasyon olmadığından, normatif anahtar kelimeler yalnızca herhangi bir çözümün taşıması gereken nitelikleri tartışan 8. bölümde, gereksinimlerin gücünü belirtmek amacıyla geçer.

**Servis (Service):** HTTP üzerinden erişilebilen, bir alan adı (domain) altında yayımlanan bir web sistemi. Bir servis; insanlara yönelik bir web sitesi, programatik bir arayüz, ya da her ikisini birden sunabilir.

**Makine Tüketicisi (Machine Consumer):** Web'i bir insanın bilişsel muhakemesi olmaksızın, otomatik biçimde tüketen herhangi bir program. Tarayıcılar, programatik API istemcileri ve otonom agent'lar bu sınıfa girer.

**Otonom Agent (Autonomous Agent):** Bir insan adına görevleri yerine getiren; bu görevleri tamamlamak için, entegrasyonu tasarım zamanında elle kurulmamış servislerle çalışma zamanında karşılaşabilen ve onlarla etkileşime girebilen bir makine tüketicisi.

**Makine Arayüzü (Machine Interface):** Bir servisin, makine tüketicileri tarafından programatik olarak tüketilmek üzere sunduğu herhangi bir erişim noktası veya yetenek. Bir servis sıfır, bir ya da birden çok makine arayüzü sunabilir; bu arayüzler farklı protokollere dayanabilir.

**Keşif (Discovery):** Bir makine tüketicisinin, bir servis hakkında — özellikle o servisin hangi makine arayüzlerini sunduğu ve bunların nerede bulunduğu hakkında — ihtiyaç duyduğu temel bilgiye, önceden özel bir entegrasyon yapmaksızın ulaşma süreci.

**Soğuk Karşılaşma (Cold Encounter):** Bir makine tüketicisinin, daha önce hiç entegre olmadığı bir servisle, yalnızca o servisin alan adını bilerek ilk kez karşılaşması durumu. Bu belgede ele alınan problem, doğrudan bu durumla ilgilidir.

**Arayüz Açıklaması (Interface Description):** Bir makine arayüzünün yapısını, işlemlerini ve davranışını makine tarafından okunabilir biçimde tarif eden belge. Arayüz açıklamaları, bu belgenin ele aldığı keşif probleminin **konusu değil**, keşfedilen şeydir; yani keşif gerçekleştikten sonra ulaşılan içeriktir.

---

## 4. Problem Bildirimi

Bu bölüm, belgenin merkezindeki problemi mümkün olan en net biçimde tanımlar.

### 4.1. Problemin Tanımı

Otonom bir agent, bir görevi yerine getirmek üzere daha önce hiç entegre olmadığı bir servisle karşılaştığında — yani bir **soğuk karşılaşma** anında — o servisin hangi makine arayüzlerini sunduğunu ve bu arayüzlerin nerede bulunduğunu belirleyebileceği **standart, öngörülebilir bir yöntem yoktur**.

Problemin özünü tek bir cümle taşır:

> *Bir agent yalnızca bir alan adı biliyor. Daha önce bir entegrasyon yok. Nereden başlamalı?*

Bu soruya standart bir cevap bulunmadığında agent, bir dizi sezgisel (heuristic), kırılgan ve servise özgü stratejiye başvurmak zorunda kalır: insanlar için biçimlendirilmiş sayfaları ayrıştırmaya ve anlamlandırmaya çalışmak; bir arayüzün bulunabileceği yaygın yolları tahmin etmek; arama yoluyla dokümantasyon bulmaya çalışmak; ya da bir insan geliştiricinin, agent çalışmadan önce o servise özel bir entegrasyon inşa etmesini gerektirmek.

### 4.2. Problemin İki Temel Bileşeni

Problem iki ayrı soruya indirgenebilir; bugün ikisinin de standart bir cevabı yoktur:

1. **Varlık sorusu:** "Bu servis, makine tüketilebilir arayüzler sunuyor mu?" Bir agent, yalnızca bir alan adına bakarak, o servisin programatik olarak tüketilip tüketilemeyeceğini öngörülebilir biçimde bilemez.

2. **Konum sorusu:** "Sunuyorsa, bu arayüzler nerededir?" Servis arayüz sunuyor olsa bile, agent bu arayüzlerin nerede bulunduğunu, hangi protokollere dayandığını ve ilgili açıklamalara nereden ulaşılacağını standart bir biçimde belirleyemez.

### 4.3. Problemin Başlatma (Bootstrapping) Doğası

Problemin özü bir **başlatma (bootstrapping)** problemidir. Mevcut araçların ve standartların çoğu, keşfin **zaten gerçekleşmiş olduğunu** varsayar. Bir arayüz açıklaması, agent o arayüzün varlığını ve yerini zaten bildiğinde işe yarar; bir iletişim protokolü, agent ilgili sunucunun nerede olduğunu zaten bildiğinde işe yarar. Hiçbiri, en baştaki soruyu — yalnızca bir alan adı verildiğinde nereden başlanacağını — kendi konusu yapmaz.

### 4.4. Problemin "Standartlaşmamış Olma" Boyutu

Vurgulanması gereken kritik nokta, problemin teknik olarak **çözülemez** olması değildir. Aksine, her agent geliştiricisi bu problemi kendi yöntemiyle, kendi servise özgü çözümleriyle hâlihazırda çözmektedir. Problem, bu çözümlerin **ortak ve öngörülebilir olmamasıdır**. Her tüketicinin her servis için ayrı entegrasyon yazması, web'in daha önceki dönemlerinde de var olan ancak ortak konvansiyonlarla aşılan bir maliyettir; agent sınıfı için bu maliyet bugün yeniden ödenmektedir.

> **Bölüm Özeti.** Problem bir başlatma problemidir: yalnızca bir alan adı verildiğinde, bir makine tüketicisinin bir servisin arayüzlerini nereden bulmaya başlayacağının ortak ve öngörülebilir bir cevabı yoktur. Problem çözülemez değil; standartlaşmamıştır.

---

## 5. Mevcut Keşif Manzarası

Bu bölüm, web üzerinde bugün var olan, makine tüketicilerine yönelik keşif ve tanımlama mekanizmalarını inceler. Bu incelemenin önemli bir ilkesi vardır: **hiçbir mekanizma eleştirilmemekte, hiçbiri "yetersiz" olarak nitelendirilmemektedir.** Bu mekanizmaların her biri, tasarlandığı problemi başarıyla çözmektedir. Bu bölümün amacı, her birinin **hangi** problemi çözdüğünü ve kapsamını tarafsız biçimde ortaya koymaktır. Her mekanizma aşağıdaki ortak çerçeveyle ele alınmıştır: amacı, çözdüğü problem ve kapsamı.

### 5.1. Tarayıcı Erişim Kuralları (Robots Exclusion)

**Amaç:** Bir sitenin operatörünün, otomatik tarayıcılara hangi bölümleri gezip gezemeyeceklerini bildirmesini sağlamak.

**Çözdüğü problem:** Tarayıcı erişiminin yönetimi. Bir tarayıcının bir sitenin hangi kısımlarına erişmesinin uygun olduğunu belirten ortak bir konvansiyon sunar.

**Kapsam:** İçeriğin tarayıcılar tarafından gezilmesine ilişkin **izin ve dışlama**. Bu mekanizma, bir servisin makine arayüzlerini tanımlamayı veya bunların yerini bildirmeyi amaçlamaz; tasarımı gereği bambaşka bir problemi çözer.

### 5.2. İçerik Listeleme (Sitemaps)

**Amaç:** Bir sitenin içeriğindeki adreslerin makine tarafından okunabilir bir listesini indeksleyicilere sunmak.

**Çözdüğü problem:** İçeriğin keşfedilebilirliği. İndeksleyicilerin, bir sitedeki içerik adreslerini eksiksiz ve verimli biçimde öğrenmesini sağlar.

**Kapsam:** İndeksleme amacıyla **içerik adreslerinin numaralandırılması**. Bu mekanizma, içeriğin nerede olduğunu söyler; bir servisin programatik arayüzlerinin varlığını veya yerini söylemeyi amaçlamaz. Bu da farklı bir problemdir.

### 5.3. Kimlik Sağlayıcı Yapılandırma Keşfi (OpenID Connect Discovery)

**Amaç:** Bir kimlik istemcisinin, bir kimlik sağlayıcısının yapılandırma bilgilerini öğrenmesini sağlamak.

**Çözdüğü problem:** Kimlik doğrulama akışının başlatılması için gereken yapılandırmanın keşfi. İstemcinin, sağlayıcının ilgili adreslerini ve parametrelerini öğrenmesini sağlar.

**Kapsam:** Belirli bir kimlik protokolüne özgü **yapılandırma keşfi**. Bu mekanizma, kendi alanında son derece etkilidir; ancak yalnızca o protokole özgüdür ve genel bir servis-arayüz keşfini amaçlamaz. Bu nedenle farklı bir problemi çözer.

### 5.4. Güvenlik İletişim Bilgisi (security.txt)

**Amaç:** Bir güvenlik araştırmacısının, bir serviste bulduğu açığı kime bildireceğini öğrenmesini sağlamak.

**Çözdüğü problem:** Güvenlik açığı bildirim sürecinin kolaylaştırılması. Bir servisin güvenlik iletişim bilgilerine ulaşmak için ortak bir konvansiyon sunar.

**Kapsam:** **Güvenlik iletişimi**. Bu mekanizma, bir servisin makine arayüzlerini tanımlamayı veya keşfetmeyi amaçlamaz; tamamen farklı bir problemi çözer. Burada anılmasının nedeni, web'in küçük ve ortak keşif konvansiyonlarıyla problem çözme geleneğinin başarılı bir örneği olmasıdır.

### 5.5. Arayüz Açıklamaları (OpenAPI ve Benzerleri)

**Amaç:** Belirli bir HTTP arayüzünün yapısını — işlemlerini, parametrelerini, yanıtlarını — makine tarafından okunabilir biçimde tarif etmek.

**Çözdüğü problem:** Bir arayüzün **tarif edilmesi** ve o arayüzün yeteneklerinin anlaşılması. Bir arayüz açıklaması, kendi içinde bir keşif boyutu taşır: bir programatik istemci, böyle bir açıklamayı okuyarak arayüzle nasıl etkileşeceğini anlayabilir.

**Kapsam:** Buradaki ayrım inceliklidir ve dikkat gerektirir. Bir arayüz açıklaması, **bir arayüz bulunduktan sonra** onu güçlü biçimde anlaşılır kılar. Ancak belirli bir alan adı altında **kaç** böyle açıklamanın bulunduğunu, bunların **nerede** yayımlandığını ve servisin **başka protokoller de** sunup sunmadığını, yalnızca alan adı seviyesinden başlayan standart bir başlangıç noktasından cevaplamayı amaçlamaz. Bir servis hiç açıklama sunmayabilir, tek bir açıklama sunabilir veya farklı protokollere ait birden çok açıklama sunabilir. Yani açıklama, "bu arayüzü nasıl kullanırım?" sorusunu cevaplar; "bu servisin hangi arayüzleri var ve nereden başlamalıyım?" sorusunu domain seviyesinde cevaplamayı hedeflemez.

### 5.6. Agent-Servis İletişim Protokolleri (Model Context Protocol)

**Amaç:** Bir agent veya istemci ile bir servis arasındaki etkileşimi — istemcinin servisin sunduğu araçları ve veri kaynaklarını nasıl kullanacağını — tanımlamak.

**Çözdüğü problem:** İstemci ile servis arasındaki **iletişim**. Bir istemcinin, bir servisin yeteneklerini standart bir protokolle kullanabilmesini sağlar.

**Kapsam:** Bu mekanizma, bir istemci ile bir sunucu arasındaki etkileşimi tanımlar. Ancak bir web servisinin hangi bu tür arayüzleri — varsa hangi diğer arayüzlerle birlikte — sunduğunu, yalnızca alan adı seviyesinden başlayarak genel bir servis keşif indeksinde toplama problemi, bu protokolün doğrudan kapsamı değildir. Protokol, iletişimin **nasıl** yürüyeceğini tanımlar; bu indeksleme ve başlatma sorusunu hedeflemez. İletişimin başlayabilmesi için ilgili sunucunun yerinin bilinmesi gerekir; bu yerin yalnızca alan adından nasıl bulunacağı ise ayrı bir problemdir.

### 5.7. Agent Kimlik ve İşbirliği Yaklaşımları (Agent-to-Agent)

**Amaç:** Bir agent'ın kimliğini, yeteneklerini ve onunla nasıl iletişim kurulacağını diğer agent'lara makine tarafından okunabilir biçimde tanımlamak; agent'ların birbirini keşfetmesini ve birlikte çalışmasını sağlamak.

**Çözdüğü problem:** Agent'ların birbirini tanıması, keşfetmesi ve işbirliği yapması. Bu yaklaşımlar kendi içlerinde bir keşif mekanizması tanımlar: bir agent, makine tarafından okunabilir kimlik ve yetenek tanımını öngörülebilir, konvansiyonel bir konumda yayımlar; diğer agent'lar onu orada bulur. Dolayısıyla agent-to-agent bağlamında etkili bir keşif sağlarlar.

**Kapsam:** Bu yaklaşımlar genellikle keşfedilen varlığı **agent kimliği** etrafında modellemeye odaklanır. Bu belgede ele alınan problem ise daha geniş bir bağlamdadır: herhangi bir web servisinin — bir e-ticaret sitesi, bir rezervasyon servisi, bir kamu kurumu gibi — keşfedilebilir kılmak istediği farklı türden makine arayüzlerini, tek bir servis-arayüz keşif bağlamında, yalnızca alan adından başlayarak bulmaktır. Bu nedenle agent-to-agent yaklaşımları bu problem alanıyla çelişmez; ancak bu belgede ele alınan genel servis-arayüz keşfiyle aynı kapsamda değildir.

### 5.8. LLM'e Yönelik Dokümantasyon İpuçları (llms.txt ve Benzeri Konvansiyonlar)

**Amaç:** Bir sitenin, dil modeli temelli istemcilere yönelik olarak, en önemli içeriğine işaret eden, insan ve makine tarafından okunabilir, küratörlü bir özet sunması.

**Çözdüğü problem:** İçeriğin dil modelleri için sadeleştirilmiş ve küratörlü biçimde sunulması. Bir istemcinin, bir sitenin en değerli dokümantasyon ve içerik sayfalarına işaret eden bir listeye ulaşmasını sağlar.

**Kapsam:** Bu, **resmî bir IETF veya benzeri standart değil**, bir topluluk konvansiyonudur. Kapsamı, dil modellerine yönelik **içerik küratörlüğüdür**; bir servisin programatik makine arayüzlerinin varlığını ve yerini bir servis-arayüz keşfi bağlamında bildirmeyi amaçlamaz. İçeriğe işaret eder; arayüzlere değil. Bu da bu belgede tanımlanan problemden farklı bir problemdir.

### 5.9. Manzaranın Özeti (Tarafsız Karşılaştırma)

Aşağıdaki tablo, incelenen mekanizmaları tarafsız biçimde özetler. Tabloda hiçbir yerde "yetersiz" ifadesi kullanılmamıştır; bunun yerine, her mekanizmanın çözdüğü problemin **farklı** olduğu gösterilmektedir. Son sütun, mekanizmanın bu belgede tanımlanan soğuk-karşılaşma servis-arayüz keşif problemini ele alıp almadığını belirtir.

| Mekanizma | Birincil Tüketici | Çözdüğü Problem | Soğuk-Karşılaşma Servis-Arayüz Keşfini Ele Alır mı? |
|---|---|---|---|
| Tarayıcı erişim kuralları | Tarayıcı | Tarayıcı erişiminin yönetimi | Hayır — farklı problem |
| İçerik listeleme | İndeksleyici | İçerik adreslerinin numaralandırılması | Hayır — farklı problem |
| Kimlik sağlayıcı keşfi | Kimlik istemcisi | Belirli bir protokole özgü yapılandırma keşfi | Hayır — farklı problem |
| Güvenlik iletişim bilgisi | Güvenlik araştırmacısı | Güvenlik iletişimi | Hayır — farklı problem |
| LLM'e yönelik içerik ipuçları | Dil modeli istemcisi | İçerik küratörlüğü | Hayır — içeriğe işaret eder, arayüze değil |
| Arayüz açıklamaları | Programatik istemci | Bir arayüzün tarif edilmesi | Kısmen — bir arayüz bulunduktan sonra; domain-seviyesi indeksi hedeflemez |
| Agent-servis iletişim protokolleri | Agent / istemci | İstemci-servis iletişimi | Kısmen — iletişimi tanımlar; genel servis indeksini hedeflemez |
| Agent kimlik / işbirliği yaklaşımları | Agent | Agent kimliği ve işbirliği | Kısmen — varlığı agent kimliği etrafında modeller; genel servis-arayüz indeksi değildir |

Bu tablonun ortaya koyduğu örüntü, her mekanizmanın ya **farklı bir problemi** çözdüğü, ya da kendi alanında etkili bir keşif sağlasa bile bu keşfin genel bir servis-arayüz indeksi olmadığıdır. Bu, bir kusur değildir; bu mekanizmalar bunun için tasarlanmamıştır. Ortaya çıkan tablo, basitçe, henüz hiçbir mekanizmanın bu belirli problemi kendi kapsamına almamış olduğudur.

> **Bölüm Özeti.** Mevcut mekanizmalar ya içeriği listeler, ya bilinen bir arayüzü tarif eder, ya bilinen uç noktaların iletişim kurmasını sağlar, ya da bir agent'ın kimliğini agent-to-agent bağlamında keşfedilebilir kılar. Hiçbiri, herhangi bir web servisi için, yalnızca alan adından başlayan genel bir soğuk-başlangıç servis-arayüz keşif katmanı tanımlamaz.

---

## 6. Boşluk Analizi

Bir önceki bölüm, mevcut mekanizmaların her birini kendi başına inceledi. Bu bölüm, ortaya çıkan boşluğu doğrudan adlandırır ve bu boşluğun neden mevcut mekanizmaların doğal bir uzantısıyla kapanmadığını gösterir.

### 6.1. Boşluğun Tam Tanımı

Boşluk, iki sınıf mekanizma arasında yer alır. Bir yanda, **içeriğe** yönelik keşif konvansiyonları bulunur; bunlar bir sitedeki içeriğin gezilmesini ve numaralandırılmasını ele alır, ancak içerik, bir servisin **programatik arayüzleriyle** aynı şey değildir. Diğer yanda, **arayüze ve agent'a** yönelik tanımlama, iletişim ve kimlik mekanizmaları bulunur; bunlar bir arayüzün nasıl tarif edileceğini, bir istemciyle bir servisin nasıl konuşacağını veya bir agent'ın kimliğinin nasıl ifade edileceğini ele alır. Bu ikinci grup, kendi bağlamlarında etkili keşif sağlasa bile, ya ilgili arayüzün/agent'ın **bağlamına özgüdür**, ya da bir servisin **heterojen arayüzlerini tek bir indekste** toplamayı hedeflemez.

Boşluk tam olarak bu ikisinin arasındadır: bir makine tüketicisinin, **içerik gezmeden** ve **belirli bir protokolün veya agent modelinin var olduğunu önceden varsaymadan**, yalnızca bir alan adından yola çıkarak bir servisin makine arayüzlerinin varlığını ve yerini öğrenmesini sağlayacak ortak bir başlangıç noktası yoktur.

### 6.2. "Neden Mevcut Bir Mekanizma Bunu Çözmüyor?" Sorusuna Cevaplar

Deneyimli bir okuyucunun aklına haklı olarak gelecek itirazları tek tek ele almak, problemin gerçekliğini test etmenin en dürüst yoludur.

**"Arayüz açıklaması (OpenAPI) zaten bir keşif yöntemi sayılamaz mı?"**
Bir arayüz açıklaması, bir arayüzü tarif eder ve bu tarif kendi içinde bir keşif boyutu taşır. Ancak bu, **bir arayüz zaten bulunduktan sonra** geçerlidir. Açıklama, belirli bir alan adı altında kaç açıklamanın bulunduğunu, bunların nerede yayımlandığını ve servisin başka protokoller de sunup sunmadığını, alan adı seviyesinden başlayan standart bir başlangıç noktasından cevaplamaz. Yani "nasıl kullanırım?" sorusunu güçlü biçimde cevaplar; "nereden başlamalıyım?" sorusunu domain seviyesinde değil.

**"Agent-servis iletişim protokolü (MCP) bu boşluğu kapatmıyor mu?"**
İletişim protokolü, bir istemci ile bir sunucu arasındaki etkileşimi tanımlar. Ancak bir web servisinin hangi bu tür arayüzleri, varsa hangi diğer arayüzlerle birlikte sunduğunu alan adı seviyesinden başlayarak bir indekste toplamak, protokolün doğrudan kapsamı değildir. Üstelik iletişimin başlayabilmesi için ilgili sunucunun yerinin zaten bilinmesi gerekir; bu yerin yalnızca alan adından nasıl bulunacağı, protokolün hedeflediği bir soru değildir.

**"Agent kimlik ve işbirliği yaklaşımları (A2A) bu işi görmüyor mu?"**
Bu yaklaşımlar, agent-to-agent bağlamında gerçek ve etkili bir keşif tanımlar; ilgili kimlik tanımı öngörülebilir, konvansiyonel bir konumda yayımlanır. Dolayısıyla itiraz, "yerin bilindiğinin varsayılması" üzerinden kurulamaz. Ayrım başka bir eksende durur: bu yaklaşımlar genellikle keşfedilen varlığı agent kimliği etrafında modeller ve tek bir agent'a odaklanır. Bir servisin keşfedilebilir kılmak istediği farklı türden makine arayüzlerini tek bir genel indekste toplamak ise farklı bir kapsamdır. Bu yaklaşımlar güçlü bir agent-keşif katmanıdır; genel bir servis-arayüz keşif katmanı değildir.

**"Bir servis tüm bağlantılarını ana sayfasına koyabilir; agent bunları okuyamaz mı?"**
Bir agent, insanlar için biçimlendirilmiş bir sayfayı ayrıştırmaya çalışabilir. Ancak bu, web'in tarayıcı sınıfı için zaten reddettiği bir yaklaşımdır: makine tüketicisini insan-okunur sunumu yorumlamaya zorlamak kırılgandır, öngörülemezdir ve her servis için yeniden mühendislik gerektirir. Web, tam da bu nedenle tarayıcılara yönelik ortak konvansiyonları geliştirmiştir; aynı kırılganlığın agent sınıfı için kabul edilmesi, daha önce öğrenilen bir dersin göz ardı edilmesi olur.

### 6.3. Boşluğun Birleştirici İfadesi

Tüm bu itirazların ortak cevabı tek bir cümlede toplanabilir: mevcut mekanizmaların her biri ya **farklı bir problemi** çözmekte, ya **belirli bir bağlama özgü** bir keşif sağlamakta, ya da bir servisin **heterojen arayüzlerini tek bir genel indekste** toplamayı hedeflememektedir. Hiçbiri, herhangi bir web servisi için yalnızca bir alan adı verildiğinde bir makine tüketicisinin nereden başlayacağı sorusunu kendi konusu yapmaz. Boşluk gerçektir ve ancak söz konusu başlatma sorusunu açıkça kendi konusu yapan bir mekanizmayla kapanabilir.

> **Bölüm Özeti.** Boşluk, içerik keşfi ile arayüz tanımı/iletişimi/agent kimliği arasındadır. Mevcut mekanizmalar kendi bağlamlarında etkili keşif sağlayabilir; ancak hiçbiri, herhangi bir web servisinin heterojen arayüzlerini, yalnızca alan adından başlayan genel bir indekste toplamayı kendi konusu yapmaz.

---

## 7. Kullanım Senaryoları

Bu bölüm, tanımlanan problemi somut hâle getiren senaryolar sunar. Senaryoların hiçbiri bir çözüm önermez; her biri, bugün bu durumun nasıl kırılgan ve servise özgü bir çabayı gerektirdiğini ortaya koyar.

### 7.1. Kullanıcı Adına İşlem Yapan Agent

Bir kullanıcı, kişisel bir agent'tan kendisi için bir seyahat düzenlemesini ister. Agent, daha önce hiç entegre olmadığı bir havayolu şirketinin alan adıyla karşılaşır. Bilmesi gereken şey basittir: bu havayolu makine tüketilebilir bir arayüz sunuyor mu, sunuyorsa nerede? Bugün agent bu soruyu standart bir biçimde cevaplayamaz; ya bu havayolu için önceden inşa edilmiş özel bir entegrasyona güvenmek, ya insan-okunur sayfaları ayrıştırmaya çalışmak, ya da yaygın yolları tahmin etmek zorundadır. Her havayolu için bu çaba yeniden ödenir.

### 7.2. Yeni Bir Tedarikçiyi Değerlendiren Kurumsal Agent

Bir şirketin tedarik sürecini destekleyen bir agent, yeni bir yazılım tedarikçisinin sitesini değerlendirmektedir. Agent'ın, bu tedarikçinin programatik arayüzlerini ve ilgili koşullarını bulması gerekir. Bugün bu, tedarikçiye özgü bir araştırmayı gerektirir; çünkü agent, tedarikçinin arayüzlerinin var olup olmadığını ve nerede olduğunu öngörülebilir biçimde bilemez. Bu, ölçekte tekrar eden ve standartlaştırılmamış bir maliyettir.

### 7.3. Üçüncü Taraf Bir Servise Yönlendirilen Geliştirici Agent'ı

Bir geliştiricinin kodlama agent'ı, üçüncü taraf bir servisle entegrasyon kodu üretmekle görevlendirilir. Agent'ın, o servisin arayüz açıklamasını — geliştirici ilgili adresi elle vermeden — bulması beklenir. Bugün geliştirici çoğu zaman ilgili açıklamanın adresini agent'a elle sağlamak zorundadır; çünkü agent, yalnızca alan adından yola çıkarak servisin açıklamasının var olup olmadığını ve nerede olduğunu standart biçimde belirleyemez.

### 7.4. Yalnızca Tek Bir Protokol Sunan Servis

Bir servis, yalnızca tek türden bir makine arayüzü sunmaktadır; geleneksel bir HTTP arayüzü sunmuyor olabilir. Bir agent'ın yine de bu tek arayüzün varlığını ve yerini bulması gerekir. Bu senaryo, keşfin neden belirli bir protokole bağımlı olmaması gerektiğini gösterir: eğer keşif yalnızca tek bir protokol türünü varsayarsa, farklı bir protokol sunan servisler görünmez kalır.

### 7.5. Birden Çok Protokol Sunan Servis

Bir servis aynı anda birden çok türden makine arayüzü sunmaktadır: geleneksel bir HTTP arayüzü, bir sorgu arayüzü, bir agent iletişim arayüzü ve bir agent kimlik tanımı. Ancak bir agent, yalnızca alan adına bakarak bu arayüzlerin tümünün var olduğunu bilemez. Bu senaryo, problemin yalnızca "hiç arayüz yok mu?" durumuyla sınırlı olmadığını gösterir: arayüzler **bol** olduğunda bile, agent bunların listesini ve yerlerini standart biçimde öğrenemez; bir kısmını keşfedip diğerlerini gözden kaçırabilir.

> **Bölüm Özeti.** Her senaryoda agent'ın ihtiyacı basittir — "bu servisin hangi makine arayüzleri var ve nerede?" — ancak bu basit bilgiye ulaşmanın standart bir yolu yoktur. Sonuç; önceden inşa edilmiş özel entegrasyonlar, insan müdahalesi veya kırılgan tahminlerdir.

---

## 8. Bir Keşif Mekanizmasının Gereksinimleri

Bu bölüm, tanımlanan problemi çözecek **herhangi bir** mekanizmanın taşıması gereken nitelikleri sıralar. Burada kritik bir ayrım vardır: bu bölüm **çözümü tanımlamaz.** Yalnızca, makul bir çözümün karşılaması gereken gereksinimleri ortaya koyar. Çözümün biçimi, yapısı ve mekaniği RFC-0001'in konusudur.

Bu bölüm, RFC-0001 için aday gereksinimleri ifade eder; burada kullanılan normatif dil, bu belgenin bir protokol tanımladığı anlamına gelmez. Bu bölümdeki büyük harfli anahtar kelimeler, RFC 2119 ve RFC 8174 anlamlarıyla kullanılmıştır.

### 8.1. Öngörülebilirlik (Predictability)

Mekanizma, yalnızca bir alan adı bilindiğinde, önceden bir entegrasyon veya bant-dışı (out-of-band) bilgi olmaksızın bulunabilmelidir (MUST). Keşfin tüm anlamı, tahminin ortadan kaldırılmasıdır.

### 8.2. Makine Tarafından Okunabilirlik (Machine-Readability)

Mekanizma, bir programın insan-okunur sunumu yorumlamak zorunda kalmadan tüketebileceği biçimde olmalıdır (MUST). Web'in tarayıcı sınıfı için öğrendiği ders burada doğrudan geçerlidir.

### 8.3. Protokolden Bağımsızlık (Protocol Neutrality)

Mekanizma, herhangi bir tek arayüz protokolünü ayrıcalıklı kılmamalı veya varsaymamalıdır (MUST NOT). Bir servis tek bir protokol, birden çok protokol ya da hiçbiri kullanıyor olabilir; mekanizma bu durumların hepsini barındırabilmelidir (MUST).

### 8.4. Asgarilik (Minimalism)

Mekanizma, önemsiz biçimde üretilebilecek ve önemsiz biçimde tüketilebilecek kadar küçük olmalıdır (SHOULD). Keşif katmanı, ağır bir veri modeline dönüşmemelidir (SHOULD NOT). Başarılı konvansiyonlar küçük başlar ve küçük kalır.

### 8.5. Çoğaltma Değil, Yönlendirme (Indirection, Not Duplication)

Mekanizma, yetkili açıklamaların **nerede bulunduğuna** işaret etmeli; bu açıklamaların içeriğini yeniden kodlamamalıdır (SHOULD). Bu, hem katmanı küçük tutar hem de tek bir doğruluk kaynağı (single source of truth) ilkesini korur. Bu ilke, gelecekteki bir çözümü gereksiz büyümekten koruyan temel prensiptir.

### 8.6. Operatör Kontrolü (Operator Control)

Bir servisin operatörü, hangi arayüzleri keşfedilebilir kılacağını açıkça kontrol edebilmelidir (MUST). Keşfedilebilirlik, operatörün bilinçli kararına bağlı olmalıdır; bir mekanizma, operatöre neyi açığa çıkaracağı konusunda tam denetim tanımadan kullanılmamalıdır. Bu gereksinim, 11.2'de ele alınan bilgi ifşası değerlendirmesinin doğrudan karşılığıdır.

### 8.7. Geriye Dönük Uyumluluk ve Genişletilebilirlik (Backward Compatibility & Extensibility)

Mekanizma, mevcut tüketicileri bozmadan yeni ihtiyaçların eklenmesine olanak tanımalıdır (MUST). Tanımadığı bilgiyi hoşgörüyle karşılayabilmeli (MUST); yani bir tüketici, anlamadığı bir bilgiyle karşılaştığında bunu güvenle yok sayabilmelidir. Bu, ekosistemin zamanla, çekirdeği bozmadan büyümesini mümkün kılar.

### 8.8. Yetkilendirmeden Ayrışıklık (Separation from Authorization)

Bir keşif yüzeyinin var olması, ilgili kaynakların erişim hakları hakkında hiçbir ima taşımamalıdır (MUST NOT). Keşif, bir şeyin var olduğunu ve nerede olduğunu söyler; o şeye erişim hakkının olup olmadığını söylemez. Kimlik doğrulama ve yetkilendirme, mevcut standartların alanında kalmaya devam etmelidir.

### 8.9. Düşük Benimseme Maliyeti (Low Adoption Cost)

Mekanizma, sıradan bir servis operatörü tarafından, özel bir altyapı gerektirmeden uygulanabilir olmalıdır (SHOULD). Bir konvansiyonun yaygınlaşması, doğrudan onu uygulamanın kolaylığına bağlıdır.

### 8.10. Gereksinimlerin Ortak Ruhu

Bu gereksinimler birlikte okunduğunda ortaya çıkan resim; küçük, öngörülebilir, protokolden bağımsız, operatör kontrollü ve var olan standartlara saygılı bir keşif katmanıdır. Dikkat edilirse, bu bölüm hâlâ bir çözüm tarif etmemektedir; yalnızca bir çözümün taşıması gereken nitelikleri sıralamaktadır.

> **Bölüm Özeti.** Çözüm; küçük, öngörülebilir, protokolden bağımsız, operatör kontrollü, genişletilebilir ve var olan standartlara saygılı olmalıdır. Ancak bu nitelikler çözümü tanımlamaz; yalnızca sınırlarını çizer.

---

## 9. Hedef-Dışı Konular

Bu bölüm, problemi tekil ve net tutmak amacıyla, bu belgenin ve dolayısıyla tanımlanan keşif probleminin kapsamı **dışında** kalan konuları açıkça belirtir. Bu konuların her biri meşru ve önemlidir; ancak hiçbiri keşif probleminin parçası değildir ve bunların keşif problemine karıştırılması, problemi gereksiz yere büyütür ve bulanıklaştırır.

Aşağıdakiler bu belgenin ve ele alınan keşif probleminin **hedefi değildir**:

- **Yetenek (capability) ve niyet (intent) anlam bilgisi.** Bir servisin yeteneklerinin veya bir agent'ın niyetlerinin standart biçimde modellenmesi, keşiften bağımsız bir problemdir.
- **Kimlik doğrulama, yetkilendirme ve güven.** Bir kaynağa erişim hakkının nasıl belirleneceği ve tarafların birbirine nasıl güveneceği, mevcut ve gelecekteki ayrı standartların konusudur.
- **İletişim ve mesajlaşma protokolü.** Bir agent ile bir servisin nasıl konuşacağı, keşif gerçekleştikten sonra devreye giren ayrı bir problemdir ve bunun için yerleşik yaklaşımlar mevcuttur.
- **Fiyatlandırma, koşullar ve politika anlam bilgisi.** Bir servisin kullanım koşullarının, fiyatlandırmasının veya politikalarının makine tarafından okunabilir biçimde modellenmesi, keşiften ayrı bir konudur.
- **Servisler arasında seçim ve sıralama.** Bir agent'ın keşfettiği servisler arasından hangisini seçeceği — sıralama, değerlendirme, pazar yeri mantığı — keşiften sonra gelen kararların konusudur.
- **Arayüz açıklamalarının kendisi.** Arayüzlerin nasıl tarif edileceği, halihazırda mevcut standartların alanıdır. Keşif, bu açıklamaların yerini gösterir; içeriğini veya formatını yeniden tanımlamaz.

Bu hedef-dışı konuların açıkça dışarıda bırakılması, problemin gücünün kaynağıdır. Tek bir problem net biçimde çözüldüğünde, geri kalan konular onun üzerine bağımsız katmanlar olarak eklenebilir.

---

## 10. Mevcut Standartlarla İlişki

Bu bölüm, tanımlanan keşif probleminin mevcut standartlarla ilişkisini netleştirir. Buradaki temel ilke şudur: bu problem, mevcut standartların hiçbiriyle **rekabet etmez**; onlara **ortogonaldir** (orthogonal) ve onları tamamlar.

Bu ortogonallik şu biçimde ifade edilebilir:

- Arayüz açıklama standartları, **bir arayüzü tarif eder**.
- Agent-servis iletişim protokolleri, **istemci ile servis arasındaki iletişimi tanımlar**.
- Agent kimlik ve işbirliği yaklaşımları, **bir agent'ın kimliğini tanımlar ve onu agent-to-agent bağlamında keşfedilebilir kılar**.
- Burada tanımlanan keşif problemi ise, yalnızca **bunların herhangi bir web servisi bağlamında nerede bulunduğunu keşfetmeyi** konu alır.

Bu konular farklı eksenlerde durur. Biri diğerinin yerini almaz; biri diğerinin üstünde veya altında değildir. Bir keşif konvansiyonu olgunlaştığında, mevcut standartların değerini azaltmaz; tersine, onların bir agent tarafından soğuk bir karşılaşmada bulunabilmesini sağlayarak değerlerini artırır. Dolayısıyla bu belge, mevcut hiçbir standardın yerine geçme iddiası taşımaz; yalnızca, bir agent'ın bu standartların somutlaştığı arayüzleri en baştan nasıl bulacağı sorusunun henüz ortak bir cevabının olmadığını gösterir.

---

## 11. Güvenlik Değerlendirmeleri

Bu bölüm, tanımlanan problemin güvenlik boyutunu **problem düzeyinde** ele alır. Amaç, belirli bir çözümün güvenlik özelliklerini tartışmak değildir — çünkü bu belge bir çözüm önermez — yalnızca, bir keşif katmanının doğası gereği taşıdığı güvenlik değerlendirmelerine işaret etmektir.

### 11.1. Keşif, Erişim Anlamına Gelmez

Bir keşif yüzeyinin var olması, ilgili arayüzlerin herkese açık olduğu anlamına gelmez. Bir şeyin var olduğunu ve nerede olduğunu bildirmek, ona erişim hakkı vermekten tamamen ayrıdır. Kimlik doğrulama ve yetkilendirme, mevcut standartların alanında kalmaya devam eder.

### 11.2. Bilgi İfşası Değerlendirmesi

Bir keşif yüzeyi, doğası gereği bir servisin hangi arayüzlere sahip olduğunu görünür kılar. Bu, bir servis operatörü için bir değerlendirme konusudur: operatör, neyi keşfedilebilir kılacağına bilinçli olarak karar vermelidir. Bazı arayüzlerin varlığının açıkça duyurulması istenmeyebilir. Bu, mevcut keşif konvansiyonlarında da karşılaşılan bilinen bir değerlendirmedir ve 8.6'da bir gereksinim olarak da ifade edilmiştir.

### 11.3. Bütünlük ve Sahtecilik

Bir keşif yüzeyinden okunan bilginin doğruluğu ve bütünlüğü güvenlik açısından önemlidir. Yanlış veya sahte keşif bilgisi, bir agent'ı yanlış arayüzlere yönlendirebilir. Taşıma katmanı güvenliği (TLS) bu riskin önemli bir bölümünü ele alır; ek bütünlük ve özgünlük garantileri ise gelecekteki ayrı belgelerin (örneğin imza temelli bir uzantının) konusu olabilir.

### 11.4. Keşif, Güven Tesis Etmez

Bir keşif yüzeyinin, işaret ettiği arayüzlerin özgünlüğünü veya güvenilirliğini garanti etmesi beklenmez. Güvenin tesis edilmesi — bir arayüzün gerçekten iddia ettiği taraf tarafından sunulduğunun doğrulanması — keşiften ayrı bir problemdir ve bu belgenin kapsamı dışındadır.

### 11.5. Anlamsal ve Talimat Enjeksiyonu Riski

Otonom agent ekosisteminde, bir keşif yüzeyinin doğurduğu güvenlik kaygıları yalnızca taşıma güvenliği, sahtecilik ve bilgi ifşasıyla sınırlı değildir. Keşif sürecinde elde edilen bilgiler, bir agent tarafından doğrudan okunduğu ve çoğu zaman onun planlama bağlamına dâhil edildiği için, başlı başına bir saldırı yüzeyi oluşturur.

Özellikle, keşif sürecinde karşılaşılan insan-okunur açıklamalar, dokümantasyon bağlantıları, araç tanımları veya politika metinleri bir agent tarafından tüketildiğinde, bunlar **talimat enjeksiyonu (prompt injection), araç zehirlenmesi (tool poisoning) ve kötü amaçlı meta veri** için bir vektör hâline gelebilir. Bir agent, keşif yüzeyinden okuduğu betimsel meta veriyi, eğer onu güvenilir bir talimat gibi ele alırsa, kötü niyetli bir servis tarafından yönlendirilebilir.

Bu nedenle, herhangi bir çözümde ve onu tüketen her agent'ta temel bir ilke geçerli olmalıdır: **betimsel meta veri, güvenilir bir talimat olarak ele alınmamalıdır.** Keşif yüzeyinden gelen açıklamalar ve metinler, agent'ın muhakemesine yön veren bir veri kaynağı olarak değil, doğrulanması ve sınırlandırılması gereken, güvenilmeyen bir girdi olarak görülmelidir. Bu ilkenin nasıl uygulanacağı bu belgenin kapsamı dışındadır; ancak bu riskin varlığı, agent bağlamındaki herhangi bir keşif mekanizmasının olgunluğu için açıkça kaydedilmelidir.

---

## 12. Gelecek Spesifikasyon Yol Haritası

Belge boyunca, bilinçli bir tercihle, hiçbir çözüm önerilmemiştir. Bu bölümün amacı, problemin nasıl çözüleceğini anlatmak değil, çözümün **nerede** tanımlanacağını ve bu belge setinin bundan sonra nasıl şekilleneceğini belirtmektir.

### 12.1. Çözümün Yeri

Bu belgede inşa edilen problemin önerilen çözümü, ayrı bir spesifikasyon belgesi olan RFC-0001'de tanımlanmaktadır. Bu ayrım bilinçlidir: problem statement'ın görevi çözümü satmak değil, problemin gerçekliğini ortaya koymaktır. Çözümün teknik biçimi, ancak problem net biçimde anlaşıldıktan sonra anlamlı biçimde değerlendirilebilir.

### 12.2. Katmanlı Genişleme Yaklaşımı

Çözümün çekirdeğinin, bu belgenin 8. bölümünde sıralanan gereksinimlere uygun olarak **kasıtlı biçimde asgari** tutulması öngörülmektedir. Hedef-dışı olarak belirtilen konular — yetenek anlam bilgisi, güven ve imza, politika, fiyatlandırma, olay keşfi gibi — çekirdeği büyütmek yerine, onun üzerine bağımsız ve ayrı belgeler olarak eklenebilir. Böylece keşif katmanı küçük kalırken, ekosistem zamanla genişleyebilir. Bu, web'in keşif geleneğinin doğrudan bir yansımasıdır: küçük başlamak ve yeni ihtiyaçları çekirdeği bozmadan ayrı katmanlar olarak eklemek.

### 12.3. Adlandırma Üzerine Bir Not

Bu belge setinde kullanılan "ADP" adı bir **proje kod adıdır** (codename), nihai bir isim değildir. İsim, bilinçli olarak ertelenmiştir. İnternet standartları tarihinde isimler bazen yıllar sonra değişebilir; belirleyici olan, önce problemin doğru tanımlanması ve ardından çözümün teknik olarak sağlam olmasıdır. İsim, bu iki koşul sağlandıktan sonra verilecek son kararlardan biri olacaktır. Bu nokta, mevcut keşif yaklaşımlarıyla olası adlandırma örtüşmelerinin de bilinçli olarak çözümün tasarım aşamasına bırakıldığı anlamına gelir.

### 12.4. Kapanış

Bu belgenin tek bir hedefi vardı: okuyucuyu, kendi muhakemesiyle, web üzerinde bugün standartlaşmamış gerçek bir keşif probleminin var olduğu sonucuna ulaştırmak. Web'in tüketici sınıflarının evrimi, mevcut keşif manzarasının tarafsız incelemesi, boşluğun analizi, somut kullanım senaryoları ve bir çözümün taşıması gereken nitelikler — bunların tamamı bu tek sonucu inşa etmek içindir.

Bu problemin çözümü, ayrı bir spesifikasyon belgesi olan RFC-0001'de tanımlanmaktadır.

---

## Ek A. Makine Tüketicilerinin Evrimi (Özet Diyagram)

Aşağıdaki diyagram, 2. bölümde anlatılan istemci sınıflarının evrimini ve her sınıfın keşif durumunu özetler.

```
   TÜKETİCİ SINIFI            KEŞİF İHTİYACININ DURUMU
   ───────────────           ────────────────────────

   İnsan Okuyucu        →     Keşif, insanın bilişsel işlemi
        │                     (özel bir makine konvansiyonu gerekmez)
        ▼
   Tarayıcı /           →     Ortak konvansiyonlarla karşılandı
   İndeksleyici               (tarayıcı erişimi, içerik listeleme)
        │
        ▼
   Mobil Uygulama       →     Noktadan noktaya, önceden inşa edilmiş
                              (genel keşif konvansiyonu oluşmadı)
        │
        ▼
   Programatik          →     Arayüz açıklamaları yaygınlaştı
   API İstemcisi              (keşif hâlâ insan aracılığıyla)
        │
        ▼
   Otonom Agent         →     YAYGIN İHTİYAÇ VAR, ORTAK KONVANSİYON YOK
   (Bugün)                    (bu belgenin tanımladığı boşluk)
```

---

## Ek B. Bilgilendirici Referanslar

Aşağıdaki belgeler, bu çalışmanın bağlamını oluşturan mevcut standart ve konvansiyonlara işaret eder. Bu referanslar bilgilendirme amaçlıdır (informative); bu belge bir spesifikasyon olmadığından normatif referans içermez.

- RFC 2119 — Key words for use in RFCs to Indicate Requirement Levels.
- RFC 8174 — Ambiguity of Uppercase vs Lowercase in RFC 2119 Key Words.
- RFC 8615 — Well-Known Uniform Resource Identifiers (URIs).
- RFC 8288 — Web Linking.
- RFC 9309 — Robots Exclusion Protocol.
- RFC 9116 — A File Format to Aid in Security Vulnerability Disclosure (security.txt).
- OpenID Connect Discovery — OpenID Foundation.
- Sitemaps Protocol — sitemaps.org.
- OpenAPI Specification — OpenAPI Initiative (Linux Foundation).
- Model Context Protocol (MCP) — açık spesifikasyon.
- Agent2Agent (A2A) Protocol — Linux Foundation.
- llms.txt — llmstxt.org topluluk konvansiyonu.

---

## Ek C. Belge Hakkında

**Belge Türü:** Problem Bildirimi (Bağımsız Çalışma Taslağı, IETF Internet-Draft stili)
**Belge Tanımlayıcısı:** RFC-0000 (dahili proje numarası)
**Proje Kod Adı:** ADP
**Durum:** Çalışma Taslağı — Tartışmaya Açık
**İlişkili Belge:** Önerilen çözüm RFC-0001'de tanımlanmaktadır.
**Yazar:** Aybars Mete Keleş (Bağımsız)
**Tarih:** 27 Haziran 2026

> Bu belge bir IETF belgesi değildir ve herhangi bir standart organının resmî yayını olarak sunulmamaktadır. IETF Internet-Draft yazım geleneğini benimseyen, halka açık tartışma amaçlı bağımsız bir çalışma taslağıdır.
