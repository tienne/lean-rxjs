# mapTo
#### signature: `mapTo(value: any): Observable`

## Map emissions to constant value.

### Examples

##### Example 1: Map every emission to string

( [jsBin](http://jsbin.com/qujolenili/1/edit?js,console) | [jsFiddle](https://jsfiddle.net/btroncone/4ojq56ng/) )

```js
//emit value every two seconds
const source = Rx.Observable.interval(2000);
//map all emissions to one value
const example = source.mapTo('HELLO WORLD!');
//output: 'HELLO WORLD!'...'HELLO WORLD!'...'HELLO WORLD!'...
const subscribe = example.subscribe(val => console.log(val));
```

##### Example 2: Mapping clicks to string

( [jsBin](http://jsbin.com/xaheciwara/1/edit?js,console,output) | [jsFiddle](https://jsfiddle.net/btroncone/52fqL4nn/) )

```js
//emit every click on document
const source = Rx.Observable.fromEvent(document, 'click');
//map all emissions to one value
const example = source.mapTo('GOODBYE WORLD!');
//output: (click)'GOODBYE WORLD!'...
const subscribe = example.subscribe(val => console.log(val));
```

### Related Recipes
* [Smart Counter](../../recipes/smartcounter.md)

### Additional Resources
* [mapTo](http://reactivex.io/rxjs/class/es6/Observable.js~Observable.html#instance-method-mapTo) :newspaper: - Official docs
* [Changing behavior with mapTo](https://egghead.io/lessons/rxjs-changing-behavior-with-mapto?course=step-by-step-async-javascript-with-rxjs) :video_camera: :dollar: - John Linquist
* [Transformation operator: map and mapTo](https://egghead.io/lessons/rxjs-transformation-operator-map-and-mapto?course=rxjs-beyond-the-basics-operators-in-depth) :video_camera: :dollar: - André Staltz

---
> :file_folder: Source Code:  [https://github.com/ReactiveX/rxjs/blob/master/src/operator/mapTo.ts](https://github.com/ReactiveX/rxjs/blob/master/src/operator/mapTo.ts)
