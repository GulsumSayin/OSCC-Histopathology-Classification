# 🧬 Oral Squamous Cell Carcinoma (OSCC) Histopathology Classification

Bu proje, histopatolojik ağız içi görüntülerini kullanarak **Oral Skuamöz Hücreli Karsinom (OSCC)** ve **normal epitel** sınıflarını ayırt eden bir derin öğrenme modeli geliştirmeyi amaçlamaktadır. Çalışmanın hedefi, sınırlı veriyle yüksek doğruluk sunan, açıklanabilir ve güvenilir bir yapay zeka sistemi oluşturmaktır.  


## 📁 Veri Seti
Bu projede kullanılan veri seti, **Mendeley Data** platformundan alınmış olup DOI numarası:

🔗 **10.17632/ftmp4cvtmb.1**

- Görüntüler H&E boyalı histopatolojik doku kesitleridir.
- Leica ICC50 HD mikroskobu ile **100×** ve **400×** büyütmede elde edilmiştir.
- Toplam **1224 görüntü** bulunmaktadır:
  - **Normal epitel:** 290
  - **OSCC:** 934

Bu durum sınıf dengesizliği oluşturduğu için veri artırma uygulanmıştır.

---

## 🔁 Veri Artırma & Bölünme
Her sınıf için görüntü sayısı artırılarak **1500’e eşitlenmiştir**.  
Kullanılan augmentasyon teknikleri:

- Döndürme
- Zoom
- Yatay çevirme
- Kaydırma (shift)

Veri seti **StratifiedShuffleSplit** ile 3’e ayrılmıştır:

- **Eğitim:** 2400  
- **Doğrulama:** 300  
- **Test:** 300  

Tüm görüntüler 224×224 boyutuna yeniden ölçeklendirilmiş ve 1/255 oranında normalize edilmiştir.

---

## Kullanılan Modeller

Bu projede 6 farklı derin öğrenme mimarisinin performansı karşılaştırılmıştır:

1. **InceptionResNetV2**  
2. **CBAM-ResNet50V2**  
3. **InceptionV3**  
4. **DenseNet121**  
5. **EfficientNetV2B0**  
6. **CBAM-MobileNetV2**

Ortak noktalar:

- ImageNet ön eğitimi
- Fine-tuning ile tüm/son katmanların eğitimi
- Adam / Adamax optimizer
- Label smoothing veya Focal Loss
- EarlyStopping & ReduceLROnPlateau callback’leri

---

## 📊 Değerlendirme Metrikleri

Model performansı aşağıdaki metriklerle ölçülmüştür:

- **Accuracy**
- **Precision**
- **Recall**
- **F1-Score**
- **ROC-AUC**
- **Cohen’s Kappa**
- **Confusion Matrix**
- **ROC Curve**

---

## 🔍 Açıklanabilirlik (Explainable AI)

Model kararlarını daha şeffaf hale getirmek için:

### 📌 **Grad-CAM**
- Modelin karar verirken görüntünün hangi bölgelerine odaklandığını ısı haritası olarak gösterir.
- Klinik açıdan yorumlanabilirliği artırır.

### 📌 **Integrated Gradients**
- Piksel bazında karar katkısını hesaplar.
- Grad-CAM’e göre daha ince detayları açıklayabilir.
