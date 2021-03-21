Here is a video explaining https://www.youtube.com/watch?v=wE3PmZyVNsU

```javascript

// 1. for loop approach
function range(from, to) {
  // return the result array
  const result = []
  while (from <= to) {
    result.push(from++)
  }
  return result
}


// 2. implement iterable/iterator protocol
// for ... of uses interable protocol
// [Symbol.iterator]: () =>  Iterator
// next: () => {done: bolean, value?: any} 

function range(from, to) {
  return {
    // iterable protocol
    [Symbol.iterator]() {
      // iterator protocol
      return {
        next() {
          return {
            done: from > to,
            value: from++
          }
        }
      }
    }
  }
}


// 3. use geneator function to make things simpler
// geneator function returns generator which implements iterator protocol
function range(from, to) {
  return {
    // iterable protocol
    [Symbol.iterator]: function * () {
      while (from <= to) {
        yield from++
      }
    }
  }
}

// 4. actualy geneator also implements iterable protocol
function range(from, to) {
  return (function * () {
    while (from <= to) {
      yield from++
    }
  })(from, to)
}

// 5. maybe just change the entry function?
function * range(from, to) {
  while (from <= to) {
    yield from++
  }
}
```
