
# Riscrivi con funzioni freccia

<<<<<<< HEAD:1-js/02-first-steps/15-function-expressions-arrows/1-rewrite-arrow/task.md
Rimpiazza le espressioni di funzione con funzioni freccia:
=======
Replace Function Expressions with arrow functions in the code below:
>>>>>>> f489145731a45df6e369a3c063e52250f3f0061d:1-js/02-first-steps/17-arrow-functions-basics/1-rewrite-arrow/task.md

```js run
function ask(question, yes, no) {
  if (confirm(question)) yes()
  else no();
}

ask(
  "Do you agree?",
  function() { alert("You agreed."); },
  function() { alert("You canceled the execution."); }
);
```
