
```js

/**
 * @param {Function} func
 */
function curry(func) {
  return function curried(...args) {
    // 1. if enough args(need to filter out the placeholder), call func 
    // 2. if not enough, bind the args and wait for new one
    
    // _,_,_,1,2
    const expectedArgLength = func.length
    const isArgsEnough = args.length >= expectedArgLength &&
          args.slice(0, expectedArgLength).every(arg => arg !== curry.placeholder)
    
    if (isArgsEnough) {
      return func.apply(this, args)
    } else {
      // _,_,_,1,2,2,2,2,
      // 3,_
      // if bind _,_,_,1,2,3,_  X 
      // we want 3,_,_,1,2
      return function(...newArgs) {
        // we need merge two args,  newArgs, args
        const finalArgs = []
        let i = 0
        let j = 0
        while (i < args.length && j < newArgs.length) {
          if (args[i] === curry.placeholder) {
            finalArgs.push(newArgs[j])
            i += 1
            j += 1
          } else {
            finalArgs.push(args[i])
            i += 1
          }
        }
        
        while (i < args.length) {
          finalArgs.push(args[i])
          i += 1
        }
        
        while (j < newArgs.length) {
          finalArgs.push(newArgs[j])
          j += 1
        }
        
        return curried(...finalArgs)
      }
    }
  }
}

curry.placeholder = Symbol()
```

Also I recored a video explaining this. 

https://www.youtube.com/watch?v=zfu-WBlaWPQ 

hope it helps
