# MNIST Rakam Sınıflandırma Projesi

Bu proje, MNIST veri seti üzerinde derin öğrenme tabanlı bir rakam sınıflandırma modeli içermektedir. Model, 0-9 arası el yazısı rakamlarını sınıflandırmak için bir Yapay Sinir Ağı (YSA) kullanmaktadır.

## Proje Yapısı

```
MNIST-Classification/
│
├── MNIST-Classification.ipynb       # Ana Jupyter Notebook (tüm analiz ve kodlar)
├── README.md                        # Proje dokümantasyonu (bu dosya)
```

## Model Mimarisi

Model, 4 katmanlı bir Yapay Sinir Ağından oluşmaktadır:

1. **Giriş Katmanı**: 512 nöron, ReLU aktivasyon
2. **Gizli Katman 1**: 256 nöron, ReLU aktivasyon
3. **Gizli Katman 2**: 128 nöron, ReLU aktivasyon
4. **Çıkış Katmanı**: 10 nöron, Softmax aktivasyon

### Katman Seçim Gerekçeleri

- **ReLU Aktivasyonu**: Hesaplama verimliliği ve gradyan kaybını önleme
- **Nöron Sayıları**: 512 → 256 → 128 şeklinde kademeli azaltma
- **Softmax**: Çok sınıflı sınıflandırma için ideal çıkış aktivasyonu

## Eğitim Parametreleri

- **Optimizer**: RMSprop (learning_rate=0.001)
  - Otomatik öğrenme oranı ayarlama
  - MNIST için etkili performans
- **Loss Fonksiyonu**: Categorical Crossentropy
- **Batch Size**: 128 (bellek ve performans dengesi)
- **Epoch**: 15 (erken durdurma olmadan optimal öğrenme)
- **Validation Split**: 0.2 (eğitim verisinin %20'si doğrulama için)

## Sonuçlar ve Performans

Model test setinde **%98.18 doğruluk** elde etmiştir. Detaylı performans metrikleri:

### Karışıklık Matrisi Analizi

- En yüksek performans: 0 ve 1 rakamları (F1-score > 0.98)
- En çok karıştırılan rakamlar: 4-9, 5-3, 7-9
- Genel dengeli performans (tüm sınıflarda benzer precision ve recall)

### Sınıflandırma Raporu

```
              precision    recall  f1-score   support

           0     0.9808    0.9929    0.9868       980
           1     0.9947    0.9903    0.9925      1135
           2     0.9686    0.9874    0.9779      1032
           3     0.9792    0.9812    0.9802      1010
           4     0.9876    0.9735    0.9805       982
           5     0.9875    0.9742    0.9808       892
           6     0.9783    0.9896    0.9839       958
           7     0.9882    0.9796    0.9839      1028
           8     0.9773    0.9743    0.9758       974
           9     0.9752    0.9732    0.9742      1009

    accuracy                         0.9818     10000
   macro avg     0.9818    0.9816    0.9817     10000
weighted avg     0.9819    0.9818    0.9818     10000
```

## Kullanım

### Gereksinimler

```bash
pip install numpy matplotlib tensorflow scikit-learn seaborn
```

### Çalıştırma

1. Jupyter Notebook'u başlatın:
```bash
jupyter notebook MNIST-Classification.ipynb
```

2. Alternatif olarak, Python scriptleriyle çalıştırabilirsiniz:
```bash
python -m models.mnist_model
```

## İyileştirme Önerileri

1. **Veri Artırma (Data Augmentation)**: Yanlış sınıflandırılan örnekler için dönüşümler uygulama

2. **Model Mimarisi**:
   - Konvolüsyonel Sinir Ağları (CNN) deneme
   - Batch Normalization ekleme
   - Dropout katmanlarıyla aşırı uyumu önleme

3. **Optimizasyon**:
   - Öğrenme oranı zamanlaması (Learning Rate Scheduling)
   - Farklı optimizerlar (Adam, Nadam) test etme

4. **Detaylı Analiz**:
   - Yanlış sınıflandırılan örnekleri inceleme
   - Model kararlılığını anlama teknikleri (ör. Grad-CAM)

## Katkı

Katkıda bulunmak isterseniz lütfen fork edip pull request gönderin. Özellikle:

- Model performansını artıracak öneriler
- Kod iyileştirmeleri
- Yeni özellikler ve analizler

## Lisans

Bu proje MIT lisansı altında lisanslanmıştır. Daha fazla bilgi için `LICENSE` dosyasına bakınız.