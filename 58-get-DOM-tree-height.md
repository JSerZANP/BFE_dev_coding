Also a video explaining 

https://www.youtube.com/watch?v=dmI2ZVaqaCE


```js

/**
 * @param { HTMLElement | null } tree
 * @returns { number }
 */
// function getHeight(tree) {
//   // your code here
//   if (tree === null) return 0
//   return Math.max(...Array.from(tree.children).map(getHeight), 0) + 1
// }


function getHeight(tree) {
  // your code here
  if (tree === null) return 0
  const queue = [tree]
  let height = 0
  while (queue.length > 0) {
    let count = queue.length
    height += 1
    while (count > 0) {
      const head = queue.shift()
      queue.push(...head.children)
      count -= 1
    }
  }
  return height
}


```
