# Understanding Package Declarations and Imports
Java puts classes in packages. These are logical groupings for classes. Suppose you try to compile this code:
```java
public class NumberPicker {
    public static void main(String[] args) {
        Random r = new Random(); // DOES NOT COMPILE
        System.out.println(r.nextInt(10));
    }
}
```
The Java compiler helpfully gives you an error that looks like this:
```commandline
error: cannot find symbol
```
This error could mean you made a typo in the name of the class. You double-check
and discover that you didn’t. The other cause of this error is omitting a needed import statement.
A statement is an instruction, and import statements tell Java which packages to look in for
classes. Since you didn’t tell Java where to look for Random, it has no clue.  
Trying this again with the import allows the code to compile.
```java
import java.util.Random; // import tells us where to find Random

public class NumberPicker {
    public static void main(String[] args) {
        Random r = new Random();
        System.out.println(r.nextInt(10)); // a number 0-9
    }
}
```
Now the code runs; it prints out a random number between 0 and 9. Just like arrays, Java
likes to begin counting with 0.
## Packages
As you saw in the previous example, Java classes are grouped into packages. The import
statement tells the compiler which package to look in to find a class. In the following sections, we look at imports with wildcards, naming conflicts with
imports, how to create a package of your own, and how the exam formats code.
## Wildcards
Classes in the same package are often imported together. You can use a shortcut to import all
the classes in a package.
```java
import java.util.*; // imports java.util.Random among other things

public class NumberPicker {
    public static void main(String[] args) {
        Random r = new Random();
        System.out.println(r.nextInt(10));
    }
}
```
The import statement doesn’t bring in  child packages, fields, or methods; it imports only classes directly under the package. Let’s
say you wanted to use the class AtomicInteger in the java.util.concurrent.atomic package. Which import or imports support this?
```java
import java.util.*;
import java.util.concurrent.*;
import java.util.concurrent.atomic.*;
```
Only the last import allows the class to be recognized because child packages are not
included with the first two.  
You might think that including so many classes slows down your program execution, but
it doesn’t. The compiler figures out what’s actually needed.
team. Listing the classes used makes the code easier to read, especially for new programmers. Using the
wildcard can shorten the import list. You’ll see both approaches on the exam.
## Redundant Imports
There’s one special package in the Java world called java.lang. This package is special in that it is automatically imported. You can type this
package in an import statement, but you don’t have to. In the following code, how many of
the imports do you think are redundant?
import java.lang.System;
```java
import java.lang.*;
import java.util.Random;
import java.util.*;

public class NumberPicker {
    public static void main(String[] args) {
        Random r = new Random();
        System.out.println(r.nextInt(10));
    }
}
 ```
The answer is that three of the imports are redundant. Lines 1 and 2 are redundant because
everything in java.lang is automatically imported. Line 4 is also redundant in this example
because Random is already imported from java.util.Random.  
Another case of redundancy involves importing a class that is in the same package as the
class importing it. Java automatically looks in the current package for other classes.
Let’s take a look at one more example to make sure you understand the edge cases for
imports. For this example, Files and Paths are both in the package java.nio.file. The
exam may use packages you may never have seen before. The question will let you know
which package the class is in if you need to know that in order to answer the question.
Which import statements do you think would work to get this code to compile?
```java
public class InputImports {
    public void read(Files files) {
        Paths.get("name");
    }
}
```
There are two possible answers. The shorter one is to use a wildcard to import both at the
same time.  
```java
import java.nio.file.*;
```
The other answer is to import both classes explicitly.
```java
import java.nio.file.Files;
import java.nio.file.Paths;
```
Now let’s consider some imports that don’t work.
```java
import java.nio.*; // NO GOOD -a wildcard only matches
                    // class names, not "file.Files"
import java.nio.*.*; // NO GOOD -youcan only have one wildcard
                    // and it must be at the end
import java.nio.file.Paths.*; // NO GOOD -you cannot import methods
                            // only class names
```
## Naming Conflicts
One of the reasons for using packages is so that class names don’t have to be unique across
all of Java. This means you’ll sometimes want to import a class that can be found in multiple
places. A common example of this is the Date class. Java provides implementations of
java.util.Date and java.sql.Date.
```java
public class Conflicts {
    Date date;
    // some more code
}
```
The answer should be easy by now. You can write either import java.util.*; or
import java.util.Date;. The tricky cases come about when other imports are present.
```java
import java.util.*;
import java.sql.*; // causes Date declaration to not compile
```
When the class name is found in multiple packages, Java gives you a compiler error. In
our example, the solution is easy—remove the import java.sql.* that we don’t need. But
what do we do if we need a whole pile of other classes in the java.sql package?
```java
import java.util.Date;
import java.sql.*;
```
Ah, now it works! If you explicitly import a class name, it takes precedence over any
wildcards present.  
One more example. What does Java do with “ties” for precedence?
```java
import java.util.Date;
import java.sql.Date;
```
Java is smart enough to detect that this code is no good.
Because there can’t be two defaults, the compiler tells you the imports are
ambiguous.
> Sometimes you really do want to use Date from two different packages. When this happens,
you can pick one to use in the import statement and use the other’s fully qualified
class name. Or you can drop both import statements and always use the fully qualified
class name.
> ```java
> public class Conflicts {
>   java.util.Date date;
>   java.sql.Date sqlDate;
> }
> ```
## Creating a New Package
In real life, always name your packages to avoid naming conflicts and to allow others to reuse your code.
Now it’s time to create a new package. The directory structure on your computer is
related to the package name. Suppose we have these two classes:
```java
package packagea;
public class ClassA {}

package packageb;

import packagea.ClassA;

public class ClassB {
    public static void main(String[] args) {
        ClassA a;
        System.out.println("Got it");
    }
}
```
When you run a Java program, Java knows where to look for those package names.
In this case, running from this folder works because both packagea and packageb are
underneath it.
## Compiling and Running Code with Packages
You’ll learn Java much more easily by using the command line to compile and test your
examples. Once you know the Java syntax well, you can switch to an IDE. But for the exam,
your goal is to know details about the language and not have the IDE hide them for you.  
The first step is to create the two files from the previous section. Table bellow shows the
expected fully qualified filenames and the command to get into the directory for the
next steps.

