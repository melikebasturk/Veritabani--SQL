# VERİTABANI-SQL

*Birbiriyle ilişkili halinde bulunan verilerin bir arada tutuldukları yapılardır.*

**VERİ(DATA);** *Bilgisayar ortamına aktarlan, işlenmemiş bilgiler veri olarak adlandırılabilir. Bilgisayara girilen, bilgisayar tarafından saklanabilen ve işlenebilen herşeye veri denir.*

*Kullandığım veritabanı [BTK Akademide Uygulamalarla SQL Öğreniyorum ]([Uygulamalarla SQL Öğreniyorum](https://www.btkakademi.gov.tr/portal/course/uygulamalarla-sql-oegreniyorum-8249)) programında kullanılan veritabanıdır, oradan öğrendiğim bilgileri pekiştirmek adına hazırladığım döküman.*

*-Veritabanı programı olarak Micrasoft SQL Server Management Stadio 18 kullandım.*

*-ETRADE Veritabanındaki CUSTOMERS tablosu üzerinden işlemler yapıldı.*

---

## DATA MANİPÜLASYON KOMUTLARI

- **SELECT** : Veritabanındaki tablolardan kayıtları çeker.
  
  ```sql
  SELECT * FROM CUSTOMERS /*CUSTOMERS Tablosunun tamamını getirir*/
  ```
  
  ```sql
  SELECT CITY,DISTRICT FROM CUSTOMERS 
  /*CUSTOMERS Tablosundaki CITY,DISTRICT kolonlarını getirir*/
  ```

- **UPDATE** : Bir tablodaki kaydın bir ya da daha fazla alanını günceller, değiştirir.
  
  ```sql
  UPDATE CUSTOMERS SET GENDER='KADIN' WHERE GENDER='K'
  UPDATE CUSTOMERS SET GENDER='ERKEK' WHERE GENDER='E'
  /*CUSTOMERS Tablosundaki GENDER Kolonundaki K harfini KADIN ile 
  E harfin ERKEK ile değiştirir*/
  ```
  
  ```sql
  UPDATE CUSTOMERS SET AGE=DATADIFF(YEAR,BIRTHDATE,GETDATE()) 
  /*CUSTOMERS Tablosundaki BIRTHDATE kolonundaki tarihleri bugünün 
  tarihleri ile yaşları hesaplar ve AGE kolonunun içine yazar*/
  ```

- **DELETE** : Bir tablodan kayıt siler.
  
  ```sql
  DELETE CUSTOMERS WHERE ID='1000'/*CUSTOMERS Tablosundaki ID numarası
  1000 olan satır silindi.Delete komutu ile tabloyu silersek tablonun 
  yapısını bozmadan siler ve yeni girilen değerler en son kaldığı 
  sayılardan devam eder*/
  ```

- **INSERT** : Tabloya yeni kayıt ekler.
  
  ```sql
  INSERT INTO CUSTOMERS (CUSTOMERNAME,CITY,BIRTHDATE,DISTRICT,
  GENDER,NATION,AGE) VALUES ('Melike Baştürk','Zonguldak',
  '2000-04-22','Çaycuma','KADIN','TR','22') /*CUSTOMERS Tablosuna yeni 
  bir kayıt ekledi.ID değeri Primary Key olduğu için hangi sayıda 
  kaldıysa oradan devam eder*/
  ```

- **TRUNCATE** : Tablonun içini boşaltır.
  
  ```sql
  TRUNCATE TABLE CUSTOMERS /*CUSTOMERS tablosunun içini tamamen siler.
  Tablo ilk haline döner ve ID değeri ilk halindeki gibi başlar,hızlı
  işlem yapar*/
  ```
  ---
*-İstenilen verileri getirme işlemlerine ağırlık verildi.*
- **WHERE** : SQL'de Şartlı Sorgulamamalar için kullanılır
  
  ```sql
  SELECT * FROM CUSTOMERS WHERE ID=13
  /*CUSTOMERS tablosundaki ID'si 13 olanı getirir.*/
  ```
  
- **IN** : İstenilen verileri karşılaştırır ve istenilen verileri getirir. Olumsuz hali NOT IN'dir sadece IN başına NOT getirerek olumsuz hali kullanılır.
  
  ```sql
  SELECT * FROM CUSTOMERS WHERE CITY IN('ANKARA','İSTANBUL')
  /*CUSTOMERS Tablosundaki CITY kolonun içinde ANKARA ya da İSTANBUL 
  yazanları getirir.*/
  ```
  
- **AND** : İstenilen şartların hepsini karşılaması gerekiyor.
  
  ```sql
  SELECT * FROM CUSTOMERS WHERE CITY='ZONGULDAK'AND 
  AGE BETWEEN '20'AND'50' GENDER='KADIN'
  /*CUSTOMERS Tablosundaki CITY kolonundan ZONGULDAK ve AGE kolonundan 
  belirtilen yaş aralığı ve GENDER kolonundan KADIN olan ve bu şartların 
  tamamını sağlayanları getir*/
  ```
  
- **OR** : İstenilen şartların en az bir tanesini karşılaması yeterli.
  
  ```sql
  SELECT * FROM CUSTOMERS WHERE CITY='ANKARA' OR CITY='RİZE' OR CITY='MUŞ'
  /*CUSTOMERS Tablosundaki CITY kolonundan ANKARA ya da RİZE ya da MUŞ 
  yazanları getirir*/
  ```
  
  ```sql
  SELECT * FROM CUSTOMERS WHERE AGE='30' OR AGE='40' OR AGE='50'
  SELECT * FROM CUSTOMERS WHERE AGE IN('30','40','50')
  /*CUSTOMERS tablosundaki AGE kolonundan 30,40,50 yaşında olanları getirir.
  OR VE IN komutunun aynı çıktı verebildiği bir örnekdir.*/
  ```
  

- **BETWEEN** : Tablodaki bir kolonun üst ve alt limit değerleri arasındaki şartı sağlayan verileri getirir.
  
  ```sql
  SELECT * FROM CUSTOMERS WHERE AGE BETWEEN 50 AND 20
  /*CUSTOMERS tablosundaki AGE kolonundan belirtilen yaş aralığını 
  getirir*/
  ```
  
  ```sql
  SELECT * FROM CUSTOMERS WHERE BIRTHDATE BETWEEN'19900101'AND'19991231'
  /*CUSTOMERS tablosundaki BIRTHDATE kolonundan belirtilen tarih 
  aralığını getirir.*/
  ```
  

- **LIKE** : İsim string gibi ifadeler için kullanılır. Olumsuz hali NOT LIKE'dır içerisinde geçmesini istemediğimiz kelimleler gibi şeyler için kullanırız.
  
  ```sql
  SELECT * FROM CUSTOMERS WHERE CUSTOMERSNAME LIKE 'Ali%'
  /*CUSTOMERS tablosundaki CUSTOMERSNAME kolonunun içinde Ali ile başlayan
  satırları getirir.
  Ali% Ali ile başlayanları getirir.
  %Me Me ile bitenleri getirir.
  %Al% içinde Al geçenleri getir. 
  % işaret nereye geldiği önemlidir.*/
  ```
  
- **DISTINCT** : Veri tekrarını önler ve tek kolonda getirir.
  
  ```sql
  SELECT DISTINCT CITY FROM CURSOMERS
  /*CUSTOMERS tablosundaki CITY kolonundaki verileri tekrarsız listeler*/ 
  ```
  
  ```sql
  SELECT DISTINCT CITY,DISTRICT FROM CURSOMERS WHERE CITTY='ANKARA'
  /*CUSTOMERS tablosundaki CITY kolonunda olan ANKARA'nın DISTRICT 
  kolunda karşılığındaki verileri tekrarsız listeler.*/
  ```
  

- **ORDER BY** : Yapılan sorguların sıralı halde gelmesi için kullanılır. Sayıları büyükten küçüğe ya da küçükten büyüğe ve string kısmını A'dan Z'ye ya da Z'den A'ya sıralar.
  
  ```sql
  SELECT * FROM CUSTOMERS ORDER BY CITY,AGE /*CUSTOMERS tablosundaki 
  CITY ve AGE kolonlarını artan sırya göre listeler.*/
  ```
  
  ```sql
  SELECT * FROM CUSTOMERS ORDER BY ASC CITY,AGE /*CUSTOMERS tablosundaki 
  CITY ve AGE kolonlarını artan sırya göre listeler.*/
  ```
  
  ```sql
  SELECT * FROM CUSTOMERS ORDER BY DESC CITY,AGE /*CUSTOMERS tablosundaki 
  CITY ve AGE kolonlarını azalan sırya göre listeler.*/
  ```
  
  ```sql
  SELECT * FROM CUSTOMERS ORDER BY 2 /*CUSTOMERS tablosundaki 
  2 kolonuna göre artan sırayla listeler, tablonun kolon sayılarını 
  yazarak da listeleme işlemi yapabiliriz*/
  ```
  
- **TOP** : Tablonun görmek istediğimiz kadarını gösterir.
  
  ```sql
  SELECT TOP 20 * FROM CUSTOMERS /*CUSTOMERS tablosunun 20 satırını getirir.*/
  ```
  
  ```sql
  SELECT TOP 100 PERCENT * FROM CUSTOMERS /*CUSTOMERS tablosunun tamamını
  getirir. TOP 50 yazarsak yarısını getirir.*/
  ```
