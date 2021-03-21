Here is a video explaining this :

 https://www.youtube.com/watch?v=Do46g92OFUw

```typescript



function t(translation: string, data?: any): string {
  let isPossiblePropertyName = false
  let propertyName = ''
  let result = ''

  for (let i = 0; i < translation.length; i++) {
    if (isPossiblePropertyName) {
      // if }} is found, end it
      if (translation[i] === '}' && translation[i + 1] === '}') {
        if (data && propertyName in data) {
          result += data[propertyName]
        }

        isPossiblePropertyName = false
        i += 1
      } else {
        propertyName += translation[i]
      }
    } else {
      // if {{ are met
      if (translation[i] === '{' && translation[i + 1] === '{') {
        isPossiblePropertyName = true
        propertyName = ''
        i += 1
      } else {
        result += translation[i]
      }
    }
  }

  // for propertyName left
  if (isPossiblePropertyName) {
    result += '{{' + propertyName
  }

  return result
}
```
