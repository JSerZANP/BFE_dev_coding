And here is a video explaining it .

https://www.youtube.com/watch?v=-Bk52GV2N0g

```js

/**
 * @param {string} str - roman numeral string
 * @returns {number} integer
 */
const valueMap = {
  I: 1,
  V: 5,
  X: 10,
  L: 50,
  C: 100,
  D: 500,
  M: 1000
}

function romanToInteger(str) {
   let result = 0
   for (let i = 0; i < str.length; i++) {
     const val = valueMap[str[i]]
     const nexVal = i < str.length - 1 ? valueMap[str[i + 1]] : undefined
     
     const sign = nexVal !== undefined && nexVal > val ? -1 : 1
     result += sign * val
   }
   return result
}
```
