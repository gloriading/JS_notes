# JS_notes

## What is a predicate?
```
const lessThanTen = (x) =>  x < 10 
[1,7,15,22].filter( lessThanTen ) 
```
the function lessThanTen is the predicate here, which is applied to each item in the list.


## Immutability

* Example 1
```
let first_colour = {
  title: "apple",
  color: "red",
  rating: 2
}
// Method 1:
// const rateColour = (colour, rating) => Object.assign({}, colour, {rating})

// Method 2: (es6)
const rateColour = (colour, rating) => ({ ...colour, rating })

// copy all colours to a new object and update it's rating
// colour is an immutable object, need ({ }) , can't be just { }

console.log(rateColour(first_colour, 5).rating)

```

* example 2
```
const stuList = [
  {name: 'Amy'},
  {name: 'Ivy'},
  {name: 'Helen'}
];

// Method 1: use concat since it won't mutate the original 
// const addToList = (newItem, list) => (list.concat({newItem}))


// Method 2: es6
// copy the entire array to a new array and add newItem to it
const addToList = (newItem, list) => [...list, {newItem}];

console.log(addToList('Ben', stuList));
// Result:
/*
[ { name: 'Amy' },
  { name: 'Ivy' },
  { name: 'Helen' },
  { newItem: 'Ben' } ]
*/
console.log(stuList)
//[ { name: 'Amy' }, { name: 'Ivy' }, { name: 'Helen' } ]

```


## Call, Apply, Bind

*Example 1
```
const list = [1,2,3,4,5];

function add(){
  return Array.from(arguments).reduce(function(acc, cur){
    return acc + cur;
  });
}

add.call(null, 1,2) // 3
add.apply(null, list) // 15
const addOne = add.bind(null, 1)
addOne(2,2)//5
const addTen = add.bind(this, 10)
addTen(23)//33
```

*Example 2
```
const companyInfo = {
  companyName: "Google",
  location: "LA",
}

const greeting = function(firstName, lastName, department){
    return `Welcome ${firstName} ${lastName} to ${department} department of ${this.companyName} at ${this.location}`;
};

greeting.call(companyInfo, "Jackie", "Chan", "R&D")

const newHireInfo = ["Steve", "Rogers", "Security"]
greeting.apply(companyInfo, newHireInfo)

const welcomeMessage = greeting.bind(companyInfo)
welcomeMessage("Tony", "Stark", "Accounting")
```

## Arguments
`The arguments object is not an Array. It is similar to an Array, but does not have any Array properties except length. For example, it does not have the pop method. However it can be converted to a real Array:
`

*Example
```
function test(){
  console.log(arguments)
  // { '0': 'apple', '1': 12, '2': null, '3': {}, '4': [ 1, 2, 3, 4 ] }

  const arr1 = [].slice.call(arguments);
  console.log(arr1)
  const arr2 = [...arguments]
  console.log(arr2)
  const arr3 = Array.from(arguments)
  console.log(arr3)
  // the above three give array
  //[ 'apple', 12, null, {}, [ 1, 2, 3, 4 ] ]
}

test('apple', 12, null, {}, [1,2,3,4])
```
