# You-dont-know-js-summary-20 page-
This is my summary of the <a href="https://pepa.holla.cz/wp-content/uploads/2016/08/You-Don-t-Know-JS-this-Object-Prototypes.pdf">You Don't Know JS </a>book series by Kyle Simpson.
<hr> 
The book defines this as “a binding made for each function invocation based entirely on its call-site… the location in code where a function is called (not where it’s declared)”.
<br><br> 
 •If a function is called with the new keyword,<mark> this</mark> will be the resulting object<br>
 •If a function is called with .call(), this will be the object that is passed in<br>
 •If a function is called on an objet, obj.foo(), this will be the object it was called on<br>
 •If a function is called on its own, foo(), this will be either undefined (if in strict mode) or the global object (if in non-strict mode)<br>
 <br>
 <img width="334" alt="1" src="https://user-images.githubusercontent.com/123558998/223497223-e3202a2b-89ca-44fb-856f-e9158a36cd70.PNG">
<img width="317" alt="2" src="https://user-images.githubusercontent.com/123558998/223497306-fc29bdc4-6dc8-4234-b5ff-53e7c81eb5d6.PNG">
<img width="366" alt="3" src="https://user-images.githubusercontent.com/123558998/223497407-e265d48f-d7ee-4996-9def-eb0871c92a4a.PNG">
<img width="339" alt="4" src="https://user-images.githubusercontent.com/123558998/223497440-dd08974a-4b1b-46ed-a624-88906686e762.PNG">

<h1>Chapter 1</h1><a href=#> <bold>What is Scope?<bold></a> <br>
Scope is the set of rules that determines where and how a variable (identifier) can be looked-up. This look-up may be for the purposes of assigning to the variable, which is an LHS (left-hand-side) reference, or it may be for the purposes of retrieving its value, which is an RHS (right-hand-side) reference.

LHS references result from assignment operations. Scope-related assignments can occur either with the = operator or by passing arguments to (assign to) function parameters.

The JavaScript Engine first compiles code before it executes, and in so doing, it splits up statements like var a = 2; into two separate steps:

First, var a to declare it in that Scope. This is performed at the beginning, before code execution.

Later, a = 2 to look up the variable (LHS reference) and assign to it if found.

Both LHS and RHS reference look-ups start at the currently executing Scope, and if need be (that is, they don't find what they're looking for there), they work their way up the nested Scope, one scope (floor) at a time, looking for the identifier, until they get to the global (top floor) and stop, and either find it, or don't.
<hr>
<h1>Call-Site</h1>
 the
location in code where a function is called (not where it’s declared).
We must inspect the call-site to answer the question: what is this this
a reference to?
Finding the call-site is generally “go locate where a function is called
from,” but it’s not always that easy, as certain coding patterns can ob‐
scure the true call-site.
What’s important is to think about the call-stack (the stack of functions
that have been called to get us to the current moment in execution).
The call-site we care about is in the invocation before the currently
executing function.
<br>
**You must inspect the call-site and determine which of four rules ap‐
plies. We will first explain each of these four rules independently, and
then we will illustrate their order of precedence, if multiple rules could
apply to the call-site.
<br>
<h1> Binding</h1>
In JS, the context in where we invoke a function has a lot of importance</h1>
<h1>Implicit binding</h1><br>

Implicit Binding is applied when you invoke a function in an Object using the dot notation. this in such scenarios will point to the object using which the function was invoked. Or simply the object on the left side of the dot.<br>
Ex:-
function myFunction() {
    console.log(this)     
  }
 
const obj = {<br>
  someKey: 1, <br>
  myFunction: myFunction,<br>
}<br>

obj.myFunction();   
// {someKey: 1, myFunction: ƒ}
<br>
<h1>Explicit binding</h1>
In this method, you can force a function to use a certain object as its this. Explicit Binding can be applied using call(), apply(), and bind().

call(): Pass in the required object as the first parameter during the function call. The actual parameters are passed after the object.

apply(): Similar to call() with a difference in the way the actual arguments are passed. Here, the actual arguments are passed as an array.<br>
<img width="376" alt="6" src="https://user-images.githubusercontent.com/123558998/223499635-27f88dd7-8957-41f4-9484-15d5189368c0.PNG">
<h1> Let's talk about Hard Binding in JavaScript</h1>

 with the built-in utility bind(..) You need to pass an object to bind(object) and it returns a new function that is hardcoded to call the original function with this context set as you want. The new function is permanently bound to the first argument of bind , regardless of how the function is being used.
