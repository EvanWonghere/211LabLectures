# C++ Basic Course

## Chapter 1 —— Hello, C++!

### What is C++?

***C++ = C + Object-Oriented Programming + Generic Programming***

#### C Programming Philosophy

Let's talk about C  programming philosophy first. Like most mainstream language when C was created, C is a ***procedural*** language. That means it emphasizes the algorithm side of programming. Conceptually, procedural programming consists of figuring out the actions a computer should  take and then using the programming language to implement those actions. In short, ***Data + algorithms = program***. BTW, procedural programming, AKA ***Procedural-Oriented Programming***.

Earlier procedural languages, such as FORTRAN and BASIC, ran into organizational problems as problems as programs grew larger. Many older programs had such tangled routing (called "**spaghetti programming**") that is virtually impossible to understand a program by reading it, and modifying such a program was an invitation to disaster. In response, computer scientists developed a more disciplined style of programming called ***structured programming***. C includes features to facilitate this approach. The primary idea behind structured programming is to avoid the use of undesirable control flow structures such as infinite loops, unrestricted goto statements, and deeply nested conditional statements, and instead focus on using clear, organized control structures.

Structured programming has the following characteristics:

1. Sequential Structure: Programs execute statements sequentially, from top to bottom, one after the other.

2. Selection Structure: Conditional statements (e.g., if statements) are used to choose different code blocks for execution based on specific conditions.

3. Iteration Structure: Loop statements (e.g., for loops, while loops) are used to repeat a section of code until a specific condition is met.

What else need to be mentioned is the ***Top-down design***. With C, the idea is to break a large program into smaller, more manageable tasks. If one of these tasks is still too broad, you divide it into yet smaller tasks. You continue this process until the program is compartmentalized into small, easily programmed modules. C's design facilitates this  approach, encouraging you to develop program units called ***functions*** to represent individual task modules. As you may have noticed, **the structured programming techniques reflect a procedural mind-set, thinking of a program in terms of the actions it perform.**

#### The C++ Shift: Object-Oriented Programming

Although the principle of structured programming improved the clarity, reliability, and ease of maintenance of programs, large-scale programming still remains a challenge. ***Object-Oriented Programming*** brings a new approach to that challenge. Unlike procedural programming, which emphasizes algorithms, OOP emphasizes the data. Rather than try to fit a problem to the procedural approach of language, OOP attempts to fit the language to the problem. The idea is to design data forms that correspond to the essential features of a problem. That data forms are called "***Classes***".

The OOP approach to program design is to first design classes that accurately represent those thing with which the program deals. Then you would proceed to design a program, suing  objects of those classes. The process of going from a lower level of organization, such as classes, to a high level, such as program design, is called ***bottom-up programming***. However, top-down programming and bottom-up programming are **not contradictory**.

#### C++ and Generic Programming

Generic programming is yet another programming paradigm supported by C++. It shares with OOP the aim of making it simpler to reuse code and the technique of abstracting general concepts. But whereas OOP emphasizes the data aspect of programming, generic programming emphasizes independence from a particular data type. And its focus is different. OOP is a tool for managing large projects, whereas generic programming provides tools for performing common tasks, such as sorting data or merging lists. The term generic refers to code that is type independent. C++ data representations come in many types— integers, numbers with fractional parts, characters, strings of characters, and user-defined compound structures of several types. If, for example, you wanted to sort data of these various types, you would normally have to create a separate sorting function for each type. Generic programming involves extending the language so that you can write a function for a generic (that is, an unspecified) type once and use it for a variety of actual types. C++ templates provide a mechanism for doing that. 



### Basic syntax

***Our goal is to completely understand the code below!***

