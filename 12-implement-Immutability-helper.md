Here is a video explaining https://www.youtube.com/watch?v=mupUtwJi2AU

```javascript
const isObject = (data) => {
  return typeof data === 'object' && data !== null
}
/**
 * @param {any} data
 * @param {Object} command
 */
function update(data, command) {
  // for simple cases, which $command is in the first layer
  if ('$push' in command) {
    if (!Array.isArray(data)) {
      throw new Error('not array')
    }

    return [...data, ...command['$push']]
  }

  if ('$merge' in command) {
    if (!isObject(data)) {
      throw new Error('not object for $merge')
    }

    return {
      ...data,
      ...command['$merge']
    }
  }

  if ('$apply' in command) {
    return command['$apply'](data)
  }

  if ('$set' in command) {
    return command['$set']
  }

  // for cases with path

  // first shallow copy
  if (!isObject(data)) {
    throw new Error('not object for complex data')
  }

  const newData = Array.isArray(data) ? [...data] : {...data}

  for (const key of Object.keys(command)) {
    newData[key] = update(newData[key], command[key])
  }

  return newData
}
```
