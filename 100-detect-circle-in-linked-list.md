A video explaining this : https://www.youtube.com/watch?v=S3VajiqdjMY

```javascript

/**
 * @param {Node} head
 * @return {boolean}
 */
function hasCircle(head) {
  // fast slow pointer
  let fast = head
  let slow = head

  while (fast && slow) {
    fast = fast.next?.next
    slow = slow.next

    if (fast === slow) {
      return true
    }
  }

  return false
}
```
