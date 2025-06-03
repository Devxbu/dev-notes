### `useEffect()` – A React Hook for Side Effects

### What Is a Side Effect?

A **side effect** is any action that happens **outside of rendering the UI**.  
Think of it like this: you're cooking food and you set a timer for 3 minutes. Each time it rings, you check on the food.  
The checking is not part of the cooking itself — it’s a side effect triggered by the timer.

In React, side effects include things like:

- Fetching data from an API
    
- Subscribing to a data stream
    
- Manually changing the DOM
    
- Setting a timer or interval

---

Before React introduced Hooks, class components were the main way to handle side effects using lifecycle methods like `componentDidMount()` or `componentDidUpdate()`.

For example, if we want to fetch data when a component loads **and** when the `userId` prop changes, we would need multiple lifecycle methods in a class component. With Hooks, `useEffect()` simplifies this.

---

### Syntax of `useEffect()`

```js
useEffect(() => {
  // Side effect runs when dependencies change
}, []);
```

### Example

```js
useEffect(() => {
  // Fetch new data when the user ID changes
  fetch(`http://localhost:8000/api/user/${userId}`)
    .then((response) => response.json())
    .then((data) => {
      setData(data);
    });
}, [userId]); // Dependency array
```

The function inside `useEffect()` runs when the component renders and whenever one of the **dependencies** in the array changes — in this case, `userId`.

---

## Real-Time Data Example

`useEffect()` is especially useful when we want the component to respond immediately after the data changes.  
For example, in a financial application where data updates every second:

```js
useEffect(() => {
  // Fetch stock prices immediately on render
  fetch_stock_prices(); 

  // Set up a 1-second interval to fetch prices continuously
  const intervalId = setInterval(fetch_stock_prices, 1000); 

  // Cleanup interval when component unmounts
  return () => clearInterval(intervalId);
}, []);
```

---

### Cleanup Function

The function returned inside `useEffect()` is called a **cleanup function**.  
React calls this function when the component is about to be removed from the screen (unmounted).

This is important to **prevent memory leaks** — for example, stopping an interval when the user navigates away.

In short:

- `useEffect` runs your side effect
    
- The **dependency array** controls when it runs
    
- The **cleanup function** handles what happens when the component goes away