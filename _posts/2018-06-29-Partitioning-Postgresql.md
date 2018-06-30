---
layout: post
title: "Declarative Partition Postgresql 10"
#tagline: "postgresql"
description: "Steps to convert an existing table to a declarative partition in Postgresql 10"
category: articles
tags: [postgresql;partition]
image:
  feature: elephants.jpg
  credit: NH53
---

## Upgrading your existing unpartition table to declarative partition available in Postgresql 10

All my existing tables were built with postgresql 9.6 and before. One of those tables is XM rows. With the recent upgrade to Postgresql 10.4, it seem like a good time to make the switch to partitions.

Declarative partition is easier to set up than inheritance based partitioning available in Postgresql 9. Inheritance required creating a trigger that calls the trigger function with every insert of a record. When the child tables changed, the triggers needed to be updated. With Declaritive partitioning those steps go away.

My large table is a set of edits going back to 2005. Breaking the main table into years seemed like a reasonable approach to keep the partition size efficient. The first few years are group into one child partition with the remaining years in individual partitions. It looks like:
```
-edits
--edits_2010
--edits_2011
--edits_2012
--edits_2013
--edits_2014
--edits_2015
--edits_2016
--edits_2017
--edits_2018
--edits_2019
```
## What to watch for
My table also included a trigger that updated another smaller table when data was being inserted. I learned that triggers have be applied to the child tables not the parent.

The parent table can not contain a primary key.

## Steps to move to declarative partitioning

### Backup your table
Backup the database. Seem obvious, but my guess is you don't want to rebuild your tables.

### Create new parent/child Structure
Create your new parent table and all of your child tables. I used a dummy name for the parent. I'll change it once I copy the data to the new table. That way any scripts needing the original table will still work.  Below is a sample script that creates the parent table, the child tables and all of the index and triggers that update another table as data is inserted.

```
CREATE TABLE edit_1
(
  id bigint NOT NULL,
  user_id bigint,
  created timestamp without time zone,
  closed timestamp without time zone,
  user_name character varying(255),
  geom geometry(Polygon,4326)
) PARTITION BY RANGE(created);

CREATE TABLE edit_2010
PARTITION of edit_1
FOR VALUES FROM ('2005-04-09 19:54:12') TO ('2010-12-31 23:59:59.999');

CREATE INDEX edit_id_2010 ON edit_2010(id);
CREATE INDEX edit_user_id_2010 on edit_2010(user_id);

CREATE TABLE edit_2011
PARTITION of edit_1
FOR VALUES FROM ('2011-01-01 00:00:00') TO ('2011-12-31 23:59:59.999');

CREATE INDEX edit_id_2011 ON edit_2011(id);
CREATE INDEX edit_user_id_2011 on edit_2011(user_id);

CREATE TABLE edit_2012
PARTITION of edit_1
FOR VALUES FROM ('2012-01-01 00:00:00') TO ('2012-12-31 23:59:59.999');

CREATE INDEX edit_id_2012 ON edit_2012(id);
CREATE INDEX edit_user_id_2012 on edit_2012(user_id);

CREATE TABLE edit_2013
PARTITION of edit_1
FOR VALUES FROM ('2013-01-01 00:00:00') TO ('2013-12-31 23:59:59.999');

CREATE INDEX edit_id_2013 ON edit_2013(id);
CREATE INDEX edit_user_id_2013 on edit_2013(user_id);

CREATE TABLE edit_2014
PARTITION of edit_1
FOR VALUES FROM ('2014-01-01 00:00:00') TO ('2014-12-31 23:59:59.999');

CREATE INDEX edit_id_2014 ON edit_2014(id);
CREATE INDEX edit_user_id_2014 on edit_2014(user_id);

CREATE TABLE edit_2015
PARTITION of edit_1
FOR VALUES FROM ('2015-01-01 00:00:00') TO ('2015-12-31 23:59:59.999');

CREATE INDEX edit_id_2015 ON edit_2015(id);
CREATE INDEX edit_user_id_2015 on edit_2015(user_id);

CREATE TABLE edit_2016
PARTITION of edit_1
FOR VALUES FROM ('2016-01-01 00:00:00') TO ('2016-12-31 23:59:59.999');

CREATE INDEX edit_id_2016 ON edit_2016(id);
CREATE INDEX edit_user_id_2016 on edit_2016(user_id);

CREATE TABLE edit_2017
PARTITION of edit_1
FOR VALUES FROM ('2017-01-01 00:00:00') TO ('2017-12-31 23:59:59.999');

CREATE INDEX edit_id_2017 ON edit_2017(id);
CREATE INDEX edit_user_id_2017 on edit_2017(user_id);

CREATE TABLE edit_2018
PARTITION of edit_1
FOR VALUES FROM ('2018-01-01 00:00:00') TO ('2018-12-31 23:59:59.999');

CREATE INDEX edit_id_2018 ON edit_2018(id);
CREATE INDEX edit_user_id_2018 on edit_2018(user_id);

CREATE TABLE edit_2019
PARTITION of edit_1
FOR VALUES FROM ('2019-01-01 00:00:00') TO ('2019-12-31 23:59:59.999');
CREATE TRIGGER add_new_user_trigger
  BEFORE INSERT ON edit_2019
  FOR EACH ROW
  EXECUTE PROCEDURE add_new_user();

CREATE INDEX edit_id_2019 ON edit_2019(id);
CREATE INDEX edit_user_id_2019 on edit_2019(user_id);
```

### Add existing data to the new partitions.
I moved the data over directly to the child tables. You could move it to the parent table and let the declarative partitioning do its thing.

```
INSERT INTO edit_2010(id,
  user_id,
  created,
  closed,
  user_name,
  geom
) SELECT * from edit where date_part('year',created) < 2011;


INSERT INTO edit_2011(id,
  user_id,
  created,
  closed,
  user_name,
  geom
) SELECT * from edit where date_part('year',created) = 2011;
... do the same for all of the years
INSERT INTO edit_2018(id,
  user_id,
  creat,
  closed,
  user_name,
  geom
) SELECT * from edit where date_part('year',created) = 2018;
```

### Add the trigger to
Now that the data has been imported into the new child table, we can now turn our triggers back on.
```
CREATE TRIGGER add_new_user_trigger
  BEFORE INSERT ON edit_2018
  FOR EACH ROW
  EXECUTE PROCEDURE add_new_user();
  ```
### Rename new Parent table
  After verifying that the new parent/child structure is complete, it's time to drop the original table and rename the new Parent.

  For this step, I used PGAdmin4. PGAdmin4 gives a good visual layout of the new structure. When you rename the parent, all of the child tables will changed to the new parent table. ![PGAdmin4]({{site_url}}/assets/pgadmin4.jpg)
