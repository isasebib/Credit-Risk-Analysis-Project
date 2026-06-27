# 📊 Credit Risk Analysis

**Veri Bilimi Final Projesi**

---

## 👤 Proje Ekibi

| Alan | Bilgi |
|------|-------|
| **Ad Soyad** | İsa Şebib |
| **Öğrenci Numarası** | 1306220177 |
| **Proje Türü** | Bireysel |

---

## 📁 Proje Yapısı

```
Veri-Bilimi-Final-Projesi/
│
├── notebooks/
│   └── credit_risk_nb.ipynb           # Ana notebook (EDA, modelleme, bulgular)
│
├── datasets/
│   ├── raw_credit_risk_dataset.csv    # Ham veri seti (Kaggle'dan indirilen)
│   └── processed_dataset.csv         # Temizlenmiş ve özellik mühendisliği uygulanmış veri
│
├── dashboards/
│   └── Credit Risk Dashboard.pbix    # Power BI interaktif dashboard (ek çalışma)
│
├── Project-Report.pdf                # Kısa rapor (3-5 sayfa, Türkçe)
├── prompt_log.md                     # Geliştirme sürecinde kullanılan AI promptları
└── README.md                         # Bu dosya
```

---

## 📦 Kullanılan Kütüphaneler

| Kütüphane | Sürüm | Kullanım Amacı |
|-----------|-------|----------------|
| `numpy` | ≥1.24 | Sayısal hesaplamalar, dizi işlemleri |
| `pandas` | ≥2.0 | Veri yükleme, temizleme, gruplama |
| `matplotlib` | ≥3.7 | Temel görselleştirmeler (histogram, scatter) |
| `seaborn` | ≥0.12 | İstatistiksel görselleştirmeler (heatmap, barplot) |
| `scikit-learn` | ≥1.3 | Lojistik Regresyon, model değerlendirme |

Kurulum:
```bash
pip install numpy pandas matplotlib seaborn scikit-learn
```

---

## 🗂️ Veri Kaynağı

| Alan | Bilgi |
|------|-------|
| **Veri Seti Adı** | Credit Risk Dataset |
| **Kaynak** | [Kaggle — laotse/credit-risk-dataset](https://www.kaggle.com/datasets/laotse/credit-risk-dataset) |
| **Lisans** | CC0: Public Domain |
| **Kayıt Sayısı** | 32,574 (temizleme sonrası) |
| **Hedef Değişken** | `loan_status` (0 = İyi Kredi, 1 = Temerrüt) |

---

## 🚀 Projeyi Çalıştırma

1. Repoyu klonlayın:
```bash
git clone https://github.com/isasebib/credit-risk-analysis.git
cd credit-risk-analysis
```

2. Gerekli kütüphaneleri yükleyin:
```bash
pip install numpy pandas matplotlib seaborn scikit-learn
```

3. Veri setini indirin:
   - [Kaggle](https://www.kaggle.com/datasets/laotse/credit-risk-dataset) adresinden `credit_risk_dataset.csv` dosyasını indirin
   - Notebook içindeki `pd.read_csv()` satırını kendi dosya yolunuzla güncelleyin

4. Jupyter Notebook'u başlatın:
```bash
jupyter notebook Credit-risk.ipynb
```

5. Tüm hücreleri sırayla çalıştırın (**Kernel → Restart & Run All**)

---

## 🔬 Araştırma Soruları

1. Kredi geçmişi uzunluğu, temerrüt olasılığını nasıl etkiler?
2. Hangi kredi amacı en yüksek temerrüt riskini taşır ve bu durum faiz oranlarıyla örtüşüyor mu?
3. Üç mühendislik özelliğinden hangisi temerrüdü en iyi tahmin eder: istihdam istikrarı, kredi/gelir oranı veya kredi yük endeksi?

---

## 📈 Model Sonuçları

| Metrik | Değer |
|--------|-------|
| Doğruluk (Accuracy) | %83.61 |
| ROC-AUC | 0.8323 |
| Temerrüt Duyarlılığı (Recall) | %41 |

---

## 📊 Ek Görselleştirme — Power BI Dashboard

Veri setinin interaktif görselleştirmesi için Power BI dashboard'u hazırlanmıştır.

| Alan | Bilgi |
|------|-------|
| **Dosya** | `dashboard/Credit_Risk_Dashboard.pbix` |
| **Araç** | Microsoft Power BI Desktop |
| **İçerik** | Kredi riski dağılımı, müşteri segmentleri, risk metrikleri |

> ⚠️ Açmak için [Power BI Desktop](https://powerbi.microsoft.com/desktop/) gereklidir (ücretsiz).

---

## 🤖 AI Kullanımı

Bu proje AI yardımıyla geliştirilmiştir. Geliştirme sürecinde kullanılan tüm AI promptları kronolojik sırayla `prompt_log.md` dosyasında belgelenmiştir.
