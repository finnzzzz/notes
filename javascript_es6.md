# javascript-es6
![](https://i.imgur.com/frFIcGk.png)
![](https://i.imgur.com/hCzCSV6.png)

## 變量問題
### 變量聲明： 
    1. 允許重複聲明 
    2. 聲明提前 
## 變量解決
### 關鍵字 let
![](https://i.imgur.com/2DNxW08.png)
![](https://i.imgur.com/GUo1r4U.png)


1. 不會汙染全局變量
2. 不允許重複生命同名變量，聲明時會在當前作用域中，檢查之前是否聲明過同名變量
        
- 同時引入塊級作用域：
代碼執行時，遇到大括號會創建一個塊級作用域，大括號結束，塊級銷毀。
在塊級作用域中用let聲明的變量，在塊級之外是無法訪問的。

- 底層：
let的提昇會被提升到 "暫時性死區" 中，當代碼運行到變量的聲明語句時，會將其從暫時性死區中移出。
- 關於循環：
每一次循環都會開啟一個新的作用域，每個作用域使用的都是新的變量，當循環結束，變量跟隨釋放。

![](https://i.imgur.com/VEDWwwC.png)
![](https://i.imgur.com/CKebii7.png)


:::info
ES6建議用let取代var，聲明變量時使用let而不是用var
:::

### const常量
用const聲明的常量，必須在聲明時賦值，而且不可以重複賦值。
開發中很多情況都是不會更改也不應該更改，後續許多的框架/第三方js庫都要求數據不可變
1. 常量不可變：指的是聲明的常量內存空間不可變
2. 循環中，循環變量不可以使用常量，但是在for in循環中可以使用

![](https://i.imgur.com/1Bs4MM0.png)

## 作用域問題
```javascript=
      var a = 1;
      var b = 1;
      function fn() {
        console.log(a, b);
        var a = b = 2; // var a = 2; b = 2
        console.log(a, b);
      }
      fn();
      console.log(a, b);

//undefined 1
//2 2
//1 2
```
![](https://i.imgur.com/AUdLmqd.png)

---
```javascript=
    <script>
      var a = [1, 2];
      var b = a;
      console.log(a, b);
      b[0] = 110;
      console.log(a, b);
    </script>

//數組存在推
//a和b指向同一個推地址
//[1, 2][1, 2]
//[110, 2][110, 2]
```
```javascript=
    <script>
      var a = { m: 666 };
      var b = a;
      b = { m: 888 };
      console.log(a.m); //666

      var a = { m: 666 };
      var b = a;
      b.m = 888 };
      console.log(a.m); //888
    </script>
```
```javascript=
    <script>
      console.log(a, b); //undefined undefined
      if (1) {
        var a = 1;
      } else {
        var b = 2;
      }
      console.log(a, b); //1 undefined
    </script>
```
```javascript=
    <script>
      function fn() {
        var a = 11;
      }
      fn();
      console.log(window.a); //undefined(對象身上不存在屬性)
      console.log(a); //error
    </script>
```
```javascript=
    <script>
      console.log(a); //undefined
      if ("a" in window) {
        var a = 110;
      }
      console.log(a); //110
    </script>
```
```javascript=
    <script>
      var a = 12;
      b = 13;
      c = 14;
      function fn(a) {
        console.log(a, b, c); //10 13 14
        a = 100;
        b = 200;
        console.log(a, b, c); //100 200 14
      }
      b = fn(10);
      console.log(a, b, c); //12 undefined(函數執行完畢 返回undefined) 14
    </script>
```

```javascript=
    <script>
      var ary = [12, 13];
      function fn(ary) {
        console.log(ary); //12 13
        ary[0] = 100;
        ary = [100];
        ary[0] = 0;
        console.log(ary); //0
      }
      fn(ary);
      console.log(ary); //100,13
    </script>
```
```javascript=
    <script>
      console.log(fn); //undefined
      if (1) {
        console.log(fn); //funciotn fn()
        function fn() {
          console.log("ok");
        }
      }
      console.log(fn); //funciotn fn()
    </script>
```
## 解構賦值
![](https://i.imgur.com/C8OKRT4.png)
![](https://i.imgur.com/ZVkhqMK.png)
> 對象解構
```javascript=
const user = {
  name: "tom",
  age: 18,
};
let { name, age } = user;
console.log(name, age); //tom 18
```
> 字符串
```javascript=
const str = "tom";
let [a, b, c] = str;
console.log(a, b, c); //t o m

```
## 箭頭函數
![](https://i.imgur.com/ZS6ZG4e.png)
1. 假如函數體中只有一句代碼，且代碼的執行結果就是返回值，可以省略大括號和return
![](https://i.imgur.com/WzqVTNO.png)
```javascript=
//const sum = (n1, n2) => {
//    return n1 + n2;
//}
const sum = (n1+ n2) => n1 + n2;
const result = (10, 20);
console.log(result)
```
2. 如果形參只有一個，可以省略小括號
![](https://i.imgur.com/9Y9TcnF.png)
#### 箭頭函數不綁定this關鍵字，箭頭函數中的this，指向的是函數定義位置的上下文this
```javascript=
var age = 100;
var obj = {
    age:20;
    say:() => {
        alert(this.age)
    }
}
obj.say(); //100
```
## 剩餘參數
剩餘參數語法允許我們將一個不定數量的參數表示為一個數組
![](https://i.imgur.com/GE6jccB.png)

```javascript=
    <script>
      const sum = (...args) => {
        let total = 0;
        args.forEach((item) => (total += item));
        return total;
      };
      console.log(sum(10, 20));
      console.log(sum(10, 20, 30));
    </script>
```
```javascript=
let ary1 = ['red','blue','white'];
let [s1, ...s2] = ary1;
console.log(s1);// red
console.log(s2);//['blue','white']
```
## 擴展運算符(展開語法)
擴展運算符可以將數組或者對象轉為用逗號分隔的參數序列
```javascript=
let ary = [1,2,3];
...ary //1,2,3
console.log(...ary); //1 2 3
```
擴展運算符可應用於**合併數組**
![](https://i.imgur.com/VobtKWs.png)

**將偽數組或可遍歷對象轉換為真正的數組**
(偽数组是指類似数组一样可以遍历查找，但是无法修改里面的任何元素
```javascript=
var divs = document.getElementsByTagName('div');
var ary = [...divs];
ary.push('a');
console.log(ary);
```
**計算隨機數量數值相加(在函數中使用)**
```javascript=
 <script>
      function sum(...numbers) {
        return numbers.reduce((preValue, currentValue) => {
          return preValue + currentValue;
        });
      }
      console.log(sum(1, 2, 3, 4));
    </script>
```
**構造字面量對象時使用展開語法**
```javascript=
<script>
      let person = { name: "tom", age: 18 };
      let person2 = { ...person };
      //console.log(..person) >報錯，展開運算符不能展開對象
      person.name = "jerry";
      console.log(person2); //name:'tom', age:18
      console.log(person); //name:'jerry', age:18

    //合併
    let person3 = {...person,name:'jack',address:'地球'}
    console.log(person3)
    </script>
```
### Array的擴展方法
#### Array.from()
![](https://i.imgur.com/Eo29pyn.png)
![](https://i.imgur.com/Z3B7Bbw.png)
#### find()
![](https://i.imgur.com/cfUxIcv.png)
#### findIndex()
![](https://i.imgur.com/cTZm1Pb.png)
#### includes()
![](https://i.imgur.com/TvlH0Yj.png)
```javascript=
let ary = ["A", "B", "C"];
let result = ary.includes('a')
console.log(result)//true
```
### String的擴展方法
#### 模板字符串 
![](https://i.imgur.com/nHQdGmG.png)

**解析變量**
![](https://i.imgur.com/mpu6KzD.png)

**可以換行**
![](https://i.imgur.com/nVnZWzZ.png)

**可以調用函數**
![](https://i.imgur.com/6wDYp7k.png)

#### startsWith() endsWith()
![](https://i.imgur.com/vtR2KKS.png)

#### repeat()
![](https://i.imgur.com/JYIF9kv.png)

### Set 數據結構
![](https://i.imgur.com/eXEUHvj.png)
```javascript=
const s1 = new Set();
console.log(s1.size)//0

const s2 = new Set(["a", "b"]);
console.log(s2.size)//2

const s3 = new Set(["a","a", "b"]);
console.log(s3.size)//2
const ary = [...s3];
console.log(ary)//["a", "b"] 數組去重
```
![](https://i.imgur.com/FrpbqLa.png)
```javascript=
const s4 = new Set();
s4.add('a').add('b');
console.log(s4.size)

const r1 = s4.delete('a');
console.log(s4.size)
console.log(r1);//true

const r2 = s4.has('d');
console.log(r2)//false

s4.clear();
console.log(s4.size)//0
```

#### 遍歷
![](https://i.imgur.com/Hd5JfAK.png)
```javascript=
const s5 = new Set(['a', 'b', 'c']);
s5.forEach(value => {
    console.log(value)
})
```
### WeakSet
![](https://i.imgur.com/4LG1tyM.png)

### 數據結構Map
![](https://i.imgur.com/BbJQuZH.png)
```javascript=
//JS中對象中是不能使用對象來做為key的
const obj1 = { name: "tom" };
const obj2 = { name: "anna" };

const info = {
  [obj1]: "aaa",
  [obj2]: "sss",
};

console.log(info); //{ '[object Object]': 'sss' }
```
> 使用map即可
```javascript=
const map = new Map();

map.set(obj1, "aaa");
map.set(obj2, "sss");
map.set(1, "ccc");

console.log(map);  
// Map(3) {
//     { name: 'tom' } => 'aaa', 
//     { name: 'anna' } => 'sss',
//     1 => 'ccc'
//   }

//第二種創建方式
const map2 = new Map([
  [obj1, "aaa"],
  [obj2, "sss"],
  [1, "ccc"],
]);
```
#### Map常用方法
![](https://i.imgur.com/fFTsVVu.png)
### WeakMap
![](https://i.imgur.com/wJxJif0.png)
![](https://i.imgur.com/8YhvapP.png)


## 表示數值方法
```javascript=
const num1 = 100 //十進制

const num2 = 0b100 //二進制 binary

const num3 = 0o100 //八進制 octonary
 
const num4 = 0x100 //十六進制 hexadecimal

//數值連接符(ES12)
const num = 100_000_000_000_000
```

## 指數運算符(ES7)
```javascript=
const result = Math.pow(3,3)
// es7 **
const result2 = 3 ** 3
```

## Object.entries(ES8)
> 可獲取到一個數組，數組中會存放key value
```javascript=
const obj = {
  name: "tom",
  age: 18,
};

console.log(Object.entries(obj));
//[ [ 'name', 'tom' ], [ 'age', 18 ] ]

-------------------------

console.log(Object.entries(["abc", "efg"]));
//[ [ '0', 'abc' ], [ '1', 'efg' ] ]

console.log(Object.entries("abc"));
//[ [ '0', 'a' ], [ '1', 'b' ], [ '2', 'c' ] ]

```

## padStar & padEnd(ES8)
> 填充首尾字符串
```javascript=
const cardNumber = "5853457438534";
const last4Number = cardNumber.slice(-4);
const finalNumber = last4Number.padStart(cardNumber.length, "*");

console.log(finalNumber);//*********8534
```

## Object的fromEntries(ES10)

> 將entries轉換為對象
```javascript=
const obj = {
  name: "tom",
  age: 18,
};

const entries = Object.entries(obj);
console.log(entries);// [ [ 'name', 'tom' ], [ 'age', 18 ] ]

const info = Object.fromEntries(entries);
console.log(info); // { name: 'tom', age: 18 }

```
```javascript=
const queryString = "name=tom&age=18&height=122";
const queryParams = new URLSearchParams(queryString);
const paramObj = Object.fromEntries(queryParams);

console.log(queryParams);
console.log(paramObj);
// URLSearchParams { 'name' => 'tom', 'age' => '18', 'height' => '122' }
//{ name: 'tom', age: '18', height: '122' }

```

## BigInt使用(ES11)
```javascript=
//ES11之前
const maxInt = Number.MAX_SAFE_INTEGER;
console.log(maxInt); //9007199254740991

//ES11
const bigInt = 9007199254740991900n;
console.log(bigInt + 10n); //9007199254740991910n

const num = 20;
console.log(bigInt + BigInt(num)); //9007199254740991910n

const smallNum = Number(bigInt);
console.log(smallNum); //9007199254740992000 error

```

## 空值合併計算符 ?? (ES11)
Nullish Coalescing Operator
> 可判斷undefined null "" <br>
> || 無法判斷""
```javascript=
const foo = undefined //null ""

const bar = foo ?? 'defualt value'

console.log(bar)// 'defualt value'
```

## 可選鏈 Optional Chaning(ES11)
> 進行null和undefined判斷時更加清晰簡潔`
```javascript=
const info = {
  name: "TOM"
  friend: {},
}
//之前方法
if(info && info.friend && info.friend.girlfriend)


console.log(info.friend?.girlFriend?.name)//undefined
```

