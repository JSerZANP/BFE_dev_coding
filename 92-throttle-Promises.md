Here is a video explaining https://www.youtube.com/watch?v=ua1W86n4bdE

```javascript

/**
 * @param {() => Promise<any>} func
 * @param {number} max
 * @return {Promise}
 */
function throttlePromises(funcs, max){
  return new Promise((resolve, reject) => {
    let concurrentCount = 0
    let latestCalledFuncIndex = -1
    let resultCount = 0
    let hasError = false
    const result = []

    const fetchNext = () => {
      // already done
      if (hasError || latestCalledFuncIndex === funcs.length - 1) {
        return
      }
      // get the func
      // trigger
      // update the count
      // if ok for next fetch, trigger next

      const nextFuncIndex = latestCalledFuncIndex + 1
      const next = funcs[nextFuncIndex]

      concurrentCount += 1
      latestCalledFuncIndex += 1

      next().then((data) => {
        result[nextFuncIndex] = data
        resultCount += 1
        concurrentCount -= 1

        if (resultCount === funcs.length) {
          resolve(result)
          return
        }

        fetchNext()
      }, (err) => {
        hasError = true
        reject(err)
      })
      
      if (concurrentCount < max) {
        fetchNext()
      }
    }

    fetchNext()
  })
}

```
