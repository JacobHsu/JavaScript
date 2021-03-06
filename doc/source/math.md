title: 問題
---

# [Math](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Math)

`Math.pow(x, y)` 回傳 x 的 y 次方

```js
const decimals = 6
console.log(Math.pow(10, decimals)) //1000000`
```

# 浮點數運算的坑

[JavaScript 浮点数陷阱及解法](https://github.com/camsong/blog/issues/9)

當你拿到 1.4000000000000001 這樣的數據要展示時，建議使用 toPrecision 湊整併 parseFloat 轉成數字後再顯示，如下：

`parseFloat(1.4000000000000001.toPrecision(12)) === 1.4  // True`


百分比 轉 小數 問題
```js
var a = 0.9;
var b = a / 100;
var c = parseFloat( (a / 100).toPrecision(12)) 

console.log(b) // 0.009000000000000001
console.log(c) // 0.009
```

# 科學符號處理

npm [from-exponential](https://www.npmjs.com/package/from-exponential)  

```js
<span v-text="getPriceValue(order.itemPrice)"></span>
import fromExponential from 'from-exponential'
methods: {
    getPriceValue(value) {
      return fromExponential(value)
    }

}
```

# why 0.1 + 0.2 != 0.3

> 0.1 + 0.2 == 0.3
false

在兩數相加時，會先轉換成`二進制`，0.1 和 0.2 轉換成二進制的時候尾數會發生無限循環，然後進行對階運算，JS 引擎對二進制進行截斷，所以造成精度丟失。

總結：**精度丟失可能出現在進制轉換和對階運算中**

> 0.1 + 0.2
0.30000000000000004

這只是JavaScript遵循IEEE 754標準所產生的必然結果。`IEEE 754標準中`的浮點數並不能精確地表達小數（比如說0.1），

JavaScript中的小數採用的是雙精度(64位)表示的，由三部分組成：　符 + 階碼 + 尾數
IEEE 754 雙精度。六十四位中符號位佔一位，整數位佔十一位，其餘五十二位都為小數位。
因為浮點數隻有52位有效數字，從第53位開始，就舍入了。這樣就造成了“浮點數精度損失”問題。
因為 0.1 和 0.2 都是無限循環的二進制了，所以在小數位末尾處需要判斷是否進位（就和十進制的四捨五入一樣）。

計算機表示十進制是採用二進製表示的，所以 0.1 在二進製表示為  
`0.1.toString(2) // "0.00011 0011 0011 0011 0011 0011 0011 0011 0011 0011 0011 0011 0011 01"


小數的算法，是乘2

0.1
× 2
￣￣￣￣
0.2 → 取小數前的 0 

0.2
× 2
￣￣￣￣
0.4 → 取小數前的 0 

0.4
× 2
￣￣￣￣
0.8  → 取小數前的 0 


0.8
× 2
￣￣￣￣
1.6  → 取小數前的 1

0.6
× 2
￣￣￣￣
1.2  → 取小數前的 1

0.2
× 2
￣￣￣￣
0.4  → 取小數前的 0

十進位 0.1  = 二進位 0.000110

0.1 * 2 = 0.2 # 0
0.2 * 2 = 0.4 # 0
0.4 * 2 = 0.8 # 0
0.8 * 2 = 1.6 # 1
0.6 * 2 = 1.2 # 1
0.2 * 2 = 0.4 # 0

從上面可以看出，0.1的二進制格式是：0.0001100011....。這是一個二進制無限循環小數，但計算機內存有限，我們不能用儲存所有的小數位數。那麼在精度與內存間如何取捨呢？

答案是：`在某個精度點直接捨棄`(第53位開始)。當然，代價就是，0.1在計算機內部根本就不是精確的0.1，而是一個有舍入誤差的0.1。當代碼被編譯或解釋後，0.1已經被四捨五入成一個與之很接近的計算機內部數字，以至於計算還沒開始，一個很小的舍入錯誤就已經產生了。這也就是 0.1 + 0.2 不等於0.3 的原因。

使用JavaScript內置的函數`toPrecision`或`toFixed`來保留一定的精度：  

`(0.1 + 0.2).toPrecision(10) == 0.3`     
> true

`(0.1 + 0.2).toFixed(10) == 0.3`  
> true

不要相信js的計算 善用 [math.js](https://mathjs.org/)

### Rreferences
http://ourjs.com/detail/54695381bc3f9b154e000046
https://segmentfault.com/a/1190000012175422
https://github.com/InterviewMap/CS-Interview-Knowledge-Map/blob/master/JS/JS-ch.md#%E4%B8%BA%E4%BB%80%E4%B9%88-01--02--03