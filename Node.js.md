# Node.js
## node.js簡介
node.js是一個基於chrome v8引擎的javascript運行環境
![](https://i.imgur.com/2SeTZON.png)

## fs 文件系統模塊
![](https://i.imgur.com/nS6C4Jq.png)
### fs.readFile()
可讀取指定文件中的內容
![](https://i.imgur.com/fHQwa1f.png)
![](https://i.imgur.com/WRbP0B1.png)
![](https://i.imgur.com/OtHqeoQ.png)

### fs.writeFile()
可向指定文件中寫入內容
只能用來創建文件，不能創建路徑
重複調用寫入文件會覆蓋舊的文件
![](https://i.imgur.com/pdYhKo5.png)
![](https://i.imgur.com/J3YaQ8E.png)
![](https://i.imgur.com/w0FN2jn.png)

### 整理成績案例
```javascript=
//導入fs模塊
const fs = require('fs')

fs.readFile('成績.txt','utf8',function(err,dataStr){
    if(err){
        return console.log('./讀取文件失敗' + err.message)
    }
    //console.log('讀取文件成功' + dataStr);

    //把成績數據按照空格進行分割
    const arrOld = dataStr.split(' ')
    
    const arrNew = []

    arrOld.forEach(item => {
        arrNew.push(item.replace('=', '：'))
    })
    
    const newStr = arrNew.join('\r\n')
    console.log(newStr);
})
```
![](https://i.imgur.com/l43IOpT.png)
![](https://i.imgur.com/xMSHZkN.png)


### fs模塊-路徑動態拼接問題
![](https://i.imgur.com/vVLm5yP.png)

**解決方式:__dirname(表示當前文件所處的目錄)**
```javascript=
__dirname + '/成績.txt'
```
/
## path 路徑模塊
![](https://i.imgur.com/hCrPyy5.png)
### path.join()
![](https://i.imgur.com/jHPMDFL.png)
![](https://i.imgur.com/ijTGxDz.png)
### path.basename()
![](https://i.imgur.com/IWhCZMx.png)
![](https://i.imgur.com/WZhxQQ5.png)
### path.extname()
![](https://i.imgur.com/3smeS5Q.png)
![](https://i.imgur.com/9BwFMTI.png)

## http模塊
![](https://i.imgur.com/edrjcYp.png)

### 域名和域名服務器
![](https://i.imgur.com/YwtcPdC.png)

### 端口號
![](https://i.imgur.com/Nl0l2zF.png)

### 創建基本的web服務器
1. 導入http模塊
![](https://i.imgur.com/8py4HNa.png)

2. 創建web服務器實例![](https://i.imgur.com/tiFRqnp.png)

3. 為服務器實例綁定request事件，監聽客戶端的請求![](https://i.imgur.com/uizUs3I.png)

4. 啟動服務器![](https://i.imgur.com/V2JxNCr.png)

### req請求對象
![](https://i.imgur.com/x0u0Aqj.png)

### res響應對象
![](https://i.imgur.com/zRypplf.png)

#### 解決中文亂碼問題
![](https://i.imgur.com/GlpDNbF.png)

### 根據不同url響應不同html內容
1. 獲取請求的url地址
2. 設置默認的響應內容為404 not found
3. 判斷用戶請求的是否為 / 或 /index.html首頁
4. 判斷用戶請求的是否為/about關於頁面
5. 設置content-type響應頭，防止中文亂碼
6. 使用res.end()把內容響應給客戶端
![](https://i.imgur.com/OxDZYFv.png)

## 模塊化
![](https://i.imgur.com/CX6a6D9.png)
![](https://i.imgur.com/2JpUOb7.png)

### node.js模塊的分類
- 內置模塊(由node.js官方提供的，例如fs, path, http等)
- 自訂義模塊(用戶創建的每個.js文件，都是自訂義模塊)
- 第三方模塊(由第三方開發出來的模塊，使用錢需要先下載）

###  加載模塊 require()
![](https://i.imgur.com/3SfJrw1.png)

### 模塊作用域
![](https://i.imgur.com/C0WylLr.png)
可防止全局變量污染的問題

### module對象
可向外共享模塊作用域中的成員
![](https://i.imgur.com/UpNPVeF.png)

#### **module.exports對象**
![](https://i.imgur.com/vv54VFa.png)
使用require()方法導入模塊時，導入的結果永遠以module.exports指向的對象為準
![](https://i.imgur.com/phfAigB.png)
#### **exports對象**
![](https://i.imgur.com/JAXNfKx.png)
![](https://i.imgur.com/VBn4gEZ.png)
![](https://i.imgur.com/XJBjRA5.png)

### 模塊化規範
![](https://i.imgur.com/j4weuUs.png)

## NPM & 包
![](https://i.imgur.com/In1zVmq.png)
![](https://i.imgur.com/0h7Swkx.png)
![](https://i.imgur.com/Tof7BfN.png)
**NPM (node package manager)**
![](https://i.imgur.com/221FYDB.png)

### 安裝包的命令

```javascript
npm insatall 包的完整名稱

npm i 包的完整名稱
```

### devDependencies節點
![](https://i.imgur.com/lMxJggO.png)

### 規範包的結構
![](https://i.imgur.com/CJvCy2Q.png)

### 自訂義模塊加載機制
![](https://i.imgur.com/GoiJxyh.png)
![](https://i.imgur.com/WugxdWp.png)

## express
![](https://i.imgur.com/RD1kNDa.png)
![](https://i.imgur.com/bKIAUhq.png)
### 創建基本web服務器
![](https://i.imgur.com/yMSPD9q.png)
### 監聽get請求
![](https://i.imgur.com/XOYbFcr.png)
### 監聽post請求
![](https://i.imgur.com/uzgtqZA.png)
### 把內容響應給客戶端
![](https://i.imgur.com/vkZAHgx.png)
### 獲取url中攜帶的查詢參數
![](https://i.imgur.com/9UmGbHN.png)
### 獲取url中的動態參數
![](https://i.imgur.com/otgscOo.png)
### 託管靜態資源 express.static()
![](https://i.imgur.com/IG2MxYZ.png)
![](https://i.imgur.com/zDHlWgF.png)
## express路由
![](https://i.imgur.com/e1lN8Ng.png)
![](https://i.imgur.com/RBnvvN2.png)
### 路由的匹配過程
![](https://i.imgur.com/tNnqW4h.png)
### 模塊化路由
![](https://i.imgur.com/P9LZS0z.png)
#### 創建路由模塊
![](https://i.imgur.com/z59qd3J.png)
#### 註冊路由模塊
![](https://i.imgur.com/2A8H7te.png)
#### 路由模塊添加前綴
![](https://i.imgur.com/h4JMvOE.png)
## express中間件
**middleware，物物流程的中間處理環節**
### express中間件調用流程
![](https://i.imgur.com/0G27lhG.png)
### 中間件的格式
![](https://i.imgur.com/zQby01W.png)
:::info
next函數是實現多個中間件連續調用的關鍵，它表示把流轉關係轉交給下一個中間件或路由
:::
### 定義中間件函數
![](https://i.imgur.com/LOPVMFe.png)
### 全局生效的中間件
![](https://i.imgur.com/C6snAQ7.png)
### 中間件的作用
![](https://i.imgur.com/UlOXl3U.png)

定義多個全局中間件
![](https://i.imgur.com/TUJu7XS.png)

### 局部生效中間件
![](https://i.imgur.com/MPus4hM.png)
定義多個局部中間件
![](https://i.imgur.com/x9Dq04R.png)
### 中間件使用注意事項
![](https://i.imgur.com/K0EGq96.png)
### 中間件的分類
1. 應用級別中間件
![](https://i.imgur.com/wQukWJg.png)

2. 路由級別中間件
![](https://i.imgur.com/gAMtBcA.png)

3. 錯誤級別中間件
![](https://i.imgur.com/PCRiNwX.png)
:::info
錯誤級別中間件必須註冊在所有路由之後
:::

4. express內置的中間件
![](https://i.imgur.com/76eR6Kd.png)

5. 第三方中間件
![](https://i.imgur.com/1qDYRuO.png)
---
### 中間件跨域問題解決
![](https://i.imgur.com/b76TYL4.png)

![](https://i.imgur.com/1FeOm3i.png)
CORS注意事項
![](https://i.imgur.com/INt3Bco.png)

