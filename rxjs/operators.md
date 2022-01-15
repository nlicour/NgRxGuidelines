# Operators - Pipe 

Utiliser la fonction pipe pour faire des traitements sur les observables.

On va pourvoir chainer les traitements sur les observables.

```ts
const pipe = (...fns) => (x) => fns.reduce((v, f) => f(v), x);
```

```ts
let source$ = of(1,2,3,4,5);

source$.pipe(
    map(x => x * 2),
    filter(x => x > 5),
)
.subscribe(x => console.log(x));
```

Il y a plus de 100 opérateurs dans rxjs.


* Transformation
* Filtering
* Combination
* Utility ==> Controle - How, When 
* Conditional ==> if 
* Aggregate
* Multicasting

## Exemple

```ts
ajax('/api/errors/500') // correct URL is '/api/books'
  .pipe(
    mergeMap(ajaxResponse => ajaxResponse.response),
    filter(book => book.publicationYear < 1950),
    tap(oldBook => console.log(`Title: ${oldBook.title}`)),
    // 1. On retourne sur le canal de valeur
    // 1. catchError(err => of({title: 'Corduroy', author: 'Don Freeman'})) 
    
    // 2. On retourne sur le canal d'error
    // 2. catchError((err, caught) => caught)
    
    // 3. On re déclenche une erreur
    // 3.1 catchError(err => throw `Something bad happened - ${err.message}`)
    // 3.2 catchError(err => return throwError(err.message))
  )
  .subscribe(
    finalValue => console.log(`VALUE: ${finalValue.title}`),
    error => console.log(`ERROR: ${error}`)
  );
```

## Catch Error

CatchError est une fonction qui prend en paramètre une function qui va retourner un observable. 

C'est donc la valeur qui va être lue au lieux du canal erreur. 

On peut aussi l'utiliser pour re déclencher une erreur.

## Marble diagrams 
