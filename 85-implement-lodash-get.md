with a video explaining this

https://www.youtube.com/watch?v=bISjPvOvlbs


```js
/**
 * @param { object } source
 * @param { string | string[] } path
 * @param { any? } defaultValue
 * @returns { any }
 */
function get(source, path, defaultValue = undefined) {
  // 1. normalize the path into array notation
  // 2. get the result layer by layer
  const segs = Array.isArray(path) ? path : path.split(/[\.\[\]]+/g)
  
  if (segs[segs.length - 1] === '') {
    segs.pop()
  }
  
  if (segs.length === 0) {
    return defaultValue
  }
  
  let result = source
  
  while (result && segs.length > 0) {
    let head = segs.shift()
    result = result[head]
  }
  
  return result === undefined ? defaultValue : result
}
```
