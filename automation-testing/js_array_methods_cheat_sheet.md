# 🧰 JavaScript Array Methods & Properties Cheat Sheet

## 📦 Properties
| Property      | Description                                  | Example                    |
|---------------|----------------------------------------------|----------------------------|
| `length`      | Number of elements in the array              | `arr.length`               |
| `constructor` | Returns the array's constructor function     | `arr.constructor === Array`|

## 🔹 Adding/Removing Elements
| Method        | Description                                  | Example                      |
|---------------|----------------------------------------------|------------------------------|
| `push()`      | Adds to the end                              | `arr.push(4)`                |
| `pop()`       | Removes from the end                         | `arr.pop()`                  |
| `unshift()`   | Adds to the beginning                        | `arr.unshift(0)`             |
| `shift()`     | Removes from the beginning                   | `arr.shift()`                |
| `splice()`    | Adds/removes at a specific index             | `arr.splice(2, 1, 'new')`    |
| `slice()`     | Returns a shallow copy of a portion          | `arr.slice(1, 3)`            |

## 🔹 Searching/Checking
| Method         | Description                                 | Example                      |
|----------------|---------------------------------------------|------------------------------|
| `includes()`   | Checks if value exists                      | `arr.includes(3)`            |
| `indexOf()`    | First index of value                        | `arr.indexOf(2)`             |
| `lastIndexOf()`| Last index of value                         | `arr.lastIndexOf(2)`         |
| `find()`       | Finds first element that matches condition  | `arr.find(x => x > 5)`       |
| `findIndex()`  | Index of first element that matches         | `arr.findIndex(x => x > 5)`  |
| `some()`       | Returns true if at least one matches        | `arr.some(x => x > 10)`      |
| `every()`      | True if all elements match condition        | `arr.every(x => x > 0)`      |

## 🔹 Transforming Arrays
| Method         | Description                                 | Example                      |
|----------------|---------------------------------------------|------------------------------|
| `map()`        | Creates new array by applying function      | `arr.map(x => x * 2)`        |
| `filter()`     | Filters elements based on condition         | `arr.filter(x => x > 3)`     |
| `reduce()`     | Reduces array to single value               | `arr.reduce((a, b) => a + b)`|
| `flat()`       | Flattens nested arrays                      | `[[1],[2]].flat()`           |
| `flatMap()`    | `map()` followed by `flat()`                | `arr.flatMap(x => [x, x])`   |

## 🔹 Sorting & Reordering
| Method         | Description                                 | Example                      |
|----------------|---------------------------------------------|------------------------------|
| `sort()`       | Sorts the array in place                    | `arr.sort((a, b) => a - b)`  |
| `reverse()`    | Reverses the array in place                 | `arr.reverse()`              |

## 🔹 Combining & Joining
| Method         | Description                                 | Example                      |
|----------------|---------------------------------------------|------------------------------|
| `concat()`     | Combines arrays                             | `arr.concat([4, 5])`         |
| `join()`       | Joins into string                           | `arr.join(', ')`             |
| `toString()`   | Converts to string                          | `arr.toString()`             |