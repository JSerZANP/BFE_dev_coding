A video explaining this 

https://www.youtube.com/watch?v=dTMyjyJFTLo

```js
/**
 * @param {any[]} args
 * @returns {string}
 */
// first try , a little chaotic
// function classNames(...args) {
//   return args.filter(item => {
//     if (['string', 'number', 'object'].includes(typeof item)) {
//       return item !== null
//     }
//     return false
//   }).map(item => {
//     if (Array.isArray(item)) {
//       return classNames(...item)
//     }
    
//     if (['string', 'number'].includes(typeof item)) {
//       return item
//     }
    
//     return classNames(...Object.keys(item).filter(key => !!item[key]))
//   }).join(' ')
// }

// cleaner code with reduce
function classNames(...args) {
  return args.flat(Infinity).reduce((result, item) => {
    
    if (item === null) return result
    
    switch (typeof item) {
      case 'string':
      case 'number':
        result.push(item)
        break
      case 'object':
        for (let [key, value] of Object.entries(item)) {
          if (!!value) {
            result.push(key)
          }
        }
        break
    }
    
    return result
  }, []).join(' ')
}












```
