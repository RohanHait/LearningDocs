
# Installation 
 install from openjdk 
# First Program 
```java
/**
 * File Name Must be Example.java
 */

public class Example {
    public static void main(String[] args) {
        IO.println("Hello World!!");

        String name = IO.readln("What Your Name? ");

        IO.println("नमस्ते " + name);

    }
}

```
## Java Listed Keywords 
Keywords are reserves words that have a predefined meaning 

java has total 53 Keywords.



# Data Types, Variables and Arrays 
## Primitive Data Types
- **Integers**: java have 4 types of integers

| Name    | Size(bit) |
| ------- | --------- |
| `long`  | 64        |
| `int`   | 32        |
| `short` | 16        |
| `byte`  | 8         |
```java
int x = 26 
int x = 0b11010 
int x = 0x1b
int x = 124_134_123 // Value of the x will be 124,134,123.  '_' will be ignored
int x = 124__134__123 // value will be 124,134,123 as more then one '_' is permissable 
int x = 0b01010__01010__01010 // is still valid as '_' will be ignored
```
- **Floating Points Type:** 

| Name     | Size(bits) |
| -------- | ---------- |
| `double` | 64         |
| `float`  | 32         |

```java
double x = 3.14159 
double x = -0.667
/** e or E followed by number represent 10 ^ {number}*/
double x = 6.022E23 // Valid 6.023 * 10^23 *
double x = 314159E-05 // valid 3.14159
double x = 2e100  // valid 2*10^100

/**
Hexadecimal Floating-point 
*/
double x = 0x12.2P2 // 0x12.2p2 both are valid hexadecimal representation. 

double x = 123_143.02 // is valid and equal to 123,143.02 as underscore will be ignored 
if (x== Double.NaN) // is never true 
if(Double.isNan(x)) // check whether x is "not a number"
```
- **Characters:** java store characters in `char`. It use Unicode to represent characters. so it's size is 16 bit (2 Byte) 

| Escape Sequence | Name            | Unicode Value |
| --------------- | --------------- | ------------- |
| \b              | Backspace       | \u0008        |
| \t              | Tab             | \u0009        |
| \n              | Line feed       | \u000a        |
| \r              | Carraige Return | \u000d        |
| \f              | Form feed       | \u000c        |
| \\"             | Double quote    | \u0022        |
| \\'             | Single quote    | \u0027        |
| \\\             | Blackslash      | \u005c        |

> [!CAUTION] 
> Unicode excape sequences are processed before the code is parsed. For example 
> "\u0022 + \u0022" is not a string consisting of a plus sign surrounded by quotation marks (U+0022). Instead the \u0022 are converted into " before parsing, yielding "" + "" or an empty string.
> // \u000A is a newline 
> yields to syntax error as \u000A is replaced with new line
> // look inside c:\users 
> also yields a syntax error because \u is not followed by four hex digits

- **Boolean:**  size 1 bit . only have two possible value `True` or `False` 

## Variable
**Declaration:** `type identifier[ = value] [, identifier [= value]....];` ex. `int a , b , c= 10 ;`

## Type Castings 
### Automatic Type Casting 
- if two types are compatible, then java will perform the conversion  automatically 
- The destination type is larger then source type. 
### Casting Incompatible Types 
If The Type Conversion is incompatible then we need to explicitly type conversion. 
	(target type) value
	Ex: int a= 300; byte b ; b = (byte) a ;
> Note : In Explicit type casting they will convert the value different way for different things 
> Like for 
> 1. Big size Integer to small size integer it will  reduce by modulo operation 
> 2. For floating-point to integer  first it will convert to nearest small integer (**ceil**) then it will reduce module to the target type range .

### Type Promotion Rule
1. In Java Expression if  automatically promotes to a larger size if at any time it exceed the current limit. 
2. If any one of highest promotion type are present in the expression then whole expression is promotes to the highest promotion type. 
**Promotion Hierarchy:** `double > float > long > int >  (short , char) > byte`

