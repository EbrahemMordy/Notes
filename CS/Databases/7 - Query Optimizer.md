# Explanation
## Why do we need the optimizer
the initial plan can not be the most optimized plan and can be optimized with a lot of ways so we need some component to try every possible optimization and give us the most one
- plan enumeration 
- plan selection 
## Plan Enumeration
find all plans that give us the same output as initial plan
> Initial plan is just Logical operations
### Logical operations 
cannot be executed 
- Join
- Scan
- Aggregation 
- Sorting
### Physical operations 
implementation for logical operations and can be executed and has a cost function 
## Rule-Based Optimization 
get initial plan and transform it with some fixed rules
![](Pasted%20image%2020250526152351.png) 
![](Pasted%20image%2020250526152713.png)
## Cost-Based Optimization
calculate cost for plans to check if the transform was optimized or doesn't matter as they are same cost, calculate cost with **cost model** as it has cost function for each operation
- join order
- Full scan, index scan....
- Join Algorithms
- Aggregation Algorithms
- Sorting Algorithms
- etc.
## Bottom-Up Optimization
start from leaves and for each node or operation find the most optimized plan for it and for each level save the most optimized plan and use it in higher level
![](Pasted%20image%2020250526154502.png)
## Top-Down Optimization
start form logical plan and try to find the most optimized plan
> **search for more details** 
# Sources
[SQL Query Optimizer (Arabic - عربي) with Amr Elhelw - Tech Vault](https://www.youtube.com/watch?v=iAxFGRbAh8s&list=PLE8kQVoC67PzGwMMsSk3C8MvfAqcYjusF&index=12&pp=iAQB "SQL Query Optimizer (Arabic - عربي) with Amr Elhelw - Tech Vault") 