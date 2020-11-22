also a video explaining this https://www.youtube.com/watch?v=seeui0prOcs


```js

/**
 * @param { () => Promise<any> } fetcher
 * @param { number } maximumRetryCount
 * @returns { Promise<any> }
 */
function fetchWithAutoRetry(fetcher, maximumRetryCount) {
  return new Promise((resolve, reject) => {
    let retryCount = 0
    const callFetcher = () => fetcher().then((data) => {
      resolve(data)
    }, (error) => {
      if (retryCount < maximumRetryCount) {
        callFetcher()
        retryCount += 1
      } else {
        reject(error)
      }
    })
    
    callFetcher()
  })
}
```
