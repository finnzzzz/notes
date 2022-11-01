# Web APIs
![](https://i.imgur.com/SmeQC13.png)

### API
![](https://i.imgur.com/fc6irf5.png)

## DOM 文檔對象模型
![](https://i.imgur.com/rxwrJfH.png)
#### DOM樹
![](https://i.imgur.com/DHUpsZZ.png)
## 獲取元素
1. getElementById()
```javascript=
<div id='time'>2020-10-27</div>
<script>
    var timer = document.getElementById('time');
    console.log(timer);
</script>
```
querySelector('選擇器')<br>返回第一個元素對象

querySelectorALL('選擇器')<br>所有元素對象

```javascript=
var xxx = document.querySelector('.box');// class='box'
document.querySelector('#nav');//id='nav'
document.querySelector('li');//<li>xxx</li>
```
![](https://i.imgur.com/d3wKxRD.png)
## 事件基礎
![](https://i.imgur.com/Ixqn3wK.png)

事件三要素
* 事件源
* 事件類型
* 事件處理程序
![](https://i.imgur.com/XxYa9cW.png)

```javascript=
<button id = 'btn'>123</button>
<script>
    var btn = document.getElementById('btn');
btn.oncclick = function(){
    alert('yes');
}
</script>
```
![](https://i.imgur.com/hw1jzj6.png)

改變元素內容
![](https://i.imgur.com/9WG6yuj.png)
```javascript=
var div = document.quertSelector('div');
div.innerText = '<strong>123123</strong>'; //不識別<strong>
```

點擊按鈕換圖片
![](https://i.imgur.com/qSep4po.png)

判斷系統時間顯示文字
```javascript=
<div>上午好</div>
    <script>
      var div = document.querySelector("div");
      var date = new Date();
      var h = date.getHours();
      if (h < 12) {
        div.innerHTML = "上午好";
      } else if (h < 18) {
        div.innerHTML = "下午好";
      }
    </script>
```

#### 表單元素的屬性操作
:::success
type, value, checked, selected, disabled
:::
```javascript=
btn.onclicck = function(){
    input.value = '被點擊了'; 表單中的文字內容須通過value修改
    this.disabled = true; //按鈕禁用button
    //this指向事件函數的調用者>btn
}
```
密碼顯示切換案例
![](https://i.imgur.com/tsLArS6.png)
![](https://i.imgur.com/5fLncBE.png)
```javascript=
<head>
<style>
      .box {
        position: relative;
        width: 400px;
        border-bottom: 1px solid #ccc;
        margin: 100px auto;
      }
      .box input {
        width: 370px;
        height: 30px;
        border: 0;
        outline: 0;
      }
      .box img {
        position: absolute;
        top: -7px;
        right: 7px;
        width: 24px;
      }
    </style>
</head>
////////////////////
<body>
<div class="box">
      <label for=""> <img src="images/close.png" id="eye" /> </label>
      <input type="password" name="" id="pwd" />
    </div>
    <script>
      var eye = document.getElementById("eye");
      var pwd = document.getElementById("pwd");
      var flag = 0;
      eye.onclick = function () {
        if ((flag = !flag)) {
          pwd.type = "text";
          eye.src = "images/open.png";
        } else {
          pwd.type = "password";
          eye.src = "images/close.png";
        }
      };
    </script>
<body>
```
樣式屬性操作
![](https://i.imgur.com/s6PoKeh.png)

點擊關閉圖片
```javascript=
var btn = document.querySelector(".close-btn");
      var box = document.querySelector(".tao-box");
      btn.onclick = function () {
        box.style.display = "none";
      };
```

### 排他思想
![](https://i.imgur.com/ITGomJe.png)
```javascript=
    <button>001</button>
    <button>002</button>
    <button>003</button>
    <button>004</button>
    <button>005</button>
    <script>
      var btns = document.getElementsByTagName("button");

      for (var i = 0; i < btns.length; i++) {
        btns[i].onclick = function () {
          //(1)先把所有按鈕背景刪除
          for (var i = 0; i < btns.length; i++) {
            btns[i].style.backgroundColor = "";
          }
          //(2)讓元素背景為pink
          this.style.backgroundColor = "pink";
        };
      }
    </script>
```

##### 鼠標經過事件 onmouseover
##### 鼠標離開事件 onmouseout


#### (1)全選按鈕控制所有按鈕作法
```javascript=
//j_cbAll全選按鈕id
j_cbAll.onclick = function(){
    for(var i = 0; i < j_tbs.length; i++){
        j_tbs[i].checked = this.checked;
        //this.checked 可得到當前複選框選中狀態,true false
    }
}
```
#### (2)複選按鈕控制全選按鈕作法
```javascript=
for (var i = 0; i < j_tbs.length; i++){
    j_tbs[i].onclick = function(){
        //flag控制全選按鈕是否選中
        var flag = true;
        //每次點擊下方複選框 循環檢查4個小按鈕是否全被選中
        for(var i = 0; i < j_tbs.length; i++){
            if (!j_tbs[i].checked){ //複選框沒被選中false
                flag = false;
                break; //退出for循環提高效率,一個沒有選中就無需在檢查
            }
    }
        j_cbAll.checked = flag;
}
```

![](https://i.imgur.com/8rYlsLx.png)
```javascript=
<div id='demo' index='1'></div>
<script>
    var div = document.querySelector('div');
    console.log(div.id);
    console.log(div.getAttribute('id'));
    console.log(div.getAttribute('index'));
</script>
```
### 節點操作
#### 父節點 parentNode
得到離元素最近的父級節點
```javascript=
<div class='box'>
    <span class='erweima'>x</span>
</div>
<script>
        var erweima = document.querySelector('erweima');
        console.log(erweima.parentNode);
</script>
```
#### 子節點 childNodes
1. childNodes 得到所有的子節點 包刮 元素節點 文本節點等等
2. children 只得到所有的子元素節點 實際開發較常用
3. children[0] 第一個<br>children[o1.children.length - 1] 最後一個

#### 創建元素節點 creatElement
#### 添加節點 node.appendChild(child)
```javascript=

<ul>
    <l1>123</l1>
</ul>
<scritp>
    // 1. 創建節點元素
    var li = document.createElement('li');
    var ul = document.querySelector('ul');
    //2.添加節點 (後面追加)
    ul.appendChild(li);
    //3.添加節點 node.insertBefore(child, 指定元素); (之前追加)
    var lili = document.createElement('li');
    ul.insertBefore(lili, ul.children[0]);
```
#### 刪除節點 node.removeChild(child)
#### 複製節點 node.cloneNode()
()內為空或者為false,為**淺拷貝**,只複製節點本身,不複製裡面的子節點<br>
()內為true,為**深度拷貝**,會複製本身以及裡面所有子節點
#### 三種動態創建元素區別
![](https://i.imgur.com/pKAjh8f.png)

### 註冊事件(綁定事件)
給元素添加事件，稱為註冊事件或者綁定事件<br>
分為**傳統事件**和**方法監聽註冊方式**

![](https://i.imgur.com/cZxIBds.png)
![](https://i.imgur.com/ektyj2s.png)
![](https://i.imgur.com/4CR7nox.png)
### 刪除事件(解綁事件)
![](https://i.imgur.com/WsGEOGA.png)
![](https://i.imgur.com/f8btoVB.png)
### DOM 事件流
![](https://i.imgur.com/CdspRgD.png)
![](https://i.imgur.com/8SL72Is.png)
![](https://i.imgur.com/TiWrZuy.png)
### 事件對象
![](https://i.imgur.com/SpcHVMj.png)
![](https://i.imgur.com/4N1Yo1f.png)

事件對象常見屬性和方法
![](https://i.imgur.com/T16logv.png)
![](https://i.imgur.com/bNx0jmC.png)

圖片跟隨鼠標小案例
```javascript=
img {
      position: absolute;
     }
<img src="images/angel.gif" />
    
    <script>
      var pic = document.querySelector("img");
      document.addEventListener("mousemove", function (e) {
        var x = e.pageX;
        var y = e.pageY;
        pic.style.left = x + "px";
        pic.style.top = y + "px";
      });
    </script>
```
#### 常用鍵盤事件
![](https://i.imgur.com/7UHv7Re.png)

## BOM 瀏覽器對象模型
![](https://i.imgur.com/n1HuTbL.png)
![](https://i.imgur.com/n52v7x7.png)

![](https://i.imgur.com/6DPNllv.png)
### 窗口加載事件
![](https://i.imgur.com/L3CihJZ.png)
![](https://i.imgur.com/funccR6.png)
### 調整窗口大小事件
![](https://i.imgur.com/Vcxirlj.png)
### 定時器
![](https://i.imgur.com/aG122nU.png)
```javascript=
//setTimeout(function(){
// console.log('boom');
//        }, 2000);

function callback(){
         console.log('boom');
      }
var timer1 = setTimeout(callback. 3000);
var timer2 = setTimeout(callback. 5000);
</script>
```
#### 停止定時器
window.clearTimeout(timeoutID)

#### 循環定時器
window.setInterval(回調函數, 間隔毫秒數)



#### 回調函數
![](https://i.imgur.com/GUhhY6V.png)

#### JS執行機制
![](https://i.imgur.com/vSG7Tci.png)
![](https://i.imgur.com/xSUmMd2.png)

### location 對象
#### URL 統一資源定位符
![](https://i.imgur.com/YNidhmI.png)

#### location對象屬性
![](https://i.imgur.com/aMh094m.png)
#### location對象方法
![](https://i.imgur.com/dWwJP0l.png)
#### navigator 對象
判斷客戶端電腦or手機
![](https://i.imgur.com/ADYo2x2.png)
#### history 對象
![](https://i.imgur.com/GchYlo0.png)


