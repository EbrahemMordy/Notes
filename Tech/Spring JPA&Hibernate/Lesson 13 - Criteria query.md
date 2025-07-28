# Explanation
only working with `select` and it used in cases like filters in the products and so on, its dynamic query
## How to write the Criteria query
- first one is to create the `builder` which is `CriteriaBuilder = em.getCriteriaBuilder` 
- then use the builder to create the query and store it `CriteriaQuery q=builder.createQuery(Name.class)` 
- now we need to make the root `Root<Name> root=q.from(Name.class)`
- after that we need to make the select for the root `q.select(root` 
- now generate the `TypedQuery` with the cq you make with `em.createQuery(cq)` 
- now you can work it as usual with `TypedQuery` 
- you can multi select in it with `cq.multiselect()` and in this time you change the type of `CriteriaQuery` to be `Object[]` but make sure the from is same as the Entity you want to select from
- if you want to select a function, you can use it from `builder` itself 
- also if you want to use where, you can add it in the select and use `builder` to use greater than and so on

# Source
[Lesson 13 - Criteria query](https://www.youtube.com/live/nkTA2XYvku4?si=4KGKYxB26hm4Ablg) 