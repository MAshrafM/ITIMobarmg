# ITI Web Development Track  
[Youtube Playlist](https://www.youtube.com/user/mido330664/videos?sort=da&view=0&flow=grid)  
[Facebook Page](https://www.facebook.com/mobarmgofficial/)

## JavaScript Track
- L01: JS Introduction  
> History, Functional/OOP programming, Loose typing, dynamic/static language, lambda  
---
- L02: JS types (Numbers)  
> - JS types: [Number, String, Boolean, Null, Undefined, Object]  
> - Numbers  
64-bit floating point  
IEEE-754 (aka 'Double')  
> - NaN  
> special number; does not equal anything, including NaN, NaN === NaN is false.  
> - Convert a value to a number: [Number, +, parseInt]  
> - parseInt(str, radix)  
> For empty string return NaN unlike Number which will return 0  
> If first character is a digit it reads till a non digit character and return the number of the digits  
> **Always specify the radix**: radix is integer between 2-36.  
> - Associative Law does not hold   
> (a+b)+c === a+(b+c) false for some values of a,b,c; this because of the double. Integers above 9 quadrillion || decimal fractions.  
> In case of decimal fraction it is better to use a tolerance value   
>   ```javascript
>   Math.abs(exp1 - exp2) < tolerance  
---  
- L03: JS types (Numbers, Strings)  
> - Numbers Methods: [toExponential, toFixed, toLocaleString, toPrecision, toString, valueOf]
> - Numbers Constants: [MAX_VALUE, MIN_VALUE, NEGATIVE_INFINITY, NaN, POSITIVE_INFINITY]
> - Math: [abs, floor, log, max, pow, random, sin, sqrt]
> - Math Constants: [E, LN10, LN2, LOG10E, LOG2E, PI, SQRT_2, SQRT2]
> - Number is a first class object: {stored in a variable, passed as a parameter, returned from a function, store in an object}
> - Extending Number type  
> ```javascript 
> // check if method exists already or not 
> if(!Number.prototype.hasOwnProperty('isEqual')){
>   // define the new method
>   Number.prototype.isEqual = function(x){
>     return Math.abs(this - x) < 1e-10
>   }
> }
> ```
> - Strings  
>  16-bit characters  
>  UCS-2 not quite UTF-16  
>  No seperate characters type  
>  They are immutable  
>  Similar Strings are equal (===)  
---  
- L04: JS types (String, Objects)
> - String Methods:  
>  [charAt(index), charCodeAt(index), concat, split, indexOf, lastIndexOf, search(regexp), substring, slice, match(regexp), toLowerCase, toUpperCase, replace, trim]  
> - Objects: Arrays  
>  it inherits from objects.  
>  indexes are converted to strings and used as name fir retrieving values.  
>  no performance gained from being an array, because it is an object.  
>  No need to provide a length or type when creating an array.  
> - Array Literals  
>  [] equals to new Array()  
>  can append new items arr[arr.length] = 'sth';  
>  dot notation should not be used with arrays.  
>  delete array[index]; removes the element but leaves a hole in the numbering.  
>  array.splice(index, 1); removes the element and renumbers the following elements.  
> - Array Methods:  
>  [concat, join, pop, push, reverse, shift, slice, sort, splice, toLocaleString, toString, unshift, indexOf, lastIndexOf, every, some, forEach, map, filter, reduce, reduceRight, isArray]  
>  Do not use sort as sort algorithm; it converts elements to string and sort by chars; ex: 2, 24, 4 , 50 to 2,24, 4, 50.  
> - null: value that is not anything  
> - undefined: default value for vars and params  
---  
- L05: JS types (Objects - functions)
> - functions expressions  
>  are first class objects  
>  optional name  
>  parameters (wrapped in parens, zero or more, seperated by commas )   
>  body (wrapped in curly braces, zero or more )
>   ```javascript
>   // ex: 
>   var f = function foo(){
>   }
>   (function foo(){
>   })
>    !function foo(){
>   }
>   ```
> - functions statement  
>  mandatory name  
>  parameters (wrapped in parens, zero or more, seperated by commas )   
>  body (wrapped in curly braces, zero or more )  
>  It is just a short hand for a var statement with a function value 
>   ```javascript
>   function foo(){
>   }
>   ```
> - Scope: Block scope V function scope  
> - return statement
>  if there is no expression then the return value is undefined, except for constructors its return is (this).  
> - function arguments[], don't swap arguments
>   ```javascript
>   // same are Array.reduce
>   function sum(){
>     var i,
>         n = arguments.length,
>         total = 0;
>     for(i = 0; i < n; i++){
>       total += arguments[i];
>     }
>     return total;
>   }
>   var ten = sum (1,2,3,4);
>   ```
> - this  
>  this parameter contains a reference to the object of invocation  
>  allow single function object to service many functions  
>  is key to prototypal inheritance  
>  Its value depends on the calling form.  
>  Is bound at invocation time  
> - Invocation (function form, method form, constructor form, apply form)  
>  Function form; functionObject(arguments)  
>  Method form; thisObject.methodName(arguments)  
>  Apply form; functionObject.apply(thisObject, argsArray)  
---  
- L06: Closure
> The context of an inner function includes the scope of the outer function.  
> An inner function enjoys that context even after the parent functions have returned.  
> Closure is when a function is able to remember and access its lexical scope even when that function is executing outside its lexical scope.  
> ```javascript
> var digit_name = (function(n){  
>   var names = ['zero', 'one', 'two', 'three', 'four', 'five', 'six', 'seven', 'eight', 'nine'];  
>   return function(n){
>     return names[n];
>   };
> }());
> var str = digit_name(3); //three
> ```

> ```javascript
> function add_ten_inputs(){
> 	var i;
> 	for(i = 0; i < 10; i++){
> 		var btn = document.createElement('input');
> 		btn.value = 'input' + i;
> 		/* This is Wrong, wont work fine
> 		btn.onclick = alert('input' + i);
> 		this will always return 10
>		*/
> 		btn.onclick = (function(n){
> 			return function(){
> 				alert('input' + n);
> 			};
> 		}(i));
>		window.document.body.appendChild(btn);
>	}
> }
> add_ten_inputs();
> ```
---
- L07: JS types (boolean)
> passing by values; with primitive pass copy of the value itself, with objects passing copy of reference  
> - Boolean(value)  
>  return true if the value is truthy  
>  return false if the value is falsy  
> - Falsy values:  
>  false  
>  null  
>  undefined  
>  "" (empty string)  
>  0, +0, -0  
>  NaN  
>  All other values consider truthy even "0", "false"  
> - The Equals Operator (==)
>  if they are primitive values then compare the values.  
>  else(Object) then compare the reference.  
>  if one of them is null return false; else convert to numbers and compare.  
>  Exceptions: NaN == NaN (false) | Null == undefined (true)  
> - The Strict Equals Operator (===)  
>  Different types return false.  
>  same types: if they are primitive then compare values; else compare the reference.  
>  Exceptions: NaN === NaN (false)  
> - Not Equal Operators  
>  A != B // !(A==B)  
>  A !==B // !(A===B)  
> - &&  
>  The guard operator
>  if the first operand is truthy then the result is the second operand, else result is the first operand.  
> - ||  
>  the default operator  
>  if the first operand is truthy then result  is first operand else result is second operand.  
> - to check type use: Object.prototype.toString.call(x) instead of typeof x;  
> - Throw statement
>  throw new Error(msg);  
>  throw{ name: exception Name, message: msg};  
> - Try statement  
>  only one catch as all the error as of type object.  
>  try{...} catch(e){ switch(e.name){}}  
---
- L08: Throw Exception / Handling Tech. Ex.
> ```javascript
> // module
> (function(){
>  var add = function(x, y){
>    if(Object.prototype.toString.call(x) !== '[object Number]'){
>      throw{
>        name: 'Invalid Argument',
>        message: 'Please provide a number for x'
>      };
>    }
>    if(Object.prototype.toString.call(y) !== '[object Number]'){
>      throw{
>       name: 'Invalid Argument',
>        message: 'Please provide a number for y'
>      };
>    }
>    return x + y;
>  };
>  
>  // expose namespace
>  window.itworx = window.itworx || {};
>  window.itworx.math = window.itworx.math || {};
>  window.itworx.math.add = add;
> }());
>```
---
- L09: JS types (object)  
> An object is a dynamic collection of properties. Every property has a key string that is unique within that object.  
> - Get, Set, Delete  
>  Dot notation (only works for valid identifiers)|| Subscript notation.  
>  obj.propName || obj['propName']  
>  obj.propName = value
>  delete obj.propName  
> - Object Literals  
>  var myObj = {name: 'js', age: 12, grade: 'A'}  
> - Inheritance (Classes Vs Prototypes)    
---  
- L10: DOM
> - Document Tree Structure  
>  document.body
>  firstChild, lastChild, nextSibling, previousSibling  
>  childNodes
> - Walk The Dom (DFS)  
> ```javascript
> function walkTheDom(node, func){
>   func(node);
>   node = node.firstChild;
>   while(node){
>     walkTheDom(node, func);
>     node = node.nextSibling;
>   }
> }
> ```
> - getElementsByClassName
> ```javascript
> function getElementsByClassName(className){
>   var results = [];
>   walkTheDom(document.body, function(node){
>     var arr, c = node.className, i;
>     if(c){
>       arr = c.split(' ');
>       for(i = 0; i < arr.length; i+= 1){
>         if(arr[i] === className){
>           results.push(node);
>           break;
>         }
>       }
>     }
>   });
>   return results;
>}  
>```  
> - Retrieving Nodes  
>  document.getElementById(id)  
>  document.getElementsByName(name)  
>  node.getElementsByTagName(tagName)  
>  document.querySelectorAll(cssSelector)  
>  
> - Retrieving Nodes Using JQuery  
>  $('selector') by [TagName, Id, class, Mix]  
>  Attributes Selectors:  *$('[title]')*, *$('a[title]')*, *$('a[title \*= amazing]')*, *$('a[title ^= my]')*, *$('a[title $= my]')*, *$('a[id][title $= my]')*  
>  Form Selectors: *$(':input')*, *$(':checkbox')* ie. this is faster *$('input[type="checkbox"]')*; if the selector started with : then the universal selector is implied; *$(':checked')* works for radio, checkboxes; *$(':selected')* works for select; *$(':enabled')* enable property true same for disabled; *$(':hidden')*.  
> - Element is considered hidden if: they have a CSS display value of none, They are form elements with type hidden, Their width and height are explicitly set to 0.  
> - Hirarchy  
>  ("parent > child") direct children.  
>  ("ancestor descendant") select descendant of a given ancestor.  
>  ("prev + next") select all "next" elements matching next that are immediately preceded by a sibling "prev".  
> - Child Filter: *$(':first-child')*, *$(':last-child')*, *$(':nth-child(index/even/odd/equation)')*.  
>  - Resulted element at Index: *$(':first')*, *$(':last')*, *$(':odd')*, *$(':even')*, *$(':eq(#)')*, *$(':lt(#)')*, *$(':gt(#)')*.  
> - Others: *$(':animated')*, *$(':root')* the html element itself, *$(':focused')* using document.activeElement is better.  
> - Filteration Methods: $(selector). first()/last()/eq(index)/siblings()/next()/nextAll()/nextUntil('selectorToStopAt')/prev()/prevAll()/prevUntil(selectorToStopAt)/children()/parent()/Parents() - all parents till the html element/closest(selector)/filter(selector)/find(selector)- search in the descendants to match the selector/end() - works with find.  
>  Use filter for non pure selectors ie *$('div input').filter(':radio');*  
>  Be specific on the right, light on the left  
>  Be more specific, better to descend from an id  
>  Do not be over-specific.  
> - DOM Manipulation  
>  Manipulating Attributes  
>  Memory Leaks  
---  
- L11: Events  
> The browser has an event-driven, single-threaded, asynchronous programming model.  
> Mouse and Keyboard Events are targeted to particular nodes.  
> Events cause the invocation of event handler functions.  
> - Mouse Events  
>  The target is the topmost (z-index) node containing the cursor.  
>  [click, dbclick, mousedown, mousemove, mouseout, mouseover, mouseup]  
> - Input Events  
>  The target is the node having focus.  
>  [blur, change, focus, keydown, keypress, keyup, reset, submit]  
> - Event Handlers.  
>  *node.addEventListener(type, f, false);*  
> - Capturing and Bubbling  
>  Bubbling means that the event is given to the target, and then its parent, and then its parent, and so on until the event is canceled.  
>  Cancel Bubbling to keep the parent nodes from seeing the event.  *e.stopPropagation()*  
>  Prevent Default Action to prevent browser action associated with the event. *e.preventDefault()*  
---
- L12: Events example  
> ```javascript
> document.getElementById('grandparent')
>   .addEventListener('click', function(e){
>     e = e || event;
>     var target = e.srcElement || e.target;
>     alert(target.id);
>   }, false);
> ```
---  
- L13: Promises And Deferred *No Audio*  
> ```javascript
> $('input[type="button"]').on('click', function(){
>   $.ajax({
>     url: '/Math/Add?x=' + $('#num1').val() + '&y=' + $('#num2').val(),
>     method: 'PUT',
>     contentType: 'application/json',
>     data: JSON.stringify({x : $('#num1').val(), y: $('#num2').val()}),
>     cache: false
>   }).done(function(result){
>     alert(result);
>   }).fail(function(response){
>     alert(response);
>   });
> });
> ```
---
- L14: Promises And Deferred  
> ```javascript
> var adder = function(){
>   var result = 0,
>       i;
>   for(i=0; i< arguments.length; i++){
>     result += Number(arguments[i]);
>   }
>   return result;
> }
> 
> var alerter = $.Deferred();
> setTimeout(function(){
>   var result = adder(2, 4, 2);
>   alerter.resolve(result);
>   alerter.reject('can\'t add');
> }, 5000);
>
> alerter
>   .done(function(x){
>     alert(x + 'in done');
>   }).fail(function(x){
>     alert(x + 'in fail');
>   }).always(function(x){
>     alert(x + 'in always');
>   });
>
> alert('here');
> ```
> Refactor
> ```javascript
> // dataLayer
> (function(){
>  var add = function(){
>    var result = 0,
>        i;
>    for(i = 0; arguments.length; i++){
>      result += Number(arguments[i]);
>    }
>    return result;
>  },
>  
>  dataLayer = {
>    myAdd: function(x, y){
>      var def = $.Deferred();
>      
>      setTimeout(function(){
>        def.resolve(add(x,y));
>      }, 5000);
>     
>      return def.promise();
>    }
>  };
>  
>  window.dataLayer = dataLayer;
>}());
>
>// Service Layer
>(function(dlayer){
>  var serviceLayer = {
>   add: function(x, y){
>      return dlayer.myAdd(x, y)
>          .done(function(m){
>            alert('service layer: ' + m)
>          });
>    }
>  }
>  
>  window.serviceLayer = serviceLayer;
>}(window.dataLayer)
> ```
---
- L15: SPA
> Web API 
> MoviesSPA/Controllers/MoviesController.cs
> ```cs
> using System;
> using System.Collections.Generic;
> using System.Linq;
> using System.Web;
> using System.Web.Http;
> 
> namespace MoviesSPA.Controllers
> {
>     public class MoviesController : ApiController
>     {
>         [HttpGet]
>         public IEnumerable<Movie> Get(int startIndex, int pageSize, string sorting)
>         {
>             var movies = AddOrderBy(MoviesDb, sorting);
>             movies.Skip(startIndex).Take(pageSize).ToList();
>             return movies;
>         }
>         [HttpPut]
>         public void Add(Movie movie)
>        {
>             movie.Id = MoviesDb.Max(m => m.Id) + 1;
>             MoviesDb.Add(movie);
>         }
>         [HttpDelete]
>         public void Remove(int id)
>         {
>             MoviesDb.RemoveAll(m => m.Id == id);
>         }
>         [HttpPost]
>         public void Modify(Movie movie)
>         {
>             MoviesDb.RemoveAll(m => m.Id == movie.Id);
>             MoviesDb.Add(movie);
>         }
> 
> 
>         private IEnumerable<Movie> AddOrderBy(IEnumerable<Movie> MoviesDb, string sorting)
>         {
>             if (string.IsNullOrWhiteSpace(sorting)) return MoviesDb;
>             var sortFieldAndOrder = sorting.Split(' ');
>             var sortField = sortFieldAndOrder[0];
>             var sortOrder = sortFieldAndOrder[1];
> 
>             switch (sortField)
>             {
>                 case "Id":
>                     return sortOrder == "ASC" ? MoviesDb.OrderBy(m => m.Id) : MoviesDb.OrderByDescending(m => m.Id);
>                 case "Title":
>                     return sortOrder == "ASC" ? MoviesDb.OrderBy(m => m.Title) : MoviesDb.OrderByDescending(m => m.Title);
>                 case "Rate":
>                     return sortOrder == "ASC" ? MoviesDb.OrderBy(m => m.Rate) : MoviesDb.OrderByDescending(m => m.Rate);
>                 case "Remarks":
>                     return sortOrder == "ASC" ? MoviesDb.OrderBy(m => m.Remarks) : MoviesDb.OrderByDescending(m => m.Remarks);
>                 default:
>                     return MoviesDb;
>             }
>         }
> 
>         private readonly static List<Movie> MoviesDb = new List<Movie>{
>             new Movie{Id = 1, Title = "Gone Girl", Rate = 85},
>             new Movie{Id = 2, Title = "The Dark Knight", Rate = 90},
>             new Movie{Id = 3, Title = "Lord of The Rings", Rate = 95},
>             new Movie{Id = 4, Title = "The Last Kingdom", Rate = 80},
>             new Movie{Id = 5, Title = "I Am Legend", Rate = 84},
>             new Movie{Id = 6, Title = "Resident Evil", Rate = 81},
>             new Movie{Id = 7, Title = "Cabin In The Woods", Rate = 89},
>             new Movie{Id = 8, Title = "Paranormal Activity", Rate = 70},
>             new Movie{Id = 9, Title = "Saw", Rate = 86},
>         };
>     }
> 
>     public class Movie
>     {
>         public int Id { get; set; }
>         public string Title { get; set; }
>         public int Rate { get; set; }
>         public string Remarks { get; set; }
>      }
> }
> ```
---
