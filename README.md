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
