# 🛡️ Dijital Adli Bilişim ve Olay Analizi: Otopark USB Sızma ve Veri Güvenliği İncelemesi

> **📌 SORUMLULUK REDDİ VE YASAL UYARI (DISCLAIMER):**  
> Bu rapor, siber güvenlik eğitimi kapsamındaki **simüle edilmiş (kurgusal) bir olay senaryosuna** dayanmaktadır. Raporda adı geçen "Rhetorical Hastanesi", "Jorge Bailey" vb. kurum, şahıs ve materyaller tamamen eğitim amaçlı kurgulanmıştır. Gerçek kişi veya kurumlarla bir ilgisi bulunmamaktadır.

---

## 📋 Senaryo Özet ve Metodoloji

Rhetorical Hastanesi güvenlik ekibinin bir parçası olarak, hastane otoparkında kurum logosunu taşıyan sahipsiz bir USB bellek bulunmuştur. 

Olası zararlı yazılım (Malware) bulaşma ve ağ ihlali risklerine karşı cihaz, izolasyonlu bir **sanal adli inceleme ortamında (Sandbox/Virtual Machine)** analiz edilmiş, fiziksel veya kurumsal ağ bağlantısı kesilerek içerik taraması gerçekleştirilmiştir.

---

## 🔍 İnceleme ve Bulgular

### Cihaz Aidiyeti ve İçerik Analizi
Yapılan adli incelemede, söz konusu USB belleğin **İnsan Kaynakları Müdürü Jorge Bailey**’e ait olduğu tespit edilmiştir. Cihaz içeriğinde yapılan hiyerarşik taramada aşağıdaki dosya kategorileri belirlenmiştir:

* **Kişisel Dosyalar (PII):** Aile fotoğrafları (`Family photos`), evcil hayvan fotoğrafları (`Our dog pics`), düğün davetli listeleri (`Wedding list.gslides`) ve kişisel seyahat planları (`Vacation ideas.gdoc`).
* **Kurumsal ve Hassas Veriler (SPII):** Şirkete ait maaş bütçe takip dosyası (`Employee budget.gsheet`), personel nöbet çizelgeleri (`Shift schedules.gsheet`), yeni işe alım mektupları (`New hire letter.gdoc`) ve özgeçmiş belgeleri (`JB_Resume.gdoc`).

#### 🚨 Gözlem ve Değerlendirme
Cihaz bünyesinde kişisel veriler ile kritik kurumsal verilerin bir arada bulunması (**Data Commingling / Veri Karışımı**) ve aynı taşınabilir depolama alanında saklanması, kurumun siber güvenlik duruşu açısından kritik bir zafiyet teşkil etmektedir.

---

## 🎯 Tehdit ve Saldırgan Zihniyeti Analizi (Attacker Mindset)

### 1. İç Tehdit ve Sosyal Mühendislik Senaryoları (Düşük / Orta Şiddetli Riskler)
USB belleğin kurum içi bir çalışan veya üçüncü taraf şahıslarca ele geçirilmesi durumunda; maaş bordroları, nöbet çizelgeleri ve özgeçmiş bilgileri sızdırılarak kurum içi bilgi gizliliği ihlal edilebilir. Bu durum çalışanlar arasında huzursuzluğa, kurum içi güvenin sarsılmasına ve operasyonel karmaşaya yol açabilecek bir **İç Tehdit (Insider Threat)** senaryosudur.

### 2. Gelişmiş Tehdit ve Zararlı Yazılım Enjeksiyonu (Yüksek Şiddetli Risk)
Açık alanda bırakılan veya düşürülen USB belleğin kötü niyetli bir aktör (hacker) tarafından tespit edilmesi durumunda **"Otopark USB Saldırısı" (USB Drop Attack)** senaryosu tetiklenebilir:
* **Saldırı Vektörü:** Saldırgan, USB bellek içerisine arka kapı (Backdoor), Keylogger veya zararlı bir yük (Payload) enjekte ederek cihazı tekrar eski yerine bırakabilir.
* **Etki:** Cihazın sahibi veya başka bir çalışan tarafından tekrar kurumsal bilgisayara takılması halinde, zararlı yazılım kurumsal ağa sıçrayarak (**Lateral Movement**) yetkisiz erişim, veri sızıntısı ve tüm sistem üzerinde yıkıcı bir güvenlik ihlali yaratabilir.

