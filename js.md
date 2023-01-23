### Things to remember in javascript:

1.  **this** usage:

    - When function is not inside object or class

            function_call (param) = function_call.call(undefined, param)

    - When function is inside object or class

            function_call (param) = function_call.call(class/object, param)

    - Arrow Functions don't have this extra hidden parameter

            (param)=>{} = function_call.call(param)

2.  Arrow functions: return automatically when no {}, but multiline functions need {} and thus return statement
3.  **Classes** do not use **function keyword** when function is defined inside them
4.  **Class** **constructor** is called constructor() and **extends** is used for **inheritence** and **super()** inside derived class constructor to pass down arguments
5.  **let** (no hoisting) **vs** **var** (hoisting: variable detected when parsing first time, so can be used even though declared later)
6.  Array methods map, reduce and filter. The callback function expects (element, index, array)
