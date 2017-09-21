# windowWhen
#### signature: `windowWhen(closingSelector: function(): Observable): Observable`

## Close window at provided time frame emitting observable of collected values from source.

### Examples

##### Example 1: Open and close window at interval

( [jsBin](http://jsbin.com/tuhaposemo/edit?js,console) | [jsFiddle](https://jsfiddle.net/btroncone/gnx9fb3h/) )

```js
//emit immediately then every 1s
const source = Rx.Observable.timer(0,1000);
const example = source
    //close window every 5s and emit observable of collected values from source
    .windowWhen((val) => Rx.Observable.interval(5000))
    .do(() => console.log('NEW WINDOW!'))

const subscribeTwo = example 
  //window emits nested observable
  .mergeAll()
/*
  output:
  "NEW WINDOW!"
  0
  1
  2
  3
  4
  "NEW WINDOW!"
  5
  6
  7
  8
  9
*/
  .subscribe(val => console.log(val));
```


### Additional Resources
* [windowWhen](http://reactivex.io/rxjs/class/es6/Observable.js~Observable.html#instance-method-windowWhen) :newspaper: - Official docs

---
> :file_folder: Source Code:  [https://github.com/ReactiveX/rxjs/blob/master/src/operator/windowWhen.ts](https://github.com/ReactiveX/rxjs/blob/master/src/operator/windowWhen.ts)
