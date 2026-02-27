# JAVASCRIPT-Objects

### 🧱 What an Object Is
- A container to store pieces of data as a **property**:
  - **key** (the name) and its **value**.
  - Properties are the names of the data in the object.
  - Objects can values of type: strings, numbers, arrays, functions, or even other objects.

```js
const person = {
  name: "Alice",
  age: 30,
  city: "New York"
};
```
---

### 🎯 How to Access Object Properties

#### 1. Dot notation (simple and common)
- Use on properties as valid JavaScript identifier (no spaces, no starting numbers).

```js
person.name; // "Alice"
person.age;  // 30
```

#### 2. Bracket notation (more flexible)
Use when:
- The property name
    - has spaces
    - special characters
    - starts with a number
    - accessing a property using a variable  

```js
person["city"]; // "New York"

const key = "name";
person[key]; // "Alice"
```

Works with unusual keys:

```js
const obj = {
  "1stProperty": "Hello",
  "property with spaces": "World"
};

obj["1stProperty"];          // "Hello"
obj["property with spaces"]; // "World"
```
---

### 🗑️ Removing/Mutating a Property with `delete` from the object
```js
const person = {
  name: "Alice",
  age: 30,
  job: "Engineer"
};

delete person.job;
console.log(person.job); // ***UNDEFINED***
```
---
### ✂️ Removing Properties by Creating a New Object
- Destructuring with the rest operator **builds a new object** that excludes the properties you pull out.
- You want immutability or need a clean copy without certain keys

```js
const person = {
  name: "Bob",
  age: 25,
  job: "Designer",
  city: "New York"
};

const { job, city, ...remaining } = person;

console.log(remaining); // { name: "Bob", age: 25 }
```
---

### 🔍 Checking if a Property Exists

#### **1. `hasOwnProperty()` — checks the object’s own keys** Returns **true** if the property exists
```js
person.hasOwnProperty("name"); // true
person.hasOwnProperty("job");  // false
```
---

#### **2. `in` operator — checks own + inherited properties exists anywhere on the object.** Returns **true**

```js
"name" in person; // true
```
---
#### **3. Comparing to `undefined` — check if property missing then returns `undefined`**.

```js
car.brand !== undefined; // true
car.color !== undefined; // false
car.color !== undefined; // fails if property is actually 'undefined'
```
---

### 🧠 Choosing the Right Method
- Use **`hasOwnProperty()`** when you want the safest, most explicit check.  
- Use **`in`** when inherited properties should count.  
- Use **`!== undefined`** only for quick checks when you know values won’t be `undefined`.
---

## Accessing Properties in Nested Objects and Arrays
- Requires **chaining** dot/bracket notation

### Dot notation
```js
const person = {
  name: "Alice",
  age: 30,
  contact: {
    email: "alice@example.com",
    phone: {
      home: "123-456-7890",
      work: "098-765-4321"
    }
  }
};

console.log(person.contact.phone.work);
098-765-4321
```

### Bracket notation
- Best when keys are variables or contain spaces/special characters.

```js
console.log(person['contact']['phone']['work']);
098-765-4321
```
---

## Accessing Arrays Inside Objects Access the **index first**, then the property.

```js
const person = {
  name: "Alice",
  age: 30,
  addresses: [
    { type: "home", street: "123 Main St", city: "Anytown" },
    { type: "work", street: "456 Market St", city: "Workville" }
  ]
};

console.log(person.addresses[1].city);
Workville
```

- `person.addresses` → the array  
- `[1]` → second item  
- `.city` → property inside that object  

---

## Why Some console.Logs Show Nothing --> the path doesn’t exist, so result is `undefined`.

### Example of a broken path
```js
console.log(person.contact.phone.mobile);
`undefined`
```
### Wrong array index
```js
console.log(person.addresses[5].city);
`undefined`
```
---
### 🧱 Primitive Types (value-based) **number, string, boolean, null, undefined, symbol, bigint**.
- They store the actual value, and each variable gets its **own copy**.
- Immutable, copied independently.  

