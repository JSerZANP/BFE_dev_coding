And a video explaining this https://www.youtube.com/watch?v=ZI7ZipKedfI

```js
/**
 * @param { number } num
 */

// sum(1)(2)(3)
// sum(3)(3)
// sum(6)

function sum(num, currentSum = 0) {
  const newCurrentSum = num + currentSum
  
  const func = function(arg) {
    return sum(arg, num + currentSum)
  }
  
  func.valueOf = () => newCurrentSum
//   func.toString = () => newCurrentSum.toString()
  
  return func
}

```

And a video explaining this https://www.youtube.com/watch?v=ZI7ZipKedfI
