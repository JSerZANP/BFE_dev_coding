here is a video of me explaining it : https://www.youtube.com/watch?v=zHQmtt_YIzc


```javascript

/**
 * @param {Function} func
 * @param {number} wait
 * @param {boolean} option.leading
 * @param {boolean} option.trailing
 */
function debounce(func, wait, option = {leading: false, trailing: true}) {
  let timer = null

  return function(...args) {

    let isInvoked = false
    // if not cooling down and leading is true, invoke it right away
    if (timer === null && option.leading) {
      func.call(this, ...args)
      isInvoked = true
    }

    // no matter what, timer needs to be reset
    window.clearTimeout(timer)
    timer = window.setTimeout(() => {
      if (option.trailing && !isInvoked) {
        func.call(this, ...args)
      }

      timer = null
    }, wait)
  }
}
```
