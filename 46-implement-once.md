Here is a video explaining: https://www.youtube.com/watch?v=OclvmVJ51wE

```javascript
/**
 * @param {Function} func
 * @return {Function}
 */
function once(func) {
  let result = null
  let isCalled = false
  return function(...args) {
    if (isCalled) {
      return result
    }

    result = func.call(this, ...args)
    isCalled = true
    
    return result
  }
}
```
