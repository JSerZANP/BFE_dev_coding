A video explaining it 

https://www.youtube.com/watch?v=PqElCcSfA6s


```js

/*
 type TypIsBad = (version: number) => boolean
 */

/**
 * @param {TypIsBad} isBad 
 */
function firstBadVersion(isBad) {
	// firstBadVersion receive a check function isBad
  // and should return a closure which accepts a version number(integer)
  return (version) => {
    let left = 0
    let right = version
    // the version right after right is the first bad version
    // or `left`
    // o
    
    while (left <= right) {
       const middle = Math.floor((left + right) / 2)
       if (isBad(middle)) {
         right = middle - 1
       } else {
         left = middle + 1
       }
    }
    
    return isBad(left) ? left : -1
  }
}
```
