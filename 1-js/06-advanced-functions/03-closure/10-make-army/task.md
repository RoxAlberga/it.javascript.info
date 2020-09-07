importance: 5

---

# Funzione crea eserciti

Il seguente codice crea un array di `shooters`.

Ogni funzione è pensata per ritornare il numero, Ma qualcosa non va...

```js run
function makeArmy() {
  let shooters = [];

  let i = 0;
  while (i < 10) {
    let shooter = function() { // shooter function
      alert( i ); // should show its number
    };
    shooters.push(shooter);
    i++;
  }

  return shooters;
}

let army = makeArmy();

army[0](); // the shooter number 0 shows 10
army[5](); // and number 5 also outputs 10...
// ... all shooters show 10 instead of their 0, 1, 2, 3...
```

<<<<<<< HEAD:1-js/06-advanced-functions/03-closure/8-make-army/task.md
Perché tutti gli eserciti possiedono lo stesso numero di militari? Modificate il codice in modo tale che funzioni correttamente.
=======
Why do all of the shooters show the same value? Fix the code so that they work as intended.
>>>>>>> 58f6599df71b8d50417bb0a52b1ebdc995614017:1-js/06-advanced-functions/03-closure/10-make-army/task.md

