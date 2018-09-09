# JS_notes

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
