# Commenti

Come abbiamo già appreso dal capitolo <info:structure>, i commenti possono essere di una singola-riga: ed iniziano con `//` oppure multilinea: `/* ... */`.

Normalmente li utilizziamo per descrivere come e perché funziona il codice.

Inizialmente, l'inserimento di commenti può sembrare ovvio, ma i novizi solitamente non lo fanno nella maniera corretta.

## Commenti sbagliati

I novizi tendono ad utilizzare i commenti per spiegare "cosa sta succedendo nel codice". Come in questo esempio:

```js
// Questo codice farà questa cosa (...) e questa (...)
// ...e altre cose...
very;
complex;
code;
```

Nel buon codice la quantità di commenti "esplicativi" dovrebbe essere minima. In realtà il codice dovrebbe essere facile da comprendere anche senza.

C'è una bellissima regola a riguardo: "Se il codice è cosi poco chiaro da richiedere un commento, probabilmente dovrebbe essere riscritto".

### Ricetta: raccogliere in una funzione

Qualche volta può essere un beneficio rimpiazzare un pezzo di codice in una funzione, come in questo esempio:

```js
function showPrimes(n) {
  nextPrime:
  for (let i = 2; i < n; i++) {

*!*
    // controlla se i è un numero primo
    for (let j = 2; j < i; j++) {
      if (i % j == 0) continue nextPrime;
    }
*/!*

    alert(i);
  }
}
```

La migliore variante, sarebbe raccogliere il tutto in una funzione `isPrime`:


```js
function showPrimes(n) {

  for (let i = 2; i < n; i++) {
    *!*if (!isPrime(i)) continue;*/!*

    alert(i);  
  }
}

function isPrime(n) {
  for (let i = 2; i < n; i++) {
    if (n % i == 0) return false;
  }

  return true;
}
```

Ora possiamo capire il codice più facilmente. La funzione stessa diventa un commento. Questo tipo di codice viene definito *self-descriptive* (auto-descrittivo). 

### Ricetta: creare funzioni

Anche se avete un lungo "pezzo di codice" come questo:

```js
// qui aggiungiamo whiskey
for(let i = 0; i < 10; i++) {
  let drop = getWhiskey();
  smell(drop);
  add(drop, glass);
}

// qui aggiungiamo della spremuta (juice)
for(let t = 0; t < 3; t++) {
  let tomato = getTomato();
  examine(tomato);
  let juice = press(tomato);
  add(juice, glass);
}

// ...
```

Potrebbe essere una buona idea raccogliere tutto in una funzione:

```js
addWhiskey(glass);
addJuice(glass);

function addWhiskey(container) {
  for(let i = 0; i < 10; i++) {
    let drop = getWhiskey();
    //...
  }
}

function addJuice(container) {
  for(let t = 0; t < 3; t++) {
    let tomato = getTomato();
    //...
  }
}
```

Ripeto nuovamente, le funzioni stesse dicono cosa andranno a fare. Inoltre la struttura del codice è migliore quando è spezzata. E' chiaro cosa ogni funzione faccia, cosa richiede e cosa eventualmente ritorna.

Nella pratica, non possiamo evitare del tutto i commenti "esplicativi". Ci sono algoritmi molto complesso. E ci sono vari "trucchi" con lo scopo di ottimizzare questo tipo di commenti. In linea di massima dovremmo però cercar di tenere il codice semplice ed auto-descrittivo.

## Buoni commenti

Quindi, solitamente i commenti esplicativi sono sbagliati. Quali sono allora i commenti giusti?

Descrivere l'architettura
: Fornire un visuale di alto livello dei componenti, come interagiscono, come si comporta il flusso d'esecuzione in certe situazioni... In breve -- gli "occhi d'aquila" del codice. C'è uno speciale linguaggio schematico [UML](http://wikipedia.org/wiki/Unified_Modeling_Language) per schematizzare ad alto livello. Assolutamente da conoscere.

