### Pointers and Arrays in C

#### Basic Concepts

Object is used below to denote arbitrary datatype

- Pointers are different implementation whereas Arrays are different implementation in C

- A **pointer** contains two pieces of information:

  - An **address**
  - **Size** of object(datatype) it is pointing

- Decaying of pointer is basically:

  - before decay type of pointer(array name): `char (*) p[]` - means pointer to array of character
  - after decay type of pointer(array name): `char * p` - means pointer to character

- **Array** name **decays into pointer** to first element **except** in some conditions, like:

  - `&` is used: &arr (this is still a pointer pointing to address of first element but size of object is equal to array)
  - `sizeof` is used: sizeof(arr)

- **2D Arrays are not implemented in C.** Then how are we able to use them? So what happens when you use 2D array is this:

  - `arr[][]`: denotes arr is a 1D array, but of what? Look at this: arr[]([]) . It is a 1D array of 1D arrays.

  So if we can use 2D array, then why are they are said to be not implemented? Take the following example:

  1. `char **` : This is basically a pointer to pointer to char
  2. `char [][]` : This is an array of array of char

  - - before decay type of pointer(array name): **char (\*) p[][]** - means pointer to array of array of character
    - after decay type of pointer(array name): **char \* p[]** - means pointer to array
  - - If 2D arrays would have been implemented correctly then technically 2. should decay to 1.

- **One cannot declare array of unknown size of arrays of char of unknown size.**  
  **That is arr[][] is illegal, whereas arr[N][M] is legal.**

- **This is the reason one cannot pass array of array of char to a function.**

#### How to read type Decalarations in C

- Basically how to read this:

        char *(*(**foo[][8])())[]

- There are basic types in C like int, float, char, etc.
- The "basic types" are augmented with "derived types", and C has three of them:

- - `*` : pointer to...
  - `[]` : array of...
  - `()` : function returning...

- The rule for reading type decalarations is:
- - Always start with the variable name:

        foo is ...

  - and always end with the basic type:

        foo is ... int

  - The "filling in the middle" part is usually the trickier part, but it can be summarize with this rule:

        "go right when you can, go left when you must"

- This way our example becomes:

        char *(*(**foo[][8])())[]

  **foo is** array of array of 8 pointer to pointer to function returning pointer to array of pointer to **char**

- #### Next Read about rvalues and lvalues

### Links:

- [Reading C type declarations: Steve Friedl's Unixwiz.net Tech Tips ](http://unixwiz.net/techtips/reading-cdecl.html)
- [Doesn't a 2D array decay to pointer to pointer](https://stackoverflow.com/a/22987227)
- [What is array to pointer decay?](https://stackoverflow.com/a/1461449)
- [What the memory difference between char \*array and char array?](https://stackoverflow.com/a/67865815)
- [How to pass 2D array (matrix) in a function in C?](https://stackoverflow.com/a/3912959)
