

```python
1a)
SELECT first_name, last_name
FROM actor;

1b)
SELECT concat(first_name, ' ', last_name) AS 'Actor Name'
FROM actor;

2a)
SELECT actor_id, first_name, last_name
FROM actor
WHERE first_name = 'Joe';

2b)
SELECT actor_id, first_name, last_name
FROM actor
WHERE last_name LIKE '%GEN%';

2c)
SELECT actor_id, first_name, last_name
FROM actor
WHERE last_name LIKE '%LI%'
ORDER BY last_name, first_name;

2d)
SELECT country_id, country
FROM country
WHERE country IN ('Afghanistan', 'Bangladesh', 'China');

3a)
ALTER TABLE actor
	ADD middle_name VARCHAR(50);

3b)
ALTER Table actor
	MODIFY COLUMN middle_name BLOB;

3c)
ALTER TABLE actor
DROP COLUMN middle_name;

4a)
SELECT DISTINCT last_name , COUNT(last_name)
FROM actor
GROUP BY last_name;

4b)
SELECT DISTINCT last_name , COUNT(last_name) AS num_count
FROM actor
GROUP BY last_name
HAVING num_count > 2;

4c)
UPDATE actor
SET first_name = 'HARPO'
WHERE last_name = 'WILLIAMS' AND first_name = 'GROUCHO';

4d)
UPDATE actor
SET first_name = 'GROUCHO'
WHERE first_name = 'HARPO' ;

5a)
SHOW CREATE TABLE address;

6a)
SELECT s.first_name, s.last_name, a.address
FROM staff s
INNER JOIN address a
ON s.address_id = a.address_id;

6b)
SELECT s.first_name, s.last_name, SUM(p.amount)
FROM staff s
INNER JOIN payment p
ON s.staff_id = p.staff_id
WHERE p.payment_date BETWEEN '2005-08-01' AND '2005-08-31'
GROUP BY s.first_name, s.last_name;

6c)
SELECT f.title, COUNT(fa.actor_id) AS 'Actors Count'
FROM film f
INNER JOIN film_actor fa
ON f.film_id = fa.film_id
GROUP BY f.title;

6d)
SELECT f.title, COUNT(i.film_id)
FROM inventory i
INNER JOIN film f
ON i.film_id = f.film_id
WHERE f.title = 'Hunchback Impossible'
GROUP BY f.title;

6e)
SELECT c.first_name, c.last_name, SUM(p.amount) AS 'Total Paid'
FROM customer c
INNER JOIN payment p
ON c.customer_id = p.customer_id
GROUP BY c.first_name, c.last_name
ORDER BY c.last_name;

7a)
SELECT title
FROM film
WHERE (title LIKE 'K%' OR title LIKE 'Q%' ) AND language_id = 
(
	SELECT language_id
    FROM language
    WHERE name = 'English'
);

7b)
SELECT first_name, last_name
FROM actor
WHERE actor_id IN
(
	SELECT actor_id
    FROM film_actor
    WHERE film_id = 
    (
		SELECT film_id
        FROM film
        WHERE title = 'Alone Trip'
    )

7c)
SELECT first_name, last_name, email
FROM customer
WHERE address_id IN
(
	SELECT address_id
    FROM address
    WHERE city_id IN
    (
		SELECT city_id
        FROM city
        WHERE country_id = 
        (
			SELECT country_id
            FROM country
            WHERE country = 'Canada'
        )
    )
    
);

7d)
SELECT title
FROM film
WHERE film_id IN
(
	SELECT film_id
    FROM film_category
    WHERE category_id IN
    (
		SELECT category_id
        FROM category
        WHERE name = 'Family'
    )
);

7e)
SELECT f.title, COUNT(r.rental_id) AS 'Rent Freq'
FROM rental r
INNER JOIN inventory i
ON r.inventory_id = i.inventory_id
INNER JOIN film_text f
ON i.film_id = f.film_id
GROUP BY f.title
ORDER BY COUNT(r.rental_id) DESC;

7f)
SELECT s.store_id, SUM(p.amount)
FROM store s
INNER JOIN customer c
ON s.store_id = c.store_id
INNER JOIN payment p
ON c.customer_id = p.customer_id
GROUP BY s.store_id;

7g)
SELECT s.store_id, ci.city, co.country
FROM  store s
INNER JOIN address a
ON s.address_id = a.address_id
INNER JOIN city ci
ON ci.city_id = a.city_id
INNER JOIN country co
ON co.country_id = ci.country_id;

7h)
SELECT c.name, SUM(p.amount) AS 'Revenue'
FROM payment p
INNER JOIN rental r
ON p.rental_id = r.rental_id
INNER JOIN inventory i
ON i.inventory_id = r.inventory_id
INNER JOIN film_category f
ON f.film_id = i.film_id
INNER JOIN category c
ON c.category_id = f.category_id
GROUP BY c.name
ORDER BY Revenue DESC
LIMIT 5;


```
