A video explaining this

https://www.youtube.com/watch?v=FBhQefg8fx4

```js
/**
 * MyElement is the type your implementation supports
 *
 * type MyNode = MyElement | string
 */

/**
 * @param { string } type - valid HTML tag name
 * @param { object } [props] - properties.
 * @param { ...MyNode} [children] - elements as rest arguments
 * @return { MyElement }
 */
function createElement(type, props, ...children) {
  return {
    type,
    props: {
      ...props,
      children
    }
  }
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
