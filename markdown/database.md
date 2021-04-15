\section{Проектирование архитектуры БД и наполнение данными}

Для проектирования базы использовалась платформа [*Vertabelo*](https://vertabelo.com/). База состоит из трёх таблиц: `Helicopters`, `Pilots` и `Flights`.

Ниже представлен отчёт, сгенерированный с помощью *Vertabelo*.

\includepdf[pages=-]{data/vertabelo.pdf}

\subsection{Заполнение базы данными}

```sql
-- 10-addPilots.sql
INSERT INTO Pilots (surname, position, helicopter_number, 
experience, adress, birthdate)
    VALUES ('Petro', 'captain', 1, 
	14, 'Dereska str., 56', '12-02-1989');
INSERT INTO Pilots (surname, position, helicopter_number, 
experience, adress, birthdate)
    VALUES ('Vasili', 'pilot', 1, 
	1, 'International str., 56', '06-10-19');
INSERT INTO Pilots (surname, position, helicopter_number, 
experience, adress, birthdate)
    VALUES ('Matvey', 'pilot', 2, 
	2, 'Kalinova str., 12', '15-09-1987');
INSERT INTO Pilots (surname, position, helicopter_number, 
experience, adress, birthdate)
    VALUES ('Joseph', 'pilot', 2, 
	7, 'Bobruyskaya str., 7', '03-03-1993');

-- 11-addHelicopters.sql
INSERT INTO Helicopters (brand, date, capacity, last_overhaul, till_overhaul
, pilot_identification_number)
    VALUES ('MIG72', '12-02-2012', 53.9, '19-01-2019', 240, 119);
INSERT INTO Helicopters (brand, date, capacity, 
last_overhaul, till_overhaul, pilot_identification_number)
    VALUES ('Sikorsky R-4', '16-7-2012', 78.3, '5-1-2006', 3030, 1098);
INSERT INTO Helicopters (brand, date, capacity, 
last_overhaul, till_overhaul, pilot_identification_number)
    VALUES ('Silvercraft SH-4', '3-6-2012', 75.3, '21-5-2002', 1287, 25);
INSERT INTO Helicopters (brand, date, capacity, 
last_overhaul, till_overhaul, pilot_identification_number)
    VALUES ('Yakovlev EG', '20-4-2018', 66.3, '26-1-2005', 1188, 214);
INSERT INTO Helicopters (brand, date, capacity, 
last_overhaul, till_overhaul, pilot_identification_number)
    VALUES ('Airmaster H2-B1', '5-10-2018', 85.0, '26-11-2000', 982, 419);
INSERT INTO Helicopters (brand, date, capacity, 
last_overhaul, till_overhaul, pilot_identification_number)
    VALUES ('Bell 201', '11-2-2009', 41.7, '26-11-2018', 831, 415);
INSERT INTO Helicopters (brand, date, capacity, 
last_overhaul, till_overhaul, pilot_identification_number)
    VALUES ('Agusta A103', '28-8-2007', 25.5, '6-6-2015', 659, 743);

-- 12-addFlights.sql
INSERT INTO Flights (hours, cost, date, 
helicopter_number, weight, quantity, special)
    VALUES (3, 1000, '12-03-2020', 2, 4.98, 12, 0);
INSERT INTO Flights (hours, cost, date, 
helicopter_number, weight, quantity, special)
    VALUES (2, 2000, '12-6-2009', 3, 3.160649402009925, 34, 1);
INSERT INTO Flights (hours, cost, date, 
helicopter_number, weight, quantity, special)
	VALUES (7, 750, '28-11-2016', 7, 2.991842311364755, 3, 0);	
INSERT INTO Flights (hours, cost, date, 
helicopter_number, weight, quantity, special)
    VALUES (7, 3750, '18-10-2012', 7, 2.1592498821107533, 40, 0);
INSERT INTO Flights (hours, cost, date, 
helicopter_number, weight, quantity, special)
    VALUES (0, 1250, '1-7-2012', 1, 2.9623104694339313, 17, 1);
INSERT INTO Flights (hours, cost, date, 
helicopter_number, weight, quantity, special)
    VALUES (8, 4250, '10-2-2000', 2, 1.8621057274127257, 44, 0);
INSERT INTO Flights (hours, cost, date, 
helicopter_number, weight, quantity, special)
    VALUES (9, 4750, '21-8-2003', 1, 4.867015520251796, 36, 0);
INSERT INTO Flights (hours, cost, date, 
helicopter_number, weight, quantity, special)
    VALUES (9, 4500, '10-3-2007', 1, 4.838958229113954, 29, 0);
INSERT INTO Flights (hours, cost, date, 
helicopter_number, weight, quantity, special)
    VALUES (0, 4500, '23-2-2001', 3, 2.4508831132558226, 41, 0);
INSERT INTO Flights (hours, cost, date, 
helicopter_number, weight, quantity, special)
    VALUES (4, 3750, '24-9-2011', 4, 3.0430434898680705, 45, 0);
INSERT INTO Flights (hours, cost, date, 
helicopter_number, weight, quantity, special)
    VALUES (8, 4750, '3-1-2000', 6, 4.972302049328084, 25, 0);

-- 20-deletePilot.sql
DELETE FROM Pilots
WHERE surname = 'Petro';

-- 21-deleteFlight.sql
DELETE FROM Flights
WHERE date = '12-12-2020';
```