## Type Inference(`var`)
- `var` is reserved word not a keyword (means we can declare a variable name `var` also)
- `var` can only used as a local variable and need to initialize immediately. 
- `var` is decided in compile time and change it's to the actual type.
Example 
```java
var var = 1 ;
var myArray = new int[10] ;
var i = True ? Integer.valueOf(1) : "ABC" ;
```
#### Restriction On 'var'
invalid var uses
```java
var counter ;
var[] myArray = new int[10]
var myArray[] = new int[10]
var myArray = {1,2,3}
```

### Operators
- Arithmetic Operators (+, - , / , * , % )
- Assignment (=) , binary Assignment( x += y -> x= x+ y)
- Increment and Decrement Operators(++ , --)
- Relation and `boolean` Operators(== , != , > , >= , < , <= , && , || )
- Bitwise Operators (& , | , ^ , ~ , <<(Left  Shift), >> (Right Shift except sign bit) , >>>(Right Shift with sign bit shift))
> [!Caution]
>  The right-hand argument of the shift operators is reduced modulo 32 (unless the left-hand argument is a `long`, in which case the right-hand argument is reduced modulo 64). For example, the value of `1 << 35` is the same as `1 << 3` or `8`.
- Conditional/Ternary  Operators  ($conditional ? Expression_1:  Expression_2$)
- Switch Expression 
	```java
	String season = switch(seasoneCode){
		case 0 -> "Spring" ;
		case 1 -> "Summar" ;
		case 2 -> "Fal" ;
		case 3 -> "Winter" ;
		default -> "???"
	}
	int numLetters = switch(seasonName){       
	case "Spring", "Summer", "Winter" -> 6;
	case "Fall" -> 4;
	default -> -1;
	};
	//switch value. For example: 
	enum Size { SMALL, MEDIUM, LARGE, EXTRA_LARGE }; . . . 
	Size itemSize = . . .; 
	String label = switch (itemSize){       
		case SMALL -> "S"; // no need to use Size.SMALL       
		case MEDIUM -> "M";       
		case LARGE -> "L";       
		case EXTRA_LARGE -> "XL";    
	}; // No need to add default since there was a case for each possible value

	```
> [!Caution]
> A switch expression with integer or string operand must always have a default since it must yield a value no matter what the operand value is

## Class
A class is a blueprint or template used to create objects. It define custom data type by grouping related data (instance variable) and behaviors(methods) into a single unit.
```
class classname{
type instance-variable1 ;
type instance-variable2
 .
 .
 .
type instance-variableN ;
type methodName1(arguments){
// body
}
type methodName2(arguments){
// body
}
.
.
.
type methodNameN(arguments){
// body
}

}
```

example 
```java
class Box {
double width;
double height ;
double depth ;
}
```
we can create an **instance/objects** of class  by using new keyword 
```java 
Box b1 = new Box() ;
```

> [!Note]
> Hare `b1` is a reference variable that refer to the Box object.  so if we assign `Box b2 = b1` , `b2` is still refer to the same object also ;
> a Variable can hold reference  to an object or the spacial value `null` to indicate the absence of an objects

>[!Caution] 
> ##### Working With `null` reference
> If you apply a method to a `null` value a `NullPointerException` occurs. If the program does not "catch" an exception, it is terminated. 
#### Call by Value Vs Call by Reference 
**Primitive types are always passed by value .**
```java
// Primitive types are passed by value.
class Test {
void meth (int i, int j) {
i *= 2;
j /= 2;
}
}
class CallByValue {
public static void main(String[] args) {
	Test ob = new Test();
	int a = 15, b = 20;
	System.out.println("a and b before call: " + a + " " + b); 
	// a and b before call: 15,20
	ob.meth(a, b);
	System.out.println("a and b after call: " + a + " " + b);
	// a and b after call: 15,20
	}
}
```
**Objects are always passed by their reference**
```java
class Test {
int a, b;
Test (int i, int j) {
a = i;
b = j;
}
// pass an object
void meth (Test o) {
o.a *= 2;
o.b /= 2;
}
}
class PassObjRef {
public static void main(String[] args) {
	Test ob = new Test (15, 20);
	System.out.println("ob.a and ob.b before call:"+ ob.a + " " + ob.b);
	// a and b before call: 15,20
	ob.meth (ob);
	System.out.println("ob.a and ob.b after call:" + ob.a + " " + ob.b);
	// a and b after call: 30,10
	}
}
```

