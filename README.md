# Kiểm tra dữ liệu bảng product_emissiobs với 10 dòng
```
SELECT *
from product_emissions
limit 10
```
## Result
![image](https://github.com/user-attachments/assets/79af61ec-17a5-43f8-b20a-9c393e8159dc)

# 1. Which products contribute the most to carbon emissions?
## Code
```
select product_name
		,max(carbon_footprint_pcf) as max_carbon_emission
from product_emissions
group by product_name
order by max_carbon_emission desc
limit 10;
```
## Result
![image](https://github.com/user-attachments/assets/7ec59f77-37e4-491f-83f6-3389baa96479)
=> Lấy Productname : Wind Turbine G128 5 Megawats có lượng thải carbon lớn nhất

# 2. What are the industry groups of these products?
## Code
```
SELECT pe.product_name
		,ig.industry_group
		,max(pe.carbon_footprint_pcf) as max_carbon_emission
FROM product_emissions pe 
LEFT JOIN industry_groups ig ON ig.id = pe.company_id 
GROUP BY product_name
ORDER BY max_carbon_emission desc
LIMIT 10;
```
## Result
![image](https://github.com/user-attachments/assets/93849d17-b3cd-4554-a819-47f81e445808)
=> Các sản phẩm này là Commercial & Professional Services, Consumer Durables & Apparel, Gas Utilities

# 3. What are the industries with the highest contribution to carbon emissions?
## Code
```
SELECT ig.industry_group
		,sum(pe.carbon_footprint_pcf) as sum_carbon_emission
FROM product_emissions pe 
LEFT JOIN industry_groups ig ON ig.id = pe.company_id
GROUP BY industry_group
ORDER BY sum_carbon_emission desc
LIMIT 5;
```
## Result
![image](https://github.com/user-attachments/assets/63472173-901e-4e5b-9ca3-cb5a5c2c639f)
=> Industry_group:  Commercial & Professional Services với tổng lượng carbon thải ra lớn nhất

# 4. What are the companies with the highest contribution to carbon emissions?
## Code
```
SELECT companies.company_name
		,sum(pe.carbon_footprint_pcf) as sum_carbon_emission
FROM product_emissions pe 
LEFT JOIN companies ON companies.id = pe.company_id
GROUP BY company_name
ORDER BY sum_carbon_emission desc
LIMIT 5;
```
## Result
![image](https://github.com/user-attachments/assets/6117506e-4e60-426d-b08a-9dfd4e30c9bb)
=> Company: Gamesa Corporación Tecnológica, S.A với tổng lượng carbon thải ra lớn nhất

# 5. What are the countries with the highest contribution to carbon emissions?
## Code
```
SELECT countries.country_name
		,sum(pe.carbon_footprint_pcf) as sum_carbon_emission
FROM product_emissions pe 
LEFT JOIN countries ON countries.id = pe.country_id
GROUP BY country_name
ORDER BY sum_carbon_emission desc
LIMIT 5;
```
## Result
![image](https://github.com/user-attachments/assets/8d15a063-441f-489e-8158-c07573972daf)
=> Country: Spain với tổng lượng carbon thải ra lớn nhất

# 6. What is the trend of carbon footprints (PCFs) over the years?
## Code : Đánh giá theo lượng khí thải carbon trung bình
```
SELECT year
		,round(avg(carbon_footprint_pcf),2) as average_pcf_year
FROM product_emissions 
group by year
order by year
```
## Result
![image](https://github.com/user-attachments/assets/0899040c-b82b-4a24-bd2e-3194239d9af4)
=> Năm 2014 lượng carbon trung bình có tăng nhẹ so 2013 nhưng qua 2015 tăng 1 cách đột biến ( hơn 15 lần ) , sau đó giảm mạnh tới 2016 ( giảm 6 lần ) và giảm nhẹ về 2017.

# 7. Which industry groups has demonstrated the most notable decrease in carbon footprints (PCFs) over time?
## Code
SELECT pe.year
		,round(avg(carbon_footprint_pcf),2) as average_pcf_year
		,industry_groups.industry_group
FROM product_emissions pe 
LEFT JOIN industry_groups ON industry_groups.id = pe.industry_group_id
GROUP BY year














