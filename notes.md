## Namaste Javascript Season 1

# Execution context

Everything in javascript happens inside an Execution context

-> Execution context is like a big box which has 2 things.
1. Memory space (Variable environment)
2. Code space (Thread of execution)

-> In Variable environment, all the function and data stores as key value component
-> In Thread of execution, code is executed one by one
-> Javascript is a synchronous single threaded language
-> That means it can execute one command at a time in a specific manner

# How the js code will run

-> First the global execution context is created
-> First step is memory creation
-> Code execution phase
-> For the variables it stores the spatial value of the variables (UNDEFINED)
-> For functions, it stores the whole function

-> In second phase, it starts executing the code line by line

# Function execution

-> Whenever a function is called, a new execution context is created for that function.
-> Again memory allocation and code execution happens for that

# Call stack
JS engine maintains call stack which handles all these execution context

CALL_STACK = [ GLOBAL_EXECUTION_CONTEXT, FUNCTION_1, FUNCTION_1_INNER.... ]


# Hoisting

-> Functions and variables with var keywords hoists on the top before going to code execution part of the execution context

# Variable environment
-> any new function will have it's own execution context and variables and memory
-> For any variable, it checks first in the local scope, if it doesn't find it, it checks in the previous scope
-> Once the function execution is done, it's execution context gets removed from the call stack

# window 
-> JS engine creates some functions and variables in global execution context (alert, setTimeout...)
-> This keyword can be used to access this global object
-> in case of chrome, it's called window object
-> Anything which is not inside any function is in global object

# undefined vs not defined

-> Undefined means the space is allocated to the variable but no value has been assigned.
-> not defined is when there is no memory for the variable
-> Undefined is just a placeholder


=> Javascript is a loosely types language


## Scope in Javascript

-> Scope in javascript is related to it's lexical environment
-> Scope means where you can access any particular variables
-> whenever an execution context is created, a lexical environment is also created;
-> Lexical environment is the local memory + Lexical environment of parent


## Temporal dead zone

-> Let and const declarations are hoisted but they are in temporal dead zone till their value has been assigned
-> Let and const variable has been allocated memory but not stored in global object, in temporal dead zone
-> Temporal dead zone is the time between the let/const variable's memory has been created to assigning any value
-> Even after assigning, let and const variables are not stored in global memory
-> Hence, you cannot access them using this.[name]

-> in the same scope, you cannot reinitialize let/const variable
-> const variable is meant to be initialize at declaration only


## Block in Javascript

-> { ......  }
-> Also known as compound statement
-> It is used to combine multiple statements together
-> Like if(true) false is one statement, to use multiple statements instead of false we use {}
-> Let/const exist only in block scope

## Shadowing in Javascript

-> In block scope, variable shadows the outer global variable
-> Illegal shadowing is when a var tries to shadow a let global variable


### Closures

-> Closure basically means a function bundled with lexical scope is called closure
-> Like a function will have access to it's local variable. Along with that, it will have access to it's parent's lexical scope
-> You can assign a function to a variable, return a function as well as pass as parameter to another function as well
# use
-> Module design pattern
-> Currying
-> Function like once
-> memoize
-> Maintaining state in async world
-> setTimeouts
-> Iterators

## SetTimeout

-> set timeout just stores the function that has to be executed in some other place and attaches the timer
-> Once the code execution is done, it checks that place and that start executing the functions
-> These functions will have closure with it's environment


## Issues with closures

-> Sometimes it can increase the memory consumptions
-> If not garbage collected properly, it might lead to memory fail
-> JS is a high level programming language, most of the work like how you store a variable or frees the memory when the variable is not needed, is done by garbage collector



## Function statement ->

function a(){
    ...
}

## function expression ->

let a = function(){
    ...
}

## Function declaration ->
Function statement only

## anonymous functions

(function(){
...
})()

## Parameters vs Arguments

function abc (param1, param2,...){

}

abc(argument1, argument2....)

## First class function

Since we can even pass functions as argument in any function call,
Also we can return a function from a function
it's called first class function


## Callback function

Since functions are first class function, when a function returns a function, it's called callback function

-> JS is single threaded and synchronous language but these callback function provides asynchronoucity
-> setTImeout takes 2 things, callback function and a time

## webapis 
setTimeout, dom APIS like document.,,, localstorage, fetch is a part of browser web APIs which JS code can consume
We can use it from window object

## Event loops

Whenever we have any callback functions, it goes to the callback queue (after the timer and all)
Event loop keeps checking the callback queue and if anything is there, it pushes to the call stack

## microtask Queue
-> There is something called microtask Queue
-> It is similar to the callback queue
-> It holds more priority over callback queue
-> Promises, Mutation observer goes to the microtask queue

## Callback starvation
-> Since microtask has more priority over callback queue, if there are a lot of microtask queue items, it will starve callback

## JIT compilation

-> JS engine handles to use interpreter or compilation

## SetTimeout has trust issues


## Functional programming

## Array prototypal inheritence

Array.prototype.something = function (params){

}

## Callback hell

