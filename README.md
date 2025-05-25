# 📚 Akademik Makale Benzerlik Motoru

## 🎯 Amaç
Bu proje, metin madenciliği ve doğal dil işleme (NLP) teknikleri kullanılarak akademik makalelerin özetlerinden anlamlı temsiller üretmeyi ve bu temsiller üzerinden benzerlik ölçümleri yapmayı hedeflemektedir. TF-IDF ve Word2Vec modelleriyle metin temsilleri oluşturulmuş ve giriş metnine en benzer 5 makale tespit edilmiştir.

## 📁 Kullanılan Veri Seti
- **Kaynak:** [arXiv API](https://arxiv.org/help/api/)
- **Konu:** "Artificial Intelligence"
- **Boyut:** 4000 akademik makale özeti
- **Dosya:** `ai_makaleler.csv`
- **Not:** TF-IDF dosyaları 100MB'tan büyük olduğu için buradan erişebilirsiniz: [Google Drive Linki](https://drive.google.com/drive/folders/1W31-ViSHExfEhxCL6TKL4wLH6oKf0a85?usp=sharing)

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
- Başlık ve özet birleştirilerek `full_text` sütunu oluşturuldu.

### 2. Zipf Analizi (Ham Metin)
- Ham verideki kelime sıklıkları hesaplandı.
- Log-log grafiği ile **Zipf Yasası** görselleştirildi.

### 3. Veri Ön İşleme
- Küçük harfe çevirme, noktalama temizliği, stopword çıkarımı
- Tokenization (kelime ayırma)
- Lemmatization (`WordNetLemmatizer`)
- Temizlenmiş veri `ai_clean_makaleler.csv` olarak kaydedildi.

### 4. Stem ve Lemma Sürümleri
- Lemmatized veri → `lemmatized_data.csv`
- Stemmed veri (PorterStemmer) → `stemmed_data.csv`

### 5. Temizlenmiş Veride Zipf Grafikleri
- Lemmatized ve stemmed sürümler için kelime frekansı grafikleri oluşturuldu.

### 6. TF-IDF Vektörleştirme
- `TfidfVectorizer` kullanılarak max. 10.000 özellikli TF-IDF temsili oluşturuldu.
- Sonuçlar `.csv` olarak kaydedildi:
  - `tfidf_lemmatized.csv`
  - `tfidf_stemmed.csv`

### 7. Word2Vec Model Eğitimi
- CBOW ve Skip-Gram algoritmaları ile modeller eğitildi.
- Parametre kombinasyonları:
  - window: 2, 4
  - vector_size: 100, 300
- Toplam **8 lemmatized**, **8 stemmed** model `.model` formatında kaydedildi.

### 8. Benzerlik Analizi
- Modeller, hem örnek kelimelerle (`most_similar`) hem de giriş metni ile tüm kayıtlar arasında cosine benzerliği hesaplayarak test edildi.
- Her model için giriş metnine en çok benzeyen 5 kayıt listelendi.
- Jaccard benzerliği ile sıralama tutarlılığı değerlendirildi.

---

## 📊 Çıktılar
- `ai_makaleler.csv`
- `ai_clean_makaleler.csv`
- `lemmatized_data.csv`
- `stemmed_data.csv`
- `tfidf_lemmatized.csv`
- `tfidf_stemmed.csv`
- 16 adet Word2Vec `.model` dosyası

---

## 📝 Notlar
- Sadece `title` ve `abstract` alanları kullanılmıştır.
- Model çıktıları, hem skorsal hem anlamsal olarak değerlendirilmiştir.
- Çalışma, metin kümelendirme, özetleme gibi daha ileri analizlerle genişletilebilir.
- Tüm grafikler `matplotlib` ile oluşturulmuştur.
