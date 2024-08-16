# Truy xuất để kiểm tra dữ liệu như thế nào. limit 10
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
		,max(carbon_footprint_pcf) as maximum
from product_emissions
group by product_name
order by maximum desc
limit 10;
```
## Result
![image](https://github.com/user-attachments/assets/3958a5ef-447d-4a87-a819-5a99dc824a9f)
=> Lấy Productname : Wind Turbine G128 5 Megawats có lượng thải carbon lớn nhất
