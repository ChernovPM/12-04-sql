\# Домашнее задание к занятию «SQL. Часть 2»



\*\*Выполнил: Павел Чернов\*\*



\## Задание 1



Нужно было получить информацию о магазине, в котором обслуживается более 300 покупателей.



Использовал запрос:



```sql

SELECT

&#x20;   s.first\_name,

&#x20;   s.last\_name,

&#x20;   c.city,

&#x20;   COUNT(cu.customer\_id) AS customers\_count

FROM store st

JOIN staff s ON st.manager\_staff\_id = s.staff\_id

JOIN address a ON st.address\_id = a.address\_id

JOIN city c ON a.city\_id = c.city\_id

JOIN customer cu ON cu.store\_id = st.store\_id

GROUP BY

&#x20;   st.store\_id,

&#x20;   s.first\_name,

&#x20;   s.last\_name,

&#x20;   c.city

HAVING COUNT(cu.customer\_id) > 300;

```



В результате получил:



`Mike Hillyer — Lethbridge — 326 покупателей`



!\[Задание 1](img/task1.png)



\## Задание 2



Нужно было получить количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.



Использовал запрос:



```sql

SELECT COUNT(\*) AS films\_longer\_than\_average

FROM film

WHERE length > (

&#x20;   SELECT AVG(length)

&#x20;   FROM film

);

```



Результат:



`489`



!\[Задание 2](img/task2.png)



\## Задание 3



Нужно было найти месяц, в котором была получена максимальная сумма платежей, и вывести количество аренд за этот месяц.



Использовал запрос:



```sql

SELECT

&#x20;   DATE\_FORMAT(p.payment\_date, '%Y-%m') AS payment\_month,

&#x20;   ROUND(SUM(p.amount), 2) AS total\_payments,

&#x20;   COUNT(DISTINCT p.rental\_id) AS rentals\_count

FROM payment p

GROUP BY DATE\_FORMAT(p.payment\_date, '%Y-%m')

ORDER BY total\_payments DESC

LIMIT 1;

```



В результате получил:



\- месяц: `2005-07`;

\- сумма платежей: `28373.89`;

\- количество аренд: `6709`.



!\[Задание 3](img/task3.png)

