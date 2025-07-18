
# JavaScript String & Character Operations Cheat Sheet

## Creating Strings
```js
let str1 = "Hello";
let str2 = 'World';
let str3 = `Hello, ${str2}`;
```

## Basic Properties
- `length`: Returns the length of the string
```js
"hello".length; // 5
```

## Accessing Characters
- Use bracket notation or `.charAt()`
```js
"hello"[1];     // "e"
"hello".charAt(1); // "e"
```

## Common String Methods

### 1. `toUpperCase()` / `toLowerCase()`
```js
"hello".toUpperCase(); // "HELLO"
"WORLD".toLowerCase(); // "world"
```

### 2. `includes(substring)`
```js
"hello world".includes("world"); // true
```

### 3. `startsWith()` / `endsWith()`
```js
"hello".startsWith("he"); // true
"hello".endsWith("lo");   // true
```

### 4. `indexOf()` / `lastIndexOf()`
```js
"banana".indexOf("a");      // 1
"banana".lastIndexOf("a");  // 5
```

### 5. `slice(start, end)`
```js
"hello".slice(1, 4); // "ell"
```

### 6. `substring(start, end)`
```js
"hello".substring(1, 4); // "ell"
```

### 7. `substr(start, length)`
```js
"hello".substr(1, 3); // "ell"
```

### 8. `replace()` / `replaceAll()`
```js
"hello world".replace("world", "there"); // "hello there"
"foo foo".replaceAll("foo", "bar");      // "bar bar"
```

### 9. `split(separator)`
```js
"apple,banana,cherry".split(","); // ["apple", "banana", "cherry"]
```

### 10. `trim()` / `trimStart()` / `trimEnd()`
```js
"  hello  ".trim();      // "hello"
"  hello".trimStart();   // "hello"
"hello  ".trimEnd();     // "hello"
```

### 11. `repeat(n)`
```js
"ha".repeat(3); // "hahaha"
```

### 12. `padStart()` / `padEnd()`
```js
"5".padStart(3, "0"); // "005"
"5".padEnd(3, "0");   // "500"
```

### 13. `concat()`
```js
"Hello".concat(" ", "World"); // "Hello World"
```

## Character Codes

### `charCodeAt()` / `fromCharCode()`
```js
"A".charCodeAt(0);       // 65
String.fromCharCode(65); // "A"
```

## Template Literals
```js
let name = "Kate";
let greeting = `Hello, ${name}!`; // "Hello, Kate!"
```

---

**Tip:** Strings are immutable – all methods return new strings.

