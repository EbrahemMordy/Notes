# Explanation
When you have two tables, and you want to get data from two of them with custom condition and join them in same table 
>N<sub>r</sub> is the number of rows in R
  N<sub>s</sub> is the number of rows in S
## Join Plan
it's the plan that have Join Operation as root and have two children's Left **Outer** and Right **Inner** 
## Nested Loop Join
> The Bad One

Work With all type of conditions
```
foreach tuple r in R
	foreach tuple s in S
		if(condation) output row
```
### Cost of Nested Loop
> Cost=N<sub>r</sub> +(N<sub>r</sub> \* N<sub>s</sub>) 
> Cost=min(N<sub>r</sub>, N<sub>s</sub>) + (N<sub>r</sub> \* N<sub>s</sub>)
## Index Nested Loop Join
instead of loop over the second table each time, we will search in the index with the value
```
foreach tuple r in R
	SS = Search Index for condation 'r.id'
	foreach tuple s in SS
		output row
```
### Cost of Index Nested Loop
> Cost=N<sub>r</sub> +(N<sub>r</sub> \* C<sub>index</sub>) 
## Merge Join
> Only Work With Equal condition 

Sort the tables based on the join column and start to merge them as merge sort
### Cost of Merge Join
> Cost = N<sub>r</sub> + N<sub>s</sub> + Sort
## Hash Join
> Only Work With Equal condition 

Build Hash Table for smallest table and take the other and work as we have done with Index Nested Loop Join, but now we will use the Hash Table as the index
```
Build Hash Table On S.id
foreach tuple r in R
	SS = Search Hash Table for condation 'r.id'
	foreach tuple s in SS
		output row
```
### Cost of Hash Join
> Cost = (N<sub>r</sub> + N<sub>s</sub>) \* C<sub>Hash</sub> 
# Sources
- [Join Algorithms - Nested Loop, Merge, Hash (Arabic - عربي) with Amr Elhelw - Tech Vault](https://www.youtube.com/watch?v=oVeo3i5ExaA&list=PLE8kQVoC67PzGwMMsSk3C8MvfAqcYjusF&index=10&pp=iAQB "Join Algorithms - Nested Loop, Merge, Hash (Arabic - عربي) with Amr Elhelw - Tech Vault") 
