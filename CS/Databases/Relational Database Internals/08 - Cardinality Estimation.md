# Explanation
## What is Cardinality Estimation 
calculate the number of rows for each operation
### leaves
calculated from statistics of the database
### Non-Leaf Nodes
#### With no cardinality effect
which is node that don't remove or add any rows, like projection which just change name of column also sort etc.
#### Have cardinality effect
nodes that change the rows like select where and group by etc.
## Selection Cardinality
>For Select with say number of output rows equal to
>X=Number Of input Rows \* Ratio of rows of this filter (Selectivity *sel*, and it's between 0 and 1) 
>so in final we say
>F=rows<sub>in</sub> \* sel<sub>f</sub> 
## Filter Selectivity
try for each filter to get the most valid ratio for it, and we can try more than one way to do it
- calculate for each value the ratio for it and store all of them
- calculate the number of distinct values and divide the total ratio (1) between them
- store most frequent values **MFV** as we do in first way and calculate the total ratio of stored values after if we have more than values stored we will take the remaining ratio and divide it between all the remaining values 
## Histogram
used in range queries 
### Equi Width
![](Imgs/Pasted%20image%2020250530190901.png) 
### Equal Frequency
Store range of each bucket
![](Imgs/Pasted%20image%2020250530191157.png)
## Multiple Conditions 
get **sel** for each condition and combine them by multiply them
## Aggregation Cardinality
- if we don't have group by we are sure the output is just one row
- when we have group by some row it will be a number of distinct values in this row
- when we have group by more than one column we multiply the number of distinct values of each row or the minimum between it and the number of rows as we can not have rows more than existed 
## Join Cardinality
- when join column is same column it will be the number of foreign key
- general case is calculating the number of rows for each values in table a and table b and multiply them by the minimum values of distinct values in a and b
![](Imgs/Pasted%20image%2020250530193957.png)
- use histograms
![](Imgs/Pasted%20image%2020250530194331.png)

> if we have more than two tables, treat them 2 by 2 like [[a, b], c] join a and b then join the output with c
## Estimation Errors
error between estimated and actual values of rows
### Error Propagation
error in leaf is small and keep being bigger and bigger in higher levels
### Effects
wrong Estimation can lead to choose the wrong plan from the optimizer as he chooses plan based on the values which is totally wrong
### Reasons
- Missing/Outdated Statistics, to solve you need to refresh your Statistics
- Data Correlation, data have relation between them, but we treat them as independence, to solve this some systems allow making Statistics for multi-column
- Data Skew, distribution of data are not uniform 
- Complex Filters, try to make filters easy as you can, also can solve by **Sampling** 
![](Imgs/Pasted%20image%2020250530205201.png)
# Sources
- [Cardinality Estimation - Part 1 (Arabic - عربي) with Amr Elhelw - Tech Vault](https://www.youtube.com/watch?v=PPDDLS5NSyM&list=PLE8kQVoC67PzGwMMsSk3C8MvfAqcYjusF&index=13&pp=iAQB "Cardinality Estimation - Part 1 (Arabic - عربي) with Amr Elhelw - Tech Vault") 
- [Cardinality Estimation - Part 2 (Arabic - عربي) with Amr Elhelw - Tech Vault](https://www.youtube.com/watch?v=QwqNuRSLE3M&list=PLE8kQVoC67PzGwMMsSk3C8MvfAqcYjusF&index=14&pp=iAQB "Cardinality Estimation - Part 2 (Arabic - عربي) with Amr Elhelw - Tech Vault") 
- [Cardinality Estimation - Part 3 (Arabic - عربي) with Amr Elhelw - Tech Vault](https://www.youtube.com/watch?v=ZD0ZarOR438&list=PLE8kQVoC67PzGwMMsSk3C8MvfAqcYjusF&index=15&t=216s&pp=iAQB "Cardinality Estimation - Part 3 (Arabic - عربي) with Amr Elhelw - Tech Vault") 
