And a video explaining this 
https://www.youtube.com/watch?v=FpKnR7RQaHM

```js

/**
  * @param { any[] } arr
  */

// not the right shuffle
// function shuffle(arr) {
//   for (let i = 0; i < arr.length; i++) {
//     const j = Math.floor(Math.random() * arr.length)
//     ;[arr[i], arr[j]] = [arr[j], arr[i]]
//   }
// }

// [1, 2, 3]


// step1: first digit to be 1: 1/3
// step2: first digit to be 3: 1/3

// 1, 2, 3, 1: 1/3, 3: 0
// 2, 1, 3, 1: 1/3, 3: 0
// 3, 2, 1, 1: 0, 3: 1/3

function shuffle(arr) {
  for (let i = 0; i < arr.length; i++) {
    const j = i + Math.floor(Math.random() * (arr.length - i))
    ;[arr[i], arr[j]] = [arr[j], arr[i]]
  }
}
```
