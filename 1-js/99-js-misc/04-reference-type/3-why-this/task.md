importance: 3

---

# Spiegate il valore di "this"

<<<<<<< HEAD:1-js/04-object-basics/04-object-methods/3-why-this/task.md
Nel codice sotto vogliamo chiamare il metodo `user.go()`  volte di fila.
=======
In the code below we intend to call `obj.go()` method 4 times in a row.
>>>>>>> d6e88647b42992f204f57401160ebae92b358c0d:1-js/99-js-misc/04-reference-type/3-why-this/task.md

Ma le chiamate `(1)` e `(2)` funzionano diversamente da `(3)` e `(4)`. Perché?

```js run no-beautify
let obj, method;

obj = {
  go: function() { alert(this); }
};

obj.go();               // (1) [object Object]

(obj.go)();             // (2) [object Object]

(method = obj.go)();    // (3) undefined

(obj.go || obj.stop)(); // (4) undefined
```

