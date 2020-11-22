and a video explaining it  https://www.youtube.com/watch?v=CzC1wwNKecY

```js
/**
 * @param {Function} func
 * @param {(args:[]) => string }  [resolver] - cache key generator
 */
function memo(func, resolver) {
  // Map<key, Map<this, result>>
  const cache = new Map()
  
  return function(...args) {
    const key = resolver ? resolver(...args) : args.join('_')
    // shall we check the `this` keyword?
    const cachedResults = cache.get(key)
    
    if (cachedResults?.has(this)) {
      return cachedResults.get(this)
    }
    
    const result = func.call(this, ...args)
    if (!cachedResults) {
      cache.set(key, new Map([[this, result]]))
    } else {
      cachedResults.set(this, result)
    }
    
    return result
  }
}
```
