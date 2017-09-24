# zip
#### 연산자(operator) 정의: `zip(observables: *): Observable`

### Description

###### TL;DR: After all observables emit, emit values as an array

The **zip** operator will subscribe to all inner observables, waiting for each to emit a value. Once this occurs, all values with the corresponding index will be emitted. This will continue until at least one inner observable completes. 

---
:bulb:  Combined with [interval](../creation/interval) or [timer](../creation/timer.md), zip can be used to time output from another source!

---

### Examples

##### Example 1: zip multiple observables emitting at alternate intervals

( [jsBin](http://jsbin.com/lireyisira/1/edit?js,console) | [jsFiddle](https://jsfiddle.net/btroncone/ton462sg/) )

```js
const sourceOne = Rx.Observable.of('Hello');
const sourceTwo = Rx.Observable.of('World!');
const sourceThree = Rx.Observable.of('Goodbye');
const sourceFour = Rx.Observable.of('World!');
//wait until all observables have emitted a value then emit all as an array
const example = Rx.Observable
  .zip(
    sourceOne,
    sourceTwo.delay(1000),
    sourceThree.delay(2000),
    sourceFour.delay(3000)
  );
//output: ["Hello", "World!", "Goodbye", "World!"]
const subscribe = example.subscribe(val => console.log(val));
```

##### Example 2: zip when 1 observable completes

( [jsBin](http://jsbin.com/fisitatesa/1/edit?js,console) | [jsFiddle](https://jsfiddle.net/btroncone/oamyk3xr/) )

```js
//emit every 1s
const interval = Rx.Observable.interval(1000);
//when one observable completes no more values will be emitted
const example = Rx.Observable
  .zip(
    interval,
    interval.take(2)
  );
//output: [0,0]...[1,1]
const subscribe = example.subscribe(val => console.log(val));
```


### Additional Resources
* [zip](http://reactivex.io/rxjs/class/es6/Observable.js~Observable.html#static-method-zip) :newspaper: - Official docs
* [Combination operator: zip](https://egghead.io/lessons/rxjs-combination-operator-zip?course=rxjs-beyond-the-basics-operators-in-depth) :video_camera: :dollar: - André Staltz

---
> :file_folder: Source Code:  [https://github.com/ReactiveX/rxjs/blob/master/src/operator/zip.ts](https://github.com/ReactiveX/rxjs/blob/master/src/operator/zip.ts)