When a callback function calls again another call back

Inversion of control


## Promises
promise is just an object where data will get filled later


## Apply, Call and Bind

-> every object has a method called this
-> Using call, we can call a function and provide a new context to that
-> This is called function borrowing

-> Apply is just call but the way we provide arguments is different
-> CALL -> (param1, param2, param3)
-> Apply -> ([param1,param2,param3])
-> Using bind, we can update the context of the function


-> Call and Apply invokes the method but Bind gives you a copy of the function

## Polyfills

-> If your browser doesn't have some functions, you want to add that then you can create your own polyfills
-> It's basically inhereting prototype


## Function currying


## Async and Defer attributes

-> In normal, default case -> HTML parsing stops when encountered a script, fetches that, then continue HTML parsing
-> Async -> HTML parsing continues till we get the script, then it stops HTML parsing and execute the script 
once script is executed, it continues with HTML parsing
-> Defer -> HTML parsing goes on, script also gets fetched. Once HTML parsing is done, it runs script


## Event bubbling and Capturing/Trickling

-> Event propogation from child -> Parent -> Grand parent is called Event bubbling
-> Event propogation from Grand parent -> Parent -> child is called event capturing

-> It is upto developer to decide what to use.
-> addEventHandler('click',function,useCapture)
-> useCapture is default false

-> Capturing happens first, then bubbling

## Event delegation 

-> Instead of attaching an event handler to each and every elements, we can attach the event listener to the parent 


## Prototypal Inheritance

-> Whenever we create any variable, function or array, it gets the access of a lot of different methods and properties.
-> This comes because of prototypical inheritance.
-> JS attaches an object to these variables which has these properties
-> Everything in Javascript is nothing but an object.
-> Everything is inherited from Object.

## CORS error

-> If two web apps have the same origin, they can share resources.
-> If they don't have same origin, they have to request that
-> Before the actual API call, a preflight call -> in return we get options call happens with headers.


## Debouncing vs Throttling

-> Both are used to optimise the web performance by limiting a function call
-> Search bar -> Debouncing
-> Button click to download -> Throttling

1. Debouncing
-> Only if difference between 2 events is greater than delay, make function call

2. Throttling
-> After the first event call, ignore all event till the delay time.



## Reflow and Repaint

-> Reflow and Repaint are two important concepts of browser rendering process.
-> Reflow is a process of browser recalculating the layout and position of the elements of the page.
-> Repaint is a process of redrawing the elements on the page

## Browser rendering process

1. HTML parsing and style calculations
-> Browser parses HTML into DOM and CSS to CSSDOM and merges DOM and CSS DOM into render tree

2. Layout
-> Render tree contains node for each elements and each node has the css property but that's not enough to render the page.
-> Browser creates a Layout tree which keeps the information of size and position of each node

3. Paint
-> After getting render tree and layout tree, browser need to finalize the order in which it will paint the elements.

4. Compositing
-> After getting render tree, layout tree and order of painting, in order to optimise the rendering, browser composite the information through compositing and then renders on the screen. 


-> Reflow happens when anything in the layout tree has been changed. Like position, width and height
-> Repaint happens when property of node from render tree got changes like visibility, bg color


## Micro task queue and Macro task queue

-> Micro task queue is higher priority queue -> Promises
-> Macro task queue or just Task queue is lower priority queue -> SetTimeInterval

## Promises

-> Promise is an object that represents eventual completion of an async operation.

-> .then and .catch methods are there
-> Resolve() and Reject() are the functions to call them
-> Handle the errors gracefully
-> Promise chaining
-> While chaining, all the promise's error will be catched in one catch block only
-> If you don't want that, add catch block right after then


## Async / Await

-> Async is a keyword that's used infront of a function to make it an async function
-> Async function always return a promise
-> Either we can return a promise, or the function itself wrap the value we return inside a promise and return that

-> Async / Await combination is something we use to handle promises
-> You will add await infront of a promise that you need to resolve. This would give you a resolved value
-> Await is keyword that can only be used inside an async function


-> Major difference between handling promises using normal way and Async/await way is, in normal way JS engine won't wait the promise to resolve, but in Async/Await, it will wait for it.

-> !! Important
-> In reality, JS engine doesn't wait for it, it suspends the function and remove it from the call stack.
-> When any new promise get's resolved, it then again pushes it to call stack and start execution where it left last time
-> To handle error in Async/Await, we have to wrap it inside a try/catch block
-> Or you can also use .then 


## Promises methods

1. Promise.all(Iterable....)
-> Takes an iterable and resolve when all the promises gets resolved
-> If any of the promises gets rejected, it will throw an error

2. Promise.allSettled(Iterable...)
-> It will give result the same response as .all but in case any of them gets rejected, it will still give the response

3. Promise.race(iterable...)
-> As soon as one of them gets completed, it will give you the value
-> Doesn't matter weather it will gets resolved or rejected.

4. Promise.any(Iterable...)
-> Very much like race
-> But gives you the first resolved (success) promise
-> In case of all fails -> It will give you aggregate errors
