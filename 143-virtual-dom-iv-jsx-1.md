And a video explaining this : 

https://www.youtube.com/watch?v=1-KkkYt7bRk


## without RegExp

```typescript


type JSXOpeningElement = {
  tag: string
}

type JSXClosingElement = {
  tag: string
}

type JSXChildren = string[]

type JSXElement= {
  openingElement: JSXOpeningElement
  children: JSXChildren
  closingElement: JSXClosingElement
}

function parse(code: string): JSXElement {

  let currentIndex = 0

  const goToNext = () => {
    currentIndex += 1
  }

  const goUntil = (reg: RegExp) => {
    const start = currentIndex

    while (currentIndex < code.length && !reg.test(code[currentIndex])) {
      currentIndex += 1
    }
    return code.slice(start, currentIndex)
  }

  const goUntilNonWhitespace = () => goUntil(/\S/)

  const expect = (char: string) => {
    if (code[currentIndex] !== char) {
      throw new Error('unexepcted token:' + code[currentIndex])
    }
  }

  // opening elements
  // (ignore spaces)
  // we expect first non-whitespace to be <
  // (ignore spaces)
  // expect name without <>
  // (ignore spaces)
  // expect >
  const parseOpeningElement = (): JSXOpeningElement => {
    goUntilNonWhitespace()
    expect('<')
    goToNext()
    goUntilNonWhitespace()
    const tag = goUntil(/<|>|\s/)

    const element = {
      tag
    }
    goUntilNonWhitespace()
    expect('>')
    goToNext()
    return element
  }

  const parseChildren = ():JSXChildren => {
    const text = goUntil(/<|>/)
    return [text]
  }

  const parseClosingElement = () => {
    expect('<')
    goToNext()
    goUntilNonWhitespace()
    expect('/')
    goToNext()
    goUntilNonWhitespace()
    const tag = goUntil(/<|>|\s/)
    const element = {
      tag
    }
    goUntilNonWhitespace()
    expect('>')
    goToNext()

    // there should no more non-whitespace characters
    goUntilNonWhitespace()
    return element
  }


  const openingElement = parseOpeningElement()
  const children = parseChildren()
  const closingElement = parseClosingElement()
  
  if (openingElement.tag !== closingElement.tag) {
    throw new Error('not matched')
  }

  // there should not be any extra characters
  if (currentIndex !== code.length) {
    throw new Error('unexepcted token')
  }
  return {
    openingElement,
    children,
    closingElement
  }
}

function generate(ast: JSXElement): string {
  const {openingElement, children} = ast
  if (children[0]) {
    return `h("${openingElement.tag}", null, "${children[0]}")`
  } else {
    return `h("${openingElement.tag}", null)`
  }
}



```


## with RegExp

```typescript


type JSXOpeningElement = {
  tag: string
}

type JSXClosingElement = {
  tag: string
}

type JSXChildren = string[]

type JSXElement= {
  openingElement: JSXOpeningElement
  children: JSXChildren
  closingElement: JSXClosingElement
}

function parse(code: string): JSXElement {
  const reg = /^\s*<\s*(\S+)\s*>([^<>]*)<\s*\/\s*(\S+)\s*>\s*$/
  const match = code.match(reg)
  if (match) {
    const element = {
      openingElement: {
        tag: match[1],
      },
      children: [match[2]],
      closingElement: {
        tag: match[3]
      }
    }
    if (element.openingElement.tag !== element.closingElement.tag) {
      throw new Error('no match')
    }
    return element
  } else {
    throw new Error('error')
  }
}

function generate(ast: JSXElement): string {
  const {openingElement, children, closingElement} = ast
  if (children[0]) {
    return `h("${openingElement.tag}", null, "${children[0]}")`
  } else {
    return `h("${openingElement.tag}", null)`
  }
}



```
