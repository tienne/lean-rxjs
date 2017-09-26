# concatAll
#### 연산자(operator) 정의: `concatAll(): Observable`

## observable의 observable를 결합하고 이전 Observable이 완료되면 그 다음 Observable의 구독이 실행됩니다.

---
:warning:  Be wary of [backpressure](https://github.com/Reactive-Extensions/RxJS/blob/master/doc/gettingstarted/backpressure.md) when the source emits at a faster pace than inner observables complete!

:bulb:  In many cases you can use [concatMap](../transformation/concatmap.md) as a single operator instead!

---

![](http://reactivex.io/rxjs/img/concatAll.png)

### Examples

( [example tests](https://github.com/btroncone/learn-rxjs/blob/master/operators/specs/combination/concatall-spec.ts) )

##### Example 1: concatAll with observable

( [jsBin](http://jsbin.com/nakinenuva/1/edit?js,console) | [jsFiddle](https://jsfiddle.net/btroncone/8dfuf2y6/) )

```js
//emit a value every 2 seconds
const source = Rx.Observable.interval(2000);
const example = source
  //for demonstration, add 10 to and return as observable
  .map(val => Rx.Observable.of(val + 10))
  //merge values from inner observable
  .concatAll();
//output: 'Example with Basic Observable 10', 'Example with Basic Observable 11'...
const subscribe = example.subscribe(val => console.log('Example with Basic Observable:', val));
```

##### Example 2: concatAll with promise

( [jsBin](http://jsbin.com/bekegeyopu/1/edit?js,console) | [jsFiddle](https://jsfiddle.net/btroncone/w7kp7qLs/) )

```js
//create and resolve basic promise
const samplePromise = val => new Promise(resolve => resolve(val));
//emit a value every 2 seconds
const source = Rx.Observable.interval(2000);

const example = source
  .map(val => samplePromise(val))
  //merge values from resolved promise
  .concatAll();
//output: 'Example with Promise 0', 'Example with Promise 1'...
const subscribe = example.subscribe(val => console.log('Example with Promise:', val));
```

##### Example 3: Delay while inner observables complete

( [jsBin](http://jsbin.com/pojolatile/1/edit?js,console) | [jsFiddle](https://jsfiddle.net/btroncone/8230ucbg/) )

```js
const obs1 = Rx.Observable.interval(1000).take(5);
const obs2 = Rx.Observable.interval(500).take(2);
const obs3 = Rx.Observable.interval(2000).take(1);
//emit three observables
const source = Rx.Observable.of(obs1, obs2, obs3);
//subscribe to each inner observable in order when previous completes
const example = source.concatAll();
/*
  output: 0,1,2,3,4,0,1,0
  How it works...
  Subscribes to each inner observable and emit values, when complete subscribe to next
  obs1: 0,1,2,3,4 (complete)
  obs2: 0,1 (complete)
  obs3: 0 (complete)
*/

const subscribe = example.subscribe(val => console.log(val));
```

### 추가자료 목록
* [concatAll](http://reactivex.io/rxjs/class/es6/Observable.js~Observable.html#instance-method-concatAll) :newspaper: - Official docs
* [Flatten a higher order observable with concatAll in RxJS](https://egghead.io/lessons/rxjs-flatten-a-higher-order-observable-with-concatall-in-rxjs?course=use-higher-order-observables-in-rxjs-effectively) :video_camera: :dollar: - André Staltz

---
> :file_folder: Source Code:  [https://github.com/ReactiveX/rxjs/blob/master/src/operator/concatAll.ts](https://github.com/ReactiveX/rxjs/blob/master/src/operator/concatAll.ts)
