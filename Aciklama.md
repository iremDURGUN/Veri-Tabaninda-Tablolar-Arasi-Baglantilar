## Bağlantı Türleri:
### •	Bire-Çoklu (One-to-Many): 
Bu en yaygın kullanılan bağlantı türüdür. Bir tabloda bir satırdaki veri, diğer tabloda birden fazla satıra bağlı olabilir. Örneğin, bir "Müşteriler" tablosu ve bir "Siparişler" tablosu olduğunu varsayalım. Bir müşteri birden fazla sipariş verebilir, bu nedenle "Müşteriler" tablosundaki her satır "Siparişler" tablosundaki birden fazla satıra bağlı olabilir. Bu bağlantı türünde, "Müşteriler" tablosundaki Primary Key, "Siparişler" tablosundaki Foreign Key ile ilişkilendirilir.
## Örneğin:
## Siparisler
```
+------------+-----+--------+-----
| ID | musteriID | siparisTarihi | -----
+------------+-----+-------+--------
|     1      | 5 | 10.01.2024 | -----------
|     2     | 2 | 15.02.2024 |-------
+------------+-----+-------+--------
```
* Siparisler tablosunda yukardaki gibi musteriID kolonuyla iki tablo One to Many olarak bağlanır.

### Kod:
### SQL
```SQL
SELECT musteriler.ad, siparisler.urunID, siparisler.siparisTarih
FROM musteriler
INNER JOIN siparisler ON musteriler.ID = siparisler.musteriID;
```

**Açıklama:** Bu örnekte, "musteriler" tablosu ve "siparisler" tablosu One to Many bağlantısı ile ilişkilendirilmiştir. "Müşteriler" tablosundaki her satır, "Siparişler" tablosundaki birden fazla satıra bağlı olabilir. Kod, her iki tablodan da veri seçmek için bir INNER JOIN kullanır.

### •	Çok-Çok (Many-to-Many):
Bu bağlantı türünde, bir tabloda birden fazla satırdaki veriler, diğer tabloda birden fazla satıra bağlı olabilir. Örneğin, bir "Ürünler" tablosu ve bir "Kategoriler" tablosu olduğunu varsayalım. Bir ürün birden fazla kategoriye ait olabilir ve bir kategori birden fazla ürüne ait olabilir. Bu bağlantı türünde, bir ara tablo kullanılır. Ara tablo, her iki tablodaki Primary Key içeren iki sütuna sahiptir.

## Örneğin:
## araTablo
```
+------------+-----+
| urunID | katagoriID  |
+------------+-----+
|     1      | 5 |
|     9      | 2|
+------------+-----+
```
* Bu tablo katagoriler ve urunlerin olduğu iki tablo arasında bağlantı kurmamızı sağlar. Bu sayede tabloda tekrar eden veri girişi olmaz.

### Tablolar:
**•	urunler** (ID, Ad, Fiyat)

**•	kategoriler** (ID, Ad)

**•	araTablo** (urunID, kategoriID)

### Kod:
### SQL
```SQL
SELECT urunler.Ad, urunler.Fiyat, kategoriler.Ad
FROM urunler
INNER JOIN araTablo ON urunler.ID = araTablo.urunID
INNER JOIN Kategoriler ON araTablo.kategoriID = kategoriler.ID;
```

**Açıklama:** Bu örnekte, “urunler" tablosu ve "kategoriler" tablosu Many to Many bağlantısı ile ilişkilendirilmiştir. Bir ürün birden fazla kategoriye ait olabilir ve bir kategori birden fazla ürüne ait olabilir. Kod, her üç tablodan da veri seçmek için iki INNER JOIN kullanır.

### •	Tek-Tek (One-to-One):
Bu bağlantı türünde, bir tabloda bir satır, diğer tabloda sadece bir satıra bağlı olabilir. Örneğin, bir "Kişiler" tablosu ve bir "Adresler" tablosu olduğunu varsayalım. Bir kişiye sadece bir adres atanabilir. Bu bağlantı türünde, "Kişiler" tablosundaki birincil anahtar, "Adresler" tablosundaki yabancı anahtar ile ilişkilendirilir.

## Örneğin:
## adresler
```
+------------+-----+
| ID | kisiID | adres  |
+------------+-----+
|     1 | 9 | Talatpaşa Mahallesi Boz Caddesi Daire:8 |
|     2 | 1 | Dere Mahallesi 98. Cadde Daire:2|
+------------+-----+
```
## kisiler
```
+------------+-----+
| ID | ad  | soyad |
+------------+-----+
|     1      | Kaan | Aydın |
|     9      | Naz | Gürbüz |
+------------+-----+
```

* Burada adres tablosunda tutulan adreslerin ID bilgisi kişiler tablosunda adresID kolonu ile bağlanır. Var olan adresID’ nin tuttuğu adres’ te bir kişi yaşıyabilir. Yani kisiler tablosunda tekrar eden bir adresID yoktur.


### Tablolar:
**•	kisiler** (ID, Ad, Soyad)

**•	adresler** (ID, KisiID, adres)

### Kod:
### SQL

```SQL
SELECT kisiler.Ad, kisiler.Soyad, adresler.adres
FROM kisiler
INNER JOIN adresler ON kisiler.ID = adresler.kisiID;
```

