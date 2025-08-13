# K-Means ile Müşteri Segmentasyonu: Alışveriş Merkezinden Veri Bilimine 🚀

Müşteri segmentasyonu, bir işletmenin müşterilerini benzer özelliklerine göre gruplandırarak onlara özel pazarlama stratejileri geliştirmesini sağlar. Bu yazıda **Mall Customers** veri seti üzerinde **K-Means clustering** ile segmentler oluşturacağız.

---

## 1️⃣ Veri Seti ve İlk İnceleme

Kullandığımız veri seti, bir alışveriş merkezinin 200 müşterisine ait:

- **Gender** (Cinsiyet)
- **Age** (Yaş)
- **Annual Income (k$)** (Yıllık gelir)
- **Spending Score (1-100)** (Harcanabilirlik skoru)

```python
df.head()
```

| CustomerID | Gender | Age | Annual Income (k$) | Spending Score (1-100) |
|------------|--------|-----|--------------------|------------------------|
| 1          | Male   | 19  | 15                 | 39                     |
| 2          | Male   | 21  | 15                 | 81                     |

Veri setinde eksik değer bulunmadı.

---

## 2️⃣ Özellik Seçimi ve Ölçeklendirme

Makine öğrenmesi modelleri farklı ölçeklerdeki verilerden olumsuz etkilenebilir. Bu yüzden tüm sayısal sütunları **StandardScaler** ile ölçeklendirdik, `Gender` sütununu sayısala çevirdik.

---

## 3️⃣ Kaç Küme Olmalı? – Elbow Method

**Elbow Method** ile küme sayısını belirledik.

![Elbow Method Grafiği](elbow_method.png)

Grafikte **k=5** civarında bir “dirsek” gözlemledik, optimum küme sayısı olarak 5 seçtik.

---

## 4️⃣ K-Means ile Segmentleme

K=5 ile modelimizi eğittik ve her müşteriyi bir kümeye atadık.

```python
from sklearn.cluster import KMeans
kmeans = KMeans(n_clusters=5, random_state=42)
df["Cluster"] = kmeans.fit_predict(df_scaled)
```

---

## 5️⃣ Görselleştirme

### 2D Scatter Plot
![2D K-Means](scatter_2d.png)

Yatay eksen: **Annual Income**  
Dikey eksen: **Spending Score**  
Renkler: Kümeler

---

### 3D Scatter Plot
![3D K-Means](scatter_3d.png)

Bu grafikte **Age**, **Annual Income** ve **Spending Score** ilişkisini aynı anda görebiliyoruz.

---

### Küme Profilleri (Heatmap)
![Heatmap](heatmap_clusters.png)

- **Cluster 0**: Yüksek gelir – düşük harcama (potansiyel müşteri)
- **Cluster 1**: Düşük gelir – yüksek harcama (fiyat duyarlı aktif müşteri)
- **Cluster 2**: Orta gelir – orta harcama (standart müşteri)
- **Cluster 3**: Yüksek gelir – yüksek harcama (VIP müşteri 💎)
- **Cluster 4**: Düşük gelir – düşük harcama (pasif müşteri)

---

## 🎯 Sonuç

Bu proje ile:
- **K-Means clustering** mantığını öğrendik
- Optimum küme sayısını belirledik
- Müşteri segmentlerini görselleştirdik
- Her segmentin özelliklerini çıkarımlar halinde listeledik

📌 **Bir sonraki adımda**, bu segmentleri kullanarak hedefe yönelik kampanya önerileri ve tahmin modelleri oluşturabiliriz.

---

✍ **Senin de bu veri seti üzerinde farklı analizlerin varsa yorumlarda paylaşabilirsin.**
