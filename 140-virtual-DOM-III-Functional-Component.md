And this is a video explaining https://www.youtube.com/watch?v=hgAIfW2xNok

```javascript
/**
 * MyElement is the type your implementation supports
 *
 * type MyNode = MyElement | string
 * type FunctionComponent = (props: object) => MyElement
 */

/**
 * @param { string | FunctionComponent } type - valid HTML tag name or Function Component
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
 * @param { MyElement }
 * @returns { HTMLElement } 
 */
function render(json) {
  // create the top level emlement
  // recursively append the children
  // textnode
  if (typeof json === 'string') {
    return document.createTextNode(json)
  }

  // element
  const {type, props} = json
  const {children, ...attrs} = props

  // if functional component
  if (typeof type === 'function') {
    return render(json.type(props))
  }
  
  // if intrinsic html tag
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
