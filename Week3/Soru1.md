```SQL
select name,
       car.id as car_id,
       car.model as car_model,
       manufacture.year as manufacture_year,
       array(select as struct temp.id, timestamp_add(temp.date, interval 3 hour) as date from unnest(purchase) as temp) as purchase
from `dsmbootcamp.sample.semi_structured_hw`
cross join unnest(car) as car
cross join unnest(manufacture) as manufacture 
on car.id = manufacture.id;
```