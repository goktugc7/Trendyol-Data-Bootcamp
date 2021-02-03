```SQL
SELECT view_period, (SUM(active_user_count) OVER(ORDER BY view_period ROWS BETWEEN 4 PRECEDING AND 0 FOLLOWING)) as active_user 
FROM (SELECT TIMESTAMP_TRUNC(view_ts, minute) view_period, COUNT(DISTINCT deviceid) as active_user_count
      FROM goktug_cengiz.pageview
      GROUP BY view_period
      );
```