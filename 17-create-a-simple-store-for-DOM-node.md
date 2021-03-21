Here is my video explaining this: 

https://www.youtube.com/watch?v=DAaMoriI0Xg

```javascript
// Array
// hold all the data in the array, and do search
// Array<Node>
// Array<value>

// set: push -> O(1)
// get: get -> O(n)
// has: same as get -> O(n)

// store the index in the DOM element
// dataset or set it directly
// set: push -> O(1)
// get: O(1)
// has: O(1)

// Object can only use string or symbol
// not an option

class NodeStore {
  static VALUE_KEY = '__index'
  nodeList = []
  valueList = []
   /**
   * @param {Node} node
   * @param {any} value
   */
  set(node, value) {
    node[NodeStore.VALUE_KEY] = this.nodeList.length
    this.nodeList.push(node)
    this.valueList.push(value)
  }
  /**
   * @param {Node} node
   * @return {any}
   */
  get(node) {
    if (NodeStore.VALUE_KEY in node) {
      return this.valueList[node[NodeStore.VALUE_KEY]]
    }
    return undefined
  }
  
  /**
   * @param {Node} node
   * @return {Boolean}
   */
  has(node) {
    return NodeStore.VALUE_KEY in node
  }
}
```
