And a video explaining https://www.youtube.com/watch?v=PE9WkWv2cHc

```js

/**
 * @param {Array<Promise>} promises
 * @returns {Promise}
 */
function race(promises) {
  let isSettled = false
  return new Promise((resolve, reject) => {
    promises.forEach(promise => promise.then((data) => {
      if (!isSettled) {
        resolve(data)
        isSettled = true
      }
    }, (error) => {
      if (!isSettled) {
        reject(error)
        isSettled = true
      }
    }))
  })
}
```
