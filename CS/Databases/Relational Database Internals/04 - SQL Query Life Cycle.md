# Explanation 
>SQL → Parser (Parse Tree) → Analyzer (Initial Plan) → Optimizer (Execution Plan)→ Execution Engine 
## CRUD Operations
CRUD means
- C for creating `Insert` 
- R for read `Select` 
- U for update `Update` 
- D for delete `Delete` 
## Query Engine
it's the part where we take the SQL query and process it and return the result for the user
## Parsing
Take SQL query and make it tokens and also check syntax if it's valid or not
![](Imgs/Pasted%20image%2020250520081825.png)

after parse the query the parser make them as tree

![](Imgs/Pasted%20image%2020250520082159.png)
## Query Analyzer 
Semantic Check:
- Tables
- Columns
- Data Types
- Ambiguous Columns
- Functions 

after check and validate it will create the initial plan
![](Imgs/Pasted%20image%2020250520082626.png)
### Catalog
its collection of metadata of the database to make it easy to check in analyzer 
## Query Optimizer
take the initial plan and try to optimize it 
![](Imgs/Pasted%20image%2020250520083546.png)

for each plan he tries to calculate the cost of each one by cost model from **database statistics** 
## Execution Engine
take the final plan which is the output of the optimizer and run it 
# Sources
- [SQL Query Life Cycle (Arabic - عربي) with Amr Elhelw - Tech Vault](https://www.youtube.com/watch?v=SEKF4u6Ovyw&list=PLE8kQVoC67PzGwMMsSk3C8MvfAqcYjusF&index=9&pp=iAQB "SQL Query Life Cycle (Arabic - عربي) with Amr Elhelw - Tech Vault") 
