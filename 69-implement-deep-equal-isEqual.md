And a video explaining it https://www.youtube.com/watch?v=gDhY5eV-IGk

```js

const getType = (data) => {
  const tag = Object.prototype.toString.call(data) // [object xxx]
  const match = tag.match(/\[object (.+)\]/)
  if (!match) {
    throw new Error('should not be here')
  }
  return match[1].toLowerCase()
}

class EqualMap {
  constructor() {
    this.map = new Map()
  }
  
  add(a,b) {
    const map = this.map
    if (!map.has(a)) {
      map.set(a, new Set())
    }
    
    map.get(a).add(b)
    
    if (!map.has(b)) {
      map.set(b, new Set())
    }
    
    map.get(b).add(a)
  }
  
  check(a, b) {
    return !!this.map.get(a)?.has(b)
  }
}

/**
 * @param {any} a
 * @param {any} b
 * @return {boolean}
 */

// Map<from, Set>
function isEqual(a, b, equalMap = new EqualMap()) {
  if (a === b) return true
  
  if (equalMap.check(a, b)) return true
  
  const typeA = getType(a)
  const typeB = getType(b)
  
  if (typeA !== typeB) {
    return false
  }
  
  switch (typeA) {
    case 'object':
      const keysA = Object.keys(a)
      const keysB = Object.keys(b)
      if (keysA.length !== keysB.length) return false
      
      equalMap.add(a, b)
      for (let key of keysA) {
        if (!isEqual(a[key], b[key], equalMap)) {
          return false
        }
      }
      return true
    case 'array':
      if (a.length !== b.length) return false
      equalMap.add(a, b)
      for (let i = 0; i < a.length; i++) {
        if (!isEqual(a[i], b[i], equalMap)) {
          return false
        }
      }
      return true
    default:
      throw new Error('should not be here')
  }
}
```
