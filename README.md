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


<img src="https://www.arasindakifark.net/wp-content/uploads/2016/03/sql_joins.jpg" width="75%" />

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

# LEFT JOIN
```sql
select * from bolum
select * from fakulte
```
![image](https://user-images.githubusercontent.com/37713845/151717466-2ee1f105-1d31-4155-b271-eb15b201b817.png)
![image](https://user-images.githubusercontent.com/37713845/151717470-b6639824-d2ec-4079-b2bc-73a083ca02b4.png)

```sql
select * bolumid, bolum.ad, fakulte.ad from bolum left join fakulte on bolum.bolumf = fakulte.id
```
![image](https://user-images.githubusercontent.com/37713845/151717477-035505cb-a12a-45c4-b55d-bb43d70877e5.png)


```sql
select * bolumid, bolum.ad, fakulte.ad from fakulte left join bolum on bolum.bolumf = fakulte.id
```
![image](https://user-images.githubusercontent.com/37713845/151717488-a0d0c970-67f9-4e21-bc82-fc62b17010d8.png)

# INTERSECT & EXCEPT & UNION
```sql
select * from bolum2
select * from bolum3
```
![image](https://user-images.githubusercontent.com/37713845/151772259-0b760e2d-0433-495e-ba02-e177ff960121.png)
![image](https://user-images.githubusercontent.com/37713845/151772276-15699afb-354f-4a72-add6-57061a341308.png)
```sql
select * from bolum2
intersect
select * from bolum3

select * from bolum2
except
select * from bolum3

select * from bolum2
union
select * from bolum3
```
![image](https://user-images.githubusercontent.com/37713845/151772333-703e18fa-dc40-4f7e-8998-dfb143fe2425.png)
![image](https://user-images.githubusercontent.com/37713845/151772350-d6b92169-fec0-426a-9e95-49658beb4dc2.png)
![image](https://user-images.githubusercontent.com/37713845/151772613-6f19ca01-2685-4c6c-a035-156f1d0ed8db.png)


# [SQL Server Functions](https://www.w3schools.com/sql/sql_ref_sqlserver.asp)

# VIEW
```sql
create view view1
as
select bolumid, bolum.ad, fakulte.ad as fakulte_ismi from bolum inner join fakulte on fakulte.id = bolum.bolumf

select * from view1
```
![image](https://user-images.githubusercontent.com/37713845/151782970-dbb394bb-1fcf-4ab9-aaa3-645fbbd05466.png)


# FUNCTION
```sql
create function toplam(s1 int, s2 int)
returns int
language plpgsql
as
$$
declare
	sonuc integer;
begin
	sonuc:=s1+s2;
	return sonuc;
end;
$$;

select toplam(2,3)
```
![image](https://user-images.githubusercontent.com/37713845/151790502-12269131-c027-4aa7-8426-11ba363625cb.png)


```sql
create function kdvli(fiyat float)
returns float
language plpgsql
as
$$
begin
fiyat := fiyat*1.08;
return fiyat;
end;
$$;


select ad, fiyat, kdvli(fiyat) from kitaplar
```
![image](https://user-images.githubusercontent.com/37713845/151791433-935a5d76-6f31-407e-97af-81399e52ec2d.png)


```sql
create function kitapgetir(param varchar)
returns table (
	idsutun int,
	kitapadsutun varchar,
	kitapyazarsutun varchar
)
language plpgsql
as
$$
begin
	return query 
		select id, ad, yazar from kitaplar where ad like param;
end;
$$;

select * from kitapgetir('%ikayesi%')
```
![image](https://user-images.githubusercontent.com/37713845/151792638-83d11ee0-ff85-4180-8d18-579f52885ea8.png)


# TRIGGER
### Trigger Function
```sql
create or replace function test()
returns trigger
as
$$
begin
update toplamfakulte set toplam=toplam+1;
return new;
end;
$$
language 'plpgsql'
```

### Trigger
```sql
create trigger testtrig
after insert
on fakulte
for each row
execute procedure test()
```

```sql
insert into fakulte (id, ad) values (5, 'konservatuar')
```
![image](https://user-images.githubusercontent.com/37713845/151796619-f47dde8e-b075-4b35-9f33-2465c18c1fab.png)
![image](https://user-images.githubusercontent.com/37713845/151796676-cd17c99f-e1fb-49f4-b7c9-defd86ee6005.png)



