--Who is the senior most employee based on job title?

SELECT TOP 1 * FROM employee
ORDER BY levels DESC;

--Which countries have the most Invoices?

select count(*) as c, billing_country
 from invoice
 group by billing_country
order by c desc

--What are top 3 values of total invoice?

SELECT TOP 3 total FROM invoice
ORDER BY total DESC;

--Which city has the best customers? We would like to throw a promotional Music Festival in the city we made the most money. Write a query that returns one city that
--has the highest sum of invoice totals. Return both the city name & sum of all invoice totals

select sum(total) as invoice_total,billing_city
from invoice
group by billing_city
order by invoice_total desc

--. Who is the best customer? The customer who has spent the most money will be declared the best customer. Write a query that returns the person who has spent the most money

SELECT TOP 1 customer.customer_id, customer.first_name, customer.last_name, SUM(invoice.total) AS total
FROM customer
JOIN invoice ON customer.customer_id = invoice.customer_id
GROUP BY customer.customer_id, customer.first_name, customer.last_name
ORDER BY total DESC;

-- Write query to return the email, first name, last name, & Genre of all Rock Music listeners. Return your list ordered alphabetically by email starting with A

Select Distinct email, first_name, last_name
from Customer
JOIN invoice ON customer.customer_id = invoice.customer_id
join invoice_line on invoice.invoice_id = invoice_line.invoice_id
where track_id in(
select track_id from track
join genre on track.genre_id = genre.genre_id
where genre.name like 'Rock'
)

order by email;

--Let's invite the artists who have written the most rock music in our dataset. Write a query that returns the Artist name and total track count of the top 10 rock bands

SELECT artist.artist_id, artist.name, COUNT(artist.artist_id) AS number_of_song
FROM track
JOIN album ON album.album_id = track.album_id
JOIN artist ON artist.artist_id = album.artist_id
JOIN genre ON genre.genre_id = track.genre_id
WHERE genre.name LIKE 'Rock'
GROUP BY artist.artist_id, artist.name
ORDER BY number_of_song DESC
OFFSET 0 ROWS
FETCH NEXT 10 ROWS ONLY;

--Return all the track names that have a song length longer than the average song length. Return the Name and Milliseconds for each track. Order by the song length with the
--longest songs listed first

SELECT name, milliseconds
FROM track
WHERE milliseconds > (
    SELECT AVG(milliseconds) AS avg_track_length
    FROM track
)
ORDER BY milliseconds DESC;

--Find how much amount spent by each customer on artists? Write a query to return customer name, 
--artist name and total spent


	WITH best_selling_artist AS (
    SELECT TOP 1 WITH TIES artist.artist_id AS artist_id, artist.name AS artist_name,
        SUM(invoice_line.unit_price * invoice_line.quantity) AS total_sales
    FROM invoice_line
    JOIN track ON track.track_id = invoice_line.track_id
    JOIN album ON album.album_id = track.album_id
    JOIN artist ON artist.artist_id = album.artist_id
    GROUP BY artist.artist_id, artist.name
    ORDER BY total_sales DESC
)
SELECT c.customer_id, c.first_name, c.last_name, bsa.artist_name, SUM(il.unit_price * il.quantity) AS amount_spent
FROM invoice i
    JOIN customer c ON c.customer_id = i.customer_id
    JOIN invoice_line il ON il.invoice_id = i.invoice_id
    JOIN track t ON t.track_id = il.track_id
    JOIN album alb ON alb.album_id = t.album_id
    JOIN best_selling_artist bsa ON bsa.artist_id = alb.artist_id
GROUP BY c.customer_id, c.first_name, c.last_name, bsa.artist_name
ORDER BY 5 DESC;

--. We want to find out the most popular music Genre for each country. We determine the most popular 
--genre as the genre with the highest amount of purchases. Write a query that returns each country 
--along with the top Genre. For countries where the maximum number of purchases is shared return all Genres

with popular_genre As
(
 select count(invoice_line.quantity) as Purchase, customer.country, genre.name, genre.genre_id,
 ROW_NUMBER() over (PARTITION by customer.country order by count(invoice_line.quantity) desc) as RowNo
 from invoice_line
 join invoice on invoice.invoice_id = invoice_line.invoice_id
 join customer on customer.customer_id = invoice.customer_id
 join track on track.track_id = invoice_line.track_id
 join genre on genre.genre_id = track.genre_id
 group by customer.country, genre.name, genre.genre_id
 )
 select * from popular_genre where RowNo <= 1;



-- . Write a query that determines the customer that has spent the most on music for each
--country. Write a query that returns the country along with the top customer and how
--much they spent. For countries where the top amount spent is shared, provide all
--customers who spent this amount

with customer_with_country as (
select customer.customer_id, customer.first_name, customer.last_name, billing_country ,sum(total) as total_spending
from invoice
join customer on customer.customer_id = invoice.customer_id
group by customer.customer_id, customer.first_name, customer.last_name, billing_country
),

country_max_spending as (
select billing_country, max(total_spending) as max_spending
from customer_with_country
group by billing_country
)

select cc.billing_country, cc.total_spending, cc.first_name, cc.last_name,cc.customer_id
from customer_with_country cc
join country_max_spending ms on cc.billing_country = ms.billing_country
where cc.total_spending = ms.max_spending
order by cc.billing_country;

--by cte

with customer_with_country as(
select customer.customer_id, first_name, last_name, billing_country, sum(total) as total_spending,
 ROW_NUMBER() OVER (PARTITION BY billing_country ORDER BY COUNT(total) DESC) AS RowNo
from invoice
join customer on invoice.customer_id = customer.customer_id
group by customer.customer_id, first_name, last_name, billing_country
)

select * from customer_with_country where RowNo <= 1
ORDER BY billing_country ASC, total_spending DESC;
