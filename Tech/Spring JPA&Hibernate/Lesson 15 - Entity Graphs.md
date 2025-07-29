# Explanation
it's a graph that build using the entities, used to solve N+1 problem
## How to build graph
- use entity manager to create the graph
- add for it the attributes that represent the relations
- to use, send it as Hint for the query
- you can use subgraph to build graph as you want with any depth 
## How to create
- create `EntityGraph<?>` from the Entity manager 
- add attributes that represent relations in the entities 
- and when write query, set hint to be the graph 
- to create a `subgraph` you define it from the graph itself and add the next attribute that represent the first relation, and add to it next attribute `Subgraph<?> sub=graph.addSubgraph(first)`
- `sub.addAtrr(second)` 
# Source
[Lesson 15 - Entity Graphs](https://www.youtube.com/live/i_MrUQphXvA?si=4mksd8rN9nDHfaSI) 