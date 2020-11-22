And a video explaining it https://www.youtube.com/watch?v=TOP2AgSoBz0

```js

/**
 * @param {string} str
 * @return {string}
 */
function compress(str) {
  let currentChar = ''
  let currentCount = 0
  
  let result = ''
  
  for (let i = 0; i < str.length + 1; i++) {
    const char = str[i]
    if (char === currentChar) {
      currentCount += 1
    } else {
      result += 
        currentCount === 0 ? '' :
        currentCount === 1 ? currentChar : currentChar + currentCount
      currentChar = char
      currentCount = 1
    }
  }
  
  return result
}
```
