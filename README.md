# Orders-Data-SQL-CastStudy

-- top 5 rows with highest sales values
select * from orders_data
order by sales desc
limit 5; 	

-- all quantities between 3 and 7

select * from orders_data 
where quantity between 3 and 7;
-- order by quantity desc;
-- in clause takes list of values in where clause

select * from orders_data
where quantity in (4,5)
order by quantity;

-- all the sales for san francisco and los angeles
select city, sales
from orders_data
where city in ('San Francisco','Los Angeles')
order by city,sales desc;
-- limit 3;

-- top 3 sales in both the cities. 
(select city, sales from orders_data
where city in ('San Francisco')
order by city,sales desc
limit 3)
union
(select city, sales from orders_data
where city = 'Los Angeles'
order by city,sales desc
limit 3);

-- using between clause for dates
select order_id, order_date from orders_data
where order_date between '2018-06-09' and '2019-10-11' ; 

-- total sales of return orders 

with cte as(
select order_id, sales from orders_data where order_id in (select order_id from returns_data))
select sum(sales) as returns_sale from cte;

-- give all the data which was not returned
