Here is a video explaining this : https://www.youtube.com/watch?v=IdTjYZIG4Kc

```javascript

/**
 * @param {string} str - binary string
 * @returns {string}
 */
function myBtoa(str) {
  let result = ''

  const base64table = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/'
  // keep slicing by 3 character
  while (str.length > 0) {
    const buffer = []
    const first3 = str.slice(0, 3)
    str = str.slice(3)
    let bits = ''
    for (let char of first3) {
      bits += char.charCodeAt(0).toString(2).padStart(8, '0')
    }
    // keep slicing 6 bits
    while (bits.length > 0) {
      const first6 = bits.slice(0, 6).padEnd(6, '0')
      bits = bits.slice(6)
      const char = base64table[parseInt(first6, 2)]
      buffer.push(char)
    }

    // add the padding
    if (buffer.length < 4) {
      buffer.push('='.repeat(4 - buffer.length))
    }

    result += buffer.join('')
  }

  return result
}
```
