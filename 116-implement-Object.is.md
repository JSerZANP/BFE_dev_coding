And a video explaining this : https://www.youtube.com/watch?v=0xroW_lkMos

```js

/**
 * @param {any} a
 * @param {any} b
 * @return {boolean}
 */
function is(a, b) {
  if (typeof a === 'number' && typeof b === 'number') {
    if (Number.isNaN(a) && Number.isNaN(b)) {
      return true
    }
    
    if (a === 0 && b === 0 && 1 / a !== 1 / b) {
      return false
    }
  }
  
  return a === b
}
```
