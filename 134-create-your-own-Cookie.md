And a video explaining this 

https://www.youtube.com/watch?v=RqvMgNjRJek

```js

// enable myCookie
function install() {
  // Map<string, {value: string, maxAge?: number, createdAt: number}>
  const store = new Map()
  // use getter and setter
  Object.defineProperty(document, 'myCookie', {
    get() {
      const result = []
      for (let [key, entry] of store.entries()) {
        if (entry.maxAge !== undefined) {
          if (Date.now() - entry.createdAt >= entry.maxAge) {
            // expire
            store.delete(key)
            continue
          }
        }
        result.push(`${key}=${entry.value}`)
      }
      return result.join('; ')
    },
    
    set(valueStr) {
      const [keyValuePair,...options] = valueStr.replace(/ /g, '').split(';')
      const [key, value] = keyValuePair.split('=')
      if (!key || !value) return
      
      const entry = {
        value,
        createdAt: Date.now()
      }
      
      options.forEach((option) => {
        const [key, value] = option.split('=')
        if (!key || !value) return
        
        if (key === 'max-age') {
          const maxAge = parseInt(value, 10)
          
          if (Number.isNaN(maxAge)) return
          entry.maxAge = maxAge * 1000
        }
      })
      
      store.set(key, entry)
    },
    
    configurable: true
  })
}

// disable myCookie
function uninstall() {
  delete document.myCookie
}
```
