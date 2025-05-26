# Explanation
Combining and summarizing multiple data records into a single result set based on some condition
## Aggregation Steps
- Split input rows into groups 
	- only if there is a `group by` or `distinct`
	- otherwise make them only 1 big group
- Combine values within same group
	- may use functions like `count,min,max,sum,avg,etc` 
- Output one row per group
## Sort-Based Aggregation
sort the table based on the aggregation column and loop over the sorted table and for each row add it to it's group and make whatever need for output
## Hash-Based Aggregation
create hash table and for each row apply the hash function and add the row for the bucket and update the values saved in that bucket **as required in the query** 
# Sources
[Aggregation Algorithms - Sort-based & Hash-based (Arabic - عربي) with Amr Elhelw - Tech Vault](https://www.youtube.com/watch?v=dHOYDnqJ9HY&list=PLE8kQVoC67PzGwMMsSk3C8MvfAqcYjusF&index=11&pp=iAQB "Aggregation Algorithms - Sort-based & Hash-based (Arabic - عربي) with Amr Elhelw - Tech Vault") 