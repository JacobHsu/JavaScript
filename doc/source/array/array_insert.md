title: Array Insert
---

![js-array-operations](https://raw.githubusercontent.com/tooto1985/js-array-operations/master/main.jpg)  

immutable 的重要性，處理資料要注意有沒有改變到本身。
處理 array 用 `push、pop、shift、unshift、reserve、sort、splice` 都會改變原有的陣列。這個觀念在處理複雜的全域變數陣列有幫助。

## 把數據插入陣列尾部

利用陣列長度進行賦值  
```js
let arr = [1,2,3,4,5];
arr[arr.length] = 6;
console.log(arr); // [1, 2, 3, 4, 5, 6]
```

利用 `Array.prototype.push` 方法    
```js
let arr = [1, 2, 3, 4, 5];
arr.push(6);
console.log(arr); // [1, 2, 3, 4, 5, 6]
```

利用 `Array.prototype.concat` 方法  
```js
let arr = [1, 2, 3, 4, 5];
arr = arr.concat(6);
console.log(arr); // [1, 2, 3, 4, 5, 6]
```

利用 `spread` 運算符  
```js
let arr = [1, 2, 3, 4, 5];
arr = [...arr, 6];
console.log(arr); // [1, 2, 3, 4, 5, 6]
```


## 把數據插入陣列頭部

利用 `Array.prototype.unshift` 方法

```js
let arr = [1,2,3,4,5];
arr.unshift(0);
console.log(arr); // [1, 2, 3, 4, 5, 6]
```

利用 `Array.prototype.concat` 方法

```js
let arr = [1,2,3,4,5];
arr.unshift(0);
console.log(arr); // [1, 2, 3, 4, 5, 6]
```

利用 `spread` 運算符
```js
let arr = [1, 2, 3, 4, 5];
arr = [0, ...arr];
console.log(arr); // [1, 2, 3, 4, 5, 6]
```

## 把數據插入陣列指定位置

利用 `Array.prototype.splice` 方法

```js
let items = [1, 2, 4, 5];
items.splice(items.length / 2, 0, 3);
console.log(items);
```

[Array.prototype.splice()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)

`splice()` 方法可以藉由刪除既有元素並／或加入新元素來改變一個陣列的內容

```js
const months = ['Jan', 'March', 'April', 'June'];
months.splice(1, 3);
console.log(months); // ["Jan"]
months.splice(1, 0, 'Feb'); // inserts at index 1
console.log(months); // ["Jan", "Feb"]
```

## 拼接兩個陣列

利用 `Array.prototype.concat` 方法

```js
let arr = [1,2,3,4,5];
arr = [-2, -1, 0].concat(arr); 
console.log(arr); // [-2, -1, 0, 1, 2, 3, 4, 5]
```

利用 `spread` 運算符
```js
let arr = [1,2,3,4,5];
arr = [...[-2, -1, 0], ...arr];
console.log(arr); // [-2, -1, 0, 1, 2, 3, 4, 5]  
```

## [fill()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/fill)

Array.prototype.fill() 方法會將陣列中索引的第一個到最後一個的每個位置全部填入一個靜態的值。

```js
const array1 = [1, 2, 3, 4];

// fill with 5 from position 1
console.log(array1.fill(5, 1));
// expected output: [1, 5, 5, 5]

console.log(array1.fill(6));
// expected output: [6, 6, 6, 6]
```

```js
  const tasksArr = props.tasks; // [1,2,3,4]
  const participants = tasksArr.length;
  const queuers  = 6- tasksArr.length; //4 ['Wating...','Wating...']
  let waitingArr = queuers ===0 ? [] : Array(queuers).fill('Wating...');
  const totalArr = tasksArr.concat(waitingArr);
```

## example

[unshift](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift) 把數據插入陣列頭部

下拉選單補標題　　　　
```js
const opts = this.dataOpts.map(data => ({
    value: data.id,
    text: data.name
}))
opts.unshift({
    value: null,
    text: 'select_title'
})
```

