# Explanation 
## implementing web apps with dynamic view
to start to implement dynamic pages, we use Thymeleaf as our engine, now in the controller we add parameter of type `Model` and this work as map, which you add `<Key,Value>` to it with `addAttribute(key,value)` 
so to start to work
- add page in `resources/templates` instead of `resources/static` which we use in static pages
- now in this page you can add `xmlns:th="http:.//www.thymeleaf.org"` to use th as a shortcut of thymeleaf 
- now you can use th to define things from thymeleaf
- you can now start using keys and values you send with the model, mention it with `${key}` which will get the value and assign it here whatever it was 
### Getting Data on the HTTP request
in most cases you want to send data to the server so it can handle it to make some actions or saving it to the database and so on
to send data via the request we can send it in multiple ways
- **Request Parameter** it used to send the data to server in way of `<key,value>` style, and it appends in the URL for anyone, this way can't send large quantities of data 
- **Request Header** it sends it as `<key,value>` but in the header itself, it doesn't appear in the URL, also can't be used in large data
- **Path Variable** it sends the data in the URL as path like `/{id}`, this approach is used when the data is mandatory
- **Request Body** is the main way to use when the data is too large as it can send data like string and even files 
### Using request parameters to send data from the client to server 
this way is best fit if the data is too small and if the data is optional, like filter the products based in many things like price or brand and so on
to start use this one you add parameter to controller action with `@RequestedParam` and by default it's mandatory, but if you want to make it optional you add `@RequestedParam(required=false)` so it becomes optional
### Using path variables to send data from the client to server
this way is the best use when there are values that you need to make it mandatory by default, in this way you add the values only not the key anymore, so the URL become like `/home/blue` instead of `/home?color=blue`, also it's recommended to don't use it if there is more than 2 parameters as the URL will become ugly to read 
to use it in the controller you add `@PathVariable` to the parameter and also in the `@RequestMapping("/home/{color})` you add its name in the `{}` so it knows it's a path variable 
## Using the GET and POST HTTP methods
when you create an action in the controller you just add a path to it, but you need to tell spring what this action will do like read only, or it will update or create or even delete from the data we have in our database
> don't use HTTP methods against its designed purpose as this is bad choice 

instead of mark action with `@RequestMapping` you can add `@GetMapping` or `PostMapping` and also add the URL you want to map here as usual in `@RequestMapping` 
you can add the Entity itself as parameter of the action and spring will know that the fields is match of this entity and create it
# Sources
[[B- Spring Start Here.pdf]] 