
```js

/**
 * @param {string} str
 * @return {string[]}
 */
function extract(str) {
  const regexp = /<a(\s[^>]*)?>.*?<\s*\/\s*a>/g
  return str.match(regexp) ?? []
}
```

A video explaining this https://www.youtube.com/watch?v=T2xAfZJ4o10
