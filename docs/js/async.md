# async

## Experiments

The experiments show JS is single threaded and it will not run anything before work on the thread is done. UI is freezed when code is executed.

### Macro and Micro Tasks

Macro tasks:

```js
// Macro task (the whole program is macro task 1).
console.log(1);

// Macro task (the function passed to setTimeout scheduled as macro task 2).
setTimeout(() => {
  console.log(2);
});

console.log(3);
````
```output
1
3
undefined
> 2
```

Micro tasks are completed before the next macro task.

Micro tasks:

```js
// Macro task (the whole program is macro task 1).
console.log(1);

// Macro task (the function passed to setTimeout scheduled as macro task 2).
setTimeout(() => {
  console.log(2);
});

// Micro task (the function is added as micro task during exeuction of macro task 1 and
// will be executed after macro task 1 is finished).
queueMicrotask(() => {
  console.log(3);
});

console.log(4);
```
```output
1
4
3
2
```

A micro task create micro task:

```js
// Macro task (the whole program is macro task 1).
console.log(1);

// Macro task (the function passed to setTimeout scheduled as macro task 2).
setTimeout(() => {
  console.log(2);
});

// Micro task 1 (the function is added as micro task during exeuction of macro task 1 and
// will be executed after macro task 1 is finished).
queueMicrotask(() => {
  console.log(3);
  // Micro task 2 (the function is added as micro task during exeuction of macro task 2 and
  // will be executed after micro task 1 is finished).
  queueMicrotask(() => {
    console.log(4);
  });
});

console.log(5);
```
```output
1
5
3
4
2
```

A simple promise:

```js
console.log(1);

new Promise(function(resolve, reject) {
  console.log(2);
});

console.log(3);
```
```output
1
2
3
```

Async operation inside a promise:

```js
console.log(1);

new Promise(function(resolve, reject) {
  console.log(2);
  setTimeout(() => {
    console.log(3);
    resolve("result");
  });
});

console.log(4);
```
```output
1
2
4
3
```

Promise then:

```js
console.log("Starting macro task 1");

setTimeout(() => {
  console.log("Starting macro task 2");
});

const promise = new Promise(function(resolve, reject) {
  resolve("result");
});

// The micro task will be executed after the current macro task
promise.then(
  result => {
    console.log("Starting micro task 1");
  }
);

console.log("Ending   macro task 1");
```
```output
Starting macro task 1
Ending   macro task 1
Starting micro task 1
Starting macro task 2
```

Fetch result:

```js
function fetch_result() {
  return new Promise(function(resolve, reject) {
    resolve("result");
  });
}

console.log("Starting macro task 1");

setTimeout(() => {
  console.log("Starting macro task 2");
});

// The micro task will be executed after the current macro task
fetch_result().then(
  result => {
    console.log("Starting micro task 1");
  }
);

console.log("Ending   macro task 1");
```
```output
Starting macro task 1
Ending   macro task 1
Starting micro task 1
Starting macro task 2
```

`async` function is syntactic sugar for a function that returns a promise:

```js
async function fetch_result() {
  return "result";
}

console.log("Starting macro task 1");

setTimeout(() => {
  console.log("Starting macro task 2");
});

// The micro task will be executed after the current macro task
fetch_result().then(
  result => {
    console.log("Starting micro task 1");
  }
);

console.log("Ending   macro task 1");
```
```output
Starting macro task 1
Ending   macro task 1
Starting micro task 1
Starting macro task 2
```

`await` is syntactic sugar for `then`:

```js
console.log("Starting macro task 1");

setTimeout(() => {
  console.log("Starting macro task 2");
});

await new Promise(function(resolve, reject) {
    resolve("result");
  });

// The micro task will be executed after the current macro task
console.log("Starting micro task 1");
```
```output
Starting macro task 1
Starting micro task 1
Starting macro task 2
```

Using `async` and `await` together:

```js
async function fetch_result() {
  return "result";
}

console.log("Starting macro task 1");

setTimeout(() => {
  console.log("Starting macro task 2");
});

await fetch_result();

// The micro task will be executed after the current macro task
console.log("Starting micro task 1");
```
```output
Starting macro task 1
Starting micro task 1
Starting macro task 2
```

### Long Running Functions

This experiment shows that task cannot be interrupted:

Define functions:

```js
function longRunningFunction(aproxMilliseconds) {
  const start = Date.now();

  var bln = 1000000000;
  var i = 0;
  while (i < bln) {
    i++;
  }

  const measuredMilliseconds =  Date.now() - start;

  blns = (aproxMilliseconds - measuredMilliseconds)/measuredMilliseconds;

  var bln = Math.round(blns * bln);
  var i = 0;
  while (i < bln) {
    i++;
  }

  console.log("longRunningFunction finished");
}

function delayedResult(milliseconds) {
  setTimeout(() => {
    console.log("delayedResult finished");
  }, milliseconds);
}
```

```js
delayedResult(1000);
longRunningFunction(2000);
```
```output
longRunningFunction finished
delayedResult finished
```

```js
delayedResult(1000);
longRunningFunction(1000);
longRunningFunction(1000);
```
```output
longRunningFunction finished
longRunningFunction finished
delayedResult finished
```

## Resources

* [Event loop: microtasks and macrotasks. JAVASCRIPT.INFO.](https://javascript.info/event-loop)
* [Javascript Microtasks Vs Macrotasks. Sheldons Frontend Show.](https://www.youtube.com/watch?app=desktop&v=CbyAsXUCwCU)
