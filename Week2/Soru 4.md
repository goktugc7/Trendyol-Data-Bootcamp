```SQL
CREATE OR REPLACE TABLE goktug_cengiz.content_category AS SELECT * from sample.content_category;
CREATE OR REPLACE TABLE goktug_cengiz.content_category_20201222_00_59 AS SELECT * from sample.content_category_20201222_00_59;

MERGE goktug_cengiz.content_category Target
USING goktug_cengiz.content_category_20201222_00_59 Source
ON Target.id = Source.id

WHEN MATCHED THEN
  UPDATE SET 
  Target.cdc_date = Source.cdc_date,
  Target.category = Source.category

WHEN NOT MATCHED BY TARGET THEN 
  INSERT (category, id, is_deleted, cdc_date)
  VALUES (Source.category, Source.id, Source.is_deleted, Source.cdc_date)

WHEN NOT MATCHED BY SOURCE THEN
  UPDATE SET Target.is_deleted = true;
```