Here is a video of my explaining it : https://www.youtube.com/watch?v=uWfi9UaVyKo



```typescript



function canWinStonePicking(n: number): 'A' | 'B' | null {
  if (n === 1) return 'B'
  if (n === 2) return 'A'

  const canFirstWin = new Map([[1, false],[2, true]])
  const canSecondWin = new Map([[1, true],[2, false]])

  for (let i = 3; i <= n; i++) {
    canFirstWin.set(i, (canSecondWin.get(i - 2) || canSecondWin.get(i - 1))!);
    canSecondWin.set(i, (canFirstWin.get(i - 2) && canFirstWin.get(i - 1))!);
    canFirstWin.delete(i - 2)
    canSecondWin.delete(i - 2)
  }

  return canFirstWin.get(n) ? 'A' : canSecondWin.get(n) ? 'B' : null
}

```
