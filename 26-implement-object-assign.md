And here is the video explaining it https://www.youtube.com/watch?v=2CYexxiW3lo

```javascript

/**
 * @param {any} target
 * @param {any[]} sources
 * @return {object}
 */
function objectAssign(target, ...sources) {
  if (target === null || target === undefined) throw new Error('invalid target')

  let result = target
  if (['number', 'string', 'boolean'].includes(typeof target)) {
    result = Object(target)
  }

  for (const source of sources) {
    if (source === null || source === undefined) continue
    const keys = [
      ...Object.keys(source),
      ...Object.getOwnPropertySymbols(source)
      .filter(item => Object.getOwnPropertyDescriptor(source, item).enumerable)
    ]
    for (const key of keys) {
      if (!Reflect.set(result, key, source[key])) {
        throw new Error('cannot assign to read-only properties')
      }
    }
  }
  return result
}

const target = Object.defineProperty({}, 'foo', {
  value: 1,
  writable: false
});


```
