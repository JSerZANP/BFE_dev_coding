And a video explaining this https://www.youtube.com/watch?v=ewPyXZdCQHE

```js

/**
 * @param {Function} func
 * @param {number} delay
 * @param {number} period
 * @return {number}
 */
// wrap up the logic 
const myIntervalInstance = (() => {
  // map the initial timer to the ongoing timer
  const map = new Map()
  
  function setInterval(func, delay, period) {
    let count = 0
    
    // initial timer
    const id = setTimeout(() => run(), delay + period * count++)
        
    const run = () => {
      func()
      // create next timer
      const nextId = setTimeout(run, delay + period * count++)
      map.set(id, nextId)
    }
    
    return id
  }
  
  function clearInterval(id) {
    window.clearTimeout(id)
    // clear both the intial and ongoing timer
    if (map.has(id)) {
      window.clearTimeout(map.get(id))
      map.delete(id)
    }
  }
  
  return {
    setInterval,
    clearInterval
  }
})()
      
function mySetInterval(func, delay, period) {
  return myIntervalInstance.setInterval(func, delay, period)
}

/**
 * @param { number } id
 */
function myClearInterval(id) {
  myIntervalInstance.clearInterval(id)
}
```
