# ReactiveX

### 練習來源
* https://github.com/ReactiveX/rxjs
* https://github.com/btroncone/learn-rxjs

### 實作執行
* https://github.com/Shyam-Chen/Web-Starter-Kit
* https://github.com/Shyam-Chen/Backend-Starter-Kit

***

### 目錄
* [Observable](#observable)
  * bindCallback
  * bindNodeCallback
  * [combineLatest](#combinelatest-1) :star: (1)
  * [concat](#concat-1) :star: (1)
  * [defer](#defer)
  * empty (1)
  * forkJoin (1)
  * from :star: (1)
  * fromEvent (1)
  * fromEventPattern
  * fromPromise (1)
  * if
  * interval (1)
  * merge :star: (1)
  * never
  * of (1)
  * pairs
  * range (1)
  * throw (1)
  * timer (1)
  * using
  * zip (1)
* [Scheduler](#scheduler)
* Subject
* [ReplaySubject](#replaysubject)
* AsyncSubject
* BehaviorSubject
* [Combination (組合)](#組合)
  * [combineAll](#combineall)
  * [combineLatest](#combinelatest-2) :star: (2)
  * [concat](#concat-2) :star: (2)
  * concatAll
  * forkJoin (2)
  * merge :star: (2)
  * mergeAll
  * race
  * startWith :star:
  * withLatestFrom :star:
  * zip (2)
* Conditional (條件)
  * defaultIfEmpty
  * every
* Creation (創建)
  * create
  * empty (2)
  * from :star: (2)
  * fromEvent (2)
  * fromPromise (2)
  * interval (2)
  * of (2)
  * range (2)
  * throw (2)
  * timer (2)
* Error Handling (錯誤處理)
  * catch
  * retry
  * retryWhen
* Filtering (過濾)
  * debounce
  * debounceTime :star:
  * distinctUntilChanged :star:
  * filter :star:
  * first
  * ignoreElements
  * last
  * sample
  * single
  * skip
  * skipUntil
  * skipWhile
  * take :star:
  * takeUntil :star:
  * takeWhile
  * throttle
  * throttleTime
* Multicasting (組播)
  * multicast
  * publish
  * share :star:
* [Transformation (轉化)](#轉化)
  * [buffer](#buffer)
  * [bufferCount](#buffercount)
  * [bufferTime](#buffertime) :star:
  * bufferToggle
  * bufferWhen
  * concatMap :star:
  * concatMapTo
  * expand
  * groupBy
  * [map](#map) :star:
  * [mapTo](#mapto)
  * [mergeMap](#mergemap) :star:
  * partition
  * pluck
  * scan :star:
  * switchMap :star:
  * window
  * windowCount
  * windowTime
  * windowToggle
  * windowWhen
* Utility (公用)
  * do :star:
  * delay
  * delayWhen
  * let
  * toPromise

:star: - 常用<br>
(1) - 靜態<br>
(2) - 動態

***

## Observable

```js
import { Observable } from 'rxjs/Observable';
```

### combineLatest (1)

當任何的觀察者發射一個值時，從每個值發射出最新的值。

```js
import { Observable } from 'rxjs/Observable';

import { timer } from 'rxjs/observable/timer';
import { combineLatest } from 'rxjs/observable/combineLatest';

const timerOne$ = Observable::timer(1000, 4000);
const timerTwo$ = Observable::timer(2000, 4000);
const timerThree$ = Observable::timer(3000, 4000);

Observable::combineLatest(timerOne$, timerTwo$, timerThree$)
  .subscribe((latestValues) => {
    const [timerValOne, timerValTwo, timerValThree] = latestValues;
    console.log(`${timerValOne}, ${timerValTwo}, ${timerValThree}`);
  });
  // 0, 0, 0
  // 1, 0, 0
  // 1, 1, 0
  // 1, 1, 1
  // 2, 1, 1
  // 2, 2, 1
  // 2, 2, 2
  // ...
```

使用函式投射

```js
import { Observable } from 'rxjs/Observable';

import { timer } from 'rxjs/observable/timer';
import { combineLatest } from 'rxjs/observable/combineLatest';

const timerOne$ = Observable::timer(1000, 4000);
const timerTwo$ = Observable::timer(2000, 4000);
const timerThree$ = Observable::timer(3000, 4000);

Observable::combineLatest(
    timerOne$, timerTwo$, timerThree$,
    (one, two, three) => `${one}, ${two}, ${three}`
  )
  .subscribe((latestValuesProject) => console.log(latestValuesProject));
  // 0, 0, 0
  // 1, 0, 0
  // 1, 1, 0
  // 1, 1, 1
  // 2, 1, 1
  // 2, 2, 1
  // 2, 2, 2
  // ...
```

### concat (1)

```js
import { Observable } from 'rxjs/Observable';

import { of } from 'rxjs/observable/of';
import { concat } from 'rxjs/observable/concat';

Observable::concat(
    Observable::of(1, 2, 3),
    Observable::of(4, 5, 6)
  )
  .subscribe(result => console.log(result));
  // 1
  // 2
  // 3
  // 4
  // 5
  // 6
```

```js
import { Observable } from 'rxjs/Observable';

import { concat } from 'rxjs/observable/concat';
import { interval } from 'rxjs/observable/interval';
import { of } from 'rxjs/observable/of';

Observable::concat(
    Observable::interval(1000),
    Observable::of('This', 'Never', 'Runs')  // 這個不會被執行
  )
  .subscribe(result => console.log(result));
  // 每秒打印
  // 0
  // 1
  // 2
  // 3
  // ...
```

### defer

```js
import { Observable } from 'rxjs/Observable';

import { defer } from 'rxjs/observable/defer';
import { of } from 'rxjs/observable/of';

Observable::defer(() => Observable::of(1, 2, 3))
  .subscribe(result => console.log(result + 1));
```

## Scheduler

```js
import { Scheduler } from 'rxjs/Scheduler';
```

```js
import { animationFrame } from 'rxjs/scheduler/animationFrame';
import { asap } from 'rxjs/scheduler/asap';
import { async } from 'rxjs/scheduler/async';
import { queue } from 'rxjs/scheduler/queue';
```

## Subject

```js
import { Subject } from 'rxjs/Subject';
```

## ReplaySubject

可以是可觀察的序列，也可以是觀察者的物件。

每個通知被推播給所有訂閱和未來的觀察者，並尊從緩衝區修整的策略。

```js
import { ReplaySubject } from 'rxjs/ReplaySubject';

const subject = new ReplaySubject(2);  // 緩衝區域大小為 2

subject.next(1);
subject.next(2);
subject.next(3);

subject.subscribe((val) => console.log('Received value:', val));
// 2
// 3
```

## AsyncSubject

```js
import { AsyncSubject } from 'rxjs/AsyncSubject';
```

## BehaviorSubject

```js
import { BehaviorSubject } from 'rxjs/BehaviorSubject';
```

## 組合

### combineAll

當外部的觀察者完成時，輸出內部觀者的最新值。

```js
import { Observable } from 'rxjs/Observable';

import { timer } from 'rxjs/observable/timer';
import { of } from 'rxjs/observable/of';

import { mapTo } from 'rxjs/operator/mapTo';
import { combineAll } from 'rxjs/operator/combineAll';

const timer$ = Observable::timer(2000);

timer$::mapTo(Observable::of('Hello', 'World'))
  ::combineAll()
  .subscribe((val) => console.log('Values from inner observable:', val));
  // ["Hello"]
  // ["World"]

timer$::mapTo(Observable::of('Hello', 'Goodbye'))
  ::combineAll((val) => `${val} Friend!`)
  .subscribe((val) => console.log('Values Using Projection:', val));
  // Hello Friend!
  // Goodbye Friend!
```

```js
import { Observable } from 'rxjs/Observable';

import { interval } from 'rxjs/observable/interval';

import { take } from 'rxjs/operator/take';
import { map } from 'rxjs/operator/map';
import { combineAll } from 'rxjs/operator/combineAll';

Observable::interval(1000)
  ::take(3)
  ::map((val) => Observable::interval(val + 500)::take(2))
  ::combineAll()
  .subscribe((val) => console.log(val));
  // [0, 0, 0]
  // [1, 0, 0]
  // [1, 1, 0]
  // [1, 1, 1]
```

### combineLatest (2)

當任何的觀察者發射一個值時，從每個值發射出最新的值。

```js
import { Observable } from 'rxjs/Observable';

import { timer } from 'rxjs/observable/timer';
import { interval } from 'rxjs/observable/interval';

import { combineLatest } from 'rxjs/operator/combineLatest';

const timerOne$ = Observable::timer(1000, 4000);
const timerTwo$ = Observable::timer(2000, 4000);
const timerThree$ = Observable::timer(3000, 4000);

Observable::interval(1000)
  ::combineLatest(timerOne$, timerTwo$, timerThree$)
  .subscribe((latestValues) => {
    const [timerValOne, timerValTwo, timerValThree] = latestValues;
    console.log(`${timerValOne}, ${timerValTwo}, ${timerValThree}`);
  });
  // 2, 0, 0
  // 3, 0, 0
  // 4, 0, 0
  // 4, 1, 0
  // 5, 1, 0
  // 5, 1, 1
  // 6, 1, 1
  // 6, 1, 1
  // 7, 1, 1
  // 8, 1, 1
  // 8, 2, 1
  // 9, 2, 1
  // 9, 2, 2
  // ...
```

### concat (2)

```js
import { Observable } from 'rxjs/Observable';

import { of } from 'rxjs/observable/of';

import { concat } from 'rxjs/operator/concat';

Observable::of(1, 2, 3)
  ::concat(Observable::of(4, 5, 6))
  .subscribe(result => console.log(result));
  // 1
  // 2
  // 3
  // 4
  // 5
  // 6
```

```js
import { Observable } from 'rxjs/Observable';

import { of } from 'rxjs/observable/of';

import { delay } from 'rxjs/operator/delay';
import { concat } from 'rxjs/operator/concat';

Observable::of(1, 2, 3)
  ::delay(2000)
  ::concat(Observable::of(4, 5, 6))
  .subscribe(result => console.log(result));
  // 延遲兩秒
  // 1
  // 2
  // 3
  // 4
  // 5
  // 6
```



## 轉化

### buffer

緩衝所有輸出值，直到被發射出去。反覆執行...

```js
import { Observable } from 'rxjs/Observable';

import { interval } from 'rxjs/observable/interval';
import { fromEvent } from 'rxjs/observable/fromEvent';

import { buffer } from 'rxjs/operator/buffer';

Observable::interval(1000)
  ::buffer(Observable::fromEvent(document, 'click'))  // 點擊頁面
  .subscribe((val) => console.log('Buffered Values:', val));
  // 發射數值
  // [...]
```

### bufferCount

緩衝所有輸出值，直到指定的數字被履行，然後再發射出去。反覆執行...

```js
import { Observable } from 'rxjs/Observable';

import { interval } from 'rxjs/observable/interval';

import { bufferCount } from 'rxjs/operator/bufferCount';

const interval$ = Observable::interval(1000);

interval$::bufferCount(3)
  .subscribe((val) => console.log('Buffered Values:', val));
  // [0, 1, 2]
  // 下個間隔
  // [3, 4, 5]
  // ...

interval$::bufferCount(3, 1)
  .subscribe((val) => console.log('Start Buffer Every 1:', val));
  // [0, 1, 2]
  // [1, 2, 3]
  // [2, 3, 4]
  // 下個間隔
  // [3, 4, 5]
  // [4, 5, 6]
  // [5, 6, 7]
  // ...
```

### bufferTime

緩衝所有輸出值，直到到達指定的時間點，然後再發射出去。反覆執行...

```js
import { Observable } from 'rxjs/Observable';

import { interval } from 'rxjs/observable/interval';

import { bufferTime } from 'rxjs/operator/bufferTime';

const interval$ = Observable::interval(1000);

interval$::bufferTime(2000)
  .subscribe((val) => console.log('Buffered with Time:', val));
  // [0]
  // 下個間隔
  // [1, 2]
  // 下個間隔
  // [3, 4]
  // ...

interval$::bufferTime(2000, 1000)
  .subscribe((val) => console.log('Start Buffer Every 1s:', val));
  // [0]
  // [0, 1, 2]
  // 下個間隔
  // [1, 2, 3]
  // [2, 3, 4]
  // 下個間隔
  // [3, 4, 5]
  // [4, 5, 6]
  // ...
```

### map

對來源的每個值進行應用投射。

```js
import { Observable } from 'rxjs/Observable';

import { from } from 'rxjs/observable/from';

import { map } from 'rxjs/operator/map';

Observable::from([1, 2, 3, 4, 5])
  ::map((val) => val + 10)
  .subscribe((val) => console.log(val))
  // 11
  // 12
  // 13
  // 14
  // 15

Observable::from([
    { name: 'Joe', age: 30 },
    { name: 'Frank', age: 20 },
    { name: 'Ryan', age: 50 }
  ])
  ::map((person) => person.name)
  .subscribe((val) => console.log(val))
  // Joe
  // Frank
  // Ryan
```

### mapTo

將發射值映射到所賦予的常數。

```js
import { Observable } from 'rxjs/Observable';

import { interval } from 'rxjs/observable/interval';

import { mapTo } from 'rxjs/operator/mapTo';

Observable::interval(1000)
  ::mapTo('Hello World!')
  .subscribe((val) => console.log(val));
  // 每秒打印 Hello World!
```

### mergeMap

將來源的值先映射到內部個觀察者，再將其合併發射出去。即，先 `map` 再 `mergeAll`。

```js
import { Observable } from 'rxjs/Observable';

import { of } from 'rxjs/observable/of';

import { mergeMap } from 'rxjs/operator/mergeMap';

Observable::of('Hello')
  ::mergeMap((val) => Observable::of(`${val} World!`))
  .subscribe((val) => console.log(val));
  // Hello World!
```