-- Create Weather and Flight Data
CREATE DATABASE WtF;
USE WtF;

-- Create tables for raw data to be loaded into
-- - Drop Table Weather;
-- Drop Table Flight;
-- drop view wtf_correlation;

CREATE TABLE Weather (
  id INTEGER AUTO_INCREMENT NOT NULL,
  Reading_Date varchar(10),
  raw_date int,
  Date1 varchar(15),
  minT int,
  maxT int,
  weatherCondition varchar(100),
  DOW varchar(2),
  primary key(id)
);

CREATE TABLE Flight (
  id INTEGER AUTO_INCREMENT NOT NULL,
  Reading_Date2 varchar(10),
  Date1 varchar(25),
  flight_price int,
  carrier varchar(20),
  primary key(id)
);

Alter Table Weather
Add Column city varchar(15);

Alter Table FLight
Add Column city varchar(15);

Alter VIEW WtF_correlation AS
    SELECT w.Reading_Date, w.Date1, w.minT, w.maxT, f.flight_price, w.DOW, f.city -- SUM(amount) AS Gross
        FROM Weather w
        JOIN Flight f
        ON (w.Reading_Date = f.Reading_Date2 AND w.Date1 = f.Date1)
        ORDER BY w.Date1, f.Reading_date2;




UPDATE weather
SET Reading_Date = '2019-04-11'
WHERE id<=10;
UPDATE flight
SET Reading_Date2 = '2019-04-11'
WHERE id<=10;
UPDATE flight
SET Reading_Date2 = '2019-04-12'
WHERE id>10;


#Join the tables

SELECT w.id, w.Reading_Date, w.raw_date, w.Date1, w.minT, w.maxT, w.weatherCondition, w.DOW, w.Date1, f.flight_price, f.carrier, f.city, count(w.Reading_Date) as R
FROM Weather w
JOIN Flight f
ON (w.Reading_Date = f.Reading_Date2 AND w.Date1 = f.Date1)
group by w.Reading_date
Order by w.Date1, f.Reading_Date2;

