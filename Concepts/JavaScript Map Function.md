The `map()` function is used to take a list (an array), apply a transformation to each element, and generate a **new list** with the transformed values.

Here’s a simple example:

```js
const numbers = [1, 2, 3, 4];
const doubled = numbers.map(num => num * 2);
console.log(doubled); // [2, 4, 6, 8]
```

Each number is multiplied by 2, and the `map()` function returns a new array with the results.

--- 

## Real-World Example

Let’s say you’re building the backend for an e-commerce site, and you want to generate a **customer list** from an array of **orders**.

```js
const orders = [
{ id: 1, name: "Bahri", productId: 5, amount: 1, date: "2025-05-18T10:30:00Z" },
{ id: 2, name: "Harun", productId: 3, amount: 2, date: "2025-05-18T10:30:00Z" },
{ id: 3, name: "Selim", productId: 9, amount: 5, date: "2025-05-18T10:30:00Z" },
];
```

### Extract Only Customer Names

```js
const customerNames = orders.map(order => order.name);
console.log(customerNames); // ["Bahri", "Harun", "Selim"]
```
### Extract Customer Name and Formatted Date

```js
const customerInfo = orders.map(order => ({
  customer: order.name,
  date: new Date(order.date).toLocaleDateString('en-US', {
    year: 'numeric',
    month: 'long',
    day: 'numeric'
  })
}));

console.log(customerInfo);
/*
[
  { customer: "Bahri", date: "May 18, 2025" },
  { customer: "Harun", date: "May 18, 2025" },
  { customer: "Selim", date: "May 18, 2025" }
]
*/
```

The `map()` function is perfect when you want to **transform** data. It keeps your original data untouched and gives you a new list based on the transformation you define.