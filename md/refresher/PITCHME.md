---

## ES6 Refresher

(with a bit of ES5)

Note:

- Things that you may not be familiar with today
- Common features you'll see and use in React code

+++

#### Arrow Functions

Does not define `this` in local scope

```javascript
(param1, param2, ..., paramN) => { statements }
(param1, param2, ..., paramN) => expression
() => { statements }
```

+++

#### Function Scope Binding

Maps `this` of the function to an explicit object

```javascript
function foo() {
    this.classMethod();
}

boundFoo = foo.bind(myClassInstance);
boundFoo();
```

+++

#### Array Map

Creates a new array with the result of calling the method on every element

```javascript
const arr = [1, 4, 9, 16];

const result = arr.map((x) => x * 2);

// expected output: Array [2, 8, 18, 32]
```

Note:

- Often used in React to render lists of things

+++

#### Array Filter

Creates a new array with all elements that pass the test method

```javascript
const words = [
    'spray', 'destruction', 'limit', 'elite', 'exuberant'
];

const result = words.filter((word) => word.length > 7);

// expected output: Array ["exuberant", "destruction"]
```

Note:

- Typically used to filter out a specific children when rendering in React

+++

#### Array Reduce

Creates a single output value by executing a reducer method on every element

```javascript
const arr = [1, 2, 3, 4];

const reducer = (accumulator, currentValue) => {
    return accumulator + currentValue;
};

// 1 + 2 + 3 + 4
const result = arr.reduce(reducer);

// Expected output: 10
```

+++

#### Rest Parameters

```javascript
function foo(a, b, ...other) {
    console.log('a', a);
    console.log('b', b);
    console.log('other', other);
}

foo('one', 'two', 'three', 'four', 'five', 'six');

// Console Output:
// a, one
// b, two
// other, [three, four, five, six]
```

+++

#### Spread Syntax

```javascript
const str = "hello";
const chars = [...str];
// ['h', 'e',' l',' l', 'o']

const parts = ['shoulders', 'knees'];
const lyrics = ['head', ...parts, 'and', 'toes'];
// ["head", "shoulders", "knees", "and", "toes"]
```

Note:

- Explodes any iterable objects into distinct values

+++

#### Destructuring

```javascript
const transform = { x: 10, y: 50, pitch: 0, yaw: 90 };

const { x, y, ...rotation } = transform;

console.log('x', x);
console.log('y', y);
console.log('rotation', rotation);

// Console Output:
// x, 10
// y, 50
// rotation, { pitch: 0, yaw: 90 }
```

Note:

- Extract keys from an object into variables
- Spread syntax used to extract everything not already extracted into a single variable
- Used in React to pass a subset of properties down to a child Component




