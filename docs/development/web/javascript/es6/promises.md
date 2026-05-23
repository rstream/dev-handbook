# Promises

[← back](../index.md)

A promise represents a value that may be available later.
It can be fulfilled or rejected.

## Summary

- [Create a promise](#create-a-promise) - wrap async work
- [`then()`](#then) - handle success
- [`catch()`](#catch) - handle errors
- [`finally()`](#finally) - run cleanup
- [`Promise.all()`](#promiseall) - wait for several promises

## Create a promise

```js
const promise = new Promise((resolve, reject) => {
  const ok = true;

  if (ok) {
    resolve('Done');
  } else {
    reject(new Error('Failed'));
  }
});
```

Most modern APIs return promises, so you usually consume them instead of creating them manually.

## then

```js
fetch('/data.json')
  .then(response => response.json())
  .then(data => {
    console.log(data);
  });
```

`then()` returns a new promise, so calls can be chained.

## catch

```js
fetch('/data.json')
  .then(response => response.json())
  .catch(error => {
    console.error(error);
  });
```

## finally

`finally()` runs after success or failure.

```js
setLoading(true);

fetch('/data.json')
  .then(response => response.json())
  .finally(() => {
    setLoading(false);
  });
```

## Promise.all

`Promise.all()` waits for all promises.
It rejects when one of them rejects.

```js
const [user, settings] = await Promise.all([
  fetch('/user.json').then(response => response.json()),
  fetch('/settings.json').then(response => response.json())
]);
```
