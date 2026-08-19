# 🛡️ DFIR Analysis: Parking Lot USB Incident Report

![Cybersecurity](https://img.shields.io/badge/Security-DFIR-blue?style=for-the-badge)
![Incident Response](https://img.shields.io/badge/Task-Incident%20Analysis-red?style=for-the-badge)
![Platform](https://img.shields.io/badge/Environment-Isolated%20Sandbox-green?style=for-the-badge)

## 📌 Senaryo Özeti
Rhetorical Hastanesi güvenlik ekibinin bir üyesi olarak, sabah saatlerinde otopark zemininde hastane logosu taşıyan şüpheli bir USB bellek tespit edilmiştir. Cihaz, potansiyel zararlı yazılımların kurumsal ağa sıçramasını önlemek amacıyla **izole edilmiş sanal ortam (sandbox)** üzerinde dijital adli incelemeye tabi tutulmuştur.

---

## 📂 Dijital Adli İnceleme ve USB İçeriği

Sanal ortamda yapılan dosya sistemi taramasında cihaz içeriği ve dizin yapısı aşağıdaki gibi tespit edilmiştir:

![USB İçerik Ekran Görüntüsü](./usb-drive-contents.png)

### 📊 Cihaz Dizin ve Dosya Hiyerarşisi
```text
Jorge's USB/
├── 📁 Family photos/               [Kişisel - PII]
├── 📁 Our dog pics 🐩/             [Kişisel - PII]
├── 📄 New hire letter.gdoc          [Kurumsal / İK - Hassas Veri]
├── 📄 Vacation ideas.gdoc           [Kişisel - Zamanlama Bilgisi]
├── 📊 Shift schedules.gdsheet       [Kurumsal - Operasyonel Veri]
├── 📊 Employee budget.gdsheet       [Kurumsal / Finans - Hassas Veri]
├── 📊 Wedding list.gsslides         [Kişisel - PII]
└── 📄 JB_Resume.gdoc                [Kişisel / Kurumsal - PII]