### 3. Hedefe Yönelik Fiziksel Güvenlik ve İstihbarat Riski (OSINT)
Bellek içerisinde yer alan "Tatil Fikirleri" gibi kişisel planlama dosyaları, tehdit aktörlerine hedef kişi hakkında kritik zamanlama bilgisi (**Açık Kaynak İstihbaratı - OSINT**) sağlamaktadır. Saldırganlar, kurbanın evden uzakta olacağı tarihleri tespit ederek hedef odaklı fiziksel hırsızlık veya kişiye yönelik sosyal mühendislik saldırıları kurgulayabilir.

---

## ⚠️ Risk Analizi ve Tehdit Değerlendirmesi (Risk Analysis)

### 1. Zararlı Yazılım Enjeksiyonu ve Ağ İhlali Riski
Bulunan USB bellek üzerinde gelişmiş zararlı yazılımların barınma ihtimali yüksektir:
* **Olay Senaryosu:** İyi niyetli bir çalışanın düşürülen cihazı tespit edip doğrulanmamış şekilde doğrudan kurumsal bilgisayara bağlaması (**Plug-and-Play**) kritik bir zincirleme reaksiyon başlatabilir.
* **Olası Etki:** Çalıştırılan zararlı yazılım; sistem kayıtlarını dinleyebilir, yetkili kimlik bilgilerini çalabilir ve kurumsal iç ağda yanal ilerleme kaydedebilir.

### 2. PII / SPII ve Kurumsal Veri Sızıntısı Riskleri
Cihaz içerisinde yer alan Kişisel Tanımlanabilir Bilgiler (**PII**) ve Hassas Kişisel Veriler (**SPII**), tehdit aktörleri açısından yüksek değerli bir veri kümesidir:
* **Bireysel ve Kurumsal Etki:** Yöneticinin kişisel ve kurumsal verileri aynı ortamda depolaması; verilerin sızması durumunda kurumsal iş sürekliliğini, finansal güvenliği ve yasal uyumluluk süreçlerini (**KVKK / GDPR**) doğrudan riske atar.

### 3. Sosyal Mühendislik ve Kurumsal Zafiyet Vektörleri
* **Hedef Odaklı Oltalama (Spear Phishing):** Elde edilen kişisel bilgiler, hedef kişiye veya aile yakınlarına yönelik inandırıcı sosyal mühendislik saldırıları kurgulanmasında kullanılabilir.
* **İç Karmaşa ve Sabotaj:** Maaş bordroları ve personel verilerinin sızması kurum içi güveni sarsabilir.
* **Ağa Yetkisiz Erişim:** Kurumsal veriler, dış tehdit aktörlerinin sistemlere yetkisiz erişim sağlaması için kritik birer giriş noktası (**Entry Point**) teşkil eder.

---

## 🛠️ Önerilen Önleyici ve Düzeltici Kontroller

1. **İdari Kontroller (Managerial Controls):**
   * Tüm çalışanlar için **Taşınabilir Medya Kullanım Politikası** ve **Sosyal Mühendislik Farkındalık Eğitimleri** zorunlu kılınmalıdır.
   * Düşürülen veya bulunan USB belleklerin yetkili güvenlik ekibine teslim edilmesi prosedürü sıkılaştırılmalıdır.

2. **Teknik Kontroller (Technical Controls):**
   * Kurumsal uç noktalarda (Endpoint) **GPO (Group Policy Object)** üzerinden yetkisiz USB depolama birimi kullanımı engellenmelidir.
   * Otomatik çalıştırma (**AutoPlay / AutoRun**) özellikleri tüm kurumsal bilgisayarlarda devre dışı bırakılmalıdır.
   * Taşınması zorunlu olan veriler için **BitLocker** vb. donanımsal/yazılımsal şifrelenmiş USB bellekler zorunlu kılınmalıdır.

3. **Operasyonel Kontroller (Operational Controls):**
   * Tüm kurum cihazlarında **EDR / Antivirüs** taramaları rutin olarak yürütülmeli ve yetkisiz USB takılma olayları **SIEM** sistemlerinde alarm olarak izlenmelidir.
