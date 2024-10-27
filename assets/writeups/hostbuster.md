# Host Buster

category : SQL

## Sky Wave 1 : High Tower
![](image.png)


Lets ssh and and enter the password 

```sh
ssh skywave@skywave.deadface.io
```
we enter the SQL database

```sh
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MySQL connection id is 309
Server version: 5.7.44 MySQL Community Server (GPL)

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MySQL [cell_tower_db]>
```

enter this command

```sh
SHOW DATABASES;
USE cell_tower_db;
SHOW TABLES;
DESCRIBE Towers;
SELECT tower_id FROM Towers WHERE elevation BETWEEN 119 AND 121;

```

and we get the flag

![](image-10.png)

flag{118}

## Sky Wave 2 : Trifecta
![alt text](image-8.png)

Just ssh then run this command

```sh
SELECT COUNT(*) FROM Devices WHERE device_type_id IN ('1','4','3');
```

flag{714}


# SkyWave 7 : Bad Handwriting

![alt text](image-13.png)

```SELECT * From Tower_Maintenance WHERE maintenance_date = "2024-08-26" ;```

```sh
MySQL [cell_tower_db]> SELECT * From Tower_Maintenance WHERE maintenance_date = "2024-08-26"
    -> ;
+----------------+----------+----------------------------+------------------+---------------+
| maintenance_id | tower_id | maintenance_type           | maintenance_date | technician_id |
+----------------+----------+----------------------------+------------------+---------------+
|            361 |      196 | Component replacement      | 2024-08-26       |           170 |
|            434 |       45 | Tower structure inspection | 2024-08-26       |           269 |
|            522 |      133 | Miscellaneous              | 2024-08-26       |           323 |
+----------------+----------+----------------------------+------------------+---------------+
3 rows in set (0.001 sec)
```

so we got the technition id = 323
Lets search its employee_number

```SELECT * from Technicians WHERE technician_id = 323;```


```sh
MySQL [cell_tower_db]> SELECT * from Technicians WHERE technician_id = 323;
+---------------+------------+-----------+----------------+--------------------------+------------+-------+-------------+-----------------+                                                                                                                                     
| technician_id | first_name | last_name | contact_number | street                   | city       | state | postal_code | employee_number |                                                                                                                                     
+---------------+------------+-----------+----------------+--------------------------+------------+-------+-------------+-----------------+                                                                                                                                     
|           323 | Marena     | Polson    | 717-697-8170   | 625 Manufacturers Avenue | Harrisburg | PA    | 17121       | T263739990      |                                                                                                                                     
+---------------+------------+-----------+----------------+--------------------------+------------+-------+-------------+-----------------+
1 row in set (0.001 sec)

```

flag{T263739990}

## SKywave 9 : Updates

![alt text](image-14.png)

```sh
MySQL [cell_tower_db]> select count(DISTINCT tower_id) from Tower_Maintenance where maintenance_type = "Software updates"
    -> ;
+--------------------------+
| count(DISTINCT tower_id) |
+--------------------------+
|                       70 |
+--------------------------+
1 row in set (0.001 sec)

```


# SkyWave 3 : Rabbit Ears

![alt text](image-15.png)

Lets search this operator

```sh

MySQL [cell_tower_db]> SELECT * from Operators where first_name = "Florian"
    -> ;
+-------------+------------+-----------+-----------------+
| operator_id | first_name | last_name | employee_number |
+-------------+------------+-----------+-----------------+
|           4 | Florian    | Olyff     | 3223634520      |
+-------------+------------

```

nice we got florian operator_id which is 4 , lets see which tower he operate


```sh

MySQL [cell_tower_db]> SELECT *  from Towers where operator_id = 4;
+----------+---------------+-----------+------------+-----------+--------------+-------------+--------+--------------+-----------------------+
| tower_id | location_name | latitude  | longitude  | elevation | tower_height | operator_id | status | install_date | last_maintenance_date |
+----------+---------------+-----------+------------+-----------+--------------+-------------+--------+--------------+-----------------------+
|      189 | PA            | 40.725061 | -76.969425 |     36.19 |        88.71 |           4 | active | 2011-02-09   | 2023-08-24            |
+----------+---------------+-----------+------------+-----------+--------------+-------------+--------+--------------+-----------------------+


```
i see tower_id 189, now lets see which antenna_id Florian manage the most


```sh
MySQL [cell_tower_db]> select * from Tower_Sectors where tower_id = 189;
+-----------+----------+---------+------------+----------------+--------------+
| sector_id | tower_id | azimuth | antenna_id | frequency_band | power_output |
+-----------+----------+---------+------------+----------------+--------------+
|      1140 |      189 |    0.00 |          9 | 850 MHz        |         5.06 |
|      1141 |      189 |   45.00 |          4 | 700 MHz        |         4.73 |
|      1142 |      189 |   90.00 |          2 | C-band         |         4.31 |
|      1143 |      189 |  135.00 |          9 | 3.45 GHz       |         9.17 |
|      1144 |      189 |  180.00 |          6 | 2.5 GHz        |         4.54 |
|      1145 |      189 |  225.00 |          9 | 700 MHz        |         5.89 |
|      1146 |      189 |  270.00 |          5 | C-band         |         7.83 |
|      1147 |      189 |  315.00 |          4 | 2.5 GHz        |         7.42 |
+-----------+----------+---------+------------+----------------+--------------+
8 rows in set (0.001 sec)

```

i see Florian manage antenna_id 9 the most which is 3 lets get antenna 9 name 

```sh
MySQL [cell_tower_db]> select * from Antennas where antenna_id = 9
    -> ;
+------------+---------------------------------------+
| antenna_id | antenna_name                          |
+------------+---------------------------------------+
|          9 | Multiple Input Multiple Output (MIMO) |
+------------+---------------------------------------+
1 row in set (0.000 sec)
```

flag{Multiple Input Multiple Output (MIMO) 3}