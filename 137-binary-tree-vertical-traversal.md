Here is a video explaining this: https://www.youtube.com/watch?v=7_3lG79qGKc
```javascript
// This is the class for the node
// you can use this directly as it is bundled with your code

// class Node {
//   value: number
//   left: null | Node
//   right: null | Node
//   constructor(val) {
//     this.value = val
//     this.left = null
//     this.right = null
//   }
// }

/**
 * @param {Node} root
 * @returns {number[]}
 */
function traverse(root) {
  // [1]
  // [2, 1]
  // [2, 1, 3]
  // [4, 2, 1, 3]
  // [4, 2, 1, 3, 5]
  // [6, 4, 2, 1, 3, 5]
  // [6, 3, [2, 7], 1, 3, 5]

  // set the root to index: [0: 1]
  // [-1:2, 0:1]
  // [-2:4, -1: 2, 0:1]

  // pre-order tree traversal O(n)
  // use Map<number, number[]> to hold the data O(n)
  // keep track of the minimum index: min, and maximum: max O(1)
  // length = -min + max + 1
  // initialize Array(length)
  // traverse through the map, set the item O(n)


  const map = new Map()
  let min = Infinity
  let max = -Infinity

  // DFS is not working well
  // assumption that first-in-first-out is not right about the node order
  // BFS
  const queue = [[root, 0]]
  
  while (queue.length > 0) {

    let count = queue.length

    while (count-- > 0) {
      const [node, index] = queue.shift()

      if (map.has(index)) {
        map.get(index).push(node.value)
      } else {
        map.set(index, [node.value])
      }

      min = Math.min(min, index)
      max = Math.max(max, index)

      if (node.left) {
        queue.push([node.left, index - 1])
      } 

      if (node.right) {
        queue.push([node.right, index + 1])
      }
    }

    // sort the nodes in right order
    queue.sort((a, b) => a[1] - b[1])
  }

  const length = -min + max + 1
  const result = new Array(length)

  for (const [rawIndex, value] of map.entries()) {
    result[rawIndex - min] = value
  }

  return result.flat()
}

```
