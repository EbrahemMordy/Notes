# Explanation

## DBMS Structure 
![](Imgs/Pasted%20image%2020250430015759.png)
## Storage Types
![](Imgs/Pasted%20image%2020250430020139.png)
## Data Movement
get data from Disk and save it in memory to query over it and after that save it to disk
## Files & Pages
- Files
	- Pages : block of data with unique ID for each page
## File Organization
![](Imgs/Pasted%20image%2020250430021025.png)
## Heap Files
files with unordered pages
## Page Directory 
special pages with each file contain
- location of each data page in the file
- number of free slots per page
- list of empty/free pages
## Page Layouts
- Page Header
	- Page Size
	- DBMS version
	- info of encoding and compression
- Tuples
## Slotted Pages
Add slot array that have
- number of slots
- offset of last used slot
each slot points to a tuple, and we add tuples from the end of page
## Log Structured Pages
- also known as log-structured merge trees 
- record changes rather than storing the tuples in pages
	- each entry is SET or DELETE operation
	- must include tuple ID 
how to read tuple with given ID
- find the newest entry with this ID
- scan log from end to beginning 
optimize:
- add index to mark last entry for each ID
Compaction : remove all entries that are useless and just pick the last one for each ID
## Index-Organized Tables
Store the actual data into the index
- faster read
- slower writes
- reduced storage 
## Tuple Structure 
**Header|Data**
if the data can not fit the word size we can hash it and store the data in another page or even other file like blob and then use the pointer to it and add it in the tuple
# Sources
- [Database Storage - Part 1 (Arabic - عربي) with Amr Elhelw - Tech Vault](https://www.youtube.com/watch?v=-HtHhBQbMB4&list=PLE8kQVoC67PzGwMMsSk3C8MvfAqcYjusF&index=3&pp=iAQB "Database Storage - Part 1 (Arabic - عربي) with Amr Elhelw - Tech Vault")
- [Database Storage - Part 2 (Arabic - عربي) with Amr Elhelw - Tech Vault](https://www.youtube.com/watch?v=8-LJyyAjOhE&list=PLE8kQVoC67PzGwMMsSk3C8MvfAqcYjusF&index=4&pp=iAQB "Database Storage - Part 2 (Arabic - عربي) with Amr Elhelw - Tech Vault")
