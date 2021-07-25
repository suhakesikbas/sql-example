# Ödev 11
Aşağıdaki sorgu senaryolarını dvdrental örnek veri tabanı üzerinden gerçekleştiriniz.

1. actor ve customer tablolarında bulunan first_name sütunları için tüm verileri sıralayalım.
```sql
(
SELECT first_name FROM actor
	ORDER BY first_name
	LIMIT 10
)
UNION
(
SELECT first_name FROM customer
	ORDER BY first_name
	LIMIT 10
)
```
2. actor ve customer tablolarında bulunan first_name sütunları için kesişen verileri sıralayalım.
```sql
(
SELECT first_name FROM actor
	ORDER BY first_name
	LIMIT 10
)
INTERSECT
(
SELECT first_name FROM customer
	ORDER BY first_name
	LIMIT 10
)
```
3. actor ve customer tablolarında bulunan first_name sütunları için ilk tabloda bulunan ancak ikinci tabloda bulunmayan verileri sıralayalım.
```sql
(
SELECT first_name FROM actor
	ORDER BY first_name
	LIMIT 10
)
EXCEPT
(
SELECT first_name FROM customer
	ORDER BY first_name
	LIMIT 10
)
```
4. İlk 3 sorguyu tekrar eden veriler için de yapalım.
```sql
(
SELECT first_name FROM actor
	ORDER BY first_name
	LIMIT 10
)
UNION ALL
(
SELECT first_name FROM customer
	ORDER BY first_name
	LIMIT 10
)
(
SELECT first_name FROM actor
	ORDER BY first_name
	LIMIT 10
)
EXCEPT ALL
(
SELECT first_name FROM customer
	ORDER BY first_name
	LIMIT 10
)
```