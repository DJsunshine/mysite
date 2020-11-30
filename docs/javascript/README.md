---
title: JavaScript
sidbar: true
---

::: tip
随意记录一些知识点
:::

## 防抖

```js
export function debounce(fn, delay = 500) {
  let timer = null;
  return function() {
    if (timer) clearTimeout(timer);
    timer = setTimeout(() => {
      fn.apply(this, arguments);
      timer = null;
    }, delay);
  };
}
```

## 节流

```js
export function throllte(fn, delay = 300) {
  let timer = null;
  return function() {
    if (timer) return;
    timer = setTimeout(() => {
      fn.apply(this, arguments);
      timer = null;
    }, delay);
  };
}
```

## 深拷贝

```js
function declone(obj) {
  if (typeof obj !== "object" || obj == null) return obj;

  let result;
  if (obj instanceof Array) {
    result = [];
  } else {
    result = {};
  }

  for (let key in obj) {
    if (obj.hasOwnProperty(key)) {
      result[key] = deepClone(obj[j]);
    }
  }
  return result;
}
```

## 简易实现 Call

```js
Function.prototype.myCall = function(context, ...args) {
  context = context || window;
  let fn = Symbol();
  context[fn] = this;
  context[fn](...args);
  delete context[fn];
};
```

## 简易实现 Apply

```js
Function.prototype.myApply = function(context, args) {
  context = context || window;
  let fn = Symbol();
  context[fn] = this;
  context[fn](...args);
  delete context[fn];
};
```

## 简易实现 Bind

```js
Function.prototype.myBind = function(context, args) {
  context = context || window;
  let fn = Symbol();
  return (...args2) => {
    context[fn] = this;
    context[fn](args.concat(args2));
    delete context[fn];
  };
};
```

## 排序

### 冒泡

```js
let arr = [1, 2, 5, 1, 6, 7, 12, 64];
for (let i = 0; i < arr.length; i++) {
  for (let j = 0; j < arr.length - 1 - i; j++) {
    if (arr[j] > arr[j + 1]) {
      let temp = arr[j];
      arr[j] = arr[j + 1];
      arr[j + 1] = temp;
    }
  }
}
```

### 选择

```js
function chooseSort(arr) {
  let len = arr.length;
  if (len < 1) return arr;
  for (let i = 0; i < len - 1; i++) {
    let compareVal = arr[i];
    for (let j = i + 1; j < len; j++) {
      if (arr[j] < compareVal) {
        let temp = compareVal;
        compareVal = arr[j];
        arr[j] = temp;
      }
    }
    arr[i] = compareVal;
  }
  return arr;
}
```

### 插入

```js
function insert(arr) {
    for(let i = 1; i < arr.length; i++) {
        let key = arr[i]
        let j = i - 1
        while( j >= 0 && arr[j] > key) {
            arr[j+1] = arr[j]
            j--
        }
        arr[j+1] = key
    }
    return arr
}
```

### 快排

```js
function quickSort(arr) {
    if(arr.length <=1) {return arr}
    let index = Math.floor(arr.length / 2)
    let comparVal = arr.splice(index, 1)[0]
    let left = []
    let right = []
    for (i in arr) {
        if (arr[i] < comparVal) {
            left.push(arr[i])
        } else {
            right.push(arr[i])
        }
    }
    return quickSort(left).concat([comparVal], quickSort(right))
}
```
