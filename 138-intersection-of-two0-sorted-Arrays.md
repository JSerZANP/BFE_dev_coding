A video explaining this https://www.youtube.com/watch?v=8NXyNMY7uuA

```javascript
/**
 * @param {number[]} arr1 - integers
 * @param {number[]} arr2 - integers
 * @returns {number[]}
 */
function intersect(arr1, arr2) {
  // your code here
  // n * m
  // O(n * m), 
  // preprocess arr2 -> Map<number, count>
  // time: O(n) + O(m), space: O(m)

  // keep shifting
  // O(n + m)
  // reverse it first, then poping
  // O(n + m), space: O(1)
  arr1.reverse()
  arr2.reverse()

  const result = []

  while (arr1.length > 0 && arr2.length > 0) {
    const top1 = arr1[arr1.length - 1]
    const top2 = arr2[arr2.length - 1]

    if (top1 === top2) {
      result.push(top1)
      arr1.pop()
      arr2.pop()
    } else if (top1 < top2) {
      arr1.pop()
    } else {
      arr2.pop()
    }
  }

  return result
}
```
