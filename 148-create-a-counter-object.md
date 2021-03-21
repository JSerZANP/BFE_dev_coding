Here is a video explaining this: 

https://www.youtube.com/watch?v=ilEN1KXFcYg


```typescript


function createCounter(): {count: number } {
 
  let count = 0

  const obj = {
    count: 0
  }

  Object.defineProperty(obj, 'count', {
    get: function() {
      return count++
    }
  })

  return obj
}


```