Documentare l'utilizzo di una funzione
: Esiste una particolare sintassi [JSDoc](http://en.wikipedia.org/wiki/JSDoc) per documentare le funzioni: utilizzo, parametri, valori di ritorno.

<<<<<<< HEAD
    Ad esempio:
    ```js
    /**
     * Ritorna la potenza n di x.
     *
     * @param {number} x La base della potenza.
     * @param {number} n Esponente, deve essere un numero naturale.
     * @return {number} x elevato alla n.
     */
    function pow(x, n) {
      ...
    }
    ```

    Questi commenti ci consentono di capire lo scopo della funzione e come utilizzarla correttamente senza guardarne il codice.

    In ogni caso, molti editor come [WebStorm](https://www.jetbrains.com/webstorm/) li comprendono e possono quindi utilizzarli per autocomplete e alcune verifiche automatiche del codice.

    Ci sono anche tool come [JSDoc 3](https://github.com/jsdoc3/jsdoc) che possono generare documentazione in HTML a partire dai commenti. Puoi scoprire di più riguardo JSDoc su <http://usejsdoc.org/>.
=======
For instance:
```js
/**
 * Returns x raised to the n-th power.
 *
 * @param {number} x The number to raise.
 * @param {number} n The power, must be a natural number.
 * @return {number} x raised to the n-th power.
 */
function pow(x, n) {
  ...
}
```

Such comments allow us to understand the purpose of the function and use it the right way without looking in its code.

By the way, many editors like [WebStorm](https://www.jetbrains.com/webstorm/) can understand them as well and use them to provide autocomplete and some automatic code-checking.

Also, there are tools like [JSDoc 3](https://github.com/jsdoc3/jsdoc) that can generate HTML-documentation from the comments. You can read more information about JSDoc at <http://usejsdoc.org/>.
>>>>>>> e074a5f825a3d10b0c1e5e82561162f75516d7e3

Perché l'azione viene risolta in quel modo?
: Quello che viene scritto è fondamentale. Ma quello che *non* viene scritto potrebbe esserlo anche di più per capire cosa sta succedendo. Perché l'azione viene portata a termine in quel modo? Il codice non fornisce risposte.

    Se ci sono diverse modalità di risolvere una determinata azione, perché si è scelta questa? Specialmente quando non risulta la scelta più ovvia.

    Senza dei commenti si potrebbero generare le seguenti situazioni:
    1. Tu (o un tuo collega) apre il codice un pò di tempo dopo, lo guarda e pensa che il codice è "poco ottimale".
    2. Voi stessi potreste pensare: "Quanto stupido sono stato qui, e quanto intelligente sono adesso", e riscriverla utilizzando "la più ovvia e corretta" variante.
    3. ...Lo stimolo di riscriverla sarebbe corretto. Ma quando l'avete scritta vi siete resi conto che la soluzione "più ovvia" era effettivamente peggiore. Andando a rileggerla potreste non ricordarvi neanche perché. Quindi dopo averla riscritta vi rendete conto che è meglio tornare indietro, avete sprecato tempo.

    Commenti che spiegano la soluzione sono fondamentali. Vi aiutano a sviluppare mantenendo sempre la strada corretta.

Ci sono alcune piccolezze? Dove vengono utilizzate?
: Se il codice contiene sottigliezze contro-intuitive, vale certamente la pena commentarle.

## Riepilogo

Un importante valore che possiede un bravo sviluppatore sono i commenti: la loro presenza o assenza.

I buoni commenti ci consentono di mantenere bene il codice, di poterci tornare dopo un pò di tempo e capire le scelte prese.

**Commenti utili:**

- Architettura complessiva, vista ad alto livello.
- Utilizzo delle funzioni.
- Soluzioni importanti, soprattutto quando poco ovvie.

**Commenti da evitare:**

<<<<<<< HEAD
- Quelli che dicono "come il codice funziona" e "cosa fa".
- Inseriteli solo se risulta impossibile rendere il codice semplice ed auto-descrittivo.
=======
- That tell "how code works" and "what it does".
- Put them in only if it's impossible to make the code so simple and self-descriptive that it doesn't require them.
>>>>>>> e074a5f825a3d10b0c1e5e82561162f75516d7e3

I commenti vengono utilizzati anche da strumenti che generano documentazione, come JSDoc3: li leggono e generano documenti HTML (o in altri formati).
