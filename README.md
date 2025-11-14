# 🚀 Twitter Sentiment Analysis: GOJEK vs GRAB

Analisis sentimen 500 tweet tentang **GOJEK** dan 500 tweet tentang **GRAB**, lengkap mulai dari scraping, preprocessing, ekstraksi fitur, klasifikasi sentimen, hingga visualisasi hasil.

---

## 📌 Fitur Proyek

* Scraping Twitter menggunakan **Twikit**
* Preprocessing teks: case folding, tokenizing, stopword removal, normalisasi, stemming
* Ekstraksi fitur: **TF-IDF**
* Analisis sentimen: **Naive Bayes / SVM / Logistic Regression**
* Wordcloud positif, negatif, dan netral
* Perbandingan jumlah sentimen per brand
* Visualisasi dengan Matplotlib


## 🔧 Scraping Tweet (Twikit)

Scraping 500 tweet per keyword:

```python
from twikit import Client

client = Client('en-US')
client.load_cookies('cookies.json')

tweets = await client.search('gojek', limit=500)
```

---

## 🧹 Text Preprocessing

Langkah yang digunakan:

* Case folding
* Tokenizing
* Stopword removal (dengan ekstra stopword custom)
* Normalisasi kata tidak baku
* Stemming (Sastrawi)

```python
extra_sw = {"rt", "via", "amp"}
stop_words = stop_words.union(extra_sw)
```

---

## 🧠 Feature Extraction

Menggunakan **TF-IDF Vectorizer**:

```python
from sklearn.feature_extraction.text import TfidfVectorizer
vectorizer = TfidfVectorizer(max_features=5000)
X = vectorizer.fit_transform(clean_text)
```

---

## 🤖 Sentiment Classification

Model yang digunakan:

* Logistic Regression
* Naive Bayes
* SVM

Contoh training:

```python
from sklearn.linear_model import LogisticRegression
model = LogisticRegression(max_iter=200)
model.fit(X_train, y_train)
```

---

## 📊 Visualisasi

### Grafik Perbandingan Sentimen

```python
ax = df.groupby(['keyword','ml_label']).size().unstack(fill_value=0)
ax.plot(kind='bar')
```

### Wordcloud

```python
from wordcloud import WordCloud
wc = WordCloud(width=800, height=400).generate(' '.join(text))
```

---

## 📈 Hasil Analisis

* Sebagian besar tweet cenderung **netral** karena tweet informatif/promosi
* Sentimen positif dan negatif muncul terutama dari pengalaman pengguna
* Gojek & Grab memiliki pola yang mirip, namun Grab sedikit lebih banyak keluhan soal layanan

---

## 🛠 Instalasi

```
pip install -r requirements.txt
python src/scraper.py
python src/train_model.py
```

---

## 📄 Lisensi

MIT License

---

## 🤝 Kontribusi

Pull request sangat diterima! Buat branch baru sebelum melakukan perubahan.

---

## ⭐ Dukungan

Kalau repo ini membantu, jangan lupa **⭐ star** repo-nya!
