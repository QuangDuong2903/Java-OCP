# Understanding the Class Structured
In Java programs, classes are the basic building blocks. . In later chapters, you see
other building blocks such as interfaces, records, and enums.  
To use most classes, you have to create objects. An object is a runtime instance of a class
in memory. An object is often referred to as an instance since it represents a single representation
of the class.  
A reference is a variable that points to an object.
## Fields and Methods
Java classes have two primary elements: methods, often called functions or procedures in
other languages, and fields, more generally known as variables. Together these are called the
members of the class. Variables hold the state of the program, and methods operate on that
state.  
```java
public class Animal {
    String name;
    public String getName() {
        return name;
    }
    public void setName(String newName) {
        name = newName;
    }
}
```
The method name and parameter types are called the method signature.
```java
public int numberVisitors(int month) {
    return 10;
}
```
The method name is numberVisitors. There’s one parameter named month,
which is of type int, which is a numeric type. Therefore, the method signature is
numberVisitors(int).
## Comments
Another common part of the code is called a comment. There are
three types of comments in Java. The first is called a single-line
comment:
```java
// comment until end of line
```
A single-line comment begins with two slashes. The compiler ignores anything you type
after that on the same line. Next comes the multiple-line comment:
```java
/* Multiple
* line comment
*/
```
A multiple-line  comment (also known as a multiline comment) includes anything starting
from the symbol /* until the symbol */. People often type an asterisk (*) at the beginning of
each line of a multiline comment to make it easier to read, but you don’t have to. Finally, we
have a Javadoc comment:
```java
/**
* Javadoc multiple-line
comment
* @author Jeanne and Scott
*/
```
This comment is similar to a multiline comment, except it starts with /**. Javadoc comments have a
specific structure that the Javadoc tool knows how to read. You probably won’t see a
Javadoc comment on the exam. Just remember it exists so you can read up on it online when
you start writing programs for others to use.
## Classes and Source Files
Most of the time, each Java class is defined in its own .java file. In this chapter, the only top-level
type is a class. A top-level type is a data structure that can be defined independently
within a source file. A top-level class is often public, which means any code can call it. Interestingly, Java does
not require that the type be public. For example, this class is just fine:
```java
class Animal {
    String name;
}
```
You can even put two types in the same file. When you do so, at most one of the top-level
types in the file is allowed to be public. That means a file containing the following is
also fine:
```java
public class Animal {
    private String name;
}
class Animal2 {}
```
If you do have a public type, it needs to match the filename. The declaration
public class Animal2 would not compile in a file named Animal.
