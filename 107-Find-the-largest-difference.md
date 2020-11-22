Also a video explaining this 

https://www.youtube.com/watch?v=jXDDVTlToj8

Hope it helps.

```js

/**
 * @param { number[] } arr
 * @returns { number }
 */
// function largestDiff(arr) {
//   if (arr.length === 0) return 0
//   return Math.abs(Math.max(...arr) - Math.min(...arr))
// }

function largestDiff(arr) {
  if (arr.length === 0) return 0
  
  let min = Infinity
  let max = -Infinity
  let result = Infinity
  
  for (let item of arr) {
    if (item < min) {
      min = item
      result = max - min
    }
    
    if (item > max) {
      max = item
      result = max - min
    }
  }

  return result
}
```
