here is a video explaining it 

 https://www.youtube.com/watch?v=EYoGz_sFfLM

```js
// getAPI is bundled with your code, config will only be some plain objects.
// const getAPI = <T>(path: string, config: SomeConfig): Promise<T> => { ... }


// you code here maybe, if you want some outer scope.

// Map<string, {promise: Promise, triggered: number}>
const cache = new Map()

const hash = (obj) => {
  switch (Object.prototype.toString.call(obj)) {
    case '[object Null]':
      return 'null'
    case '[object Undefined]':
      return 'undefined'
    case '[object Number]':
    case '[object Boolean]':
      return obj.toString()
    case '[object String]':
      return obj
    case '[object Object]':
      const keys = Object.keys(obj)
      keys.sort()
      return `{${keys.map(key => `"${key}":${hash(obj[key])}`).join(',')}}`
      case '[obect Array]':
      return `[${obj.map(item => hash(item)).join(',')}]`   
  }
}

const MAX_CACHE = 5
const CACHE_TIME_LIMIT = 1000
/**
 * @param { string } path
 * @param { object } config
 * only plain objects, no strange input in this problem
 * @returns { Promise<any> }
 */
function getAPIWithMerging(path, config) {
  // serialize the hash, with path + config
  const requestHash = hash({path, config})
  
  // cache is available
  if (cache.has(requestHash)) {
    const entry = cache.get(requestHash)
    if (Date.now() - entry.triggered <= CACHE_TIME_LIMIT) {
      return entry.promise
    }
    cache.delete(requestHash)
  }
  
  const promise = getAPI(path, config)
  cache.set(requestHash, {
    promise,
    triggered: Date.now()
  })
  
  // remove the oldest cache
  if (cache.size > MAX_CACHE) {
    for (let [hash] of cache) {
      cache.delete(hash)
      break
    }
  }
  
  return promise
}

getAPIWithMerging.clearCache = () => {
   cache.clear()
}
```
