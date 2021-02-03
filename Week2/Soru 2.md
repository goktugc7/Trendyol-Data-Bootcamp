```SQL
SELECT * FROM (
    SELECT Sport, Athlete,
    FIRST_VALUE(Year) OVER(partition by Sport, Athlete order by Sport, Athlete) as firstYear,
    LEAD(Year, 1) OVER(partition by Sport, Athlete order by Athlete, Year) as secondYear,
    LEAD(Year, 2) OVER(partition by Sport, Athlete order by Athlete, Year) as thirdYear
    FROM `dsmbootcamp.sample.summer_medals`
    ORDER BY Sport, Athlete
)WHERE thirdYear - secondYear = 4 and secondYear - firstYear = 4;
```