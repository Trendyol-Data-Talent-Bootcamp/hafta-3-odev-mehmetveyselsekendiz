# Soru 1

dsmbootcamp.sample.semi_structured_hw tablosunda 2 kişinin sahip olduğu araç bilgileri ve bu araçları satın alma tarihleri yer almaktadır.  
Beklenen dsmbootcamp.sample.semi_structured_hw tablosunu kullanarak dsmbootcamp.sample.semi_structured_hw_expected tablosundaki veriyi oluşturmaktır.

- name kolonunu seçmek
- car ve manufacture arraylerini unnest ederek her iki array içindeki id kolonları üzerinden joinlemek
- Unnest ettiğimiz bu 2 array içinden car.id, car.model ve manufacture.year alanlarını uygun aliaslar ile seçmek
- purchase array'i içindeki date kolonundaki her değere 3 saat eklemek ve purchase kolonunu tekrar array olarak tutmak


```SQL

create or replace table `dsmbootcamp.veysel_sekendiz.week3_answer` as
select name,car.id as car_id, car.model as car_model, manufacture.year as manufacture_year,
array( select as struct p.id, timestamp_add(p.date, interval 3 hour) as date from unnest(purchase) as p )as purchase
from `dsmbootcamp.veysel_sekendiz.semi_structured_hw`
cross join unnest(car) as car
cross join unnest(manufacture) as manufacture
where car.id= manufacture.id

```
