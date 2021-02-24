
Here is a video explaining this : https://www.youtube.com/watch?v=8Dzaxp2TUwg

```javascript

function html(strings, ...values) {
  const segs = []

  let i = 0
  for (; i < values.length; i++) {
    segs.push(strings[i])
    segs.push(values[i])
  }
  segs.push(strings[i])

  return segs.join('')  
}


// render the result from html() into the container
function render(result, container) {
  container.innerHTML = result
}
```
