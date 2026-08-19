# 🔍 Dijital Adli İnceleme ve Risk Analiz Raporu: Otopark USB Olayı

![Category](https://img.shields.io/badge/Category-Digital_Forensics_%26_Risk_Analysis-blue.svg)
![Environment](https://img.shields.io/badge/Environment-Isolated_Sandbox_VM-green.svg)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen.svg)

> [!NOTE]
> **Yasal Uyarı / Disclaimer:** Bu proje, siber güvenlik farkındalığı ve adli inceleme pratikleri geliştirmek amacıyla hazırlanmış **kurgusal bir senaryodan (Lab Scenario)** ibarettir. Raporda yer alan kişi, kurum, görsel ve belgeler tamamen simülasyon amaçlıdır; gerçek kişi veya kurumlarla bir ilgisi bulunmamaktadır.

## 📌 Olay Özet Raporu (Executive Summary)

Rhetorical Hastanesi otoparkında bulunan, üzerinde hastane logosu basılı USB bellek, kurum içi ağlardan tamamen izole edilmiş bir sanal makine (Sandbox / VM) ortamında dijital adli incelemeye tabi tutulmuştur.

Yapılan analizler sonucunda cihazın **İnsan Kaynakları Müdürü Jorge Bailey**’e ait olduğu doğrulanmış, cihaz içerisinde hem kritik kurumsal verilerin hem de kişisel dosyaların bir arada saklandığı tespit edilmiştir.

---

## 📸 Cihaz Analizi ve Dosya Yapısı

Cihaz içeriğinde tespit edilen dosya ve klasör yapısı aşağıda detaylandırılmıştır:

<img src="Jorge%20Bailey%20USB%20.png" width="700" alt="Jorge Bailey USB Drive">

### 📂 Dosya ve İçerik Sınıflandırması

| Kategori | İçerik / Dosya Adı | Açıklama / Hassasiyet Derecesi |
| :--- | :--- | :--- |
| **Kişisel Klasörler** | `Family photos`, `Our dog pics 🐩` | Kullanıcıya ait özel aile ve evcil hayvan fotoğrafları. |
| **Kişisel Dosyalar** | `Vacation ideas.gdoc`, `Wedding list.gslides` | Tatil planları ve özel etkinlik detayları (OSINT riski). |
| **Kurumsal / PII** | `New hire letter.gdoc`, `JB_Resume.gdoc` | Yeni işe alınan personel bilgileri ve özgeçmiş belgeleri. |
| **Finansal / Kritik** | `Shift schedules.gsheet`, `Employee budget.gsheet` | Çalışan vardiya düzeni, maaş bordroları ve departman bütçesi. |

> ⚠️ **Kritik Zafiyet Tespiti:** Cihaz bünyesinde kişisel veriler (PII) ile kritik kurumsal/finansal verilerin aynı depolama alanında harmanlanmış şekilde saklanması, veri gizliliği ve kurumsal güvenlik politikaları açısından ciddi bir ihlaldir.

---

## 🎯 Saldırgan Zihniyeti ve Tehdit Senaryoları (Threat Modeling)

### 1. İç Tehdit ve Sosyal Mühendislik Senaryoları *(Düşük / Orta Şiddetli Risk)*
Söz konusu USB belleğin kurum içi bir çalışan veya üçüncü bir şahıs tarafından ele geçirilmesi durumunda; içerikte yer alan maaş bordroları, bütçe verileri ve özgeçmiş bilgileri sızdırılarak kurum içi bilgi gizliliği ihlal edilebilir. 
* **Etki:** Çalışanlar arasında huzursuzluk, adalet duygusunun zedelenmesi ve kurum içi güvenin sarsılmasına yol açabilecek bir **İç Tehdit (Insider Threat)** senaryosudur.

### 2. Gelişmiş Tehdit ve Zararlı Yazılım Enjeksiyonu *(Yüksek Şiddetli Risk)*
Açık alanda düşürülen USB belleğin kötü niyetli bir aktör veya hoşnutsuz bir çalışan tarafından tespit edilmesi durumunda **"Otopark USB Saldırısı" (USB Drop Attack)** tetiklenebilir.
* **Saldırı Vektörü:** Saldırgan, USB bellek içerisine arka kapı (*Backdoor*), *Keylogger* veya zararlı bir yük (*Payload*) enjekte ederek cihazı tekrar eski yerine bırakabilir.
* **Etki:** Cihazın doğrudan kurumsal bilgisayara takılması halinde (*Plug-and-Play*), zararlı yazılım kurumsal ağa sıçrayarak (**Lateral Movement**) yetkisiz erişim, veri sızıntısı ve tüm sistem üzerinde kritik seviyede güvenlik ihlali yaratabilir.

### 3. Hedefe Yönelik Fiziksel Güvenlik ve OSINT Riski *(Açık Kaynak İstihbaratı)*
Bellek içerisinde yer alan `Vacation ideas.gdoc` gibi kişisel planlama dosyaları, tehdit aktörlerine hedef kişi hakkında kritik zamanlama bilgisi (**OSINT**) sağlamaktadır.
* **Etki:** Saldırganlar, Jorge Bailey’in evden veya işten uzak olacağı tarihleri bu dosyalar üzerinden tespit ederek hedef odaklı fiziksel hırsızlık veya kişiye yönelik **Sosyal Mühendislik / Spear Phishing** saldırıları kurgulayabilir.

---

## ⚡ Detaylı Risk Analizi (Risk Assessment)

### 🚨 1. Zararlı Yazılım Enjeksiyonu ve Ağ İhlali Riski
Bulunan USB bellek üzerinde şu anda *Backdoor*, *Keylogger* veya *Trojan* gibi gelişmiş zararlı yazılımların barınma ihtimali bulunmaktadır.
* **Olay Senaryosu:** İyi niyetli bir çalışanın düşürülen cihazı tespit edip doğrulanmamış bir şekilde İK Müdürü Jorge Bailey’e teslim etmesi ve cihazın doğrudan kurumsal bilgisayara bağlanması zincirleme bir reaksiyon başlatabilir.
* **Olası Etki:** Çalıştırılan zararlı yazılım; sistem kayıtlarını dinleyebilir, yetkili kimlik bilgilerini çalabilir ve kurumsal iç ağa sıçrayarak (**Lateral Movement**) şirket genelinde yıkıcı bir siber güvenlik krizine yol açabilir.

### 🔐 2. PII / SPII ve Kurumsal Veri Sızıntısı Riskleri
Cihaz içerisinde yer alan **Kişisel Tanımlanabilir Bilgiler (PII)** ve **Hassas Kişisel Veriler (SPII)**, tehdit aktörleri açısından yüksek değerli bir veri kümesidir.
* **Bireysel ve Kurumsal Etki:** Üst düzey bir yöneticinin kişisel ve kurumsal verileri aynı ortamda depolaması, verilerin yetkisiz kişilerin eline geçmesi durumunda kurumsal iş sürekliliğini, finansal güvenliği ve yasal uyumluluk süreçlerini (**KVKK / GDPR**) doğrudan riske atmaktadır.

### 🛡️ 3. Sosyal Mühendislik ve Kurumsal Zafiyet Vektörleri
Söz konusu USB belleğin barındırdığı verilerin sızdırılması durumunda ortaya çıkacak temel zafiyetler şunlardır:
1. **OSINT ve Hedef Odaklı Oltalama (Spear Phishing):** Elde edilen bilgiler kullanılarak hedef kişiye veya aile yakınlarına yönelik son derece inandırıcı sosyal mühendislik saldırıları kurgulanabilir.
2. **İç Karmaşa ve Kurumsal Sabotaj:** Şirkete ait maaş bordroları ve personel özgeçmişlerinin sızdırılması, çalışanlar arasında huzursuzluk yaratarak kurum içi güveni sarsabilir.
3. **Ağa Yetkisiz Erişim:** Kurumsal veriler ve olası zafiyet noktaları, dış tehdit aktörlerinin sistemlere yetkisiz erişim sağlaması için kritik birer giriş noktası (**Entry Point**) teşkil eder.

---

## 💡 Tavsiyeler ve Önleyici Tedbirler (Remediation & Countermeasures)

1. **USB ve Medya Güvenliği Politikası (GPO):** Kurumsal cihazlarda yetkisiz USB bellek kullanımını engellemek için Grup İlkesi (GPO) üzerinden depolama birimleri kısıtlanmalıdır.
2. **Veri Sınıflandırılması ve Şifreleme:** Kurumsal veriler ile kişisel veriler kesinlikle ayrıştırılmalı; taşınabilir depolama cihazları donanımsal veya yazılımsal olarak (örn. BitLocker) şifrelenmelidir.
3. **Farkındalık Eğitimleri:** Çalışanlara sokakta veya otoparkta bulunan USB belleklerin doğrudan bilgisayarlara takılmaması, derhal Güvenlik/SOC ekibine teslim edilmesi gerektiği konusunda eğitimler verilmelidir.
4. **İzole Analiz (Sandbox) Standardı:** Bulunan tüm harici medya araçları yalnızca izole edilmiş sanal ortamlarda veya dedicated adli inceleme istasyonlarında analize tabi tutulmalıdır.