```C++
#include <iostream>
#include <typeinfo>

using namespace std;

void swap(int, int);
void swap(int*, int*);
void swapPointer(int*, int*);
void swapReference(int&, int&);

void output(int a, int b) {
    cout << "a: " << a << endl
         << "b: " << b << endl << endl;
}

int main() {
	int a, b;
    cin >> a >> b;
    
    cout << "Before swap: " << endl;
    output(a, b);
    
    swap(a, b);
    cout << "After swap(int, int): " << endl;
    output(a, b);
    
    swap(&a, &b);
    cout << "After swap(int*, int*)" << endl;
    output(a, b);
    
    swapPointer(&a, &b);
    cout << "After swapPointer(int*, int*)" << endl;
    output(a, b);
    
    swapReference(a, b);
    cout << "After swapReference(int&, int&)" << endl;
    output(a, b);
	
	return 0;
}

void swap(int a, int b) {
    int tmp = a;
    a = b;
   	b = tmp;
}

void swap(int* a, int* b) {
    auto tmp = a;
    a = b;
    b = a;
    
    cout << typeid(tmp).name() << endl;
}

void swapPointer(int* a, int*b) {
    int tmp = *a;
    *a = *b;
   	*b = tmp;
}

void swapReference(int& a, int& b) {
    auto tmp = a;
    a = b;
    b = tmp;
    
    cout << typeid(tmp).name() << endl;
}
```

- ***The C++ Preprocessor***

  ​	C++, like C, uses a ***preprocessor***. This is a program that processes a source file before the main compilation takes place.  You don’t have to do anything special to invoke this preprocessor. It automatically operates when you compile the program.

  ```cpp
  #include <iostream>		// a PREPROCESSOR directive
  ```

  ​	This directive causes the preprocessor to add the contents of the iostream file to your program. This is a typical preprocessor action: adding or replacing text in the source code before it’s compiled. In essence, the contents of the iostream file replace the `#include <iostream>` line in the program. **Your original file is not altered, but a composite file formed from your file and iostream goes on to the next stage of compilation.**

- ***header***

  | Kind of header | Convention               | Example      | Comments                                                     |
  | -------------- | ------------------------ | ------------ | ------------------------------------------------------------ |
  | C++ old style  | Ends in `.h`             | `iostream.h` | Usable by C++ programs                                       |
  | C old style    | Ends in `.h`             | `math.h`     | Usable by C and C++ programs                                 |
  | C++ new style  | No extension             | `iostream`   | Usable by C++ programs, uses `namespace std`                 |
  | Converted C    | `c` prefix, no extension | `cmath`      | Usable by C++ programs, might use non-C features, such as `namespace std` |

- ***namespace***

  ​	Namespace support is a C++ feature designed to simplify the writing of large programs and of programs that combine pre-existing code from several vendors and to help organize programs. One potential problem is that you might use two prepackaged products that both have, say, a function called `wanda()`. If you then use the `wanda()` function, the compiler won’t know which version you mean. The namespace facility lets a vendor package its wares in a unit called a ***namespace*** so that you can use the name of a namespace to indicate which vendor’s product you want. So Microflop Industries could place its definitions in a namespace called `Microflop`.Then `Microflop::wanda()` would become the full name for its wanda() function. Similarly, `Piscine::wanda()` could denote Piscine Corporation’s version of wanda(). Thus, your program could now use the namespaces to discriminate between various versions:

  ```cpp
  Microflop::wanda("go dancing?");		// use Microflop namespace version
  Piscine::wanda("a fish named Desire")	// use Piscine namespace version
  ```

  ​        The using directive like `using namespace std` makes all the names in the `std` namespace available. Modern practice regards this as a bit lazy and potentially a problem in large projects. The preferred approaches are to use the std:: qualifier or to use something called a using declaration to make just particular names available:

  ```C++
  using std::cout;
  using std::cin;
  using std::endl;
  ```

  ​        However, for me, it is more customary not to use the using directive.

  ​        In addition, the using directive can also give aliases to types:

  ```cpp
  using i64 = long long;
  ```

  ​        It is somewhat similar to ```#define LL long long```, but still different:

  - ***Scope:*** "using i64 = long long;" is the syntax for creating a type alias in C++, and its scope is limited to the current namespace or scope. On the other hand, "#define i64 long long" is a preprocessing directive in C and C++ that performs text replacement during the preprocessing phase, and its scope extends throughout the entire source file.

  - ***Type Safety:*** "using i64 = long long;" preserves type safety when creating a type alias. "i64" and "long long" are essentially the same type with just a different name. This means that when using "i64," the compiler performs type checking to ensure that only "long long" operations are allowed.

    "#define i64 long long" is a simple text replacement and lacks type checking. When using "i64," the preprocessor replaces all occurrences of "i64" with "long long" without performing type checks.

  - ***Life time:*** The type alias created with "using i64 = long long;" remains valid for the entire lifetime of the program and can be used anywhere in the code. In contrast, the text replacement performed by "#define i64 long long" is only effective within the current source file and does not affect other files.

