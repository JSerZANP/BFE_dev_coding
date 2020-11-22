And a video explaining it https://www.youtube.com/watch?v=KjoJNLQ-WDY

```js
/**
 * @param { any[] } arr
 * @returns { ? }
 */
function wrap(arr) {
  // your code here
  return new Proxy(arr, {
    get(target, prop) {
      // if used ast iterable
      if (prop === Symbol.iterator) {
         return target[prop].bind(target)
      }
      
      let index = parseInt(prop, 10) 
      if (index < 0) {
        index += arr.length
        return target[index]
      }
      return target[prop]
    }, 
    set(target, prop, value) {
      let index = parseInt(prop, 10) 
      if (index < 0) {
        index += arr.length
        target[index] = value
        
        if (index < 0) {
          throw new Error('index is overflow')
        }
        return true
      }
      
      target[prop] = value
      return true
    }
  })
}
                   
```
