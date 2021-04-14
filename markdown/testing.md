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
SELECT Helicopters.brand, sum(Flights.hours) FROM Helicopters
INNER JOIN Flights ON Helicopters.number = Flights.helicopter_number
WHERE Helicopters.last_overhaul < Flights.date;
```

```
o

(null): brand = Silvercraft SH-4
sum(Flights.hours) = 8
```

- ```sql
SELECT Helicopters.brand, sum(Flights.hours),
sum(Flights.quantity), Flights.id, Flights.date FROM Helicopters 
INNER JOIN Flights ON Helicopters.number = Flights.helicopter_number;
```

```
f

(null): brand = Sikorsky R-4
sum(Flights.hours) = 57
sum(Flights.quantity) = 326
id = 1
date = 12-03-2020
```

