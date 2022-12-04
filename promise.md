# promise
## promis介紹
1. promise是一種新的技術(ES6規範)
2. promise是js中進行**異步編程**的新解決方案
    舊方案是單純使用回調函數
3. 從語法上來說：promise是一個**構造函數**
4. 從功能上來說：promise對象用來封裝一個異步操作並可以獲取其成功/失敗的結果

- 所謂Promise，簡單說就是一個容器，裡面保存著某個未來才會結束的事件（通常是一個異步操作）的結果
- 從語法上說，Promise 是一個對象，從它可以獲取異步操作的消息
- Promise 提供統一的 API，各種異步操作都可以用同樣的方法進行處理

異步編程
![](https://i.imgur.com/c4bhTBs.png)
## promise特點
### 指定回調函數的方式更加靈活
- 舊的：必須在啟動異步任務之前指定
- Promise：啟動異步任務 => 返回promise對象 => 給promise對象綁定回調函數(甚至可以在異步任務結束後指定
### 支持鏈式調用，可以解決回調地獄問題
- 回調地獄：函數嵌套調用, 外部回調函數異步執行的結果是嵌套的回調執行的條件
- 回調地獄缺點：
    - 不便於閱讀、不便於異常處理

> 案例
```javascript=
    <script>
        // 創建一個新的p對象promise
        const p = new Promise((resolve, reject) => { // 執行器函數
          // 執行異步操作任務
          setTimeout(() => {
            const time = Date.now() 
            if (time % 2 == 0) {
              resolve('成功的数据，time=' + time)
            } else {
              reject('失败的数据，time=' + time)
            }
          }, 1000);
        })

        p.then(
          value => { // 接收得到成功的value数据 onResolved
            console.log('成功的回调', value)  // 成功的回调 成功的数据，time=1615015043258
          },
          reason => { // 接收得到失败的reason数据 onRejected
            console.log('失败的回调', reason)    // 失败的回调 失败的数据，time=1615014995315
          }
        )
    </script>
```