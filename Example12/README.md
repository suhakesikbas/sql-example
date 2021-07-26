# Ödev 12
Aşağıdaki sorgu senaryolarını dvdrental örnek veri tabanı üzerinden gerçekleştiriniz.

1. **film** tablosunda film uzunluğu **length** sütununda gösterilmektedir. Uzunluğu ortalama film uzunluğundan fazla kaç tane film vardır?
```sql
SELECT COUNT(*) FROM film
WHERE length > (SELECT AVG(length) FROM film)
```
2. **film** tablosunda en yüksek **rental_rate** değerine sahip kaç tane film vardır?
```sql
SELECT COUNT(*) FROM film
WHERE rental_rate = (SELECT MAX(rental_rate) FROM film)
```
3. **film** tablosunda en düşük **rental_rate** ve en düşün **replacement_cost** değerlerine sahip filmleri sıralayınız.
```sql
WHERE film_id = ANY(
	SELECT film_id FROM film
	WHERE rental_rate = (SELECT MIN(rental_rate) FROM film)
	AND replacement_cost = (SELECT MIN(replacement_cost) FROM film)
)
```
4. **payment** tablosunda en fazla sayıda alışveriş yapan müşterileri(customer) sıralayınız.
```sql
SELECT 
	customer.customer_id, 
	CONCAT(customer.first_name, ' ',customer.last_name) AS full_name,
	COUNT(payment.customer_id) AS payment_count
FROM customer
INNER JOIN payment ON customer.customer_id = payment.customer_id
GROUP BY customer.customer_id ORDER BY COUNT(payment.customer_id) DESC
LIMIT 10
```