**Açıklama:** Bu örnekte, "kisiler" tablosu ve "adresler" tablosu bir tek-tek bağlantısı ile ilişkilendirilmiştir. Bir kişiye sadece bir adres atanabilir. Kod, her iki tablodan da veri seçmek için bir INNER JOIN kullanır.

---

## Bağlantı Kurma:

Veritabanında tablolar arası bağlantı kurmak için çeşitli yöntemler kullanılır. En yaygın yöntemler şunlardır;

**•	Primary Key:** Bir tabloda, başka bir tablodaki birincil anahtara referans veren bir sütundur.

**•	Birleştirmeler (Joins):** Birden fazla tablodaki verileri tek bir tabloda birleştirmek için kullanılır.

**•	Görünümler (Views):** Birden fazla tablodaki verileri tek bir sanal tabloda görüntülemek için kullanılır.

---

### Bağlantıların Önemi:
Veritabanındaki tablolar arası bağlantılar, birçok önemli amaca hizmet eder:
**•	Veri Tutarlılığı:** Veritabanındaki verilerin tutarlı ve güncel olmasını sağlar.

**•	Veri Erişilebilirliği:** Birden fazla tablodan veriye kolayca erişmenize olanak tanır.

**•	Veri Analizi:** Farklı tablolar arasındaki ilişkileri analiz etmenize olanak tanır.

* Veritabanı tasarımında tablolar arası bağlantıları doğru şekilde kullanmak, veritabanının verimli ve etkili bir şekilde çalışmasını sağlar.
---
### EKSTRA ÖRENKLER:
#### One-to-One (Bir-Bir) İlişkisi:

* Bir-Bir ilişkisi, bir tablodaki her satırın diğer tablodaki tam olarak bir satırla eşleştiği bir ilişki türüdür. Örneğin, bir calısanlar tablosu ve bir maaslar tablosu düşünelim. Her çalışanın tam olarak bir maaşı vardır ve her maaş tam olarak bir çalışana aittir.


#### SQL
```SQL
CREATE TABLE calısanlar (
ID INT PRIMARY KEY,
ad VARCHAR(100),
soyad VARCHAR(100)
);

CREATE TABLE maaslar (
ID INT PRIMARY KEY,
miktar DECIMAL(10, 2),
calısanID INT,
FOREIGN KEY (calısanID) REFERENCES calısanlar(ID)
);

```

#### One-to-Many (Bir-Çok) İlişkisi:

* Bir-Çok ilişkisi, bir tablodaki bir satırın diğer tablodaki birden çok satırla eşleştiği bir ilişki türüdür. Örneğin, bir ogretmenler tablosu ve bir ogrenciler tablosu düşünelim. Bir öğretmenin birden çok öğrencisi olabilir, ancak her öğrencinin tam olarak bir öğretmeni vardır.


#### SQL
```SQL
CREATE TABLE ogretmenler (
ID INT PRIMARY KEY,
ad VARCHAR(100),
soyad VARCHAR(100)
);

CREATE TABLE ogrenciler (
ID INT PRIMARY KEY,
ad VARCHAR(100),
soyad VARCHAR(100),
ogretmenID INT,
FOREIGN KEY (ogretmenID) REFERENCES ogretmenler(ID)
);
```
#### Many-to-Many (Çok-Çok) İlişkisi:

* Çok-Çok ilişkisi, bir tablodaki bir satırın diğer tablodaki birden çok satırla ve tersi durumun da geçerli olduğu bir ilişki türüdür. Örneğin, bir Öğrenciler tablosu ve bir Dersler tablosu düşünelim. Bir öğrencinin birden çok dersi olabilir ve bir dersi birden çok öğrenci alabilir. Bu tür bir ilişkiyi modellemek için genellikle bir ara tablo kullanılır.


#### SQL
```SQL
CREATE TABLE ogrenciler (
ID INT PRIMARY KEY,
ad VARCHAR(100),
soyad VARCHAR(100)
);

CREATE TABLE dersler (
ID INT PRIMARY KEY,
ders_adı VARCHAR(100)
);

CREATE TABLE ogrenciDersleri (
ogrenciID INT,
dersID INT,
PRIMARY KEY (ogrenciID, dersID),
FOREIGN KEY (ogrenciID) REFERENCES ogrenciler(ID),
FOREIGN KEY (dersID) REFERENCES dersler(ID)
);
```

## Öğrenciler
```
+------------+-----+-------+
| öğrenci_id | ad  | soyad |
+------------+-----+-------+
|     1      | Ali | Veli  |
|     2      | Ayşe| Fatma |
+------------+-----+-------+
```
## Dersler
```
+--------+----------+------------+
| ders_id | ders_adı | öğrenci_id |
+--------+----------+------------+
|   1     | Matematik|     1      |
|   2     | Fizik    |     1      |
|   3     | Kimya    |     2      |
+--------+----------+------------+
```

* Bu örnekler, SQL’deki ilişkisel veritabanı modellemesinin temel prensiplerini göstermektedir. Her biri farklı türdeki ilişkileri temsil eder ve verilerin organize ve tutarlı bir şekilde saklanmasını sağlar. Bu tür bir yapı, veritabanı tasarımında çok önemlidir ve veritabanının performansını ve verimliliğini büyük ölçüde etkiler.



