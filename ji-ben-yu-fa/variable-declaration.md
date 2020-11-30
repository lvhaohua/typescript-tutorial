# 类型声明

### 一、**var**

1. 变量提升
2. 可重复声明
3. 全局作用域下会挂载到window下

### **二、let**

**1.块级作用域**

```typescript
function f(input: boolean) {
    let a = 100;

    if (input) {
        // Still okay to reference 'a'
        let b = a + 1;
        return b;
    }

    // Error: 'b' doesn't exist here
    return b;
}
```

**2.不可重复声明**

```typescript
let x = 10;
let x = 20; // 错误，不能在1个作用域里多次声明`x`
```

**3.暂时性死区**

```typescript
a++; // illegal to use 'a' before it's declared;
let a;
```

**4.不会在全局作用域下挂载到window下**

```typescript
var a = 1; // window.a === 1
let b = 1; // window.b === undefined
```

### **三、const**

**1.声明必须赋值**

**2.声明的变量值不可改变其引用，但可改变其引用指向的值**

**3.其他同let**

注：能使用const的地方就使用const，其他用let。

### 四、Destructuring - 解构

**1.数组解构**

```typescript
let input = [1, 2];
let [first, second] = input;
console.log(first); // outputs 1
console.log(second); // outputs 2

// swap variables
[first, second] = [second, first];

let [first, ...rest] = [1, 2, 3, 4];
console.log(first); // outputs 1
console.log(rest); // outputs [ 2, 3, 4 ]

let [, second, , fourth] = [1, 2, 3, 4];
console.log(second); // outputs 2
console.log(fourth); // outputs 4
```

**2.元祖解构**

```typescript
let tuple: [number, string, boolean] = [7, "hello", true];
let [a, b, c] = tuple; // a: number, b: string, c: boolean

let [a, b, c, d] = tuple; // Error, no element at index 3

let [a, ...bc] = tuple; // bc: [string, boolean]
let [a, b, c, ...d] = tuple; // d: [], the empty tuple

let [a] = tuple; // a: number
let [, b] = tuple; // b: string
```

**3.对象解构**

```typescript
let o = {
  a: "foo",
  b: 12,
  c: "bar",
};
let { a, b } = o;

({ a, b } = { a: "baz", b: 101 });

// rest
let { a, ...passthrough } = o;
let total = passthrough.b + passthrough.c.length;

// rename
let { a: newName1, b: newName2 } = o;

// default value
function keepWholeObject(wholeObject: { a: string; b?: number }) {
  let { a, b = 1001 } = wholeObject;
}
```

### 五、函数声明

```typescript
function f({ a, b = 0 } = { a: "" }): void {
  // ...
}
f({ a: "yes" }); // ok, default b = 0
f(); // ok, default to { a: "" }, which then defaults b = 0
f({}); // error, 'a' is required if you supply an argument
```

### 六、Spread - 展开

```typescript
// in array
let first = [1, 2];
let second = [3, 4];
let bothPlus = [0, ...first, ...second, 5];
// in obj
let defaults = { food: "spicy", price: "$$", ambiance: "noisy" };
let search = { ...defaults, food: "rich" };

// 仅包含可枚举的属性
class C {
  p = 12;
  m() {}
}
let c = new C();
let clone = { ...c };
clone.p; // ok
clone.m(); // error!
```

