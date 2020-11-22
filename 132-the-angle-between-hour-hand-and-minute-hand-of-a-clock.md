
```js

/**
 * @param {string} time
 * @returns {number} 
 */
function angle(time) {
  // your code here
  const [hour, min] = time.split(':').map((seg) => parseInt(seg, 10))
  
  const h = (hour >= 12 ? hour - 12 : hour)
  const m = min

  const angleMin = (m / 60) * 360
  const angleHour = (h / 12) * 360 + angleMin / 12

  
  const angle = Math.abs(angleHour - angleMin)
  const finalAngle = angle > 180 ? 360 - angle : angle
  return Math.round(finalAngle)
}
```

And a video explaining it https://www.youtube.com/watch?v=KmEhoAfcpKM
