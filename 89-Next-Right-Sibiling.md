And a video explaining https://www.youtube.com/watch?v=obYEHo_rsAU

```js
// BFS approach
function nextRightSibling(root, target) {
  // your code here
  const queue = [root, null]
  
  while (queue.length > 0) {
    let head
    while (head = queue.shift()) {
      if (head === target) {
        return queue.shift()
      }
      
      queue.push(...head.children)
    }
    
    if (queue.length > 0) {
      queue.push(null)
    }
  }
}
```

```js

/**
 * @param {HTMLElement} root
 * @param {HTMLElement} target
 * @return {HTMLElemnt | null}
 */

// recursion solution
function nextRightSibling(root, target) {
  // your code here
  
  if (target === null) return null
  if (target.nextElementSibling) return target.nextElementSibling
  
  let parent = target.parentElement
  if (parent === root) return null
  
  do {
    parent = nextRightSibling(root, parent)
    if (parent && parent.firstElementChild) {
      return parent.firstElementChild
    }
  } while (parent)
  
  return null
}

```
