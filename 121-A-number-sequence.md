And a video for this https://www.youtube.com/watch?v=sJbgV3vKXuM

```js

const transform = (num) => {
  let currentDigit = ''
  let currentCount = 0
  let result = ''
  for (let i = 0; i <= num.length; i++) {
    if (num[i] === currentDigit) {
      currentCount += 1
    } else {
      if (currentCount > 0) {
        result += currentCount + currentDigit
      }

      currentDigit = num[i]
      currentCount = 1
    }
  }
  return result
}

/**
 * @param {number} n - integer
 * @returns {string}
 */
function getNthNum(n) {
  let num = '1'
 
  while (n > 1) {
    num = transform(num)
    n -= 1
  }
  
  return num
}
```
