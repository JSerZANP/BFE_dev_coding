And this is a video explaining this

https://www.youtube.com/watch?v=A7I3BgsZB_s


```js

/** 
 * @param {any[]} items
 * @param {number} size
 * @returns {any[][]}
 */
function chunk(items, size) {
  const result = []
  if (size < 1) return result
  
  let buffer = []
  
  for (let i = 0; i < items.length; i++) {
    buffer.push(items[i])
    
    if (buffer.length === size) {
      result.push(buffer)
      buffer = []
    }
  }
  
  if (buffer.length > 0) {
    result.push(buffer)
  }
  
  return result
}
```
