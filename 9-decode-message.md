Also a video explaining this : https://www.youtube.com/watch?v=QCq9Xoo1EXk

```js

/**
 * @param { string[][] } message
 * @returns { string }
 */
function decode(message) {
  if (message.length === 0) return ''
  if (message[0].lenght === 0) return ''
  
  const rows = message.length
  const cols = message[0].length
  
  let result = ''
  let row = 0
  let col = 0
  let directionY = 1
  
  while (col < cols && row > -1 && row < rows) {
    result += message[row][col]
    col += 1
    
    row += directionY
    
    if (row > rows - 1) {
      directionY = -1
      row -= 2
    } else if (row < 0) {
      directionY = 1
      row += 2
    }
  }
  
  return result
}
```
