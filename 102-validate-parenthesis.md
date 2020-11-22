And a video explaining this: https://www.youtube.com/watch?v=3kO5aIWEf4E

```js

/**
 * @param {string} str
 * @return {boolean} 
 */
const map = {
  '(': ')',
  '[': ']',
  '{': '}'
}

function validate(str) {
  const stack = []
  for (let char of str) {
    if (map[char]) {
      stack.push(char)
    } else {
      const top = stack.pop()
      
      if (!top) return false
      
      if (map[top] !== char) {
        return false
      }
    }
  }
  return stack.length === 0
}
```