| Step                   | Location               |
|------------------------|------------------------|
| 1. Create first class  | ./packagea/ClassA.java |
| 2. Create second class | ./packageb/ClassB.java |
| 3. Go to directory     | This directory         |

Now it is time to compile the code. To compile, type the following command:
```commandline
javac packagea/ClassA.java packageb/ClassB.java
```
Two new files will be created: packagea/ClassA.class and packageb/ClassB.class.
> You can use an asterisk to specify that you’d like to include all Java files in a directory. This
is convenient when you have a lot of files in a package. We can rewrite the previous javac
command like this:  
> ```javac packagea/*.java packageb/*.java```  
> However, you cannot use a wildcard to include subdirectories. If you were to write
javac *.java, the code in the packages would not be picked up

Now that your code has compiled, you can run it by typing the following command:
java packageb.ClassB. Figure bellow shows where the .class files were created in the directory structure.
```commandline
- packagea
    - ClassA.java
    - ClassA.clas
- packageb
    - ClassB.java
    - ClassB.class
```
## Compiling to Another Directory
By default, the javac command places the compiled classes in the same directory as the
source code. It also provides an option to place the class files into a different directory. The
-d option specifies this target directory.
> Java options are case sensitive. This means you cannot pass -D instead of -d.

Where do you think this command will create the file ClassA.class?  
```javac -d classes packagea/ClassA.java packageb/ClassB.java```
The correct answer is in classes/packagea/ClassA.class.  
The package structure is preserved under the requested target directory. Figure bellow shows this new structure.
```commandline
- packagea
    - ClassA.java
- packageb
    - ClassB.java
- classes
    - packagea
        - ClassA.clas
    - packageb
        - ClassB.class
```
To run the program, you specify the classpath so Java knows where to find the classes.
There are three options you can use. All three of these do the same thing:
```commandline
java -cp classes packageb.ClassB
java -classpath classes packageb.ClassB
java --class-path classes packageb.ClassB
```
Notice that the last one requires two dashes (--), while the first two require one dash (-).
If you have the wrong number of dashes, the program will not run.  

Important javac options

| Option                                                                                | Description                                       |
|---------------------------------------------------------------------------------------|---------------------------------------------------|
| -cp <**classpath**> <br> -classpath <**classpath**> <br> --class-path <**classpath**> | Location of classes needed to compile the program |
| -d <**dir**>                                                                          | Directory in which to place generated class files |

Important java options

| Option                                                                                | Description                                       |
|---------------------------------------------------------------------------------------|---------------------------------------------------|
| -cp <**classpath**> <br> -classpath <**classpath**> <br> --class-path <**classpath**> | Location of classes needed to run the program     |

## Compiling with JAR Files
Just like the classes directory in the previous example, you can also specify the location
of the other files explicitly using a classpath. This technique is useful when the class files are
located elsewhere or in special JAR files. A Java archive (JAR) file is like a ZIP file of mainly
Java class files.  
On Windows, you type the following:  
```commandline
java -cp ".;C:\temp\someOtherLocation;c:\temp\myJar.jar" myPackage.MyClass
```  
And on macOS/Linux, you type this:  
```commandline
java -cp ".:/tmp/someOtherLocation:/tmp/myJar.jar" myPackage.MyClass
```
The period (.) indicates that you want to include the current directory in the classpath. The
rest of the command says to look for loose class files (or packages) in someOtherLocation
and within myJar.jar. Windows uses semicolons (;) to separate parts of the classpath; other
operating systems use colons.  
Just like when you’re compiling, you can use a wildcard (*) to match all the JARs in a
directory. Here’s an example:  
```commandline
java -cp "C:\temp\directoryWithJars\*" myPackage.MyClass
```
This command will add to the classpath all the JARs that are in directoryWithJars. It
won’t include any JARs in the classpath that are in a subdirectory of directoryWithJars.
## Creating a JAR File
Some JARs are created by others, such as those downloaded from the Internet or created
by a teammate. Alternatively, you can create a JAR file yourself. To do so, you use the jar
command. The simplest commands create a jar containing the files in the current directory.
You can use the short or long form for each option.
```commandline
jar -cvf myNewFile.jar .
jar --create  --verbose --file myNewFile.jar .
```
Alternatively, you can specify a directory instead of using the current directory.
```commandline
jar -cvf myNewFile.jar -C dir .
```