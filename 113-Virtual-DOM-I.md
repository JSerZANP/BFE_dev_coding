And a video explaining this

https://www.youtube.com/watch?v=t-sWlzVGazc

```js
/**
 * @param {HTMLElement} 
 * @return {object} JSON presentation
 */
function virtualize(element) {
  // virtualize top level element
  // recursively handle the children (childNodes)
  const result = {
    type: element.tagName.toLowerCase(),
    props: {}
  }
  // props (without children)
  for (let attr of element.attributes) {
    const name = attr.name === 'class' ? 'className' : attr.name
    result.props[name] = attr.value
  }
  // children
  const children = []
  for (let node of element.childNodes) {
    if (node.nodeType === 3) { // text node
      children.push(node.textContent)
    } else {
      children.push(virtualize(node))
    }
  }

  result.props.children = children.length === 1 ? children[0] : children

  return result
}


/**
 * @param {object} valid JSON presentation
 * @return {HTMLElement} 
 */
function render(json) {
  // create the top level emlement
  // recursively append the children
  // textnode
  if (typeof json === 'string') {
    return document.createTextNode(json)
  }

  // element
  const {type, props: {children, ...attrs}} = json
  const element = document.createElement(type)

  for (let [attr, value] of Object.entries(attrs)) {
    element[attr] = value
  }

  const childrenArr = Array.isArray(children) ? children : [children]

  for (let child of childrenArr) {
    element.append(render(child))
  }

  return element
}
```
