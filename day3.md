```sql
use shop;
SELECT product_name FROM view_product;
-- 3.1
CREATE VIEW ViewPractice5_1 (product_type, sale_price,regist_date) AS SELECT product_type,sale_price,regist_date FROM product where sale_price>=1000 and regist_date="2009-09-20";
SELECT * FROM ViewPractice5_1;
-- 3.2
INSERT INTO ViewPractice5_1 VALUES (' 刀子 ', 300, '2009-11-02');
-- 3.3
select product_id ,product_name ,product_type ,sale_price , (SELECT AVG(sale_price) from product ) as sale_price_avg from product;
-- 3.4
CREATE VIEW AvgPriceByType (product_id,product_name ,product_type ,sale_price ,sale_price_avg_type) AS select product_id,product_name ,product_type ,sale_price , (SELECT AVG(sale_price) FROM product AS p2 WHERE p1.product_type = p2.product_type GROUP BY product_type) as sale_price_avg_type from product as p1;
-- 3.5 是
-- 3.6 商品成本价格不为500, 2800, 5000的商品 无法选出null的数据
-- 3.7
SELECT sum(case when sale_price<= 1000 then 1  else 0 end) as low_price, sum(case when sale_price between 1001 and 3000 then 1  else 0 end) as mid_price, sum(case when sale_price> 3000 then 1  else 0 end) as high_price FROM product;

```