For Return type same thing also thing happened ;
> [!Caution]
> Be careful not to write accessor methods that return references to mutable objects.
> As it's a reference type, changing in one reference can changed all the reference 
> ```java
> class Employee {
>     private Date hireDay;
>      . . .
>      public Date getHireDay()    
>      {       
>      return hireDay; // BAD    
>      return (Date) hireDay.clone() // Good
>      }    
>      . . . 
> }
> ```
### Constructors 
Constructor are just like a method that is invoke immediately upon creation. 
- it has the same name as class 
- it does not have any return type  not even void. 
- it can only be called  one time at the time of creation.
- all the class have a default constructor 
```
class ClassName {
ClassName(parameterList){ 
// body
}
}
```
If a constructor have parameter we call it **Parameterized Constructor**. 
A Class have more then one constructor with different parameter list  and it called **Constructor Overloading**. 
### `this` Keyword 
`this` can be used inside any method or constructor  to refer to current **objects/instance** .

Example : 
```java
class Box {
double width;
double height ;
double depth ;
Box(double w, double h , double d){
	this.width = w ;
	this.height = h ;
	this.depth = d ;
}
double getVolume(){
return this.width * this.height * this.depth ;
}
}
```

### Method Overloading
In Java, it is possible to define two or mire methods within the same class that shared the same name, **as long as their parameter declarations are different.** It's called method overloading . it's one of the way to support polymorphism. 
- Java use **type and/or number of arguments** to determine which version of method to actually call. 
- **Return Type** of method is insufficient to distinguish two versions of a method

Example :
```java
public class DemoOverloading {
    void test() {
        System.out.println("called test() with no args");
    }

    void test(int a) {
        System.out.println("called test(int a) with args:" + a);
    }

    void test(double a, double b) {
        System.out.println("called test(double a, double b) with args:" + a + " " + b);
    }

    void test(double a) {
        System.out.println("called test(double a) with args:" + a);
    }

    public static void main(String[] args) {
        int a_ = 10, b = 20;
        double a = 10.05;
        DemoOverloading obj = new DemoOverloading();
        obj.test(); // called test() with no args
        obj.test(a_); // called test(int a) with args:10
        obj.test(a); // called test(double a) with args:10.05
        obj.test(a, b); // called test(double a, double b) with args:10.05 20.0  
				    // Auto type casting
    }
}
```

### Constructors Overloading 
Same like method overloading we can overload a constructor methods
```java
class Box{
	double width;
	double height;
	double depth;
	Box(){
		width =  height = depth = -1 ;
	}
	Box(double value){
		width =  height = depth = value ;
	}
	Box(double w, double h, double d){
		width = w ;
		height = h; 
		depth = d;
	}
}

```
By passing the arguments it will called the respected constructor 
>[!Note] 
>You Can also call different constructor in the constructor also  by using this keyword example.
```java
class Demo {
Demo(){
	System.out.println("Default Constructor Called") ;
}
Demo(int a ){
	this() // Called Demo() constructor
	System.out.println("Parametarise Constructor Called") ;
}
public static void main(){
	Deom obj = new Demo(2) ;
	/* Output: 
	Default Constructor Called
	Parametarise Constructor Called
	**/
}
};
``` 
