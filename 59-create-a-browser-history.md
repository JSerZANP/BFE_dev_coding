And a video explaining this 

https://www.youtube.com/watch?v=lywZLDOh-0o


```js
class BrowserHistory {
  
  /**
   * @param {string} url
   * if url is set, it means new tab with url
   * otherwise, it is empty new tab
   */
  constructor(url) {
    this.entries = []
    this.currentIndex = 0
    if (url !== undefined) {
      this.entries.push(url)
    }
  }
  /**
   * @param { string } url
   */
  visit(url) {
    this.entries.length = this.currentIndex + 1
    this.entries.push(url)
    this.currentIndex += 1
  }
  
  /**
   * @return {string} current url
   */
  get current() {
    return this.entries[this.currentIndex]
  }
  
  // go to previous entry
  goBack() {
    this.currentIndex = Math.max(0, this.currentIndex - 1)
  }
  
  // go to next visited url
  forward() {
    this.currentIndex = Math.min(this.entries.length - 1, this.currentIndex + 1)
  }
}
```
