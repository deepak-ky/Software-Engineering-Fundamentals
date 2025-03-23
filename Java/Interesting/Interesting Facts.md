
1. why one can not import classes from default package in java?
	1. Up to Java 1.4 it was possible to import classes from the default package, just by writing: import ClassName;. This feature was removed in Java 5. **It's not a good idea to put classes in the default package - you should always put your classes in a package.**
	2. **You can't import classes from the default package. You should avoid using the default package except for very small example programs.**
		1. From the [Java language specification](http://java.sun.com/docs/books/jls/third_edition/html/packages.html#7.5):
		2. It is a compile time error to import a type from the unnamed package.


2. 