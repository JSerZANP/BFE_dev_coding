Also a video explaining this https://www.youtube.com/watch?v=YgdSt-TXio4


```js
/* you can use this Queue which is bundled together with your code
class Queue {
  enqueue(element) {
    // add new element to the queue
  }
  peek() { 
    // return the head element
  }
  dequeue() { 
    // remove head element from the queue
  }
  size() { 
    // return the queue size
  }
}
*/

// [],  [1,2]
// [3],[1,2]


// 1. when 1 element, stack === queue
// 2. use 2 queues, 1 is for pop with length 1
class Stack {
  constructor() {
    this.queue1 = new Queue()
    this.queueRest = new Queue()
  }
  
  push(element) {
    this.queue1.enqueue(element)
    this._move()
  }
  
  _move() {
    while (this.queue1.size() > 1) {
      this.queueRest.enqueue(this.queue1.dequeue())
    }
  }
  
  peek() { 
    return this.queue1.peek()
  }
  pop() {
    if (this.queue1.size() === 0) {
      return undefined
    }
    
    const element = this.queue1.dequeue()
    
    // swap if the other queue is not empty
    if (this.queueRest.size() > 0) {
      ;[this.queue1, this.queueRest] = [this.queueRest, this.queue1]
      this._move()
    }
    
    return element
  }
  size() { 
    return this.queue1.size() + this.queueRest.size()
  }
}
```
