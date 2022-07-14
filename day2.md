```sql
use shop;
show tables;
select * from product;
select product_name, product_type from product2 where product_type = '衣服';
-- select product_id As id, product_name As name from product;
-- select distinct product_type from product;
select distinct product_type from product2;
select product_name, product_type from product where sale_price = 500;
select product_name, sale_price, sale_price * 2 as "sale_price x2" from product;
select product_name, sale_price, purchase_price from product where sale_price - purchase_price >= 500;
-- chars table 这里不太懂
select chr from chars where chr > '2';
select product_name, purchase_price from product where purchase_price is null;
select product_name, purchase_price from product where purchase_price is not null;

select product_name, product_type, sale_price from product where not sale_price >= 1000;

select product_name, product_type, regist_date from product where product_type = "办公用品" and (regist_date = '2009-09-11' or regist_date = '2009-09-20');

```

### 习题
```sql
-- 2.1
select product_name, regist_date from product where regist_date >= '2009-04-28';

-- 2.2
select * from product where purchase_price = null; /* false */
select * from product where purchase_price <> null; /* false */
select * from product where product_name > null; /* true */
-- 2.3
select product_name, sale_price, purchase_price from product where sale_price -  >= 500;
select product_name, sale_price, purchase_price from product where purchase_price + 500 <= sale_price;


-- 2.4
select product_name, product_type, (sale_price * 0.9) - purchase_price as 'profit' from product where purchase_price is not null;



-- 2.5 sum() 空格

-- 2.6
select product_type, sum(sale_price) as sum, sum(purchase_price) as sum from product group by product_type having sum(sale_price) > sum(purchase_price) * 1.5;

-- 2.7
select * from product order by if(isnull(regist_date),0,1), regist_date desc,purchase_price;
```
