# Explanation
split database into some number of nodes or shards
in the sharded database we have two things
- shard manager
	- know which shards we have and metadata of it
- query router
	- route queries for correct shards
## Sharding Strategies
### Sharding key
it's like hash function 
#### Directory Based Sharding
map for each value which shard this value is in
- easy in implementation 
- query route become fast
- unbalance shards *bad* 
#### Range Based Sharding
map for each range which shard this range are in
- range queries are optimized 
- same as directory based 
#### Hash based Sharding **Most Used**
hash values to get shard it is in, modules with number of shards
## Scaling & Redistribution
when i need to reassign data into shards
very cost operation don't make it too many
## Consistent Hashing
make hash space as ring and map each key for the nearest shard in clockwise 

# Sources
- [Database Sharding (Arabic - عربي) with Amr Elhelw - Tech Vault](https://www.youtube.com/watch?v=-GXQwCIRANA&list=PLE8kQVoC67PzGwMMsSk3C8MvfAqcYjusF&index=23&pp=iAQB "Database Sharding (Arabic - عربي) with Amr Elhelw - Tech Vault") 