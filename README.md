[Playlist](https://www.youtube.com/playlist?list=PLKnjBHu2xXNOooo9pcx5Dw-6zOyk1rwyO)


# Create & Delete Table
```sql
create table musteri
(
    id integer primary key not null,
    firstname varchar(15) not null,
    lastname varchar(15) not null,
    city text
)

delete table urun
```

# Insert Rows
```sql
insert into musteri (id, firstname, lastname, city) values (6, 'Ayşe', 'Yıldırım', 'İzmir')
```

# Query
```sql
-- SELECT, WHERE
SELECT *  FROM musteri
SELECT soyisim FROM musteri
SELECT * FROM musteri WHERE isim='Mehmet'
SELECT * FROM musteri WHERE isim='Mehmet' and id=4
select * from musteri where bakiye>10000 or bakiye <= 5000
select * from musteri where sehir='Adana' or (bakiye >= 8000 and soyisim='Yıldırım')

-- LIKE
select * from musteri where isim like '%a%'
select * from musteri where isim not like '%e%'

-- DELETE
delete from musteri where id=10

-- TRUNCATE
truncate table musteri -- müşteri tablosundaki tüm verileri siler

```

# Modifying Data
```sql
update musteri set bakiye=8000 where id=1
```

# Count, Max, Min, Sum, Average
```sql
-- COUNT
select Count(*) from musteri
select Count(*) from musteri where sehir='Ankara'

-- SUM
select sum(bakiye) from musteri
select sum(bakiye) from musteri where sehir='Ankara'
select sum(bakiye) from musteri where sehir!='Ankara'

-- AVG
select avg(bakiye) from musteri where sehir='İstanbul'

-- MIN & MAX
select min(bakiye) from musteri where sehir='İstanbul'
select max(bakiye) from musteri where sehir='İstanbul'
select max(bakiye) - min(bakiye) from musteri
```

# GROUP BY
```sql
select sehir, count(*) as kisi from musteri group by sehir
```
![image](https://user-images.githubusercontent.com/37713845/151696583-c2117a29-7993-4a5b-bf26-824efad5e8eb.png)

```sql
select sehir, count(*) as kisi from musteri group by sehir order by count(*) desc
```
![image](https://user-images.githubusercontent.com/37713845/151696623-f5dea791-b5c1-4eb1-bab7-2fc08da13d32.png)


```sql
select sehir, sum(bakiye) from musteri group by sehir order by sum(bakiye) desc 
```
![image](https://user-images.githubusercontent.com/37713845/151696699-19494e7b-7363-496e-b506-5e8b2fd678a9.png)

# HAVING
```sql
select sehir, avg(bakiye) from musteri group by sehir having avg(bakiye) >= 10000 and sehir like '%e%'
```
![image](https://user-images.githubusercontent.com/37713845/151697380-4b4cd2de-bde0-4437-8520-2685992c040b.png)


# SUB QUERY
```sql
select * from musteri where bakiye=(select max(bakiye) from musteri where sehir='İstanbul')
```
![image](https://user-images.githubusercontent.com/37713845/151698190-245c7784-2c95-4a1f-84c1-667315e44a8f.png)


```sql
select * from musteri where meslek=(select id from meslek where ad='mühendis') or meslek=(select id from meslek where ad='doktor')
```
![image](https://user-images.githubusercontent.com/37713845/151698535-c6b3f8bf-e44c-4acc-8d17-efc135755da5.png)


# INNER JOIN
```sql
select isim, soyisim, meslek.ad as meslek from musteri inner join meslek on musteri.meslek = meslek.id
```
![image](https://user-images.githubusercontent.com/37713845/151699218-f5fa9021-42ca-40a5-ad23-968ba45bb879.png)


```sql
select * from fakulte
select * from bolum
select fakulte.ad, count(*) from bolum inner join fakulte on bolum.bolumf = fakulte.id group by fakulte.ad
```
![image](https://user-images.githubusercontent.com/37713845/151700221-41ecab5f-f412-4244-95db-c450abe84fbe.png)
![image](https://user-images.githubusercontent.com/37713845/151700225-08749322-57f7-4b27-a232-55b041e82e1a.png)
![image](https://user-images.githubusercontent.com/37713845/151700231-95c4657d-4743-488e-b431-580c15b0250c.png)

```sql
select fakulte.ad, count(*) as toplam from bolum inner join fakulte on bolum.bolumf=fakulte.id group by fakulte.ad order by toplam desc limit 1
```
![image](https://user-images.githubusercontent.com/37713845/151700942-e0176f4e-f7dd-4433-8294-9206b6696830.png)





