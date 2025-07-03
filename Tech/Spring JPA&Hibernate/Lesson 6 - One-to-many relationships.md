# Explanation 
One to many means that some entity have more than one row from the other entity but now the reverse, which is one row from entity is still have one row from the other
## How to create One-To-Many relationship
- *Many - One Way* 
- create the two entities as usual
- in the entity that will be the many rows you add `ManyToOne` at it above attribute of other entity type
- ---
- *One - One Way* 
- same things but in the entity which will be one, you add `OneToMany` 
- If you didn't add `JoinColumn` it will create 3 Tables
- --
- *Bidirectional Way* 
- you add in both entities, but you must add `mappedBy` in `OneToMany` 


# Sources
[Lesson 6 - One-to-many relationships](https://www.youtube.com/live/WVjXS_A_H6k?si=96SeklryyRDN4I4m) 