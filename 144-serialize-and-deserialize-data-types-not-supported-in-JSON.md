Here is a video explaining it : https://www.youtube.com/watch?v=5iYJzXMtwCo

```typescript



type SerializablePrimitives = undefined | null | number | string | bigint | boolean

type Serializable = {
  [index: string]: Serializable
} | Serializable[] | SerializablePrimitives


type DataTypeUndefined = {
  type: 'undefined',
  value: 'undefined'
}

type DataTypeNull = {
  type: 'null',
  value: 'null'
}

type DataTypeNumber = {
  type: 'number',
  value: string // NaN, Infinity
}

type DataTypeString = {
  type: 'string',
  value: string
}

type DataTypeBigInt = {
  type: 'bigint',
  value: string // without the n
}

type DataTypeBoolean = {
  type: 'boolean',
  value: boolean
}

type DataTypeWrapperPrimitives = 
  | DataTypeUndefined 
  | DataTypeNull 
  | DataTypeNumber 
  | DataTypeString 
  | DataTypeBigInt
  | DataTypeBoolean

type DataTypeObjectLiteral = {
  type: 'ObjectLiteral',
  value: Record<string, DataTypeWrapper>
}

type DataTypeArray = {
  type: 'Array',
  value: DataTypeWrapper[]
}

type DataTypeWrapper = 
  | DataTypeObjectLiteral 
  | DataTypeArray 
  | DataTypeWrapperPrimitives

const wrap = (data: Serializable, visited = new Set()): DataTypeWrapper => {
  switch (typeof data) {
    case 'undefined':
      return {
        type: 'undefined',
        value: 'undefined'
      }
    case 'string':
      return {
        type: 'string',
        value: data
      }
    case 'number':
      return {
        type: 'number',
        value: data.toString() // to support NaN, Infinity
      }
    case 'bigint':
      return {
        type: 'bigint',
        value: data.toString() // without n
      }
    case 'boolean':
      return {
        type: 'boolean',
        value: data
      }
    case 'object':
      if (data === null) 
        return {
          type: 'null',
          value: 'null'
        }
      
      if (visited.has(data)) {
        throw new Error('circular reference found')
      }
      visited.add(data)

      if (Array.isArray(data)) {
        return {
          type: 'Array',
          value: data.map((item) => wrap(item, new Set(visited)))
        }
      }

      // default treats as Object Literal
      {
        const keys = Object.keys(data)

        const value = keys.reduce((result, key) => {
          result[key] = wrap(data[key], new Set(visited))
          return result
        }, {} as Record<string, DataTypeWrapper>)

        return {
          type: 'ObjectLiteral',
          value
        }
      }

    default:
      throw new Error('unsupported data type')
  }
}


const unwrap = (wrapper: DataTypeWrapper): Serializable => {
  switch (wrapper.type) {
    case 'undefined':
      return undefined
    case 'null':
      return null
    case 'number':
      return Number(wrapper.value)
    case 'string':
      return wrapper.value
    case 'bigint':
      return BigInt(wrapper.value)
    case 'boolean':
      return wrapper.value
    case 'ObjectLiteral':
      const keys = Object.keys(wrapper.value)

      return keys.reduce((result, key) => {
        result[key] = unwrap(wrapper.value[key])
        return result
      }, {} as Record<string,Serializable>)

    case 'Array':
      return wrapper.value.map(unwrap)
    default:
      throw new Error('unexpected data')
  }
}

const stringify = (data: Serializable): string => {
  // transform all data types to {type: string, value: any}
  // then JSON.stringify()
  return JSON.stringify(wrap(data))
}

const parse = (data: string): Serializable => {
  return unwrap(JSON.parse(data))
}

```
