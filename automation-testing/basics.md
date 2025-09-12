-----
**var** - can be reassign and redeclare 

**let** - can be reassign and NOT redeclare 

**const** - can NOT be reassign and NOT redeclare
_____
const sorted = [...nums].sort((a, b) => a - b);  **//sorting**

const hash = {} **//object**

var result = new Array(nums.length);  **//array**

return [hash[targetMinusNum], i];  **//return 2 values - square brackets**
____
## FOR

for (let num of nums) {...} **//for every value (not index)**

for (let [i, num] of nums.entries()) {console.log(i, num); } **//for getting index**

array.forEach((element, index, array) => {...});

**for in objects**

``` const user = { name: "Kate", age: 30 };```
 
``` for (const key in user) {``` 

``` console.log(`${key}: ${user[key]}`);```

``` } ```
____
## MAP
array.map((element, index(*optional*), array(*optional*)) => {...})
#### example:
```const nums = [3, 1, 4];```

```const squared = nums.map((num) => num * num);```

```console.log(squared); // [9, 1, 16]```

----

```const map = new Map(); - built-in JavaScript object type```

```map - method on arrays```

```map.has(smth)```

```map.set(smth) (set(key, value)) - Adds/updates an entry with key and value```

```map.get(smth)```

```delete(key)	- Removes the entry by key ```

```clear()	    - Removes all entries from the map```

```size```
_____

| **Set Method**         | **Description**                                    |
|-------------------------|----------------------------------------------------|
| `new Set(iterable)`     | Creates a new Set                                  |
| `add(value)`            | Adds a new element to the Set                      |
| `delete(value)`         | Removes an element from the Set                    |
| `has(value)`            | Checks if value exists in the Set                  |
| `clear()`               | Removes all elements from the Set                  |
| `size`                  | Returns the number of elements                     |
| `forEach(callback)`     | Executes a function for each element               |
| `values()`              | Returns an iterator of values                      |
| `keys()`                | Same as `values()` (for compatibility)             |
| `entries()`             | Returns iterator `[value, value]` pairs            |

_____

| **Math Function**      | **Description**                                    |
|-------------------------|----------------------------------------------------|
| `Math.abs(x)`           | Returns absolute value of `x`                      |
| `Math.round(x)`         | Rounds `x` to nearest integer                      |
| `Math.floor(x)`         | Rounds `x` down (toward −∞)                        |
| `Math.ceil(x)`          | Rounds `x` up (toward +∞)                          |
| `Math.max(...values)`   | Returns largest value                              |
| `Math.min(...values)`   | Returns smallest value                             |
| `Math.sqrt(x)`          | Returns square root of `x`                         |
| `Math.pow(x, y)`        | Returns `x` to the power of `y`                    |
| `Math.trunc(x)`         | Removes fractional part of `x`                     |
| `Math.random()`         | Returns random number between 0 and 1              |


