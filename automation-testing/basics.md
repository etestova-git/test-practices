-----
Var - can be reassign and redeclare, 
let - can be reassign and NOT redeclare, 
const - can NOT be reassign and NOT redeclare
_____
const sorted = [...nums].sort((a, b) => a - b); - sorting

const hash = {} - object

var result = new Array(nums.length); - array

return [hash[targetMinusNum], i]; - return 2 values - square brackets
____
##FOR##

for (let num of nums){...} //for every value (not index)
for (let [i, num] of nums.entries()) {console.log(i, num);} // for getting index

array.forEach((element, index, array) => {...});

const user = { name: "Kate", age: 30 };
for (const key in user) {      // for in objects
  console.log(`${key}: ${user[key]}`);
}
____
##MAP##
array.map((element, index(*optional*), array(*optional*)) => {...})
####example:####
- const nums = [3, 1, 4];
- const squared = nums.map((num) => num * num);
- console.log(squared); // [9, 1, 16]

- const map = new Map(); built-in JavaScript object type
- map - method on arrays
- map.has(smth) methods provided by the Map object
- map.set(smth)(set(key, value) Adds/updates an entry with key and value
- map.get(smth)
- delete(key)	!Removes the entry by key!
- clear()	    !Removes all entries from the map!
- size
_____
