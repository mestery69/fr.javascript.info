

```js run
Function.prototype.defer = function(ms) {
  let f = this;
  return function(...args) {
    setTimeout(() => f.apply(this, args), ms);
  }
};

// vérifier
function f(a, b) {
  alert( a + b );
}

f.defer(1000)(1, 2); // montre 3 après 1 seconde
```

Please note: we use `this` in `f.apply` to make our decoration work for object methods.

So if the wrapper function is called as an object method, then `this` is passed to the original method `f`.

```js run
Function.prototype.defer = function(ms) {
  let f = this;
  return function(...args) {
    setTimeout(() => f.apply(this, args), ms);
  }
};

let user = {
  name: "John",
  sayHi() {
    alert(this.name);
  }
}

user.sayHi = user.sayHi.defer(1000);

user.sayHi();
```
