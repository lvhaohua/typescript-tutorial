# 基础类型

### Boolean

```typescript
let isDone: boolean = true; 
```

### Number

```typescript
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let octal: number = 0o744;
let big: bigint = 100n;
```

### String

```typescript
let color: string = "blue";
```

### Array

```typescript
let list: number[] = [1, 2, 3];
let list: Array<number> = [1, 2, 3];
```

### Tuple

```typescript
let x: [string, number];
x = ["hello", 10]; // OK
x = [10, "hello"]; // Error
```

### Enum

```typescript
enum Color {
  Red = 1, // 默认情况下，从0开始为元素编号
  Green,
  Blue,
}
let c: Color = Color.Green;
// 修改下标 
enum Color {
  Red = 1,
  Green = 2,
  Blue = 4
}
console.log(Color); // { '1': 'Red', '2': 'Green', '4': 'Blue', Red: 1, Green: 2, Blue: 4 } 
```

### Unknown

```typescript
let notSure: unknown = 4;
notSure = "maybe a string instead";
notSure = false;
```

### Any

```typescript
declare function getValue(key: string): any;
const str: string = getValue("myString"); // OK, return value of 'getValue' is not checked
```

### Void

```typescript
function warnUser(): void {
  console.log("This is my warning message");
}

let unusable: void = undefined;
unusable = null; // OK if `--strictNullChecks` is not given
```

### Null and Undefined

```typescript
let u: undefined = undefined;
let n: null = null;
```

### Never 

理解成函数永远不会有返回值

```typescript
function error(message: string): never {
  throw new Error(message);
}

function fail() {
  return error("Something failed");
}

function infiniteLoop(): never {
  while (true) {}
}
```

### Object

```typescript
declare function create(o: object | null): void;
create({ prop: 0 });
create(null);
```

### 类型断言

```typescript
let someValue: unknown = "this is a string";
let strLength: number = (someValue as string).length; 
// or
let strLength: number = (<string>someValue).length;
// 注：使用tsx时，只能使用 as
```

