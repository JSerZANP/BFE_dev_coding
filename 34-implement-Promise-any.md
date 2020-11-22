And a video explaining this https://www.youtube.com/watch?v=fYTmLpFJPdw

```js

/**
 * @param {Array<Promise>} promises
 * @returns {Promise}
 */
function any(promises) {
  // return a Promise, which resolves as soon as one promise resolves
  return new Promise((resolve, reject) => {
    let isFulfilled = false
    const errors = []
    let errorCount = 0
    promises.forEach((promise, index) => promise.then((data) => {
      if (!isFulfilled) {
        resolve(data)
        isFulfilled = true
      }
    }, (error) => {
      errors[index] = error
      errorCount += 1
      
      if (errorCount === promises.length) {
        reject(new AggregateError('none resolved', errors))
      }
    }))
  })
}
```
