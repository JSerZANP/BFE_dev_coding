And a video explaining it https://www.youtube.com/watch?v=1IQmEDy8JoM

```js

/**
 * @param {Function} func
 * @param {(args: any[], newArgs: any[]) => boolean} [isEqual]
 * @returns {any}
 */

function defaultIsEqual(a, b) {
  if (a.length !== b.length) return false
  return a.every((item, i) => item === b[i])
}

function memoizeOne(func, isEqual = defaultIsEqual) {
  let lastArgs = []
  let lastThis = null 
  let lastResult = null
  let isCalled = false
  
  return function (...args) {
    if ( isCalled && lastThis === this && isEqual(lastArgs, args)) {
      return lastResult
    }
    
    lastResult = func.call(this, ...args)
    lastArgs = args
    lastThis = this
    isCalled = true
    
    return lastResult
  }
}
```
