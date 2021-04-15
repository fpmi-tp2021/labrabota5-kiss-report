\section{Тестирование}

\begin{figure}[h]
\includegraphics{data/query-menu}
\caption*{Приложение выводит меню и предлагает выбрать запрос. При нажатии клавиши соответствующий запрос выполняется.}
\end{figure}

\subsection{Результаты запросов}

- ```sql
SELECT image FROM Helicopters WHERE number=1;
```

\includegraphics{data/print-image}

- ```sql
SELECT * FROM Helicopters;
```

```
H

(null): number = 1
brand = MIG72
date = 12-02-2012
capacity = 53.9
last_overhaul = 19-01-2019
till_overhaul = 240
pilot_identification_number = 119
image = farbfeld

(null): number = 2
brand = Sikorsky R-4
date = 16-7-2012
capacity = 78.3
last_overhaul = 5-1-2006
till_overhaul = 3030
pilot_identification_number = 1098
image = NULL

-- вывод обрезан для краткости --
```

- ```sql
SELECT * FROM Pilots
```

```
P

(null): identification_number = 2
surname = Vasili
position = pilot
helicopter_number = 1
experience = 1
adress = International str., 56
birthDATE = 06-10-19

(null): identification_number = 3
surname = Matvey
position = pilot
helicopter_number = 1
experience = 2
adress = Kalinova str., 12
birthDATE = 15-09-1987

(null): identification_number = 4
surname = Joseph
position = pilot
helicopter_number = 1
experience = 7
adress = Bobruyskaya str., 7
birthDATE = 03-03-1993
```

- ```sql
SELECT * FROM Flights;
```

```
F

(null): id = 1
hours = 3
cost = 1000
date = 12-03-2020
helicopter_number = 2
weight = 4.98
quantity = 12
special = 0

-- вывод обрезан для краткости --
```

- ```sql
SELECT Helicopters.brand, sum(Flights.hours)  FROM Helicopters INNER JOIN Flights ON Helicopters.number = Flights.helicopter_number WHERE Helicopters.last_overhaul < Flights.date GROUP BY Helicopters.brand;
```

```
1

(null): brand = Bell 201
sum(Flights.hours) = 8

(null): brand = MIG72
sum(Flights.hours) = 9

(null): brand = Silvercraft SH-4
sum(Flights.hours) = 0
```

- ```sql
SELECT Helicopters.brand, sum(Flights.hours), sum(Flights.quantity), Flights.id, Flights.date  FROM Helicopters INNER JOIN Flights ON Helicopters.number = Flights.helicopter_number GROUP BY Helicopters.brand;
```

```
2

(null): brand = Agusta A103
sum(Flights.hours) = 14
sum(Flights.quantity) = 43
id = 3
date = 28-11-2016

(null): brand = Bell 201
sum(Flights.hours) = 8
sum(Flights.quantity) = 25
id = 11
date = 3-1-2000

(null): brand = MIG72
sum(Flights.hours) = 18
sum(Flights.quantity) = 82
id = 5
date = 1-7-2012

(null): brand = Sikorsky R-4
sum(Flights.hours) = 11
sum(Flights.quantity) = 56
id = 1
date = 12-03-2020

(null): brand = Silvercraft SH-4
sum(Flights.hours) = 2
sum(Flights.quantity) = 75
id = 2
date = 12-6-2009

(null): brand = Yakovlev EG
sum(Flights.hours) = 4
sum(Flights.quantity) = 45
id = 10
date = 24-9-2011
```

- ```sql
SELECT Helicopters.brand, sum(Flights.hours), sum(Flights.quantity), sum(Flights.cost), COUNT(Flights.id) as Kolvo  FROM Helicopters INNER JOIN Flights ON Helicopters.number = Flights.helicopter_number WHERE Flights.special = 1 GROUP BY Helicopters.brand;
```

```
3

(null): brand = MIG72
sum(Flights.hours) = 0
sum(Flights.quantity) = 17
sum(Flights.cost) = 1250
Kolvo = 1

(null): brand = Silvercraft SH-4
sum(Flights.hours) = 2
sum(Flights.quantity) = 34
sum(Flights.cost) = 2000
Kolvo = 1
```

- ```sql
SELECT Helicopters.brand, sum(Flights.hours), sum(Flights.quantity), sum(Flights.cost), COUNT(Flights.id) as Kolvo  FROM Helicopters INNER JOIN Flights ON Helicopters.number = Flights.helicopter_number WHERE Flights.special = 0 GROUP BY Helicopters.brand;
```

```
4

(null): brand = Agusta A103
sum(Flights.hours) = 14
sum(Flights.quantity) = 43
sum(Flights.cost) = 4500
Kolvo = 2

(null): brand = Bell 201
sum(Flights.hours) = 8
sum(Flights.quantity) = 25
sum(Flights.cost) = 4750
Kolvo = 1

(null): brand = MIG72
sum(Flights.hours) = 18
sum(Flights.quantity) = 65
sum(Flights.cost) = 9250
Kolvo = 2

(null): brand = Sikorsky R-4
sum(Flights.hours) = 11
sum(Flights.quantity) = 56
sum(Flights.cost) = 5250
Kolvo = 2

(null): brand = Silvercraft SH-4
sum(Flights.hours) = 0
sum(Flights.quantity) = 41
sum(Flights.cost) = 4500
Kolvo = 1

(null): brand = Yakovlev EG
sum(Flights.hours) = 4
sum(Flights.quantity) = 45
sum(Flights.cost) = 3750
Kolvo = 1
```

- ```sql
select * from pilots inner join (select helicopters.number as hn, helicopters.brand from Helicopters inner join (select max(num_flights), sum(cost) as total, brand as b from (select count(Flights.id) as num_flights, Flights.cost as cost, Helicopters.brand as brand from Flights inner join Helicopters on Flights.helicopter_number = Helicopters.number group by brand)) on helicopters.brand = b) on pilots.helicopter_number = hn group by pilots.surname;
```

```
5

(null): identification_number = 2
surname = Vasili
position = pilot
helicopter_number = 1
experience = 1
adress = International str., 56
birthDATE = 06-10-19
hn = 1
brand = MIG72
```

- ```sql
select Flights.date, Flights.weight, Flights.cost, h from flights inner join (select h,max(total) from (select sum(fc) as total, hn as h from (select Pilots.surname as s, sum(Flights.cost) as fc, Flights.helicopter_number as hn FROM Pilots INNER JOIN Flights ON Pilots.helicopter_number = Flights.helicopter_number GROUP BY Pilots.surname) GROUP BY hn)) ON flights.helicopter_number = h;
```

```
6

(null): date = 1-7-2012
weight = 2.96231046943393
cost = 1250
h = 1

(null): date = 21-8-2003
weight = 4.8670155202518
cost = 4750
h = 1

(null): date = 10-3-2007
weight = 4.83895822911395
cost = 4500
h = 1
```

- ```sql
SELECT Flights.date, Flights.hours as Czasy, Flights.quantity as Kolvo, Flights.cost as Cena, Flights.special as Special  FROM Flights INNER JOIN
Pilots ON Pilots.helicopter_number = Flights.helicopter_number WHERE Pilots.surname = 'Vasili';
```

```
7

(null): date = 1-7-2012
Czasy = 0
Kolvo = 17
Cena = 1250
Special = 1

(null): date = 10-3-2007
Czasy = 9
Kolvo = 29
Cena = 4500
Special = 0

(null): date = 21-8-2003
Czasy = 9
Kolvo = 36
Cena = 4750
Special = 0
```
