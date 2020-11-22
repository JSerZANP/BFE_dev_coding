
```js
/**
 * @param {Promise<any>} promise
 * @param {() => void} onFinally
 * @returns {Promise<any>}
 */
function myFinally(promise, onFinally) {
  return promise.then((value) => {
    return Promise.resolve(onFinally())
      .then(() => value)
  }, (reason) => {
    return Promise.resolve(onFinally())
      .then(() => Promise.reject(reason))
  })
}
```

Here is a video explaining it 

https://www.youtube.com/watch?v=ZXcDQi_wVoM
