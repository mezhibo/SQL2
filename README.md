Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:

фамилия и имя сотрудника из этого магазина;

город нахождения магазина;

количество пользователей, закреплённых в этом магазине.


Решение 1.

SELECT s2.last_name, s2.first_name, c2.city, count(c.customer_id) FROM store s

JOIN customer c ON c.store_id = s.store_id

JOIN address a ON a.address_id = s.address_id

JOIN city c2 ON c2.city_id = a.city_id

JOIN staff s2 ON s2.store_id = s.store_id

GROUP BY s2.first_name, s2.last_name, c2.city

HAVING count(c.customer_id) > 300


![alt text](https://github.com/mezhibo/SQL2/blob/7c432ae6edf4cde9a14c7cc2a1200d476cd6da45/IMG/1.jpg)



Задание 2.

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.


Решение 2.
SELECT count(f.film_id) FROM film f

WHERE f.length > (

SELECT avg(f.length) FROM film f )


![alt text](https://github.com/mezhibo/SQL2/blob/7c432ae6edf4cde9a14c7cc2a1200d476cd6da45/IMG/2.jpg)



Задание 3.

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.


Решение 3.

SELECT sum(p.amount),count(p.payment_id) FROM payment p

GROUP BY EXTRACT(MONTH FROM p.payment_date)

ORDER BY sum(p.amount) desc limit 1


![alt text](https://github.com/mezhibo/SQL2/blob/7c432ae6edf4cde9a14c7cc2a1200d476cd6da45/IMG/3.jpg)
