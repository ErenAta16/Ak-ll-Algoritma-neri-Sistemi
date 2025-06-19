# 🤖 Akıllı Algoritma Öneri Sistemi

[![Python Version](https://img.shields.io/badge/python-3.8%2B-blue)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Status](https://img.shields.io/badge/status-active-success.svg)]()
[![Project Type](https://img.shields.io/badge/project-recommendation%20system-orange)]()

**İleri Veri Analitiği Final Projesi** - Grup Çalışması

**Takım Üyeleri:** Hatice Soğancı, Fatih Kocatahtacı, Görkem Taha Çanakcı

## 🎯 Proje Amacı

Bu proje, makine öğrenmesi dünyasındaki en büyük zorluklardan birini çözmek için geliştirilmiştir: **doğru algoritma seçimi**. Kullanıcıların proje gereksinimlerine göre 229 farklı ML algoritması arasından en uygun olanları otomatik olarak öneren akıllı bir karar destek sistemidir.

## 🚀 Sistem Özellikleri

- **229 ML Algoritması** kapsamlı veri havuzu
- **16 Değerlendirme Kriteri** ile çok boyutlu analiz
- **Ward Clustering** ile 10 akıllı algoritma grubu
- **Otomatik Öneri Sistemi** - kullanıcı kriterlerine göre algoritma önerisi
- **Gerçek Zamanlı Analiz** - anında sonuç alma
- **Kapsamlı Görselleştirme** - 15 detaylı grafik ve rapor

## 📊 Veri Seti İçeriği

### Ana Veri Seti: `Algoritma_Veri_Seti.xlsx`
**Boyut:** 229 algoritma × 17 özellik

| Özellik Kategorisi | Özellikler | Açıklama |
|-------------------|------------|-----------|
| **Kategorik Kriterler** | Öğrenim Türü (7 seçenek) | Denetimli, Denetimsiz, Derin Öğrenme, vb. |
| | Kullanım Alanı (71 seçenek) | Görüntü İşleme, NLP, Sınıflandırma, vb. |
| | Karmaşıklık Düzeyi (5 seçenek) | Düşük → Çok Yüksek |
| | Veri Büyüklüğü (5 seçenek) | Küçük → Çok Büyük |
| | Donanım Gereksinimi (9 seçenek) | Düşük → Yüksek |
| **Sayısal Kriterler** | Popülerlik Skor (0.0-1.0) | Algoritmanın yaygınlık derecesi |
| | Aşırı Öğrenme Eğilimi Skor | Overfitting riski |
| | Fine-tune Gerekliliği Skor | İnce ayar ihtiyacı |

## 🏗️ Sistem Mimarisi

### 1. Veri İşleme Pipeline
```
Veri Seti (229×17) → One-Hot Encoding → Standardization → PCA (%95 varyans) → 110 bileşen
```

### 2. Kümeleme Analizi
```python
Ward Clustering (n_clusters=10)
├── Küme 0: Klasik Algoritmalar (37 algoritma)
├── Küme 1: Gelişmiş Denetimli (65 algoritma)  
├── Küme 2: Denetimsiz Öğrenme (31 algoritma)
├── Küme 3: Karar Ağaçları (46 algoritma)
├── Küme 4: Boosting Algoritmaları (29 algoritma)
└── ...
```

### 3. Öneri Sistemi Algoritması
```python
def recommend_algorithm(user_requirements):
    # Her küme için uygunluk skoru hesapla
    cluster_scores = calculate_cluster_scores(user_requirements)
    
    # En uygun kümeyi seç
    best_cluster = max(cluster_scores)
    
    # Algoritmaları popülerlik skoruna göre sırala
    recommendations = sort_by_popularity(best_cluster)
    
    return top_5_algorithms
```

## 📁 Proje Yapısı

```
algoritma_yedek/
├── 📁 algorithms/
│   ├── analyze_dataset.py          # Veri seti analizi
│   ├── clustering_analysis.py      # Ana kümeleme analizi
│   ├── Veri_seti.csv              # CSV formatında veri
│   ├── Veri_seti.xlsx             # Excel formatında veri
│   ├── requirements.txt           # Python bağımlılıkları
│   └── README.md                  # Bu dosya
├── 📁 models/
│   ├── kmeans_model.joblib        # K-means modeli (33.2 KB)
│   └── ward_model.joblib          # Ward modeli (9.1 KB)
├── 📁 visualizations/
│   ├── 📁 clustering/             # Kümeleme görselleri (8 dosya)
│   ├── 📁 metrics/                # Metrik görselleri (7 dosya)
│   └── 📁 analysis/               # Analiz görselleri
├── Algoritma_Veri_Seti.xlsx       # Ana veri seti
└── cluster_characteristics.json   # Küme karakteristikleri
```

## 🚀 Kurulum ve Çalıştırma

### 1. Gereksinimler
```bash
pip install -r requirements.txt
```

**Gerekli Paketler:**
- pandas >= 1.3.0
- numpy >= 1.21.0
- scikit-learn >= 1.0.0
- matplotlib >= 3.4.0
- seaborn >= 0.11.0
- joblib >= 1.0.0

### 2. Hızlı Başlangıç
```bash
# Ana analizi çalıştır
python clustering_analysis.py

# Veri seti analizini çalıştır  
python analyze_dataset.py
```

### 3. Örnek Kullanım
```python
# Kullanıcı gereksinimleri
user_requirements = {
    'Öğrenim Türü': 'Derin Öğrenme',
    'Kullanım Alanı': 'Görüntü İşleme',
    'Karmaşıklık düzeyi': 'Yüksek',
    'Veri büyüklüğü': 'Büyük'
}

# Algoritma önerisi al
recommendations = recommend_algorithm(user_requirements)
print(recommendations)
```

## 📈 Performans Metrikleri

### Model Karşılaştırması (Optimal Küme Sayılarında)

| Metrik | K-means (17 küme) | Ward (20 küme) | Kazanan |
|--------|-------------------|----------------|---------|
| **Silhouette Score** | 0.0436 | **0.0603** | Ward ✅ |
| **Calinski-Harabasz** | 4.15 | **4.66** | Ward ✅ |
| **Davies-Bouldin** | 2.2138 | **1.9849** | Ward ✅ |
| **Model Boyutu** | 33.2 KB | **9.1 KB** | Ward ✅ |
| **Stabilite** | 0.4163 (ARI) | **1.0000** | Ward ✅ |

### Sistem Performansı
- **✅ Toplam Algoritma:** 229
- **✅ Küme Sayısı:** 10 grup
- **✅ Özellik Boyutu:** 214 → 110 (PCA)
- **✅ Silhouette Score:** 0.0603
- **✅ Toplam Boyut:** 5.11 MB

## 🎯 Kullanım Senaryoları

### 📷 Senaryo 1: Görüntü İşleme Projesi
```python
# Girdi
user_input = {
    'Öğrenim Türü': 'Derin Öğrenme',
    'Kullanım Alanı': 'Görüntü İşleme',
    'Karmaşıklık düzeyi': 'Yüksek'
}

# Çıktı
recommended = ['CNN', 'ResNet', 'Vision Transformer', 'EfficientNet']
```

### 📊 Senaryo 2: Basit Sınıflandırma
```python
# Girdi  
user_input = {
    'Öğrenim Türü': 'Denetimli Öğrenme',
    'Kullanım Alanı': 'Sınıflandırma',
    'Karmaşıklık düzeyi': 'Düşük'
}

# Çıktı
recommended = ['Logistic Regression', 'Naive Bayes', 'Decision Tree']
```

### 💬 Senaryo 3: NLP Projesi
```python
# Girdi
user_input = {
    'Öğrenim Türü': 'Derin Öğrenme', 
    'Kullanım Alanı': 'Doğal Dil İşleme',
    'Karmaşıklık düzeyi': 'Çok Yüksek'
}

# Çıktı  
recommended = ['LSTM', 'Transformer', 'BERT', 'GPT']
```

## 📊 Görselleştirmeler

### Kümeleme Görselleri (8 dosya - 2.89 MB)
- `dendrogram.png` - Hiyerarşik kümeleme ağacı
- `pca_clusters.png` - PCA ile küme görselleştirmesi  
- `cluster_characteristics_table.png` - Küme özellik tablosu
- `kumeleme_sonuclari.png` - Kümeleme sonuçları özeti

### Metrik Görselleri (7 dosya - 2.13 MB)
- `optimal_clusters.png` - Optimal küme sayısı analizi
- `model_performance.png` - Model performans karşılaştırması
- `dirsek_yontemi.png` - Elbow method grafiği
- `metrics_comparison.png` - Metrik karşılaştırma

## 🔧 Gelişmiş Özellikler

### API Endpoint'leri (Gelecek Sürüm)
```python
POST /api/recommend
GET /api/algorithms/{cluster_id}  
GET /api/criteria
GET /api/performance
```

### Web Arayüzü (Planlanan)
- Flask/Django tabanlı web uygulaması
- Interaktif algoritma seçim arayüzü
- Gerçek zamanlı öneri sistemi
- Kullanıcı geri bildirim sistemi

## 🤝 Takım ve Katkıda Bulunma

### 👥 Proje Takımı
- **Hatice Soğancı** - Veri Analizi ve Görselleştirme
- **Fatih Kocatahtacı** - Kümeleme Algoritmaları ve Model Optimizasyonu  
- **Görkem Taha Çanakcı** - Sistem Mimarisi ve Öneri Motoru

### 🔄 Katkıda Bulunma
1. Bu repoyu fork edin
2. Yeni bir branch oluşturun (`git checkout -b feature/amazing-feature`)
3. Değişikliklerinizi commit edin (`git commit -m 'Add amazing feature'`)
4. Branch'inizi push edin (`git push origin feature/amazing-feature`)
5. Pull Request oluşturun

## 📄 Lisans

Bu proje MIT lisansı altında lisanslanmıştır. Detaylar için `LICENSE` dosyasını inceleyiniz.

## 📞 İletişim

Proje hakkında sorularınız için:
- 📧 Email: [proje-email@domain.com]
- 💼 LinkedIn: [Takım üyelerinin LinkedIn profilleri]
- 🐙 GitHub: [Bu repository]

---

⭐ **Bu projeyi beğendiyseniz yıldız vermeyi unutmayın!**

**Proje Durumu:** ✅ Tamamlandı | 🚀 Geliştirme Devam Ediyor
