Also a video explaining this 

https://www.youtube.com/watch?v=FIFuDaxSz3w


```js

/**
 * @param { HTMLElement } root
 * @returns { HTMLElement[] }
 */
function flatten(root) {
  if (root === null) return []
  
  const queue = [root]
  
  const result = []
  
  while (queue.length > 0) {
    const head = queue.shift()
    result.push(head)
    queue.push(...head.children)
  }
  
  return result
}
```
