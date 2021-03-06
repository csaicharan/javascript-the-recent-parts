# Further Destructuring
## Named Arguments
```javascript
function lookupRecord(store = "person-records", id =-1) {
    //..
}

function lookupRecord({
    store = "person-records",
    id = -1
}) {
    //...
}

lookupRecord( {id: 42} );
```
- **named arguments** are a real thing, or at least an idiomatically named thing in other languages like Scala and Obj-C but in JS we don't have a thing called _named arguments_ but by using destructuring we can accomplish the same thing.
    - By declaring a function with an object parameter of properties... 
    - We can essentially say that, the value `42` in our example above goes to the parameter: `id`
    - In effect, it's naming the argument at the callsite
    - This has become an extremely common "idiom"/pattern in JS. KS higly recommends thinking of this when designing your functions.
    - KS' rule of thumb is that if designing a function with 3 or more input, he always uses this object destructuring now. 
    - The order of JavaScript function parameters must match what we as arguments, so we must remember what order we've established our parameters.
    - Using this object-destructuring in parameter position "idiom"  allows us to get around needing to remember the specific order of our parameters
    - The downside is that you have to remember the name that function uses. KS recommends coming up with internal naming conventions for commonly used things (e.g. if it's a callback use 'cb', if an array use 'arr', if a primitive value use 'v', and then document that so your team knows these names)

## Destructuring & Restructuring
![](https://user-images.githubusercontent.com/5563119/64034339-4ab18880-cb03-11e9-9288-1e945f56e597.png)
> A quick breakdown: essentially leverages underscores .extends() function to condense/mix/merge the two object contents into a new object. The first argument is the empty object to be filled, the second argument sets the empty object with an initial set of values, and the third argument settings overwrites or adds to that now populated object.
- KS' beef with this is it's very imperative, and not clear what's happening 
    - So instead of this API driven approach, KS came up w/ a pattern he calls: _destructuring & restructuring_ 
![](https://user-images.githubusercontent.com/5563119/64054276-26719e00-cb3b-11e9-8ec2-7d6c0e8bbd68.png)
- Basically: you pass in an object of your settings, and I'm using the default algorithm to mix in any defaults where your settings are missing at any level of the declarative structure.
- Leaves us with a whole set of individual variables that we need to restructure back into the new merged object.
    - Destructuring happens at the top, then we recreate the object structure with all the new mixed in values, and that's the restructuring part.
    - Makes it very easy to see what we default to. More clearly communicates how our mixing will happen.
    - Using this function, if you just want the defaults, just call the function without any args. : `var defaults = ajaxOptions();`, if you have settings/a settings object you can pass them in like... `ajax( ajaxOptions( settings ) );`

## Destructuring Exercise
[Solo exercise attempt can be found here](https://github.com/kelasol/javascript-the-recent-parts/blob/master/exercises/destructuring/ex-first-attempt.js)   
I think something that tripped me up is `slides` the nested object. The restructuring part. I think I thought it was a sufficient to just reference slides and not necessarily explain it's constituient parts.

- When `TestCase` is defined its taking in `data` as its parameter. The argument that we pass into `data` occurs when the function is invokedand we invoke it on line 25 within handleResponse.
The argument we are passing in on line 25 is our in-parameter-position object destructuring  which is defining `data.properties` as targets and their source are the variables that are declared when we destructure in-param-pos of the `handleResponse` function (line 16-22). 
- So the reason you can't just say `slides: slides` or `slides` in the `TestCase` invocation is: **In objects, unlike arrays, since position doesn't matter, the source must be specified or it will be ignored**. This means in a destructuring pattern, all nested objects(possibly arrays) will also be "destructured" based on the provided pattern. When you say `slides` you aren't providing an intelligible pattern to destructured the slides object and because you don't specificy the sources of the slides object to be destructured: `start` and `end`, JS does not give those values assignments in the interior to the TestCase function invocation.  
 