- ***comments***

  ​	The ***double slash (//)*** introduces a C++ comment. A comment is a remark from the programmer to the reader that usually identifies a section of a program or explains some aspect of the code. The compiler ignores comments.

  - C++ also recognizes C comments, which are enclosed between /* and */ symbols:

    ```C++
    #include <iostream> /* a C-style comment */
    ```

- ***function***

  ​	Because functions are the modules from which C++ programs are built and because they are essential to C++ OOP definitions, you should become thoroughly familiar with them. Some aspects of functions are advanced topics, so the main discussion of functions comes later (maybe, it depends on whether we will explain the template to you.).
  
  ​	However, if we deal now with some basic characteristics of functions, you’ll be more at ease and more practiced with functions later.
  
  - ***function form***
  
    ```cpp
    returnType functionName(argumentList) {
    	statements;
    }
    ```
  
    If return type is `void`, that means the function returns nothing. Similarly, if the argument is `void`, then it means that the arguments are not accepted, and `foo(void)` and `foo()` have the same meaning. However, it should be noted that in C, the argumentList is empty, which means silence to accept arguments, rather than not accepting the arguments, unless explicitly declared as `foo(void)`
  
    ```cpp
    ...
    void foo() { printf("Function running\n"); }
    ...
    foo(1);
    ...
    // In C++
    error: too many arguments to function 'void foo()'
         foo(1);
    note: declared here
    void foo() { printf("Running\n"); }
    
    /* In C */
    Function running
    ```
  
  - ***function header***
  
  - ***funtion reload***
  
    



### New types

- ***type alias***

  we said before

- the ***auto*** keyword

  ​        C++11 introduces a facility that allows the compiler to deduce a type from the type of an initialization value. For this purpose it redefines the meaning of auto, a keyword dating back to C, but one hardly ever used. (We'll discuss the previous meaning of auto later, or not.) Just use auto instead of the type name in an initializing declaration, and the compiler assigns the variable the same type as that of the initializer:

  ```c++
  auto n = 100;		// n is int
  auto x = 1.5;		// x is double
  auto y = 1.3e12L;	// y is long double
  ```

  However, this automatic type deduction isn’t really intended for such simple cases. Indeed, you might even go astray. Only use when the type is obvious or when the type is annoyingly verbose to write out.

  ```c++
  #include <iostream>
  #include <string>
  #include <map>
  #include <unordered_map>
  #include <vector>
  
  int main() {
  	std::map<std::string, std::vector<std::pair<int, std::unordered_map<char, double> > > complexType;
  	
      // What does this do? We'll find out in the iterators lecture!
  	std::map<std::string, std::vector<std::pair<int, std::unordered_map<char, double> > >::iterator it = complexType.begin();;
  	
  	// vs
  	auto it = complexType.begin();
  	
  	return 0;
  }
  ```

  

- ***array***

- ***pointer***

- ***reference***

- ***struct***

- ***class***

  

  