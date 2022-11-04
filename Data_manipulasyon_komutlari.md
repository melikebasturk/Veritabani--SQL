# VERİTABANI-SQL

*Birbiriyle ilişkili halinde bulunan verilerin bir arada tutuldukları yapılardır.*

**VERİ(DATA);** *Bilgisayar ortamına aktarlan, işlenmemiş bilgiler veri olarak adlandırılabilir. Bilgisayara girilen, bilgisayar tarafından saklanabilen ve işlenebilen herşeye veri denir.*

*Kullandığım veritabanı [BTK Akademide Uygulamalarla SQL Öğreniyorum ]([Uygulamalarla SQL Öğreniyorum](https://www.btkakademi.gov.tr/portal/course/uygulamalarla-sql-oegreniyorum-8249)) programında kullanılan veritabanıdır, oradan öğrendiğim bilgileri pekiştirmek adına hazırladığım döküman.*

*-Veritabanı programı olarak Micrasoft SQL Server Management Stadio 18 kullandım.*

*-ETRADE Veritabanındaki CUSTOMERS tablosu üzerinden işlemler yapıldı.*

---

##### DATA MANİPÜLASYON KOMUTLARI

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
  
  


