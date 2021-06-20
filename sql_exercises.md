# Exercise: SQL Queries using sakila database in MySQL
## Description of Exercise

These exercises are meant to be executed in MySQL Workbench against the demo "sakila" database.

Each exercise is presented as an English-language description of the desired query result set. 

For each of the exercises, you will be provided with an example result set.

You should make use of Google, stack overflow, etc. to work out how to create your query.

### How to format your answers
You should create one .sql script that contains your answers to all exercises.

Be sure to comment your code so it is clear which query is associated with which exercise. An example might be:

```sql
-- Excercise 1

select first_name, last_name 
from actor;

-- Exercise 2

select title, description
from film;
```

### Github repo
Please create a Github repo to hold your SQL script. You should submit a link to the repo to your instructor.

## Exercises

>1. Display the first and last name of each actor in a single column in upper case letters. Name the column `Actor Name`.

**Result set**

![Query 1 result set](https://github.com/kiresorg/amex-sql-exercise/blob/main/images/images/q1.png?raw=true)

**Query** - Don't cheat :)

<details>
  <summary>Click to expand</summary>
  
  ```sql
select upper(concat(first_name, ' ', last_name))   'Actor Name'
from actor;
  ```
</details>

</br>

>2. You need to find the ID number, first name, and last name of an actor, of whom you know only the first name, "Joe." What is one query that you could use to obtain this information?

**Result set**

![Query 2 result set](images/q2.png)

**Query**

<details>
  <summary>Click to expand</summary>
  
  ```sql
select actor_id, first_name, last_name 
from actor
where lower(first_name) = lower("Joe");
  ```
</details>

</br>

>3. Find all actors whose last name contain the letters ```GEN```.

**Result set**

![Query 3 result set](images/q3.png)

**Query**

<details>
  <summary>Click to expand</summary>
  
  ```sql
select * 
from actor 
where upper(last_name) like '%GEN%';
  ```
</details>

</br>

>4. Find all actors whose last names contain the letters ```"LI"```. This time, order the rows by last name and first name, in that order.

**Result set**

![Query 4 result set](images/q4.png)

**Query**

<details>
  <summary>Click to expand</summary>
  
  ```sql
select * 
from actor 
where upper(last_name) like '%LI%' 
order by last_name, first_name;
  ```
</details>

</br>

>5. Using ```IN```, display the ```country_id``` and ```country``` columns of the following countries: Afghanistan, Bangladesh, and China.

**Result set**

![Query 5 result set](images/q5.png)

**Query**

<details>
  <summary>Click to expand</summary>
  
  ```sql
select country_id, country 
from country 
where country in ('Afghanistan', 'Bangladesh', 'China');
  ```
</details>

</br>

>6. List last names of actors and the number of actors who have that last name, but only for names that are shared by at least two actors

**Result set**

![Query 6 result set](images/q6.png)

**Query**

<details>
  <summary>Click to expand</summary>
  
  ```sql
select last_name, count(*) actor_count 
from actor 
group by last_name
having actor_count >1
order by actor_count desc, last_name;
  ```
</details>

</br>

>7. The actor ```HARPO WILLIAMS``` was accidentally entered in the actor table as ```GROUCHO WILLIAMS```. Write a query to fix the record, and another to verify the change.

**Result set**

![Query 7 result set](images/q7.png)

**Query (your approach used to change the first name may differ; the important thing is to make the change to the correct record)**

<details>
  <summary>Click to expand</summary>
  
  ```sql
update actor set first_name = 'HARPO', last_name = 'WILLIAMS' where first_name = 'GROUCHO' and last_name = 'WILLIAMS';

select * from actor where last_name = 'WILLIAMS';
  ```
</details>

</br>

>8. Perhaps we were too hasty in changing ```GROUCHO``` to ```HARPO```. It turns out that ```GROUCHO``` was the correct name after all! In a single query, if the first name of the actor is currently ```HARPO```, change it to ```GROUCHO```. Then write a query to verify your change.

**Result set**

![Query 8 result set](images/q8.png)

**Query**

<details>
  <summary>Click to expand</summary>
  
  ```sql
update actor set first_name = 'GROUCHO', last_name = 'WILLIAMS' where first_name = 'HARPO' and last_name = 'WILLIAMS';

select * from actor where last_name = 'WILLIAMS';
  ```
</details>

</br>

>9. Perhaps we were too hasty in changing ```GROUCHO``` to ```HARPO```. It turns out that ```GROUCHO``` was the correct name after all! In a single query, if the first name of the actor is currently ```HARPO```, change it to ```GROUCHO```. Then write a query to verify your change.

**Result set**

![Query 9 result set](images/q9.png)

**Query**

<details>
  <summary>Click to expand</summary>
  
  ```sql
update actor set first_name = 'GROUCHO', last_name = 'WILLIAMS' where first_name = 'HARPO' and last_name = 'WILLIAMS';

select * from actor where last_name = 'WILLIAMS';
  ```
</details>

</br>

>10. Use ```JOIN``` to display the total amount rung up by each staff member in August of 2005. Use tables ```staff``` and ```payment```.

**Result set**

![Query 10 result set](images/q10.png)

**Query**

<details>
  <summary>Click to expand</summary>
  
  ```sql
select stf.first_name, stf.last_name, sum(pay.amount)
from staff stf
left join payment pay
on stf.staff_id = pay.staff_id
WHERE month(pay.payment_date) = 8
and year(pay.payment_date)  = 2005
group by stf.first_name, stf.last_name;
  ```
</details>

</br>

>11. List each film and the number of actors who are listed for that film. Use tables film_actor and film. Use inner join.

**Result set**

![Query 11 result set](images/q11.png)

**Query**

<details>
  <summary>Click to expand</summary>
  
  ```sql
select flm.title, count(*) number_of_actors
from film flm
inner join film_actor fim_act
on flm.film_id = fim_act.film_id
group by flm.title
order by number_of_actors desc;
  ```
</details>

</br>

>12. How many copies of the film Hunchback Impossible exist in the inventory system?

**Result set**

![Query 12 result set](images/q12.png)

**Query**

<details>
  <summary>Click to expand</summary>
  
  ```sql
select flm.title, count(*) number_in_inventory
from film flm
inner join inventory inv
on flm.film_id = inv.film_id
where lower(flm.title) = lower('Hunchback Impossible')
group by flm.title;
  ```
</details>

</br>

>13. The music of Queen and Kris Kristofferson have seen an unlikely resurgence. As an unintended consequence, films starting with the letters K and Q have also soared in popularity. Use **subqueries** to display the titles of movies starting with the letters K and Q whose language is English.

**Result set**

![Query 13 result set](images/q13.png)

**Query**

<details>
  <summary>Click to expand</summary>
  
  ```sql
select title
from film 
where (title like 'K%' or title like 'Q%')
and language_id in (
	select language_id 
	from language 
	where name = 'English'
)
order by title;
  ```
</details>

</br>

>14. Insert a record to represent ```Mary Smith``` renting ```‘Academy Dinosaur’``` from ```Mike Hillyer``` at ```Store 1``` today. Then write a query to capture the exact row you entered into the ```rental``` table.

**Result set** (your ```rental date``` value will of course show the date and time you entered the record)

![Query 14 result set](images/q14.png)

**Query**

<details>
  <summary>Click to expand</summary>
  
  ```sql
insert into rental (rental_date, inventory_id, customer_id, staff_id)
values (NOW(), 1, 1, 1);

select * from rental
where inventory_id = 1 and
customer_id = 1 and 
staff_id = 1;
  ```
</details>

</br>

