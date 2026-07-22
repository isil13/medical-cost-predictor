# Medical Insurance Cost Prediction

## Proje Özeti
Bu proje, hastaların yaş, cinsiyet, vücut kitle indeksi (VKİ), çocuk sayısı, sigara kullanımı ve yaşadıkları bölge gibi özelliklerini kullanarak sağlık sigortası masraflarını tahmin eden bir makine öğrenmesi modelidir. Proje kapsamında veriler analiz edilmiş, kategorik değişkenler işlenmiş ve **LightGBM Regressor** kullanılarak bir regresyon modeli geliştirilmiştir. Modelin performansını artırmak için hiperparametre optimizasyonu ve Box-Cox dönüşümü gibi ileri düzey teknikler uygulanmıştır.

## Veriseti
Kullanılan veri seti 1338 adet kayıt içermektedir. Veri setindeki temel özellikler şunlardır:
*   **age:** Hastanın yaşı
*   **sex:** Cinsiyet (Kadın/Erkek)
*   **bmi:** Vücut Kitle İndeksi
*   **children:** Sahip olunan çocuk sayısı
*   **smoker:** Sigara kullanım durumu (Evet/Hayır)
*   **region:** Yaşanılan bölge
*   **charges:** Bireysel tıbbi sigorta fatura tutarı (Hedef Değişken)

## Kullanılan Teknolojiler
Proje geliştirilirken aşağıdaki veri bilimi kütüphaneleri kullanılmıştır:
*   **Veri İşleme:** Pandas, NumPy
*   **Veri Görselleştirme:** Matplotlib, Seaborn
*   **Makine Öğrenmesi:** Scikit-Learn, LightGBM
*   **İstatistiksel Dönüşümler:** SciPy

## Proje Adımları ve Pipeline
1.  **Keşifçi Veri Analizi (EDA):** Veri setinin genel yapısı incelenmiş, özelliklerin dağılımı ve hedef değişken ile ilişkileri görselleştirilmiştir).
2.  **Veri Ön İşleme:** `sex` ve `smoker` değişkenleri ikili sayısal değerlere dönüştürülmüş, `region` değişkeni ise One-Hot Encoding yöntemi ile modele hazırlanmıştır.
3.  **Model Eğitimi:** İlk aşamada varsayılan parametrelerle bir LightGBM regresyon modeli eğitilmiştir.
4.  **Hiperparametre Optimizasyonu:** `RandomizedSearchCV` kullanılarak ağaç derinliği, yaprak sayısı, öğrenme oranı ve L1/L2 regülarizasyon parametreleri optimize edilmiştir.
5.  **Hedef Değişken Dönüşümü (Box-Cox):** Modelin tahmin gücünü artırmak amacıyla hedef değişkene (`charges`) SciPy kullanılarak Box-Cox dönüşümü uygulanmış ve tahmin sonuçları özel bir fonksiyon ile tekrar orijinal formata (inverse Box-Cox) dönüştürülmüştür.

## Model Performansı
Yapılan geliştirmeler sonucunda modelin $R^2$ ve MSE (Hata Kareleri Ortalaması) skorlarında adım adım elde edilen iyileşmeler aşağıdadır:
*   **Baz Model (LightGBM):** $R^2$: ~0.864
*   **Tuned Model (RandomizedSearchCV):** $R^2$: ~0.878
*   **Tuned Model + Box-Cox Dönüşümü:** $R^2$: ~0.890

Box-Cox dönüşümü sayesinde hedef değişkenin dağılımı normalleştirilmiş ve modelin doğruluk oranı en üst seviyeye taşınmıştır.
