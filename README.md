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
