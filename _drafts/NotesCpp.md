---
layout: post
title: Notes on C++
comment: true

---

## Introduction 

C++ is a compiled language. For a program to run, its source text has to be processed by a compiler, producing object files, which are combined by a linker yielding an executable program. A C++ program typically consists of many source code files (usually simply called source files). An executable program is created for a specific hardware/system combination; it is not portable,say, from a Mac to a Windows PC. When we talk about portability of C++ programs, we usually mean portability of source code.

## Variables

A declaration is a statement that introduces a name into the program. It specifies a type for the
named entity:
- A type defines a set of possible values and a set of operations (for an object).
- An object is some memory that holds a value of some type.
- A value is a set of bits interpreted according to a type.
- A variable is a named object.
C++ offers a variety of fundamental types such as bool, char, int and double.

A char variable is of the natural size to hold a character on a given machine (typically an 8-bit byte), and the sizes of other types are quoted in multiples of the size of a char. The size of a type is implementation-defined (i.e., it can vary among different machines) and can be obtained by the sizeof operator; for example, sizeof(char) equals 1 and sizeof(int) is often 4.

When defining a variable, you don’t actually need to state its type explicitly when it can be deduced from the initializer. We use **auto** where we don’t have a specific reason to mention the type explicitly. Using auto, we avoid redundancy and writing long type names. This is especially important in generic programming where the exact type of an object can be hard for the programmer to know and the type names can be quite long.

### Constants
C++ supports two notions of immutability(of an object with an unchangeable state):
- **const**: meaning roughly "I promise not to change this value". This is used primarily to specify interfaces, so that data can be passed to functions without fear of it being modified. The compiler enforces the promise made by const.
- **constexpr**: meaning roughly "to be evaluated at compile time" (§10.4). This is used primarily to specify constants, to allow placement of data in memory where it is unlikely to be corrupted, and for performance.

{% highlight cpp %}
const int dmv = 17; // dmv is a named constant
int var = 17; // var is not a constant
constexpr double max1 = 1.4∗square(dmv); // OK if square(17) is a constant expression
constexpr double max2 = 1.4∗square(var); // error : var is not a constant expression
{% endhighlight %}

### Pointers, Arrays and Loops
In declarations, [] means "array of" and ∗ means "pointer to".

{% highlight cpp %}
int *p, var; /*var is an integer, p is a pointer*/
var=100;
p= &var; /*p is a pointer storing the address of var*/
cout<<p; /*address of var*/
cout<<"Value of var: "<<*p; /*print the value of var*/
char* p= &v[3];
{% endhighlight %}

<p align="center"> 
<img src="/blog/assets/array_ptr.png" width="480" height="260" alt="fourier_gif">
</p> 
C++ also offers a simpler for-statement, called a range-for-statement, for loops that traverse a sequence in the simplest way:
{% highlight cpp %}
void print()
{
int v[] = {0,1,2,3,4,5,6,7,8,9};
for (auto x : v) // for each x in v
cout << x << '\n';
for (auto x : {10,21,32,43,54,65})
cout << x << '\n';
}
{% endhighlight %}
