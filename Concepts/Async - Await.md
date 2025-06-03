In JavaScript, certain tasks like fetching data from the internet or reading from a file system take time to complete. These are asynchronous operations.

Let’s start by looking at how we used to handle such tasks using `.then()` chaining:

```js
getCar(1).then(car => {
	console.log(`Car is ${car.name}`);
	return getCarBrand(car.id);
	}).then(brand => {
		console.log(`Car's brand is ${brand}`);   
	}).catch(error => {
		console.log(`Oops, something went wrong: ${error}`);   
	});
```

This works, but as the number of steps increases, the code becomes harder to read and maintain due to nested `.then()` calls. Now let’s simplify this using `async/await`:

```js
async function showCarDetails() {
  try {
    const car = await getCar(1); // Fetches data from API
    const brand = await getCarBrand(car.id);

    console.log(`Car is ${car.name}`);
    console.log(`Car's brand is ${brand}`);
  } catch (error) {
    console.log(`Oops, something went wrong: ${error}`);
  }
}
```

Here, `await` tells JavaScript to wait for the result of each promise before moving on. This makes the code look and behave more like regular synchronous code, which is easier to understand.

---

## Running Asynchronous Tasks in Parallel

By default, using `await` one after another causes each task to wait for the previous one to finish:

```js
async function fetchData() {
  const users = await fetch('/api/users'); // takes 1s
  const foods = await fetch('/api/foods'); // takes 2s
  const cars = await fetch('/api/cars');   // takes 1s
  const jobs = await fetch('/api/jobs');   // takes 2s
} // Total time: ~6s
```

This approach works, but it’s not the most efficient. Instead of running these tasks sequentially, we can run them **in parallel** to save time:

```js
async function fetchData() {
  const usersPromise = fetch('/api/users');  // starts immediately
  const foodsPromise = fetch('/api/foods');
  const carsPromise = fetch('/api/cars');
  const jobsPromise = fetch('/api/jobs');

  const [users, foods, cars, jobs] = await Promise.all([
    usersPromise,
    foodsPromise,
    carsPromise,
    jobsPromise,
  ]);
} // Total time: ~2s (fastest possible)
```

### Why This Works

`Promise.all()` is a built-in JavaScript method that allows you to run multiple promises in parallel. It takes an array of promises and returns a single promise that resolves when **all** of them have resolved—or rejects if **any** of them fail.

This approach improves performance by not waiting unnecessarily. You start all the tasks at once and wait for the results collectively.