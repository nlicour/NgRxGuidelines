# Create operator

Les opérateurs sont des fonctions qui retournent des parametres et qui returnent des fonctions.

On peut donc facilement créer nos propres opérateurs.

```ts
// Opérateur
function grabAndLogClassics(year, log) {
  // Input
  return source$ => {
    // Output
    return new Observable(subscriber => {
      return source$.subscribe(
        // logique
        book => {
          if(book.publicationYear < year) {
            subscriber.next(book);
            if(log) {
              console.log(`Classic: ${book.title}`);
            }
          }
        },
        err => subscriber.error(err),
        () => subscriber.complete()
      );
    });
  }
}


function grabClassics(year) {
  return filter(book => book.publicationYear < year);
}

function grabAndLogClassicsWithPipe(year, log) {
  return source$ => source$.pipe(
    filter(book => book.publicationYear < year),
    tap(classicBook => log ? console.log(`Title: ${classicBook.title}`) : null)
  );
}

ajax('/api/books')
  .pipe(
    mergeMap(ajaxResponse => ajaxResponse.response),

    // 3 customs operateurs
    // grabAndLogClassics(1930, false)
    // grabClassics(1950)
    // grabAndLogClassicsWithPipe(1930, true)
  )
  .subscribe(
    finalValue => console.log(`VALUE: ${finalValue.title}`),
    error => console.log(`ERROR: ${error}`)
  );

```