# Writing a main() Method
A Java program begins execution with its main() method. The main() method is often called an entry
point into the program, because it is the starting point that the JVM looks for when it begins
running a new program.
## Creating a main() method
The main() method lets the JVM call our code. The simplest possible class with a main()
method looks like this:
```java
public class Zoo {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```
This code prints Hello World. To compile and execute this code, type it into a file called
Zoo.java and execute the following:
```commandline
javac Zoo.java
java Zoo
```
To compile Java code with the javac command, the file must have the extension .java.
The name of the file must match the name of the public class. The result is a file of bytecode
with the same name but with a .class filename extension.
The rules for what a Java file contains, and in what order, are more detailed than what we
have explained so far (there is more on this topic later in the chapter). To keep things simple
for now, we follow this subset of the rules:
- Each file can contain only one public class.
- The filename must match the class name, including case, and have a .java extension.
- If the Java class is an entry point for the program, it must contain a valid main() method.
Finally, we arrive at the main() method’s parameter list, represented as an array of
java.lang.String objects. You can use any valid variable name along with any of these
three formats:
```java
String[] args
String options[]
String... friends
```
The compiler accepts any of these. The variable name args is common because it hints
that this list contains values that were read in (arguments) when the JVM started.
The characters ... are called varargs (variable argument lists).
> While most modifiers, such as public and static, are required for main() methods,
there are some optional modifiers allowed.  
> ```public final static void main(final String[] args) {} ```  
> In this example, both final modifiers are optional, and the main() method is a valid
entry point with or without them.
## Passing Parameters to a Java Program
Let’s see how to send data to our program’s main() method. First, we modify the Zoo
program to print out the first two arguments passed in:
```java
public class Zoo {
    public static void main(String[] args) {
        System.out.println(args[0]);
        System.out.println(args[1]);
    }
}
```
To run it, type this:
```commandline
javac Zoo.java
java Zoo Bronx Zoo
```
The output is what you might expect:
```commandline
Bronx
Zoo
```
Spaces are used to separate the arguments. If you want spaces inside an argument, you need to use quotes as
in this example:
```commandline
javac Zoo.java
java Zoo "San Diego" Zoo
```
Now we have a space in the output:
```commandline
San Diego
Zoo
```
Finally, what happens if you don’t pass in enough arguments?
```commandline
javac Zoo.java
java Zoo Zoo
```
> If you get tired of typing both javac and java every time you want to try a code example,
there’s a shortcut. You can instead run  
> ```java Zoo.java Bronx Zoo```  
> This feature is called launching single-file source-code programs and is useful for
testing or for small programs. The name cleverly tells you that it is designed for when your
program is one file.