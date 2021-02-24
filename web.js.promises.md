# Promises

[dev.to](https://dev.to/spartakyste/the-promises-guide-i-would-have-loved-as-a-junior-developper-3621)

A `Promise` is a proxy for a value not necessarily known when the promise is created. It allows you to associate handlers with an asynchronous action's eventual success value or failure reason. This lets asynchronous methods return values like synchronous methods: instead of immediately returning the final value, the asynchronous method returns a promise to supply the value at some point in the future.

## Structure

An example of a very basic Promise:

```javascript
new Promise((resolve, reject) => {
  // Your asynchronous code
});
```

A promise always take a function with two arguments: resolve and reject. When the promise must return the result, it calls resolve with the results. If something wrong happened it calls reject.

```javascript
// Promises can be stored in a variable, or returned within a function
const preparingDishes = new Promise((resolve, reject) => {
  const isIngredientMissing = false;
  const dishes = [
    // Everything that the client ordered, it would be filled up as soon as one is ready
  ];
  // But if an ingredient is missing, immedialty call back the waiter to inform the clients
  if (isIngredientMissing) return reject('An ingredient is missing !');

  // We use setTimeout to mimic an HTTP call
  setTimeout(() => {
    // 10 seconds later, once the dishes are ready, send them to the waiter
    return resolve(dishes);
  }, 10000);
});

console.log(preparingDishes); // <---- Promise {pending}
```

To fix Promise {pending}:

```javascript
const preparingDishes = new Promise((resolve, reject) => {
  // See the code above
});

// Now that our promise is created, let's trigger it, and then read the results
preparingDishes
  .then((dishes) => {
    // dishes is a arbitrary name, usually it's called result

    /* Within this function, we can access the result of the promise. The parameter will be the value you gave to the resolve.
    You are guaranted that anything you put in here, will execute when the promise is fullfilled (succesfull) */
    callWaiter(dishes);
  })
  .catch((error) => {
    // In case an error happened, this handler will catch the return value inside your above reject or any error that could happen in your promise code
    if (error === 'An ingredient is missing !') {
      sendWaiterBacktoClients();
    }
  })
  .finally(() => {
    // This one will execute anything that you put inside, either the promise succeed or not

    // For example, wether the kitchen succeed preparing the dishes or not, they'll have to start the next one
    prepareNextDishes();
  });
```

Please take note that attaching all the handlers isn't mandatory, you could only attach a .then for example or only a .then and a .catch(which is what you'll use most of the time).

## Async / Await

Note that async/await is nothing more than syntactic sugar for promises.

```javascript
// Function must be async to use the await keyword
async function waiterJob() {
  try {
    const dishes = await preparingDishes;
  } catch (error) {
    // Handle the error
  }
}
```

The async/await syntax is much cleaner (a function with the keyword async, a try/catch block, and the await keyword).

- The `await` keyword can only be used within an async function.
  - It replace the .then, you must not use it in conjuncution with .then/.catch.
- Making a function `async` will enforce it's return value to be a promise.
- To handle errors properly, you must wrap your promise call within a try/catch block.
