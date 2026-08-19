# 🛡️ Dijital Adli Bilişim ve Olay Analizi: Otopark USB Sızma ve Veri Güvenliği İncelemesi

> **📌 SORUMLULUK REDDİ VE YASAL UYARI (DISCLAIMER):**  
> Bu rapor, siber güvenlik eğitimi kapsamındaki **simüle edilmiş (kurgusal) bir olay senaryosuna** dayanmaktadır. Raporda adı geçen "Rhetorical Hastanesi", "Jorge Bailey" vb. kurum, şahıs ve materyaller tamamen eğitim amaçlı kurgulanmıştır. Gerçek kişi veya kurumlarla bir ilgisi bulunmamaktadır.

---

## 📋 Senaryo Özet ve Metodoloji

Rhetorical Hastanesi güvenlik ekibinin bir parçası olarak, hastane otoparkında kurum logosunu taşıyan sahipsiz bir USB bellek bulunmıştır. 

Olası zararlı yazılım (Malware) bulaşma ve ağ ihlali risklerine karşı cihaz, izolasyonlu bir **sanal adli inceleme ortamında (Sandbox/Virtual Machine)** analiz edilmiş, fiziksel veya kurumsal ağ bağlantısı kesilerek içerik taraması gerçekleştirilmiştir.

---

## 🔍 İnceleme ve Bulgular

### 📂 Cihaz İçi Dosya Dizini ve Hiyerarşi (Adli İnceleme Görünümü)

Adli inceleme ortamında (Google Drive / Sanal Sürücü) elde edilen cihaz içi dizin yapısı şu şekildedir:

```text
📁 Jorge's USB (E Sürücüsü)
├── 📁 Folders (Klasörler)
│   ├── 📁 Family photos                 [Kişisel / PII]
│   └── 📁 Our dog pics 🐩               [Kişisel / PII]
└── 📄 Files (Dosyalar)
    ├── 📝 New hire letter.gdoc          [Kurumsal / SPII]
    ├── 📝 Vacation ideas.gdoc           [Kişisel / OSINT Riski]
    ├── 📊 Shift schedules.gsheet        [Kurumsal / Operasyonel]
    ├── 📊 Employee budget.gsheet        [Kurumsal / Finansal Hassas Veri]
    ├── 📊 Wedding list.gslides          [Kişisel / PII]
    └── 📝 JB_Resume.gdoc                [Kurumsal & Kişisel / PII]
