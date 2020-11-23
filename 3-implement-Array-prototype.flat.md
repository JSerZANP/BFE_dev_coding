And a video explaining https://www.youtube.com/watch?v=z0Jl-UUPtEw

```js

/**
 * @param {Array} arr
 * @param {number} depth
 */

function flat(arr, depth = 1) {
  // [[1,1] [[2],1], [[3, [4]],1]]
  // [[[2],1], [[3, [4]],1]]
  // [[2,0], [[3, [4]],1]]
  // [[[3, [4]],1]]
  // [[3, 0], [[4], 0]]
  
  const result = []
  const stack = [...arr.map(item => ([item, depth]))]
  
  while (stack.length > 0) {
    const [top, depth] = stack.pop()
    if (Array.isArray(top) && depth > 0) {
      stack.push(...top.map(item => ([item, depth - 1])))
    } else {
      result.push(top)
    }
  }
  
  return result.reverse()
}


```
