# Lodash

### 練習來源
* https://github.com/lodash/lodash

### 實作執行
* https://github.com/Shyam-Chen/Frontend-Starter-Kit
* https://github.com/Shyam-Chen/Backend-Starter-Kit

***

### 目錄
* Array (陣列)
  * [compact](#compact) :star:
  * concat :star:
  * fill :sparkles:
  * findIndex :sparkles:
  * head :sparkles:
  * initial :sparkles:
  * last :sparkles:
  * tail :sparkles:
* Collection (集合)
  * filter :sparkles:
  * find :sparkles:
  * map :sparkles:
  * reduce :sparkles:
* Date (日期)
* Function (函式)
  * before :star:
  * bind :star:
  * curry :sparkles:
  * partial :sparkles:
  * rest :sparkles:
  * spread :sparkles:
* Lang (語言)
* Math (數學)
* Number (數字)
* Object (物件)
* Seq (序列)
* String (字串)
* Util (公用)

:star: - 核心<br>
:sparkles: - JS.Next

[:vertical_traffic_light:] - 排除 JS.Next 以下

***

## 陣列

### chunk

建立一個元素陣列，分成組大小的長度。如果陣列不能均勻分割，最後的塊將是剩餘的元素。

```js
import { chunk } from 'lodash';

chunk(['a', 'b', 'c', 'd'], 2);
// [['a', 'b'], ['c', 'd']]

chunk(['a', 'b', 'c', 'd'], 3);
// [['a', 'b', 'c'], ['d']]
```

### compact

建立一個刪除所有 falsey 值的陣列。

falsey: `false`、`null`、`0`、`''`、`undefined` 和 `NaN`

```js
import { compact } from 'lodash';

compact([0, true, 1, false, 2, 'foo', 3, '', 4, 'bar']);
// [true, 1, 2, "foo", 3, 4, "bar"]
```

### difference

```js
import { compact } from 'lodash';

difference([2, 1], [2, 3]);
```

## 集合

### every


### find

## 函式

### before

### bind

### defer

### delay

## 物件

### assignIn

### create

### defaults

## 序列

### chain

### value

## 語言

## 字串

### escape


`_.flatten`

`_.flattenDeep`

`_.forEach`

`_.has`

`_.head`

`_.identity`

`_.indexOf`

`_.isArguments`

`_.isArray`

`_.isBoolean`

`_.isDate`

`_.isEmpty`

`_.isEqual`

`_.isFinite`

`_.isFunction`

`_.isNaN`

`_.isNull`

`_.isNumber`

`_.isObject`

`_.isRegExp`

`_.isString`

`_.isUndefined`

`_.iteratee`

`_.keys`

`_.last`

`_.map`

`_.matches`

`_.max`

`_.min`

`_.mixin`

`_.negate`

`_.noConflict`

`_.noop`

`_.once`

`_.pick`

`_.reduce`

`_.result`

`_.size`

`_.slice`

`_.some`

`_.sortBy`

`_.tap`

`_.thru`

`_.toArray`

`_.uniqueId`

`_#value`

`_.values`
