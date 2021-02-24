A video explaining this : https://www.youtube.com/watch?v=rLZw7RWxkZs

```typescript





// copied from lib.es5.d.ts
declare interface Array<T> {
  myReduce(callbackfn: (previousValue: T, currentValue: T, currentIndex: number, array: T[]) => T): T;
  myReduce(callbackfn: (previousValue: T, currentValue: T, currentIndex: number, array: T[]) => T, initialValue: T): T;
  myReduce<U>(callbackfn: (previousValue: U, currentValue: T, currentIndex: number, array: T[]) => U, initialValue: U): U
}

Array.prototype.myReduce = function (...args:any[]) {
  const hasInitialValue = args.length > 1
  if (!hasInitialValue && this.length === 0) {
    throw new Error()
  }

  let result = hasInitialValue ? args[1] : this[0]

  for (let i = hasInitialValue ? 0 : 1;  i < this.length; i++) {
    result = args[0](result, this[i], i, this)
  }

  return result
}






```
