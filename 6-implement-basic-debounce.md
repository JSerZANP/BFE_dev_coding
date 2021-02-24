Here is a video explaining it : https://www.youtube.com/watch?v=TkQAm2MCtks

```javascript

/**
 * @param {Function} func
 * @param {number} wait
 */
function debounce(func, wait) {
  let timer = null
  return function(...args) {
    window.clearTimeout(timer)
    timer = window.setTimeout(() => {
      func.call(this, ...args)
    }, wait)
  }
}
```
