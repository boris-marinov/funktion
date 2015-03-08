[![experimental](http://badges.github.io/stability-badges/dist/experimental.svg)](http://github.com/badges/stability-badges)

Yet another functional Javascript library, created for educational purposes. The idea here is to have absolutely the simplest implementations of all the data structures, so they can be easily grasped by everyone who is familiar with the language. 

Also I won't use types. I am using the module pattern for everything, so the values can be effectively hidded away from you.

    Work in progress. Stick around for more.


#Monads
The infamous design patterns / value containers / programmable semicolons. etc.

Maybe
-----
A container for a value that may or not be there. 

`var m = f.maybe(value)`:  Creates a new `maybe`. 
If the value is equal to *undefined* it threats the container as empty.

`m.map(funk)`: Executes the function with the `maybe`'s value as an argument, but only if the value is different from *undefined*.

`m.mjoin()`: If the value of the `maybe` is another maybe, this function flattens the two maybes, by setting the value of the external one, as the value of the internal. 

`m.chain(funk)`: Takes a function that accepts a value and returns another `maybe` and applies it to the current one (Equivalent to `m.map(funk).mjoin()`).

Maybe Tutorial
--------------
The purpose of this monad is to eliminate the need for writing `null` checks. Furthermore it also eliminates the possibility of making errors by missing null-checks.

We often have the following code:

    var val = object[property]
    
    if(val !== undefined){
    	//do something with 'val'
    }

With **maybe** this becomes:

	f.maybe(object[property]).map(function(val){
		//do something with 'val'
	})
In other words `map` is executed only if the value inside the maybe is different from *undefined*.

This is the key thing in eliminating  errors. If you have access to a value that may be undefined you can easily forget to null-check it.

	var val = object[property](object)
	val.foo()//Blows up if val is undefined    
    
If you use **maybe** you cannot access the underlying value directly, and therefore you cannot execute an action on it, if it is not there.
 
	f.maybe(object[property]).map(function(val){
		val.foo()//Code does not get called.
	})

TBC