Here is a video explaining : https://www.youtube.com/watch?v=8BJvvlQEoR0

```typescript

function normalize(hex: string): string {
  const digits = hex.toLowerCase().slice(1)

  if (digits.length === 3) {
    return [...digits].map(item => item.repeat(2)).join('') + 'ff'
  }

  if (digits.length === 4) {
    return [...digits].map(item => item.repeat(2)).join('')
  }

  if (digits.length === 6) {
    return digits + 'ff'
  }

  return digits
}

// max 2 digits for the fraction, 0 should be supressed
function roundUp(num: number): string {
  return num.toFixed(2).replace(/([.0]+)$/, '') || '0'
}

function hexToRgba(hex: string): string {
  // #fff 3
  // #ffff 4
  // #ffffff 6
  // #ffffffff 8

  // 1. validate
  // 2. normalize to 8 digits
  // 3. tranform to numbers
  // 4. compose the result
  const regValidHexColor = /^#[0-9a-fA-F]+$/ 
  if (![4,5,7,9].includes(hex.length) || !regValidHexColor.test(hex)) {
    throw new Error('input is invalid')
  }

  const normalized = normalize(hex)

  const regColorParts = /(.{2})(.{2})(.{2})(.{2})/
  const match = normalized.match(regColorParts)!

  const [r, g, b, a] = match.slice(1, 5).map(part => parseInt(part, 16))

  return `rgba(${r},${g},${b},${roundUp(a / 255)})`
}
```
