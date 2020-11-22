one line with regular expression

```js

/**
 * @param {string} str
 * @return {string}
 */
function snakeToCamel(str) {
  return str.replace(/([^_])_([^_])/g, (_, before, after) => before + after.toUpperCase())
}
```

ok a video https://www.youtube.com/watch?v=4bsU-dPwv3U
