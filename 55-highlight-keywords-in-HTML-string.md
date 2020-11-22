Also a video explaining this 

https://www.youtube.com/watch?v=BtGjyYBIHRk

hope it helps


```js
/**
 * @param { string } html
 * @param { string[] } keywords
 */
function highlightKeywords(html, keywords) {
  
  let result = ''
  
  const keywordSet = new Set(keywords)
  
  // return -1 if non-existing
  const getEndForEm = (start) => {
    let isEmFound = false
    let end = start 
    while (start <= end) {
      for (let word of keywordSet) {
        const length = word.length
        if (html.slice(start, start + length) === word) {
          isEmFound = true
          end = Math.max(end, start + length - 1)
        }
      }
      
      start += 1
    }
    
    return isEmFound ? end : -1
  }
  
  for (let i = 0; i < html.length;) {
    let endForEm = getEndForEm(i)
    
    // check if there is adjacent keyword 
    while (endForEm > -1) {
      const nextEndForEm = getEndForEm(endForEm + 1)
      if (nextEndForEm === -1) {
        break
      }
      endForEm = nextEndForEm
    }
    
    if (endForEm > -1) {
      result += '<em>' + html.slice(i, endForEm + 1) + '</em>'
      i = endForEm + 1
    } else {
      result += html[i]
      i += 1
    }
  }
  
  return result
};
```
