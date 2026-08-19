# 🔍 Digital Forensics & Incident Analysis: Parking Lot USB Incident

![Cybersecurity](https://img.shields.io/badge/Focus-Digital%20Forensics%20%26%20Incident%20Response-blue)
![Role](https://img.shields.io/badge/Role-SOC%20Analyst%20%2F%20Blue%20Team-green)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

## 📌 Senaryo Özet ve Bağlam (Scenario Overview)

**Kurum:** Rhetorical Hastanesi  
**Olay:** Hastane otoparkında zemin üzerine düşürülmüş, üzerinde hastane logosu bulunan bir USB bellek tespit edilmiştir.  
**Uygulanan Prosedür:** Fiziksel olarak bulunan bilinmeyen USB bellek, doğrudan kurumsal ağa bağlı bir bilgisayara takılmamış; izole edilmiş sanal çalışma istasyonunda (Sandbox/Virtual Environment) dijital adli incelemeye tabi tutulmuştur.

> ⚠️ **Güvenlik Notu:** Yabancı veya düşürülmüş USB belleklerin doğrudan kurumsal sistemlere bağlanması "USB Drop Attack" zafiyeti doğurur. İzolasyonlu sanal ortam kullanımı, olası zararlı yazılımların iç ağa yayılmasını önlemiştir.

---

## 📂 USB Bellek Dizin Yapısı ve Delil İncelemesi

İzole adli ortamda yapılan dosya ve dizin taramasında elde edilen ekran görüntüsü aşağıdadır:

![Jorge's USB Directory Structure](./assets/jorges_usb_contents.png)

### 📊 Dosya İnceleme Tablosu

| Klasör / Dosya Adı | Türü | Veri Sınıflandırması | Risk Seviyesi |
| :--- | :--- | :--- | :--- |
| `Family photos` / `Our dog pics` | Klasör | Kişisel Tanımlanabilir Bilgi (PII) | Düşük |
| `New hire letter.gdoc` | Doküman | İK / Kurumsal Veri | Orta |
| `Vacation ideas.gdoc` | Doküman | Bireysel Planlama / OSINT Verisi | Orta |
| `Shift schedules.gsheet` | Tablo | Operasyonel Çalışan Verisi | Yüksek |
| `Employee budget.gsheet` | Tablo | Finansal / Maaş Bordrosu (SPII) | **Kritik** |
| `Wedding list.gslides` | Sunum | Kişisel Veri | Düşük |
| `JB_Resume.gdoc` | Doküman | Özgeçmiş / PII | Orta |

---

## 🔎 İnceleme ve Bulgular (Analysis & Findings)

### 1. Cihaz Aidiyeti ve İçerik Analizi
İzolasyonlu sanal ortamda gerçekleştirilen dijital adli incelemede, söz konusu USB belleğin **İnsan Kaynakları Müdürü Jorge Bailey**’e ait olduğu tespit edilmiştir. Cihaz içeriğinde yapılan detaylı hiyerarşik taramada aşağıdaki dosya kategorileri belirlenmiştir:

* **Kişisel Dosyalar:** Kullanıcıya ait aile fotoğrafları, evcil hayvan görselleri, düğün davetli listesi ve tatil planları.
* **Kurumsal ve Hassas Dosyalar:** Hastaneye ait maaş bordroları, vardiya çizelgeleri, yeni işe alınan personelin mektupları ve işe alım özgeçmişleri.

> **Gözlem ve Değerlendirme:** Cihaz bünyesinde kişisel veriler ile kritik kurumsal verilerin bir arada bulunması ve aynı depolama alanında saklanması (**Data Commingling**), güvenlik açısından kritik bir zafiyet teşkil etmektedir.

---

## 🎯 Tehdit ve Saldırgan Zihniyeti Analizi (Attacker Mindset)

### 1. İç Tehdit ve Sosyal Mühendislik Senaryoları *(Düşük / Orta Şiddet)*
Söz konusu USB belleğin kurum içi bir çalışan veya üçüncü bir şahıs tarafından ele geçirilmesi durumunda, içerikte yer alan maaş bordroları ve özgeçmiş bilgileri sızdırılarak kurum içi bilgi gizliliği ihlal edilebilir. Bu durum, çalışanlar arasında huzursuzluğa, kurum içi güvenin sarsılmasına ve operasyonel karmaşaya yol açabilecek bir **İç Tehdit (Insider Threat)** senaryosudur.

### 2. Gelişmiş Tehdit ve Zararlı Yazılım Enjeksiyonu *(Yüksek Şiddet)*
Açık alanda bırakılan veya düşürülen USB belleğin kötü niyetli bir aktör (hacker) ya da hoşnutsuz bir çalışan tarafından tespit edilmesi durumunda **"Otopark USB Saldırısı" (USB Drop Attack)** senaryosu tetiklenebilir.
* **Saldırı Vektörü:** Saldırgan, USB bellek içerisine Arka Kapı (Backdoor), Keylogger veya zararlı bir yük (Payload) enjekte ederek cihazı tekrar eski yerine bırakabilir.
* **Etki:** Cihazın sahibi veya başka bir çalışan tarafından tekrar kurumsal bilgisayara takılması halinde, zararlı yazılım kurumsal ağa sıçrayarak (**Lateral Movement**) yetkisiz erişim, veri sızıntısı ve tüm sistem üzerinde kritik seviyede güvenlik zafiyeti yaratabilir.

### 3. Hedefe Yönelik Fiziksel Güvenlik ve İstihbarat Riski *(OSINT)*
Bellek içerisinde yer alan `Vacation ideas.gdoc` (Tatil Fikirleri) gibi kişisel planlama dosyaları, tehdit aktörlerine hedef kişi hakkında kritik zamanlama bilgisi (**Açık Kaynak İstihbaratı - OSINT**) sağlamaktadır. Saldırganlar, Jorge Bailey’in evden uzakta olacağı tarihleri bu dosyalar üzerinden tespit ederek hedef odaklı fiziksel hırsızlık veya kişiye yönelik sosyal mühendislik saldırıları kurgulayabilir.

---

## 🛡️ Risk Analizi ve Tehdit Değerlendirmesi (Risk Analysis)
