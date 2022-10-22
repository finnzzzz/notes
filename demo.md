# Javascript基礎01
[黑馬前端-課程連結(48hrP473)<br>](https://www.bilibili.com/video/BV1Sy4y1C7ha?p=15&spm_id_from=pageDriver&vd_source=efe33422984f8c578cc16c5833f4cdcc)
**js組成三部分**：<br>
ECMAScript(語法)、don(文檔對象模型)、bom(瀏覽器對象模型)

**js輸入輸出語句**

![](https://i.imgur.com/gHKJRcC.png)

### **變量**<br>
一個盒子,在內存建立一個儲存空間<br>
*1.聲明變量<br>*
:::info
var(variable)<br>
var age;
:::
*2.賦值*
:::info
age = 18;
:::
*3.輸出結果*
:::info
console.log(age);
:::


*4.變量初始化<br>*
```javascript=
var myname = "xxx";
console.log(myname);
```
**變量使用**<br>
![](https://i.imgur.com/B13ePn8.png)![](https://i.imgur.com/lT3kDXG.png)


```javascript=
var myname = prompt('輸入名字');
alert(myname);
```
聲明變量的特殊情況
![](https://i.imgur.com/YEzqclc.png)

**變量命名規範**
![](https://i.imgur.com/ecSRfDL.png)
**簡單數據類型**
![](https://i.imgur.com/S05ig4K.png)

## String

檢測字符串長度 length<br>
```javascript=
var str = 'my name is xxx';
console.log(str.length)//15
```
*數值相加 字符相連*

檢測字符串類型 typeof<br>
```javascript=
var str = 'pink';
console.log(typeof str)//string

var num = 10;
console.log(typeof num)//number
```
轉換為字符串型
![](https://i.imgur.com/EEvEK0Z.png)

轉換為數字型
![](https://i.imgur.com/3MqbtmA.png)

## 算數運算符
![](https://i.imgur.com/ulh2ePP.png)

```javascript=
console.log(1 + 1); //2
console.log(5 % 3); //2
```


**前置遞增運算符** ++寫在變量前
```javascript=
var age = 10;
++age;
console.log(age);//11
```
                                  
先變量自加1 後返回值
```javascript=                         
var age = 10;
console.log(++age + 10);//21
```
\
**後置遞增運算符**<br>
先表達式返回原值 後變量再自加1
```javascript=
var age = 10;
console.log(age++ + 10);//20
console.log(age);//11
```
*Test*<br>
(++a=表達式 a=變量)
```javascript=
var a =10;
++a;                 //++a 11 a=11
var b = ++a + 2;    // a=12 ++a=12
console.log(b);    //14

_____________________
var c = 10;
c++;                  //c++ 11 c=11
var d = c++ + 2 ;    //c++=11 c=12
console.log(d);     //13

---------------------
var e = 10;
var f = e++ + ++e;  //1. e++=10 e=11 2.e=12 ++e=12
console.log(f);    //22
```
\
### 比較運算符
![](https://i.imgur.com/ZdUdWlc.png)
=賦值, ==判等號(會轉型), ===全等
### 邏輯運算符
![](https://i.imgur.com/23Furx3.png)

&&一個為false都為false
||一個為true都為true 

### 邏輯與(&&)短路運算
：表達式1結果為真 則 返回表達式2
```javascript=
console.log(123 && 456);//456
console.log(0 && 1 + 2 && 3423);//0
console.log('' && 1 + 2 && );//''
0 '' null undefined NaN
```
### 邏輯或(||)短路運算
：表達式1結果為真 則 返回表達式1
```javascript=
console.log(123 || 456);//123
console.log(0 || 1 + 2 || 3423);//3
console.log('' || 1 + 2 || );//3
```
```javascript=
var num = 0;
console.log(123 || num++);//123 num++中斷 
console.log(num);//0
```
### 運算符優先級
![](https://i.imgur.com/1DX0kEq.png)

/

## 流程控制
：順序 分支(if switch) 循環

1.if 語法結構
:::success
if (條件表達式) { //執行語句 }<BR>
條件表達式為真 執行語句<br>
條件表達式為假 執行語句後面代碼
:::
![](https://i.imgur.com/HSxuYTG.png)
```javascript=
var age = prompt('年齡');
if(age >= 18) {
    alert('進入');
} else{
    alert('離開');
}
```
多分支語句 if else if
```javascript=
if(條件1){
    //語句1;
} else if (條件2){
    //語句2;
} else if (條件3){
    //語句3;
} else{
    //最後語句;
}
```

三元表達式  ?  :<br>
簡化if else寫法

```javascript=
var num = 10;
var result = num > 5 ? 'yes' : 'no';
console.log(result);//yes
```
Switch<br>
利用表達式的值和value匹配
```javascript=
switch(表達式or變量){
    case value1:
        執行語句1;
        break;
    case value2:
        執行語句2;
        break;
    default:
        執行最後語句;
}
```
一般情況下可相互替換<br>
switch...case處理case較為確定值<br>
if...else...較靈活 處理範圍判斷

## 循環
* for循環
* while循環
* do...while循環

#### For語法結構<br>
:::success
for ( **初始化變量**; **條件表達式**; **操作表達式** ){**循環體**}

**初始化變量**：用var聲明一個普通變量,通常做為計數器使用<br>
**條件表達式**：決定循環是否繼續執行,就是終止條件<br>
**操作表達式**：循環最後執行的代碼,計數器變量進行更新(遞增或遞減)
:::
```javascript=
for (var i = 1; i <= 100; i++){
    console.log('hello');//hello*100
}
```

```javascript=
for (var i = 1; i <= 100; i++){
    if(i == 1){
        console.log('今年1歲,出生');
    }else if(i == 100){
        console.log('今年100歲,過世');
    }else {
        console.log('今年'+ i '歲');
    }
}
```

/

**計算1~100整數累加**<br>
核心算法:1+2+3+4+.... , *sum = sum + i;*
```javascript=
var sum = 0;
for(var i = 1; i <= 100; i++){
    // sum = sum + i(簡化)
    sum += i;
    }
    console.log(sum);
```
**計算1~100奇數和偶數的加**<br>
```javascript=
var even = 0;
var odd = 0;
for(var i = 1; i <= 100; i++){
    if(i % 2 == 0){
        even = even + i;
    }else{
        odd = odd + i;
    }
}
console.log('奇數和:'+even)
console.log('偶數和'+odd)

```
三元寫法<br>
```javascript=
i & 2 == 0 ? even += i : odd += i;
```

**輸入班級人數>依序輸入成績>計算總和>計算平均<br>**

```javascript=
  var num = prompt("班級人數");
      var sum = 0;
      var average = 0;
      for (var i = 1; i <= num; i++) {
        var score = prompt("輸入第" + i + "個成績");
        sum = sum + parseFloat(score);
        average = sum / num;
      }
      alert("班級總成績:" + sum);
      alert("班級平均:" + average);
```
**追加字符串應用**
```javascript=
var num = prompt('輸入星星數量');
var str = '';
for (var i = 1; i <= num; i++){
str = str + '★'}
console.log(str);
alert(str);
```
### 雙重for循環
```javascript=
var rows = prompt('輸入行號');
var cols = prompt('輸入列號');
var str = '';
for (var i = 1; 1 <= rows; i++){
    for (var j = 1; j <= cols; j++){
        str = str + '★';
    }
    str += '/n';
}
console.log(str);
```
![](https://i.imgur.com/ULkfNYb.png)
遞減

```javascript=
 var str = '';
      for (var i = 1; i <= 10; i++){
        for (var j = i ; j <=10; j++){
          str = str + '★';
        }
        str += '\n';
      }
      console.log(str);
```
![](https://i.imgur.com/iaCuQSZ.png)遞增
```javascript=
 var str = '';
      for (var i = 1; i <= 10; i++){
        for (var j = 1 ; j <= i; j++){
          str = str + '★';
        }
        str += '\n';
      }
      console.log(str);
```
### while循環
1.打印1~100歲
```javascript=
var i = 1;
while (i <= 100){
    console.log('今年'+ i + '歲'):
    i++;
}
```

2.計算1~100整數和
```javascript=
var sum = 0;
var j = 1;
while (j <= 100){
    sum += j;
    j++
}
console.log(sum);
```