Primitive types are 

```js
let num1 = 5;
let num2 = num1;   // recieves its own copy of the value
num1 = 10;          // reassing num1 but not num1 it stil has same value

console.log(num2);
```
Changing `num1` does **not** affect `num2` because primitives are copied by value
---

### 🧩 Non‑Primitive Types (reference-based)  *Objects, arrays, and functions*
- **Objects are stored by reference**
- Variables point to the object in memory, not the object
- Mutable, shared between variables. 

```js
const originalPerson = { name: "John", age: 30 };
const copiedPerson = originalPerson;  // both point to same object

originalPerson.age = 31;

console.log(copiedPerson.age);
31
```
Updating one reference updates the shared object, so all variables pointing to it see the change.
---
### 🧩 What Functions Are
- Independent pieces of code that take input and return output.

```js
function greet(name) {
  return "Hello, " + name + "!";
}

console.log(greet("Alice"));
Hello, Alice!
```
### 🧱 What is an Object Methods 
- Functions defined in a object **as properties of an object** specific to that object.
- They access any of the object's data usiing the `this` keyword.
- Called --> (person.sayHello()

```js
const person = {
  name: "Bob",
  age: 30,
  sayHello: function() {
    return "Hello, my name is " + this.name;
  }
};

console.log(person.sayHello());
Hello, my name is Bob
```
---

### 🧩 The Object() Constructor creates Objects like an object literal (`{ }`)

```js
const obj = new Object();
console.log(obj);              --> `new Object()` creates an **empty object**
{}
```
```js
const num = 42;            -->  *without** `new`, converts primitives --> object 
const numObj = Object(num);
                            --> Converts unknown values to objects 
console.log(numObj);
console.log(typeof numObj);
[Number: 42]
object
```

### 🧱 How It Handles Special Values
Passing `null` or `undefined` --> empty object:

```js
const newObj = new Object(undefined);
console.log(newObj);
{}
```
### 🔧 Constructor helps When 
- Uou need to **ensure a value is an object**

```js
function toObject(value) {
  if (value === null || value === undefined) return {};
  if (typeof value === "object") return value;
  return Object(value);
}

console.log(toObject(null)); --> {}
console.log(toObject(true)); --> [Boolean: true]
console.log(toObject([1, 2, 3])); ---> [ 1, 2, 3 ]
```
---

### What JSON (*JavaScript Object Notation*) is a format used to exchange data between applications.
- behaves like a normal JavaScript object once parsed or imported
- Supports objects, arrays, strings, numbers, booleans, and null. Keys in **double quotes**.

Example JSON:
```json
{
  "name": "Alice",
  "age": 30,
  "isStudent": false,
  "list of courses": ["Mathematics", "Physics", "Computer Science"]
}
```
---

### Accessing JSON Values with Dot Notation
- For keys as valid identifier (no spaces or special characters).

```js
console.log(data.age);
30
```
---

### Accessing JSON Values with Bracket Notation
- For KEYS THAT CONTAIN SPACES OR SYMBOLS

```js
console.log(data["list of courses"]);
["Mathematics", "Physics", "Computer Science"]
```
```
Bracket notation also works with variables:
```js
const key = "name";
console.log(data[key]);
Alice
```
---

### 🟦 JSON.stringify() (Objects → JSON Strings)
--> converts a JS object **into a JSON string** TO STORE OR SEND OVER A NETWORK.

```js
const user = { name: "John", age: 30, isAdmin: true };
const jsonString = JSON.stringify(user);
console.log(jsonString);
{"name":"John","age":30,"isAdmin":true}
```
#### Optional: Replacer (choose which properties to include)
```js
console.log(JSON.stringify(developerObj, ["firstName", "country"]));
{"firstName":"Jessica","country":"USA"}
```
#### Optional: Spacing (pretty-printing)
```js
console.log(JSON.stringify(developerObj, null, 2));
{"firstName":"Jessica","country":"USA"}
```

### 🟩 `JSON.parse()` JSON Strings → Objects  **back into a JavaScript object**

```js
const jsonString = '{"name":"John","age":30,"isAdmin":true}';
const userObject = JSON.parse(jsonString);
console.log(userObject);
{ name: 'John', age: 30, isAdmin: true }
```
Now you can access properties normally:
```js
console.log(userObject.age); // 30
```
---
 lets you safely access deeply nested properties without throwing errors when something in the chain is missing. Instead of crashing, it returns **`undefined`**.

---

### 🌐 The optional chaining operator **`?.`**  PURPOSE:
- Accessing a missing nested property --> throws an error:
- `?.` stops the lookup if the value is **null** or **undefined**.
##### object?.key

```js
const person = { name: "Alice", age: 30 };
console.log(person.address.street);
TypeError: Cannot read properties of undefined
Because `person.address` does not exist.
```
---

### 🛡 How Optional Chaining Works
- Checks If the value before `?.` is **null or undefined**
- If YES --> EXPRESSION is **undefined** but does not crashing.

```js
const user = {
  name: "John",
  profile: {
    email: "john@example.com",
    address: { street: "123 Main St", city: "Somewhere" }
  }
};

console.log(user?.profile?.address?.street);
123 Main St
```

If a property doesn’t exist:

```js
console.log(user?.profile?.phone?.number); --> undefined
```
---

### What destructuring does **extract properties from an object into variables**
- with matching names.

```js
const person = { name: "Alice", age: 30, city: "New York" };
const { name, age } = person;

console.log(name); // Alice
console.log(age);  // 30
```
---

### Renaming extracted variables
You can assign a property to a variable with a different name.

```js
const { name: personName, age: personAge } = person;

console.log(personName); // Alice
console.log(personAge);  // 30
```
---

### Default values - used so if property not provided then a fallback.

```js
const { country = "Unknown" } = person;
console.log(country); // Unknown
```
---

### Nested destructuring - **extract value in 1 step for nested objects.*

```js
const recipe = {
  name: "Chocolate Cake",
  ingredients: { flour: "2 cups", sugar: "1 cup" }
};

const { ingredients: { flour } } = recipe;
console.log(flour); // 2 cups
```
---
### Shorthand object creation - **variableName = property Name*

```js
let name = "Bob";
let age = 25;

let personObj = { name, age };
console.log(personObj); // { name: "Bob", age: 25 }
```
```js
-->returning objects from functions.
function createPerson(name, age) {
  return { name, age };
}

console.log(createPerson("Charlie", 35));
// { name: "Charlie", age: 35 }
```
---
# Review:
## 🧩 Object Basics
- JavaScript objects store data as **key–value pairs**,
- Objects hold properties, accesed by **dot** or **bracket** **Notation**.
---
## 🗑 Removing Properties
Use **delete** to remove a property.
---
## 🔍 Checking for Properties
- **hasOwnProperty()** checks if the object has key.
- **in** checks if the key exists anywhere on the object.
---
## 🧱 Nested Objects
- Access by chaining.
---
## 🧬 Primitive vs. Non‑Primitive Types
- **Primitive types** store **values directly** and are **copied by value**.
- **Non‑primitive types** **references** and are **copied by reference**.
---
## 🧩 Object Methods Functions in objects
---
## 🏗 Object Constructor
`new Object()` creates an empty object, though `{}` is preferred.
---
## 🛡 Optional Chaining (?.)
- Check property exists and Prevents errors .
---
## 🧰 Object Destructuring
- Extract properties into variables quickly.

```js
const person = { name: "Alice", age: 30 };
const { name, age } = person;

console.log(name); // Alice
console.log(age);  // 30
```
---
## 📦 Working with JSON -text format for storing and sending data.

### Convert object → JSON string -> JSON.stringify({object})

### Convert JSON string → object -->JSON.parse(`string`)


