
Here is a video explaining https://www.youtube.com/watch?v=XMXWh2CF9ko


```js

/**
 * @param {number} num
 * @return {string}
 */

// naive solution
// function addComma(num) {
//    const sign = num < 0 ? -1 : 1
//    if (sign < 0) {
//      num *= -1
//    }
  
//    const str = num.toString()
//    const [integer, fraction] = str.split('.')
   
//    const arr = []
   
//    const digits = [...integer]
//    for (let i = 0; i < digits.length; i++) {
//      arr.push(digits[i])
//      // add extra commas
//      // care for the 0
//      const countOfRest = digits.length - (i + 1)
//      if (countOfRest % 3 === 0 && countOfRest !== 0) {
//        arr.push(',')
//      }
//    }
   
//    const newInteger = (sign < 0 ? '-' : '') + arr.join('')
   
//    if (fraction === undefined) return newInteger 
//    return newInteger + '.' + fraction
// }

// regular expression  1
// function addComma(num) {
//    const str = num.toString()
//    let [integer, fraction] = str.split('.')
   
//    while (true) {
//       const next = integer.replace(/(\d+)(\d{3})/, '$1,$2')
//       // 12345,678
//       // 12,345,678
//       if (next === integer) {
//         break
//       }
//       integer = next
//    }
   
//    if (fraction === undefined) return integer 
//    return integer + '.' + fraction
// }

// regular expressiong global,
// (?= )
function addComma(num) {
   const str = num.toString()
   let [integer, fraction] = str.split('.')
   
   integer = integer.replace(/(\d)(?=(\d{3})+$)/g, '$1,')
   
   if (fraction === undefined) return integer 
   return integer + '.' + fraction
}

```
