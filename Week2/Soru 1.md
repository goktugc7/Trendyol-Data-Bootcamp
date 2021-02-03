```SQL
SELECT * FROM (
    SELECT Sport, Country, COUNT(1) as Medals, ROW_NUMBER() OVER(PARTITION BY SPORT ORDER BY COUNT(1) desc) AS Row
    FROM `dsmbootcamp.sample.summer_medals`
    WHERE Medal is not null and year >= 1980
    GROUP BY Sport, Country
    ORDER BY Sport, COUNT(1) desc
)WHERE ROW IN (1,3,5)
```