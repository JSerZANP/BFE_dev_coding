Here is the video https://www.youtube.com/watch?v=T7qMFQ95MOM

```typescript



// copied from lib.es5.d.ts
declare interface Array<T> {
  myMap<U>(callbackfn: (value: T, index: number, array: T[]) => U, thisArg?: any): U[];
}


Array.prototype.myMap = function(callback, thisArg) {
  const length = this.length
  const result = new Array(length)
  
  for (let i = 0; i < length; i++) {
    if (i in this) {
      result[i] = callback.call(thisArg, this[i], i, this)
    }
  }

  return result
}

```
