
```js

/**
 * @param {string} str
 * @return {string}
 */
// naive one
// function trim(str) {
//   const arr = [...str]
  
//   const reg = /\s/
//   while (reg.test(arr[0])) {
//     arr.shift()
//   }
  
//   while (reg.test(arr[arr.length - 1])) {
//     arr.pop()
//   }
  
//   return arr.join('')
// }


// for index
// function trim(str) {
//   const reg = /\s/
//   let start = 0
//   let end = str.length - 1
  
//   while (reg.test(str[start])) {
//     start += 1
//   }
  
//   while (reg.test(str[end])) {
//     end -= 1
//   }
  
//   return str.slice(start, end + 1)
// }

// regexp replacement
function trim(str) {
  return str.replace(/^\s+|\s+$/g, '')
}



```

And a video explaining this 

https://www.youtube.com/watch?v=IvKV-1MoYxw
