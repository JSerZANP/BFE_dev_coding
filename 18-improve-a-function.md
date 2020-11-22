And a video explaining https://www.youtube.com/watch?v=EC_M8LlguC0

```js

/**
 * @param {object[]} items
 * @excludes { Array< {k: string, v: any} >} excludes
 */

/**
 * @param {object[]} items
 * @param { Array< {k: string, v: any} >} excludes
 * @return {object[]}
 */
function excludeItems(items, excludes) {
  // m k n
  // n * m
  
  // change exclude to Map<key, Set<value>>
  // m * k * 1
  
  // preprocess excludes array
  // avoid multiple for loop on items
  
  const excludeMap = new Map()
  for (let {k, v} of excludes) {
    if (!excludeMap.has(k)) {
      excludeMap.set(k, new Set())
    }
    excludeMap.get(k).add(v)
  }
  
  return items.filter(item => {
    return Object.keys(item).every(
      key => !excludeMap.has(key) || !excludeMap.get(key).has(item[key])
    )
  })
}






```
