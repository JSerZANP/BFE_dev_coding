Here is a video explaining this:  https://www.youtube.com/watch?v=jfRMnIePtjU

```javascript

function cloneDeep(data, cloned = new Map()) {
  
  const type = typeof data
  switch (type) {
    case 'undefined':
    case 'number':
    case 'boolean':
    case 'bigint':
    case 'symbol':
    case 'string':
      return data
    default:
      if (data === null) {
        return null
      }


      if (cloned.has(data)) {
        return cloned.get(data)
      }

      const tag = Object.prototype.toString.call(data)
      switch (tag) {
        case '[object Number]':
        case '[object Boolean]':
        case '[object String]':
          return Object(data)
      }

      // const a = [1]
      // a[1] = a
      if (Array.isArray(data)) {
        const result = []
        cloned.set(data, result)
        for (const item of data) {
          result.push(cloneDeep(item, cloned))
        }
        return result
      } else {
        const result = {}
        cloned.set(data, result)
        for (const key of Reflect.ownKeys(data)) {
          result[key] = cloneDeep(data[key], cloned)
        }
        return result
      }
  }
}

```
