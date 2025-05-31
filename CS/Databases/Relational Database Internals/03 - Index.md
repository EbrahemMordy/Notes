# Explanation

## How we read data from table
**Full table scan** Loop over all data in the page and compare the values with some condition 
**parallel Scan** Use multi threads to read data from the pages
- complex 
- based on ur PC like CPU

**partitioning** split the data into some parts with some condition valid for all data in this part
- diff size on each part
- insert take time to check which part to insert in
- if you need another condition other than the first condition it will be bad 

**Index** use index to find the data which we want
## What is the index
it is like a look-up table to check when you want to find some data with some conditions 
help us find two types of queries
- Point query
- Range query
## How to store index
- List
	- store them as list with key and the location
	- Take **O(N)** to find the values you want 
	- can optimize with BS but trade off with random access
- BST
	- Use BST to store the keys of the index and then query in each time we want to find some key
	- Take **O(Log(N))** as the maximum high of each path is Log **not always valid, but we can make BST always keep this true by make it balance itself or make it AVL tree** 
- B Tree
	- ordered and balanced
	- each node have to K children's in same node **each node can treat as list with size k-1** 
	- search on **O(Log(N))** for point query
	- range query **O(Log(N))** with time for reading more pages and go up and down in the tree
- B+ Tree
	- data only in leaves with pointers to next node with data
	- search on **O(Log(N))** point query
	- in range query we take **O(Log(N))** to find the first node after that we go right as we already have pointers to next node, so time is fine as we just load the pages of nodes we want no more time to find the nodes and climbs the tree
	- **Most Used**
## Hash index
- its like Hashing for strings
- take value and pass it to hash function and use the output as bucket number and add the value in it
- we assume that hash function is **one way** not sure about naming but its just when you give it x it gives u same value each time u give it x
- not ordered, not valid in range query
## Composite index
multi-column index, and we can use any type of index (hash/btree) 
- X,Y not equal Y,X
- Point X Point Y *Good and can use hash* 
- Point X Range Y *Good but can not be done with hash* 
- Range X Point Y *Working, but there are useless pages* 
- Range X Range Y *Working, but there are useless pages*
- Point X empty Y *Good if X,Y and can not be done with hash* 
- Empty X Point Y *Bad if X,Y and Good if Y,X*
- can be used to answer prefix search over the columns in the index 
	- if columns are X Y Z 
		- we can use it in:
			- X
			- X Y
			- X Y Z
- bad :
	- size due to size of more columns 
	- efficiency is not that good
	- complexity 
	- too many options due to more columns 
	- disjunction OR
## Index Intersection
use the output of two or more indexes and merge them to get the final output without use the composite index 
type of algorithms used to merge
- sort based
- hash based
- bitmap based
## Index Union
Same as intersect and just use union between them
## Covering Index 
it is indexed with data for some queries **it happens when the index columns are same as required in the query** 
## Clustered and Non-Clustered Index
**Non-Clustered**: it's index with non-sorted values in leaves, for more info it means that values in the leaves are sorted for its values but not sorted due to page number of it so it can be 121231 for pages and this lead to random access for disk

**Clustered**: we just sort the values to be sequential in the pages as it is in the index nodes and this make I/O fast, bad in update 
> can not have more than one clustered index in same table
## Bitmap Index
> Bitmap indexes are different from bitmap used in union and intersect between indexes 

designed to work with columns with small cardinality 
we put 1 in the index if the row is valid and 0 if not so it gives us a binary line for the rows he has with some 0 and 1 and any time we want to get some condition we get this index and fetch the rows with 1 for this value
![](Imgs/Pasted%20image%2020250515074029.png)
## Q&A
### The Diff between Primary ID and Row ID
![](Imgs/Pasted%20image%2020250515073035.png)
### The diff between index attribute and index page *recheck when free*
**index attribute**: is indexes that make on the attributes of table on database
**index page**: etc.
[Chat Research](https://chatgpt.com/s/dr_68257b7585e08191b5fe98de1251a54a)
### Composite Index or Index Intersection
depend on your case, when you need to choose, check them to decide
# Sources
- [Database Indexes - B and B+ Trees (Arabic - عربي) with Amr Elhelw - Tech Vault](https://www.youtube.com/watch?v=1ZhBULsbZGw&list=PLE8kQVoC67PzGwMMsSk3C8MvfAqcYjusF&index=5&pp=iAQB "Database Indexes - B and B+ Trees (Arabic - عربي) with Amr Elhelw - Tech Vault") 
- [Database Indexes - Hash & Composite Indexes (Arabic - عربي) with Amr Elhelw - Tech Vault](https://www.youtube.com/watch?v=ddWoqXw6Qic&list=PLE8kQVoC67PzGwMMsSk3C8MvfAqcYjusF&index=6&pp=iAQB "Database Indexes - Hash & Composite Indexes (Arabic - عربي) with Amr Elhelw - Tech Vault") 
- [Database Indexes - Index Intersection, Union & more (Arabic - عربي) with Amr Elhelw - Tech Vault](https://www.youtube.com/watch?v=KTEViriyc-Q&list=PLE8kQVoC67PzGwMMsSk3C8MvfAqcYjusF&index=7&pp=iAQB "Database Indexes - Index Intersection, Union & more (Arabic - عربي) with Amr Elhelw - Tech Vault") 
- [Database Indexes - Q&A (Arabic - عربي) with Amr Elhelw - Tech Vault](https://www.youtube.com/watch?v=wY_SxRMLTvA&list=PLE8kQVoC67PzGwMMsSk3C8MvfAqcYjusF&index=8&pp=iAQB "Database Indexes - Q&A (Arabic - عربي) with Amr Elhelw - Tech Vault") 
