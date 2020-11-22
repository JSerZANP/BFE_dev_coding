And here is a video explaining it 

https://www.youtube.com/watch?v=A7I3BgsZB_s

```js

/**
 * @param {Function} func
 * @param {any[]} args
 * @returns {Function}
 */
function partial(func, ...args) {
   return function(...newArgs) {
     // merge args and newArgs, then call func
     const finalArgs = []
     const argsCopy = args.slice(0)
     while (argsCopy.length > 0) {
       const head = argsCopy.shift()
       if (head === partial.placeholder) {
         // if newArgs is now empty
         // placeholder is replaced with undefined
         // which kind of ok?
         finalArgs.push(newArgs.shift())
       } else {
         finalArgs.push(head)
       }
     }
     
     finalArgs.push(...newArgs)
     
     return func.apply(this, finalArgs)
   }
}

partial.placeholder = Symbol()
```
