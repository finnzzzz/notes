# Ajax / Axios
## 簡介
**Asynchronous Javascript And XML**
**異步的JS和XML**

通過AJAX可以在瀏覽器中向服務器發向異步請求，可無刷新獲取數據。

AJAX是一種將現有的標準組合在一起使用的新方式
### XML簡介
可擴展標記語言，被設計用來傳輸和存儲數據。

XML和HTML類似，不同的是HTML中都是預定義標籤，而XML中沒有預定義標籤，全都是自定義標籤。
![](https://i.imgur.com/YDwfmQw.png)

現已被JSON取代
![](https://i.imgur.com/enrUyVD.png)

## AJAX優缺點
### 優點
1. 可無需更新頁面就與服務器端進行通信
2. 允許你根據用戶事件來更新部分頁面內容
### 缺點
1. 沒有瀏覽歷史，不能回退
2. 存在跨域問題(同源)
3. SEO不友好

## fetch函式
fetch(網址).then(function(回應物件){console.log(回應物件)})


# Axios
> https://github.com/axios/axios
### 一個ajax請求庫
## axios 特點
- 基於 xhr + promise 的**異步 ajax 請求庫**
- 瀏覽器端/node 端都可以使用
- 支持**請求／響應攔截器**
- 支持**請求取消**
- **請求/響應**數據轉換
- 批量發送多個請求

## axios 函數
>json server
```javascript=
    <script>
      const btns = document.querySelectorAll("button");

      //請求(查詢)
      btns[0].onclick = function () {
        //發送AJAX請求
        axios({
          //請求類型
          method: "GET",
          //URL
          url: "http://localhost:3000/posts/2",
        }).then((response) => {
          console.log(response);
        });
      };

      //添加一篇新文章
      btns[1].onclick = function () {
        //發送AJAX請求
        axios({
          //請求類型
          method: "POST",
          //URL
          url: "http://localhost:3000/posts",
          //設置請求體
          data: {
            title: "今天下雨",
            author: "allen",
          },
        }).then((response) => {
          console.log(response);
        });
      };

      //更新數據
      btns[2].onclick = function () {
        //發送AJAX請求
        axios({
          //請求類型
          method: "PUT",
          //URL
          url: "http://localhost:3000/posts/3",
          //設置請求體
          data: {
            title: "今天下雨,下午也下雨",
            author: "allen",
          },
        }).then((response) => {
          console.log(response);
        });
      };

      //刪除數據
      btns[3].onclick = function () {
        //發送AJAX請求
        axios({
          //請求類型
          method: "DELETE",
          //URL
          url: "http://localhost:3000/posts/3",
        }).then((response) => {
          console.log(response);
        });
      };
    </script>
```
## axios 語法
```javascript=
      btn[1].onclick = function () {
        //axios()
        axios
          .post("http://localhost:3000/posts", {
            title: "今天下雨",
            author: "allen",
          })
          .then((response) => {
            console.log(response);
          });
      };
```
## axios 常用語法
- axios(config): 通用/最本質的發任意類型請求的方式
- axios.request(config): 等同於 axios(config)
- axios(url[, config]): 可以只指定 url 發 get 請求
- axios.get(url[, config]): 發 get 請求
- axios.delete(url[, config]): 發 delete 請求
- axios.post(url[, data, config]): 發 post 請求
- axios.put(url[, data, config]): 發 put 請求
- axios.defaults.xxx: 請求的默認全局配置
- axios.interceptors.request.use(): 添加請求攔截器
- axios.interceptors.response.use(): 添加響應攔截器
- axios.create([config]): 創建一個新的 axios(它沒有下面的功能)
- axios.Cancel(): 用於創建取消請求的錯誤對象
- axios.CancelToken(): 用於創建取消請求的 token 對象
- axios.isCancel(): 是否是一個取消請求的錯誤
- axios.all(promises): 用於批量執行多個異步請求
- axios.spread(): 用來指定接收所有成功數據的回調函數的方法

## 默認配置 Config Defaults
```javascript=
axios.defaults.method = 'GET'
axios.defaults.baseURL = 'https://api.example.com';
axios.defaults.params = {id:100};
axios.defaults.timeout = 3000;
....
```

## 語法理解和使用
### axios.create(config)
- 根據指定配置創建一個新的 axios, 也就就每個新 axios 都有自己的配置
- 新 axios 只是沒有取消請求和批量發請求的方法, 其它所有語法都是一致的
1. 需求: 項目中有部分接口需要的配置與另一部分接口需要的配置不太一樣
2. 解決: 創建 2 個新 axios, 每個都有自己特有的配置, 分別應用到不同要 求的接口請求中

### 攔截器函數
- 說明: 調用 axios()並不是立即發送 ajax 請求, 而是需要經歷一個較長的流程
