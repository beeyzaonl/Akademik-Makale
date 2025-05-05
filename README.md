# 📚 Akademik Makale Benzerlik Motoru

## 🎯 Amaç
Bu proje, metin madenciliği ve doğal dil işleme (NLP) teknikleri kullanılarak akademik makalelerin özetlerinden anlamlı temsiller üretmeyi ve bu temsiller üzerinden benzerlik ölçümleri yapmayı hedeflemektedir.

## ÖNEMLİ: TF-IDF 100 mb üstü olduğundan drive linki koydum. Link ->
## 📁 Kullanılan Veri Seti
- **Kaynak:** [arXiv API](https://arxiv.org/help/api/)
- **Konu:** "Artificial Intelligence"
- **Boyut:** 4000 akademik makale özeti
- **Dosya:** `ai_makaleler.csv`

## 🧰 Kullanılan Kütüphaneler ve Teknolojiler
- Python 3.x
- pandas, numpy
- nltk
- matplotlib
- scikit-learn (TF-IDF)
- gensim (Word2Vec)

---

## 🔧 Proje Aşamaları

### 1. Veri Toplama
- `requests` ve `xml.etree.ElementTree` ile arXiv API üzerinden 4000 makale özeti çekildi.
- Başlık ve özetler birleştirilerek `full_text` oluşturuldu.

### 2. Zipf Analizi (Ham Metin)
- Ham verideki kelime sıklıkları sayıldı.
- Log-log grafiğiyle **Zipf Yasası** görselleştirildi.

### 3. Veri Ön İşleme
- Küçük harfe çevirme, noktalama temizliği, stopword çıkarımı
- Tokenization (kelime ayırma)
- Lemmatization (`WordNetLemmatizer`)
- `ai_clean_makaleler.csv` olarak kaydedildi.

### 4. Stem ve Lemma Sürümleri
- Lemmatized veri → `lemmatized_data.csv`
- Stemmed veri (PorterStemmer) → `stemmed_data.csv`

### 5. Temizlenmiş Veride Zipf Grafikleri
- Her iki versiyon için kelime frekansları görselleştirildi.

### 6. TF-IDF Vektörleştirme
- `TfidfVectorizer` ile 10.000 kelimeye kadar temsil oluşturuldu.
- Sonuçlar `.csv` formatında kaydedildi:
  - `tfidf_lemmatized.csv`
  - `tfidf_stemmed.csv`

### 7. Word2Vec Model Eğitimi
- CBOW ve Skip-Gram modelleri eğitildi.
- Parametre kombinasyonları:
  - window: 2, 4
  - vector size: 100, 300
- Toplamda **8 lemmatized**, **8 stemmed** model `.model` olarak kaydedildi.

### 8. Benzerlik Analizi
- Modeller `"intelligence"` ve `"intellig"` kelimeleri üzerinden test edildi.
- `most_similar()` fonksiyonu ile semantik yakınlık ölçüldü.

---

## 📊 Çıktılar
- `ai_makaleler.csv`
- `ai_clean_makaleler.csv`
- `lemmatized_data.csv`
- `stemmed_data.csv`
- `tfidf_lemmatized.csv`
- `tfidf_stemmed.csv`
- Word2Vec `.model` dosyaları (16 adet)

---

## 📝 Notlar
- Çalışmalar yalnızca `abstract` ve `title` alanlarında yapılmıştır.
- Genişletilebilir: metin kümelendirme, sınıflandırma, özetleme vb.
- Tüm grafikler `matplotlib` ile çizilmiştir.

---
