# Explanation 
## Row Oriented Storage 
tables stored in files, each file stored in pages, each page contains rows 
### Pros
- Good in queries that read limited number of rows and many attributes
- fast writes
### Cons
- in OLAP queries, this is not the most performance storage
## Column Oriented Storage 
instead of store rows in pages, we store each column as one part 
### Connecting Values
#### Offsets
for fixed length values like integers and doubles and so on
- simple implementation
- no additional storage needed
- *Bads*
- only works with fixed-length
- all columns must store in same order
#### Explicit Row IDs
generate row ID for each row and store it with values
- work with any data type
- work better with OLAP
- *Bads*
- row IDs must store with every column with use more storage 
- limits data compression
- bad in OLTP
### Data Compression
compress data to make faster I/O but still take more CPU in encode and decode data
> original → compressed → run query → decompress 
#### Run Length Encoding **RLE**
instead of have same words repeats, we put the word and number of repeats
>hi hi hi → hi 3
>worst case when each word is unique
>the best case when data is sorted
#### Dictionary Encoding 
map each value for integer and instead of real value put the mapped integer 



# Sources
- [Columnar Databases/Column Stores - Part 1 (Arabic - عربي) with Amr Elhelw - Tech Vault](https://www.youtube.com/watch?v=8bDJPLhleeo&list=PLE8kQVoC67PzGwMMsSk3C8MvfAqcYjusF&index=24&pp=iAQB "Columnar Databases/Column Stores - Part 1 (Arabic - عربي) with Amr Elhelw - Tech Vault") 
- [Columnar Databases/Column Stores - Part 2 (Arabic - عربي) with Amr Elhelw - Tech Vault](https://www.youtube.com/watch?v=4IJ9hK4BuiI&list=PLE8kQVoC67PzGwMMsSk3C8MvfAqcYjusF&index=25&pp=iAQB "Columnar Databases/Column Stores - Part 2 (Arabic - عربي) with Amr Elhelw - Tech Vault") 
