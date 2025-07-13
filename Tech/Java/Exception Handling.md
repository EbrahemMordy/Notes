# Explanation
## What is Exception Handling
unwanted or unexpected even, which case unexpected flow in the program
## Error Vs Exception
Error is something doesn't work 
Exception is something work but have unexpected behavior 
## Try-Catch Block
when you have block of code that can cause an exception you can add it within try-catch block
```java
try{
	String s="123";
	sout(s[5]);
}
catch(){}
```
### Multi Catch Block
```java
try{
	String s="123";
	sout(s[5]);
}
catch(1){}
catch(2){}
catch(3){}
```
### Union Catch
```java
try{
	String s="123";
	sout(s[5]);
}
catch(1 | 2 | 3){}
```
## Finally Block
always runs this block at end of try, used to clean up sessions like db or network and so on
## Exceptions Types
### Checked Exceptions
it's exceptions that compiler can detect
### Unchecked Exceptions
runtime exceptions that only occur in runtime
### Errors
it's errors that happen with no solution
## Try with Resources
you add the instance in the try so you don't need to close it by hand as it will auto closed
```java
try(file f1;file f2){}
```
## Throws
when you don't want to handle exceptions here, you can propagate it to parent 
## Throw
used when you want to throw any error or exception here 
## Custom Exceptions
create a class that extend from Exception or Runtime Exception




# Sources
- [Adel Nasim Lec1](https://youtu.be/QtqPn4qxEL8?si=DomuYx39j9-hUC1s) 
- [Adel Nasim Lec2](https://youtu.be/hhwwFxSJGM0?si=bwntAecCvXO0LWgT) 
- [Adel Nasim Lec3](https://youtu.be/ebyGDZXWajQ?si=XZfbm4ZfmY9JBYOQ) 